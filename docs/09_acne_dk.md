# 09_acne_dk — 여드름·이소트레티노인

> *Cutibacterium and Staphylococcus dysbiosis of the skin microbiome in acne and its decline after isotretinoin treatment*  
> JEADV Clin Pract 3(5):1454–1466 (2024) · doi:10.1002/jvc2.487

## 연구 설계

- **코호트**: 덴마크 성인 68명 · 여드름 32명(19–43세) / 건강 36명(22–39세) · Aarhus University
- **채취 부위**: 볼 · 등 (+ 이소트레티노인 추적군은 이마 추가)
- **마커**: 16S V1–V3 (27F–534R) · 같은 프로젝트에 C. acnes SLST·포도상구균 tuf2 타이핑 동거

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `09_acne_dk_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `09_acne_dk_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `09_acne_dk_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `09_acne_dk_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `09_acne_dk_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `09_acne_dk_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `09_acne_dk_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `09_acne_dk_16S_sample_info.tsv` 컬럼 (181행 × 50컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 181/181 | 181종 (예: SRR26945181, SRR26945182, SRR26945183 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 181/181 | PRJNA1044749 | BioProject accession |
| `sample_id` | 181/181 | 181종 (예: 13B, 13C, 14B …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 181/181 | 68종 (예: A1, A10, A11 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 181/181 | Cheek / Forehead / Upper back | 채취 부위 |
| `assay` | 181/181 | 16S | 마커 종류 |
| `region` | 181/181 | V1-V3 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 181/181 | Acne / Healthy | 비교군 라벨 |
| `group_type` | 181/181 | acne | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 181/181 | 19 ~ 43 | 나이 (세) |
| `age_group` | 0/181 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 181/181 | F / M | 성별 |
| `read_count` | 181/181 | 23247 ~ 122830 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 181/181 | 14 ~ 486 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 181/181 | 0.397518 ~ 5.53819 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 181/181 | 0.125145 ~ 0.989293 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 181/181 | 1.14305 ~ 93.396 | 역 Simpson 지수 |
| `read_depth_final` | 181/181 | 2710 ~ 58447 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 181/181 | 9종 (예: Acinetobacter, Chryseobacterium, Corynebacterium …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 181/181 | 9.9 ~ 99.16 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 181/181 | 2 ~ 171 | 검출된 속의 개수 (리드 1개 이상) |
| `paper_id` | 181/181 | 61종 (예: 1, 10, 10A …) | 논문 보충표의 샘플 번호 |
| `timepoint` | 109/181 | baseline / post_isotretinoin | 종단 설계의 시점. 스터디마다 값이 다르다 (예: M0/M24h/M7d, T0/T2w/T4w) |
| `sex_raw` | 181/181 | F / K / M | BioSample 원문 성별 표기 (정규화 전) |
| `acne_grade_site` | 109/181 | 0 / 1 / 2 / 3 / 4 | **그 부위의** 여드름 등급 (0~4). 이마·볼·윗등을 따로 매겼으므로 샘플마다 자기 부위 값이 들어 있다 — 등급-조성 용량반응을 볼 수 있다 |
| `acne_grade_highest` | 109/181 | 0 / 1 / 2 / 3 / 4 | 세 부위 중 가장 높은 등급 (환자 단위 중증도) |
| `past_treatment` | 109/181 | 18종 (예: Acnetac and tetracycline, Antibiotics, Basiron and fucidin …) | 과거 치료력 (P-pills 경구피임약, Epiduo, 항생제 등). 치료 후 시료는 `Isotretinoin for N months` |
| `current_treatment` | 68/181 | 8종 (예: Basiron and fucidin, Doxycycline and Epiduo for 3 weeks, Epiduo …) | 채취 시점의 치료 (None / Epiduo / Doxycycline …) |
| `isotretinoin_months` | 41/181 | 4 / 4.5 / 5 / 6 | 이소트레티노인 복용 개월수 (4~6). 치료 후 시료에만 값이 있다 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `09_acne_dk_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Staphylococcus`, `g_Corynebacterium`, `g_Unassigned`, `g_Streptococcus`, `g_Micrococcus`, `g_Paracoccus`, `g_Finegoldia` …

## 임상 데이터 — 없음

논문 Table S1A(건강 36명)·S1B(여드름 32명)에 개인별 연령·성별·IGA 중증도와 이소트레티노인 치료 전후 시점이 있지만, Wiley가 보충자료 내려받기를 403으로 막아 이 환경에서는 받지 못했다. 필요하면 논문 페이지에서 `jvc2487-sup-0003-Table_S1_rev.xlsx` 를 직접 받아 `sample_id` 로 붙이면 된다.

샘플명에서 복원한 군(여드름/건강)·부위(볼/등/이마)·피험자는 전부 채워져 있다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
