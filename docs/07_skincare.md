# 07_skincare — 화장품 중재

> *Effect of the skincare product on facial skin microbial structure and biophysical parameters: A pilot study*  
> MicrobiologyOpen 10(5):e1236 (2021) · doi:10.1002/mbo3.1236

## 연구 설계

- **코호트**: 한국인 여성 25명 · 30–58세(평균 43) · LG생활건강 R&D, 대전
- **채취 부위**: 볼(cheek) — 같은 사람을 3시점 추적 (0주 / 2주 / 4주)
- **마커**: 16S V3–V4 (341F–805R) · Illumina MiSeq

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `07_skincare_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `07_skincare_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `07_skincare_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `07_skincare_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `07_skincare_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `07_skincare_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `07_skincare_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `07_skincare_16S_sample_info.tsv` 컬럼 (75행 × 47컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 75/75 | 75종 (예: ERR5924075, ERR5924076, ERR5924077 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 75/75 | PRJEB44885 | BioProject accession |
| `sample_id` | 75/75 | 75종 (예: P1-0-S01, P1-0-S02, P1-0-S03 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 75/75 | 25종 (예: S01, S02, S03 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 75/75 | Cheek | 채취 부위 |
| `assay` | 75/75 | 16S | 마커 종류 |
| `region` | 75/75 | V3-V4 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 75/75 | 0W / 2W / 4W | 비교군 라벨 |
| `group_type` | 75/75 | skincare_time | group이 무슨 축인지 (age / sensitivity / acne / metformin_time) |
| `age` | 0/75 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/75 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 75/75 | female | 성별 |
| `read_count` | 75/75 | 106474 ~ 277830 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 75/75 | 118 ~ 639 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 75/75 | 1.9182 ~ 4.77018 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 75/75 | 0.654656 ~ 0.978217 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 75/75 | 2.89567 ~ 45.9063 | 역 Simpson 지수 |
| `read_depth_final` | 75/75 | 18567 ~ 62976 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 75/75 | 6종 (예: Cutibacterium, Pseudomonas, Staphylococcus …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 75/75 | 13.65 ~ 61.22 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 75/75 | 50 ~ 180 | 검출된 속의 개수 (리드 1개 이상) |
| `panel` | 75/75 | P1 | 논문의 패널 번호 (P1) |
| `timepoint` | 75/75 | 0W / 2W / 4W | 종단 설계의 시점. 스터디마다 값이 다르다 (예: M0/M24h/M7d, T0/T2w/T4w) |
| `reads_paper` | 75/75 | 66246 ~ 213198 | 논문이 보고한 리드 수 |
| `observed_otus_paper` | 75/75 | 548 ~ 1021 | 논문이 보고한 관측 OTU 수 |
| `shannon_paper` | 75/75 | 4.37078 ~ 7.80425 | **논문이 보고한** Shannon 지수 (우리 `Shannon`과 대조용) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `07_skincare_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Unassigned`, `g_Staphylococcus`, `g_Wolbachia`, `g_Sphingomonas`, `g_Streptococcus`, `g_Pseudomonas`, `g_Corynebacterium` …

## `metadata/clinical_data/07_skincare_clinical.tsv` (75행 × 8컬럼)

**출처**: Table A2 (본문 부록) · MicrobiologyOpen

표가 시점(0/2/4주)을 가로로 펼친 형태라 세로로 폈다. 논문 `P1_S01` 은 ENA `P1-0-S01`(패널-주차-피험자)의 주차를 뺀 형태이며 **75/75 완전히 대응**한다.

다양성 지표는 **논문이 보고한 값**이라 우리가 계산한 `Shannon`·`Observed`와 나란히 놓고 비교할 수 있다 (실측 상관 rho=+0.86, 값의 범위는 다르다).

피부 물성치(수분·거칠기·피지·pH)는 논문이 군 평균만 보고해 붙일 수 없다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`sample_id`**, 이 표에서 **`sample_id`** 다.

- `07_skincare_16S`: 75행과 매칭

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 75/75 | 75종 (예: P1-0-S01, P1-0-S02, P1-0-S03 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 75/75 | 25종 (예: S01, S02, S03 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `panel` | 75/75 | P1 | 논문의 패널 번호 (P1) |
| `timepoint` | 75/75 | 0W / 2W / 4W | 종단 설계의 시점. 스터디마다 값이 다르다 (예: M0/M24h/M7d, T0/T2w/T4w) |
| `paper_sample_id` | 75/75 | 25종 (예: P1_S01, P1_S02, P1_S03 …) | 논문 표기 샘플 ID (데이터 표기와 다를 수 있음) |
| `reads_paper` | 75/75 | 66246 ~ 213198 | 논문이 보고한 리드 수 |
| `observed_otus_paper` | 75/75 | 548 ~ 1021 | 논문이 보고한 관측 OTU 수 |
| `shannon_paper` | 75/75 | 4.37078 ~ 7.80425 | **논문이 보고한** Shannon 지수 (우리 `Shannon`과 대조용) |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
