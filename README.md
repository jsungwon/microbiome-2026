# microbiome-2026 — 마이크로바이옴 실습 데이터

논문 17편의 공개 데이터(ENA/SRA)를 내려받아 앰플리콘 파이프라인(DADA2)으로 처리하고,
**논문 보충자료의 샘플별 임상정보와 결합**해 둔 수업용 자료다.
FASTQ를 다루지 않고 TSV만 읽어서 바로 분석할 수 있다.

> 원 데이터는 각 논문 저자의 것이며 이 저장소는 수업 목적의 재가공물이다.
> 결과를 발표할 때는 **원 논문을 인용**해야 한다 → [`docs/data_provenance.md`](docs/data_provenance.md)

## 스터디 목록

**BioProject accession을 스터디 번호와 함께 적어 뒀다.** 같은 코호트가 세균·진균으로
나뉘어 등록된 경우가 많고(예: `04_acne`는 16S와 ITS가 서로 다른 accession),
같은 accession이 여러 논문에 걸쳐 재등록된 사례도 있어 번호만으로는 헷갈린다.

| 폴더 접두사 | 스터디 | **BioProject** | 논문 | 비교군 | 샘플 | **임상항목** |
|---|---|---|---|---|---|---|
| `01_aging` | 노화 (한국) | `PRJNA614620`(16S+ITS)<br>`PRJNA613934`(중복 제외) | Sci Rep 2022 | 젊은(Y) / 고령(O) | 16S 55 · ITS 58 | **21종**<br><sub>수분·피지·pH·TEWL 4종 + 연령군</sub> |
| `02_healthy` | 건강한 한국인 | `PRJNA723064` | Sci Rep 2021 | 젊은(Y) / 고령(O) | 16S 102 | **27종**<br><sub>피부물성 7종 + 주름·색소·설문</sub> |
| `03_sensitive` | 민감성 피부 (한국) | `PRJNA627788`(16S)<br>`PRJNA627798`(ITS) | Microorganisms 2020 | 민감 / 비민감 | 16S 42 · ITS 42 | **37종**<br><sub>물성 6종 + **주관 설문 20여종** + 기온</sub> |
| `04_acne` | 여드름 (한국) | `PRJNA669317`(16S)<br>`PRJNA673754`(중복 제외) | J Microbiol 2021 | 여드름 / 건강 | 16S 60 · ITS 53 | **16종**<br><sub>수분·피지·pH·TEWL + 논문 다양성값</sub> |
| `05_metformin` | 메트포르민 **장내** | `PRJEB24497` | PLoS One 2018 | M0 / M24h / M7d (+ 부작용 중증도) | 16S 53 | **9종**<br><sub>**부작용 중증도**(셀 색에서 복원) + 일수</sub> |
| `06_cosmetics` | 화장품·피부수분 (한국) | `PRJNA345237` | MicrobiologyOpen 2018 | 고수분 HHG / 저수분 LHG × 3시점 | **임상표만 90행** | **11종**<br><sub>수분군 + 논문 다양성값 (**정량 데이터 없음**)</sub> |
| `07_skincare` | 화장품 중재 (한국) | `PRJEB44885` | MicrobiologyOpen 2021 | 0주 / 2주 / 4주 (25명 종단) | 16S 75 | **10종**<br><sub>시점 + 논문 다양성값<br>물성치는 군 평균만</sub> |
| `08_atopic` | 아토피 (덴마크) | `PRJEB42898` | Microorganisms 2021 | AD 병변 / 비병변 / 코 / 대조 | 16S 466 | **9종**<br><sub>성별·해부학부위·피부타입<br>SCORAD는 개인정보 규정으로 비공개</sub> |
| `09_acne_dk` | 여드름·이소트레티노인 (덴마크) | `PRJNA1044749` | JEADV Clin Pract 2024 | 여드름 / 건강 × 치료 전후 | 16S 181 | **14종**<br><sub>**부위별 여드름 등급** + 치료력 + 이소트레티노인 개월수</sub> |
| `10_psoriasis` | 건선 6부위 (미국) | `PRJEB25915` | Microbiome 2018 | 병변 / 비병변 / 건강 | 16S 417 | **7종**<br><sub>host_phenotype(병변/비병변/건강)</sub> |
| `11_scalp` | 두피 건선·지루피부염 (중국) | `PRJNA788988`(16S)<br>`PRJNA789592`(ITS) | Exp Dermatol 2022 | 건선 / 지루 / 건강 × 병변 | 16S 187 · ITS 186 | **4종**<br><sub>군·부위만 (논문이 2쪽 연구서한)</sub> |
| `12_rosacea` | 주사 — **피부·장·혈액** (헝가리) | `PRJNA1189573` | Microorganisms 2024 | 검체 3종 (같은 27명) | 16S 93 | **4종**<br><sub>검체종류만 (논문이 군 단위 요약)</sub> |
| `13_lipid` | 지질–미생물 (독일) | `PRJEB66070` | 미게재 | 아토피 / 여드름 / 건강 × 병변 | 16S 111 | **4종**<br><sub>질환·병변·부위 (샘플명에서 복원)</sub> |
| `14_atopic_zh` | 아토피 종단 (스위스) | `PRJEB44392` (16S+ITS) | 미게재 | AD 병변 / 비병변 / 건강 × t1–t3 | 16S 325 · ITS 327 | **12종**<br><sub>**SCORAD 연속형 0–79.1** + 중증도·병변·계절·두필루맙</sub> |
| `15_season` | 사계절 가구 코호트 (홍콩) | `PRJNA390040`(16S)<br>`PRJNA421247`(ITS) | Microbiome 2018<br>mSystems 2019 | 가구 × 개인 × 부위 × 4계절 | 16S 484 · ITS 481 | **10종**<br><sub>가구·주손·민족·도농 + 계절</sub> |
| `16_dandruff` | 비듬 두피 (인도) | `PRJNA415710` (16S+ITS) | Front Cell Infect Microbiol 2018 | Day 0 / 84 / 112 | 16S 398 · ITS 400 | —<br><sub>연령·성별·시점 (파이프라인 진행 중)</sub> |
| `17_ad_myco` | 아토피 마이코바이옴 (폴란드) | `PRJNA1046129` | Exp Dermatol 2025 | 아토피 50 / 건강 50 | ITS 100 | **5종**<br><sub>군·채취일 (논문 Table 1은 군 요약)</sub> |

**임상항목**은 `metadata/sample_info/`의 각 파일에 **이미 병합돼 있는** 변수 수다
(기술 컬럼과 계산값 제외). 별도 조인이 필요 없다.
항목이 4개뿐인 스터디는 군·부위·피험자만 있다는 뜻이고, 그 이유를 각 문서에 적어 뒀다.

### accession을 볼 때 주의할 점

- **한 스터디가 accession 2개인 경우가 많다.** `03`·`04`·`11`·`15`는 세균과 진균을
  서로 다른 BioProject에 등록했다. `14`·`16`은 **하나의 accession 안에 16S와 ITS가 섞여** 있어
  우리가 나눴다(`14`는 BioSample 속성으로, `16`은 리드 선두 프라이머를 직접 읽어서).
- **중복 등록 2건을 제외했다.** `PRJNA613934`는 `PRJNA614620`과, `PRJNA673754`는
  `PRJNA669317`과 리드 내용이 같다. 합치면 표본 수가 부풀려진다.
- **`05`만 장내(분변), `12`는 피부·대변·혈액 세 검체**다. 나머지는 피부다.
- `01`–`07`은 한국인 코호트, `08`–`17`은 덴마크·미국·중국·헝가리·독일·스위스·홍콩·인도·폴란드
  질환 코호트다. **스터디를 가로질러 합칠 때는 배치 효과를 반드시 의심할 것.**

> `06`과 `07`은 **같은 질문(화장품 4주 사용 → 피부 미생물)**인데 데이터 등록 상태가 다르다.
> `07`은 75개 시료가 각각 올라와 속 수준 분석이 되고, `06`은 아래 이유로 안 된다.
>
> `06_cosmetics`는 **미생물 정량 데이터가 없다.** SRA의 2개 run이 서로 동일한 파일이고
> 90개 시료의 바코드가 이미 제거돼 있어 샘플별로 나눌 수 없다.
> 논문이 보고한 다양성 지표(OTU·Chao1·Shannon·Evenness)만 샘플 단위로 확보했다.

각 스터디의 논문·DOI·BioProject accession은 [`docs/data_provenance.md`](docs/data_provenance.md),
기계가독 목록은 `metadata/study_index.tsv`.

## 데이터가 만들어진 경로

```
ENA FASTQ (482 run · 10.2 GB, md5 검증)
  └─ 앰플리콘 분리 → cutadapt 4.9 → DADA2 1.30.0 → SILVA 138.2 / UNITE
       └─ ASV 테이블 → 속(genus) 집계 → 논문 임상정보와 결합 → 이 저장소
```

입력 리드 20,135,148개 중 **14,316,761개(71.1%)**가 최종 ASV로 남았다.
단계별 파라미터·도구 버전·통과율은 [`docs/pipeline.md`](docs/pipeline.md).

**원시 FASTQ는 이 저장소에 없다** (`example_fastq/`의 예제 1쌍만 포함).
accession으로 ENA/SRA에서 직접 받을 수 있다.

## 폴더 구조

```
metadata/sample_info/   <스터디>_<마커>_sample_info.tsv   ← 여기서 시작
                        샘플 1행 = 설계 + 임상 메타데이터 + 다양성 + 상위 20속(%)
metadata/clinical_data/ <스터디>_clinical.tsv
                        논문 보충자료에서 추출한 원본 임상표 (샘플 단위 1행)
                        sample_info에 이미 병합돼 있음 — 원본이 필요할 때만 쓴다
16S_count/              세균 정량 — genus_count(정수) · genus_pct(%) · genus_long · genus_taxonomy
ITS_count/              진균 정량 — 동일 구성
asv/                    ASV 수준 원자료 (속보다 세밀) + 대표 서열 FASTA
example_fastq/          예제 paired FASTQ (7.3 MB) — 전처리 실습용
docs/data_provenance.md 데이터 출처 · accession · 인용 정보
docs/pipeline.md        처리 파이프라인 · 도구 버전 · 파라미터
docs/                   스터디별 컬럼 설명 (06은 임상표만)
docs/figures/           데이터 표 예시 스크린샷 (PPT용, 01번 스터디 기준)
```

## 시작하기

```r
d <- read.delim("metadata/sample_info/01_aging_16S_sample_info.tsv")
boxplot(g_Cutibacterium ~ group, data = d)
cor.test(d$sebum, d$Shannon, method = "spearman")
```

```python
import pandas as pd
d = pd.read_csv("metadata/sample_info/01_aging_16S_sample_info.tsv", sep="\t")
d.groupby("group")["g_Cutibacterium"].describe()
```

**컬럼 뜻을 모르겠으면 `docs/<스터디>.md`를 보면 된다.**
`sample_info`와 `clinical_data` 두 파일의 컬럼마다 채움 개수·값 범위·설명이 있다.

> ⚠ `03_sensitive`는 두 파일의 샘플 식별 컬럼 표기가 다르다 —
> sample_info는 `Non.03_bac`(컬럼 `subject`는 `Non.03`), 임상표는 `Non.03`이다.

## 어떤 파일을 쓸까

| 하려는 것 | 쓸 파일 |
|---|---|
| 군 간 조성 비교, 시각화 | `metadata/sample_info/*_sample_info.tsv` |
| 상위 20속으로 부족할 때 | `16S_count/*_genus_pct.tsv` (전체 속, %) |
| rarefaction · CLR · 카운트 모델 | `16S_count/*_genus_count.tsv` (정수) |
| 막대그래프·박스플롯 (long 포맷) | `16S_count/*_genus_long.tsv` |
| 문(Phylum) 수준으로 묶기 | `16S_count/*_genus_taxonomy.tsv` 조인 |
| ASV 수준 정밀 분석 | `asv/*_asv_count.tsv` + `*_asv_taxonomy.tsv` |
| 전처리(프라이머 제거·DADA2) 실습 | `example_fastq/` |

## 분석 과제 예시

1. **연령과 미생물** — `01_aging_16S`에서 `g_Cutibacterium`을 `group`으로 비교하라.
   차이가 크다. 그런데 `sebum`도 함께 보면 원인을 무엇이라 말할 수 있는가?
2. **교란 찾기** — `sebum`과 `Shannon`의 상관을 구하고, `group`별로 나눠 다시 구하라.
   `01_aging_16S`와 `04_acne_16S` 둘 다에서 같은 패턴이 나온다.
3. **부위 효과** — `body_site`로 나눠 우점 속이 달라지는지 보라.
   `02_healthy`와 `04_acne`는 같은 사람의 두 부위가 있어 `subject`로 짝지을 수 있다.
4. **재현 검증** — `04_acne_16S`에서 `g_Staphylococcus`/`g_Cutibacterium` 비를 군 간 검정하라.
   논문은 여드름군이 높다고 했다. 유의한가?
5. **논문 값과 대조** — `01_aging_16S`·`04_acne_16S`에는 논문이 보고한 `shannon_16S`와
   우리가 계산한 `Shannon`이 나란히 있다. 산점도로 그려 보라. 같은 데이터인데 왜 다른가?
6. **설문과 미생물** — `03_sensitive_16S`의 `perceived_skin_sensitivity`(1–7)와 조성이
   관련 있는가? 이분법 군 라벨보다 연속값이 더 잘 설명하는가?
7. **투약 반응 예측** — `05_metformin_16S`에서 투여 **전(M0)** 조성만으로
   `side_effect_group`(없음/경증/중증)을 가를 수 있는가? 종단 데이터라
   `subject`로 묶어 시점 변화도 함께 볼 수 있다.

## 데이터를 다룰 때 반드시 알 것

- **상대풍부도(compositional)다. 절대 균수가 아니다.** qPCR·spike-in 없이 앰플리콘만
  시퀀싱했으므로 "균이 더 많다"가 아니라 **"구성 비율이 다르다"**까지만 말할 수 있다.
- **합이 100%로 고정** → 한 속이 늘면 나머지는 기계적으로 준다. 단순 t검정·Wilcoxon으로
  속별 비교하면 실제 변화가 없는 속도 유의하게 나온다. CLR 변환 후 검정할 것.
- **시퀀싱 심도가 샘플마다 크게 다르다.** 검출 속 수는 심도에 직접 영향을 받는다.
  `read_depth_final` 컬럼으로 확인하고, 다양성 비교 전에 보정할 것.
- **스터디를 가로질러 속을 합치지 말 것.** 증폭 영역이 V3 / V3–V4 / V4–V5로 제각각이고,
  **`05_metformin`은 피부가 아니라 장내**이며 플랫폼도 Ion Torrent라 다른 넷과 성격이 다르다.
  01–04(피부)와 05(장내)는 별개 데이터로 다룰 것.
- **`01_aging`과 `04_acne`는 27개 run이 같은 시퀀싱 데이터**다 (배포 파일 기준 `sample_id` 13개 중복).
  두 스터디를 합쳐 표본 수를 늘리면 안 된다 → `docs/data_provenance.md`
- **물성치는 스터디마다 측정 기기와 단위가 다르다.** 스터디 내 비교는 괜찮지만
  절대값을 가로질러 비교하려면 표준화가 필요하다.
