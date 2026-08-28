# 05_metformin — 메트포르민 장내

> *Association of metformin administration with gut microbiome dysbiosis in healthy volunteers*  
> PLoS One 13(9):e0204317 (2018) · doi:10.1371/journal.pone.0204317

## 연구 설계

- **코호트**: 건강한 성인 18명 (여 11 / 남 7) · 나이 중앙값 25.5세 · BMI 중앙값 24.2
- **채취 부위**: 분변 — 같은 사람을 3시점 추적 (개체 내 반복측정)
- **마커**: 16S V3 (341F–518R) · Ion Torrent PGM 단일말단

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `05_metformin_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `05_metformin_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `05_metformin_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `05_metformin_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `05_metformin_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `05_metformin_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `05_metformin_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `05_metformin_16S_sample_info.tsv` 컬럼 (53행 × 47컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 53/53 | 53종 (예: ERR2662893, ERR2662894, ERR2662895 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 53/53 | PRJEB24497 | BioProject accession |
| `sample_id` | 53/53 | 53종 (예: S10_M0, S10_M24h, S10_M7d …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 53/53 | 18종 (예: S1, S10, S11 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 53/53 | Gut (feces) | 채취 부위 |
| `assay` | 53/53 | 16S | 마커 종류 |
| `region` | 53/53 | V3 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 53/53 | M0 / M24h / M7d | 비교군 라벨 |
| `group_type` | 53/53 | metformin_time | group이 무슨 축인지 (age / sensitivity / acne / metformin_time) |
| `age` | 0/53 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/53 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/53 | (전부 빈 칸) | 성별 |
| `read_count` | 53/53 | 258523 ~ 958486 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 53/53 | 145 ~ 568 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 53/53 | 3.32446 ~ 4.60876 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 53/53 | 0.917677 ~ 0.981534 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 53/53 | 12.1472 ~ 54.1529 | 역 Simpson 지수 |
| `read_depth_final` | 53/53 | 145631 ~ 554693 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 53/53 | 11종 (예: Bacteroides, Blautia, Catenibacterium …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 53/53 | 10.29 ~ 29.84 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 53/53 | 60 ~ 134 | 검출된 속의 개수 (리드 1개 이상) |
| `side_effect_group` | 53/53 | mild / none / severe | **위장관 부작용 중증도** (none / mild / severe). 논문 S1.2 표의 셀 색에서 복원 |
| `n_obs_days` | 53/53 | 6 ~ 12 | 부작용이 기록된 칸 수 (병합 셀 때문에 7보다 클 수 있다) |
| `n_days_none` | 53/53 | 0 ~ 7 | 부작용 없음으로 기록된 칸 수 |
| `n_days_mild` | 53/53 | 0 ~ 7 | 경증으로 기록된 칸 수 |
| `n_days_severe` | 53/53 | 0 / 1 / 2 / 3 / 4 / 5 | 중증으로 기록된 칸 수 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `05_metformin_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Unassigned`, `g_Bacteroides`, `g_Blautia`, `g_Faecalibacterium`, `g_Bifidobacterium`, `g_Pseudobutyrivibrio`, `g_Mediterraneibacter`, `g_Roseburia` …

## `metadata/clinical_data/05_metformin_clinical.tsv` (18행 × 7컬럼)

**출처**: S1.2 Table (docx) · PLoS One 보충자료

⚠ 이 표는 **중증도를 셀 배경색으로만** 표시한다 — 텍스트는 비어 있어서 일반적인 표 추출로는 안 나온다. docx의 셀 음영(`w:shd/@w:fill`)을 읽어 복원했다 (초록=없음 / 노랑=경증 / 빨강=중증). 피험자의 군은 관측된 날들 중 최중증도로 정했고, 그 결과 **없음 3 / 경증 6 / 중증 9** 로 논문 보고치와 정확히 일치한다.

⚠ `Subject_N` → ENA `S{N}` 대응은 **추론**이다. 둘 다 1–18이고 같은 논문·같은 순서라 자연스러운 읽기이지만 논문이 명시적으로 연결해 두지는 않았다.

나이·성별·BMI는 논문에 중앙값만 있어 피험자별로는 붙일 수 없다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`subject`**, 이 표에서 **`sample_id`** 다.

- `05_metformin_16S`: 53행과 매칭

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 18/18 | 18종 (예: S1, S10, S11 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `paper_subject_id` | 18/18 | 18종 (예: Subject_1, Subject_10, Subject_11 …) | 논문 표기 피험자 ID (`Subject_1` …) |
| `side_effect_group` | 18/18 | mild / none / severe | **위장관 부작용 중증도** (none / mild / severe). 논문 S1.2 표의 셀 색에서 복원 |
| `n_obs_days` | 18/18 | 6 ~ 12 | 부작용이 기록된 칸 수 (병합 셀 때문에 7보다 클 수 있다) |
| `n_days_none` | 18/18 | 0 ~ 7 | 부작용 없음으로 기록된 칸 수 |
| `n_days_mild` | 18/18 | 0 ~ 7 | 경증으로 기록된 칸 수 |
| `n_days_severe` | 18/18 | 0 / 1 / 2 / 3 / 4 / 5 | 중증으로 기록된 칸 수 |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
