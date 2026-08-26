# 처리 파이프라인

FASTQ → ASV → 속(genus) 테이블까지의 처리 내역. **Snakemake로 실행했고 전 단계가 재현 가능하다.**

```
① 원시 FASTQ  →  ② 앰플리콘 분리  →  ③ 프라이머 제거  →  ④ DADA2  →  ⑤ 분류 할당  →  ⑥ 집계
   ENA (md5 검증)   (혼합 run만)      cutadapt        denoising     SILVA / UNITE   genus 테이블
```

## 도구 버전

| 도구 | 버전 |
|---|---|
| Snakemake | 9.19.0 |
| cutadapt | 4.9 |
| R | 4.3.3 |
| DADA2 | 1.30.0 |
| phyloseq | 1.46.0 |
| vegan | 2.7.1 |

## 참조 데이터베이스

| 마커 | DB | 파일 |
|---|---|---|
| 16S (세균) | **SILVA 138.2** | `silva_nr99_v138.2_toGenus_trainset.fa.gz` (속까지)<br>`silva_v138.2_assignSpecies.fa.gz` (종 할당) |
| ITS (진균) | **UNITE** | `sh_general_release_dynamic_all.fasta.gz` |

## 처리 단위 — "unit"

프로젝트가 아니라 **unit** 단위로 독립 처리했다.
DADA2 오차 모델은 시퀀싱 run 단위로 학습해야 하므로 프로젝트를 섞으면 안 된다.

**01 노화와 04 여드름은 한 run에 16S와 ITS가 섞여 있어**(이중 앰플리콘 풀),
프라이머로 리드를 두 갈래로 나눈 뒤 각각을 별도 unit으로 처리했다.

| unit | 마커 | 영역 | 프라이머 |
|---|---|---|---|
| `01_aging_16S` | 16S | V4–V5 | 518F–926R (분리 후 제거) |
| `01_aging_ITS` | ITS | ITS1 | ITS1F–ITS2 (분리 후 제거) |
| `02_healthy_16S` | 16S | V3–V4 | 341F–805R |
| `03_sensitive_16S` | 16S | V4–V5 | 이미 제거된 상태로 등록됨 |
| `03_sensitive_ITS` | ITS | ITS1 | 이미 제거된 상태로 등록됨 |
| `04_acne_16S` | 16S | V4–V5 | 518F–926R (분리 후 제거) |
| `04_acne_ITS` | ITS | ITS1 | ITS1F–ITS2 (분리 후 제거) |

> **`02_healthy`만 V3–V4다.** 나머지는 V4–V5라 ASV를 가로질러 합칠 수 없다.
> 프로젝트 간 비교는 속(genus) 수준에서만 유효하다.

## DADA2 파라미터

공통: `maxEE = c(2, 5)` (R2 품질이 대체로 낮음) · `truncQ = 2` · `maxN = 0` · `minLen = 50`
키메라 제거: `removeBimeraDenovo(method = "consensus")`

| unit | truncLen (R1/R2) | 근거 |
|---|---|---|
| `01_aging_*` · `04_acne_*` (16S) | **260 / 200** | 리드 301 bp, V4–V5 약 400 bp |
| `02_healthy_16S` | **233 / 220** | 아래 참조 |
| `*_ITS` | **자르지 않음 (0)** | ITS는 길이가 가변이라 truncLen을 쓰면 안 된다 |

### `02_healthy`의 truncLen을 실측으로 정한 이유

V3–V4 앰플리콘이 **407 bp와 427 bp 이중 분포**인데 리드는 251 bp뿐이다.
흔히 쓰는 230/200으로 자르면 합이 430이라 427 bp급의 오버랩이 3 bp로 줄어
**해당 분류군이 통째로 사라진다** (실측 회수율 0%).
8개 샘플로 조합을 비교해 **233/220**을 골랐다 — 병합 95.8%, 427 bp급 24.3% 회수.

**품질 그래프만 보고 truncLen을 정하면 특정 분류군이 조용히 전멸한다.**

## 리드 통과율

| unit | 입력 | 최종 | 유지율 |
|---|---|---|---|
| `01_aging_16S` | 2,170,537 | 1,649,312 | 76.0% |
| `01_aging_ITS` | 871,958 | 526,564 | 60.4% |
| `02_healthy_16S` | 7,192,698 | 4,870,536 | 67.7% |
| `03_sensitive_16S` | 1,829,697 | 1,553,287 | 84.9% |
| `03_sensitive_ITS` | 3,804,340 | 2,594,134 | 68.2% |
| `04_acne_16S` | 3,468,838 | 2,629,384 | 75.8% |
| `04_acne_ITS` | 797,080 | 493,544 | 61.9% |
| **합계** | **20,135,148** | **14,316,761** | **71.1%** |

## 배포 파일이 만들어진 방식

| 파일 | 만든 방법 |
|---|---|
| `asv/*_asv_count.tsv` | DADA2 키메라 제거 후 ASV 테이블 (정수) |
| `asv/*_asv_taxonomy.tsv` | SILVA/UNITE 할당 결과 |
| `*_count/*_genus_count.tsv` | ASV를 속으로 합산 (`tax_glom`). 속 미할당은 `Unassigned` 하나로 통합 |
| `*_count/*_genus_pct.tsv` | 위를 샘플별 합 100%로 환산 |
| `*_count/*_genus_long.tsv` | 롱 포맷. 평균 0.01% 미만 속과 0인 칸 제외 |
| `metadata/sample_info/*` | 설계 + 임상 + 다양성 + 상위 20속을 한 행으로 결합 |

**다양성 지표**(`Observed`·`Shannon`·`Simpson`·`InvSimpson`)는
**심도 1,000 리드로 rarefy한 뒤 ASV 수준에서** 계산했다.
그 미만 샘플은 빈 칸이다. 속 수준에서 다시 계산하면 값이 달라진다 (묶으면 다양성이 낮아진다).

## 재현

원본 워크플로는 이 저장소가 아니라 처리 환경에 있다.

```
config/config.yaml          프로젝트별 프라이머·영역·truncLen
workflow/Snakefile          unit 정의
workflow/rules/             split → trim → dada2 → taxonomy → diversity → …
workflow/scripts/           앰플리콘 분리, 논문 보충자료 파싱, 배포 패키지 생성
```

Snakemake 744 job이 오류 없이 완주했다.
