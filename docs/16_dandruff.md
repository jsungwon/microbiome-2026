# 16_dandruff — 비듬 두피

> *Comparison of Healthy and Dandruff Scalp Microbiome Reveals the Role of Commensals in Scalp Health*  
> Front Cell Infect Microbiol 8:346 (2018) · doi:10.3389/fcimb.2018.00346

## 연구 설계

- **코호트**: 인도 성인 · 20–45세 · 벵갈루루
- **채취 부위**: 두피 — Day 0 / Day 84 / Day 112 3시점
- **마커**: 16S V3 (341F–534R) + ITS1 · 한 프로젝트에 두 마커(메타데이터에 표시 없음)

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `16_dandruff_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `16_dandruff_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `16_dandruff_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `16_dandruff_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `16_dandruff_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `16_dandruff_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `16_dandruff_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `16_dandruff_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `16_dandruff_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `16_dandruff_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `16_dandruff_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `16_dandruff_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `16_dandruff_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## 임상 데이터 — 없음

798샘플 전부에 **연령(20–45세)·성별·시점**(Day 0 / 84 / 112)이 있다.

⚠ **한 프로젝트에 16S 398 + ITS 400 런이 섞여 있는데 메타데이터에 아무 표시가 없다.** BioSample·샘플명·library 어디에도 마커 구분이 없어 리드 선두의 프라이머를 직접 읽어 판정했다(16S=341F, ITS=ITS1F). 섞은 채 돌리면 ITS 400런이 통과율 0%로 조용히 버려진다.

⚠ 비듬/건강 군 라벨은 BioSample 에 없다. 논문 보충표(Table 1–5)를 받아 뒀으니 필요하면 `sample_id` 로 붙이면 된다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
