# 12_rosacea — 주사 — 피부·장·혈액

> *Characteristics of the Stool, Blood and Skin Microbiome in Rosacea Patients*  
> Microorganisms 12(12):2667 (2024) · doi:10.3390/microorganisms12122667

## 연구 설계

- **코호트**: 헝가리 성인 27명 · 주사 18명(남4/여14) / 건강 9명(남2/여7) · Semmelweis University
- **채취 부위**: **피부(양볼) · 대변 · 혈액 세 검체** — 같은 사람에서 동시 채취
- **마커**: 16S V3–V4 (341F–805R)

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `12_rosacea_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `12_rosacea_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `12_rosacea_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `12_rosacea_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `12_rosacea_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `12_rosacea_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `12_rosacea_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `12_rosacea_16S_sample_info.tsv` 컬럼 (92행 × 42컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 92/92 | 92종 (예: SRR31465416, SRR31465417, SRR31465418 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 92/92 | PRJNA1189573 | BioProject accession |
| `sample_id` | 92/92 | 92종 (예: Blood1, Blood10, Blood11 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 92/92 | 1 ~ 27 | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 92/92 | Blood / Gut (feces) / Skin | 채취 부위 |
| `assay` | 92/92 | 16S | 마커 종류 |
| `region` | 92/92 | V3-V4 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 92/92 | Blood / Skin / Stool | 비교군 라벨 |
| `group_type` | 92/92 | rosacea_sampletype | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/92 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/92 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/92 | (전부 빈 칸) | 성별 |
| `read_count` | 92/92 | 9095 ~ 217022 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 92/92 | 6 ~ 249 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 92/92 | 0.0213667 ~ 4.55173 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 92/92 | 0.00501454 ~ 0.984915 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 92/92 | 1.00504 ~ 66.2923 | 역 Simpson 지수 |
| `read_depth_final` | 92/92 | 3584 ~ 69991 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 92/92 | 15종 (예: Acinetobacter, Aquabacterium, Bacteroides …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 92/92 | 9.41 ~ 99.7 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 92/92 | 5 ~ 126 | 검출된 속의 개수 (리드 1개 이상) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `12_rosacea_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Escherichia-Shigella`, `g_Sphingobium`, `g_Staphylococcus`, `g_Enhydrobacter`, `g_Acinetobacter`, `g_Cutibacterium`, `g_Unassigned`, `g_Aquabacterium` …

## 임상 데이터 — 없음

논문 Table 1이 군 단위 요약만 준다: 주사 18명(남4/여14, 중앙값 42세), 건강 9명(남2/여7, 39세), 아형은 구진농포형 14 / 홍반혈관확장형 1 / 혼합 3. 개인 단위 행이 없어 나이·성별·아형을 샘플에 붙일 수 없다.

**이 스터디의 비교축은 질환군이 아니라 검체 종류다** — 같은 27명에서 피부(양볼)·대변·혈액을 동시에 받았다. 혈액은 저바이오매스라 시약 오염 신호를 반드시 확인하고 해석할 것.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
