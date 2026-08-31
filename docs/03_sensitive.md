# 03_sensitive — 민감성 피부

> *Structures of the Skin Microbiome and Mycobiome Depending on Skin Sensitivity*  
> Microorganisms 8(7):1032 (2020) · doi:10.3390/microorganisms8071032

## 연구 설계

- **코호트**: 한국인 여성 42명 · 민감성 23명 / 비민감성 19명 · 22–52세
- **채취 부위**: 오른쪽 볼 4 cm²
- **마커**: 16S V4–V5 · ITS1 — 두 마커를 별도 라이브러리로 제작

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `03_sensitive_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `03_sensitive_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `03_sensitive_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `03_sensitive_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `03_sensitive_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `03_sensitive_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `03_sensitive_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `03_sensitive_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `03_sensitive_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `03_sensitive_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `03_sensitive_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `03_sensitive_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `03_sensitive_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `03_sensitive_16S_sample_info.tsv` 컬럼 (42행 × 73컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 42/42 | 42종 (예: SRR11605054, SRR11605055, SRR11605056 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 42/42 | PRJNA627788 | BioProject accession |
| `sample_id` | 42/42 | 42종 (예: Non.03_bac, Non.19_bac, Non.28_bac …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 42/42 | 42종 (예: Non.03, Non.19, Non.28 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 42/42 | Right cheek | 채취 부위 |
| `assay` | 42/42 | 16S | 마커 종류 |
| `region` | 42/42 | V4-V5 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 42/42 | Non-sensitive / Sensitive | 비교군 라벨 |
| `group_type` | 42/42 | skin_sensitivity | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 42/42 | 22 ~ 52 | 나이 (세) |
| `age_group` | 0/42 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 42/42 | female | 성별 |
| `read_count` | 42/42 | 4414 ~ 214779 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 42/42 | 25 ~ 411 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 42/42 | 0.36814 ~ 5.21374 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 42/42 | 0.128467 ~ 0.986414 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 42/42 | 1.1474 ~ 73.6064 | 역 Simpson 지수 |
| `read_depth_final` | 42/42 | 3678 ~ 181223 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 42/42 | Cutibacterium / Unassigned | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 42/42 | 21.74 ~ 94.56 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 42/42 | 53 ~ 188 | 검출된 속의 개수 (리드 1개 이상) |
| `perceived_skin_type` | 42/42 | Combination / Dry / Dry (severe) / Normal / Oil | 자각 피부타입 (Dry / Combination / Normal / Oil) |
| `perceived_facial_skin_thickness` | 42/42 | 1 / 2 / 3 | 자각 피부 두께 (1–3) |
| `perceived_skin_pores` | 42/42 | 1 / 2 / 3 / 4 | 자각 모공 크기 (1–4) |
| `degree_of_pimple_or_acne` | 42/42 | 1 / 2 / 3 | 자각 여드름 정도 (1–3) |
| `skin_trouble_1st_rank` | 42/42 | 11종 (예: Blackhead/Whitehead, Dry skin, Enlarged pores …) | 가장 신경 쓰이는 피부 고민 1순위 |
| `skin_trouble_2nd_rank` | 42/42 | 12종 (예: Blackhead/Whitehead, Dark circles, Dry skin …) | 피부 고민 2순위 |
| `skin_trouble_3rd_rank` | 42/42 | 11종 (예: Blackhead/Whitehead, Dark circles, Dry skin …) | 피부 고민 3순위 |
| `perceived_skin_sensitivity` | 42/42 | 1 ~ 7 | **자각 민감도 (1–7)** — 군 라벨보다 세밀한 연속값 |
| `sensitive_skin_cognitive_cause` | 20/42 | 11종 (예: Affect of childbirth, After starting makeup, After starting makeup/In-between seasons …) | 민감성을 느끼게 된 계기 (자유응답) |
| `recognizing_truble_when_using_cosmetics` | 42/42 | 1 / 2 / 3 | 화장품 사용 시 트러블 인지 (1–3). 원본 오타 `truble` |
| `experience_of_sun_allergy_inflammation_burn` | 42/42 | 1 / 2 / 3 | 햇빛 알레르기·염증·화상 경험 (1–3) |
| `experience_of_skin_allergy` | 42/42 | 1 / 2 / 3 | 피부 알레르기 경험 (1–3) |
| `recognition_of_skin_condition_change` | 42/42 | 1 / 2 / 3 | 피부 상태 변화 인지 (1–3) |
| `unpleasant_sensation_on_skin` | 42/42 | 1 / 2 / 3 | 피부 불쾌감 (1–3) |
| `embarrassment_due_to_skin_problems` | 42/42 | 1 / 2 / 3 / 4 | 피부 문제로 인한 당혹감 (1–4) |
| `difficylties_in_daily_life_due_to_skin_probl` | 42/42 | 1 / 2 / 3 | 일상생활 어려움 (1–3). 원본 오타 `difficylties` |
| `effects_of_skin_problems_when_choosing_cloth` | 42/42 | 1 / 2 / 3 / 4 | 옷 선택에 미치는 영향 (1–4) |
| `effects_of_skin_problems_on_social_life_and_` | 42/42 | 1 / 2 / 3 | 사회생활·여가에 미치는 영향 (1–3) |
| `effects_of_skin_problems_on_work_or_study` | 37/42 | No / Yes | 업무·학업에 미치는 영향 (Yes/No) — 이 항목만 형식이 다름 |
| `effects_of_skin_problems_on_human_relationsh` | 42/42 | 1 / 2 / 3 | 대인관계에 미치는 영향 (1–3) |
| `skin_treatment_problems_time_cost_etc` | 42/42 | 1 / 2 / 3 | 치료 부담 (시간·비용 등) (1–3) |
| `maximum_temperature` | 41/42 | 35.7 ~ 37.4 | 피부 표면 최고 온도 (°C) |
| `minimum_temperature` | 41/42 | 22.1 ~ 32.8 | 피부 표면 최저 온도 (°C) |
| `average_temperature` | 41/42 | 32.3 ~ 36 | 피부 표면 평균 온도 (°C) |
| `melanin_right` | 42/42 | 0.439 ~ 0.676 | 멜라닌 지수 |
| `dullness_right` | 42/42 | 0.0227 ~ 0.0825 | 칙칙함 지수 |
| `corneometer_hydration_right_1` | 42/42 | 14.4 ~ 84.7 | 수분 1회차 (Corneometer, 오른쪽 볼) |
| `corneometer_hydration_right_2` | 42/42 | 12 ~ 84.3 | 수분 2회차 |
| `corneometer_hydration_right_3` | 42/42 | 11.9 ~ 78.4 | 수분 3회차 — 3회 평균을 쓰는 것이 안정적 |
| `skintouch_elasticity_right` | 42/42 | 43 ~ 90 | 피부 탄력 (Skintouch) |
| `sebumeter_sebum_rigth` | 42/42 | 0 ~ 87 | 피지 (Sebumeter, 오른쪽 볼). 원본 오타 `rigth` 그대로 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `03_sensitive_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Unassigned`, `g_Staphylococcus`, `g_Delftia`, `g_Rhodanobacter`, `g_Polaribacter`, `g_Pseudomonas`, `g_Lactobacillus` …

## `03_sensitive_ITS_sample_info.tsv` 컬럼 (42행 × 73컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 42/42 | 42종 (예: SRR11604870, SRR11604871, SRR11604872 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 42/42 | PRJNA627798 | BioProject accession |
| `sample_id` | 42/42 | 42종 (예: Non.03_fun, Non.19_fun, Non.28_fun …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 42/42 | 42종 (예: Non.03, Non.19, Non.28 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 42/42 | Right cheek | 채취 부위 |
| `assay` | 42/42 | ITS | 마커 종류 |
| `region` | 42/42 | ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 42/42 | Non-sensitive / Sensitive | 비교군 라벨 |
| `group_type` | 42/42 | skin_sensitivity | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 42/42 | 22 ~ 52 | 나이 (세) |
| `age_group` | 0/42 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 42/42 | female | 성별 |
| `read_count` | 42/42 | 7572 ~ 542815 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 42/42 | 16 ~ 191 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 42/42 | 0.516707 ~ 3.95695 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 42/42 | 0.181507 ~ 0.958582 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 42/42 | 1.22176 ~ 24.1438 | 역 Simpson 지수 |
| `read_depth_final` | 42/42 | 4527 ~ 361037 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 42/42 | Unassigned / g__Lasiobolus / g__Malassezia | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 42/42 | 17.06 ~ 99.69 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 42/42 | 12 ~ 43 | 검출된 속의 개수 (리드 1개 이상) |
| `perceived_skin_type` | 42/42 | Combination / Dry / Dry (severe) / Normal / Oil | 자각 피부타입 (Dry / Combination / Normal / Oil) |
| `perceived_facial_skin_thickness` | 42/42 | 1 / 2 / 3 | 자각 피부 두께 (1–3) |
| `perceived_skin_pores` | 42/42 | 1 / 2 / 3 / 4 | 자각 모공 크기 (1–4) |
| `degree_of_pimple_or_acne` | 42/42 | 1 / 2 / 3 | 자각 여드름 정도 (1–3) |
| `skin_trouble_1st_rank` | 42/42 | 11종 (예: Blackhead/Whitehead, Dry skin, Enlarged pores …) | 가장 신경 쓰이는 피부 고민 1순위 |
| `skin_trouble_2nd_rank` | 42/42 | 12종 (예: Blackhead/Whitehead, Dark circles, Dry skin …) | 피부 고민 2순위 |
| `skin_trouble_3rd_rank` | 42/42 | 11종 (예: Blackhead/Whitehead, Dark circles, Dry skin …) | 피부 고민 3순위 |
| `perceived_skin_sensitivity` | 42/42 | 1 ~ 7 | **자각 민감도 (1–7)** — 군 라벨보다 세밀한 연속값 |
| `sensitive_skin_cognitive_cause` | 20/42 | 11종 (예: Affect of childbirth, After starting makeup, After starting makeup/In-between seasons …) | 민감성을 느끼게 된 계기 (자유응답) |
| `recognizing_truble_when_using_cosmetics` | 42/42 | 1 / 2 / 3 | 화장품 사용 시 트러블 인지 (1–3). 원본 오타 `truble` |
| `experience_of_sun_allergy_inflammation_burn` | 42/42 | 1 / 2 / 3 | 햇빛 알레르기·염증·화상 경험 (1–3) |
| `experience_of_skin_allergy` | 42/42 | 1 / 2 / 3 | 피부 알레르기 경험 (1–3) |
| `recognition_of_skin_condition_change` | 42/42 | 1 / 2 / 3 | 피부 상태 변화 인지 (1–3) |
| `unpleasant_sensation_on_skin` | 42/42 | 1 / 2 / 3 | 피부 불쾌감 (1–3) |
| `embarrassment_due_to_skin_problems` | 42/42 | 1 / 2 / 3 / 4 | 피부 문제로 인한 당혹감 (1–4) |
| `difficylties_in_daily_life_due_to_skin_probl` | 42/42 | 1 / 2 / 3 | 일상생활 어려움 (1–3). 원본 오타 `difficylties` |
| `effects_of_skin_problems_when_choosing_cloth` | 42/42 | 1 / 2 / 3 / 4 | 옷 선택에 미치는 영향 (1–4) |
| `effects_of_skin_problems_on_social_life_and_` | 42/42 | 1 / 2 / 3 | 사회생활·여가에 미치는 영향 (1–3) |
| `effects_of_skin_problems_on_work_or_study` | 37/42 | No / Yes | 업무·학업에 미치는 영향 (Yes/No) — 이 항목만 형식이 다름 |
| `effects_of_skin_problems_on_human_relationsh` | 42/42 | 1 / 2 / 3 | 대인관계에 미치는 영향 (1–3) |
| `skin_treatment_problems_time_cost_etc` | 42/42 | 1 / 2 / 3 | 치료 부담 (시간·비용 등) (1–3) |
| `maximum_temperature` | 41/42 | 35.7 ~ 37.4 | 피부 표면 최고 온도 (°C) |
| `minimum_temperature` | 41/42 | 22.1 ~ 32.8 | 피부 표면 최저 온도 (°C) |
| `average_temperature` | 41/42 | 32.3 ~ 36 | 피부 표면 평균 온도 (°C) |
| `melanin_right` | 42/42 | 0.439 ~ 0.676 | 멜라닌 지수 |
| `dullness_right` | 42/42 | 0.0227 ~ 0.0825 | 칙칙함 지수 |
| `corneometer_hydration_right_1` | 42/42 | 14.4 ~ 84.7 | 수분 1회차 (Corneometer, 오른쪽 볼) |
| `corneometer_hydration_right_2` | 42/42 | 12 ~ 84.3 | 수분 2회차 |
| `corneometer_hydration_right_3` | 42/42 | 11.9 ~ 78.4 | 수분 3회차 — 3회 평균을 쓰는 것이 안정적 |
| `skintouch_elasticity_right` | 42/42 | 43 ~ 90 | 피부 탄력 (Skintouch) |
| `sebumeter_sebum_rigth` | 42/42 | 0 ~ 87 | 피지 (Sebumeter, 오른쪽 볼). 원본 오타 `rigth` 그대로 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `03_sensitive_ITS_genus_pct.tsv`를 쓴다.

우점 속: `g_g__Malassezia`, `g_Unassigned`, `g_g__Lasiobolus`, `g_g__Cercozoa_gen_Incertae_sedis`, `g_g__Cladosporium`, `g_g__Enterocarpus`, `g_g__Mucor`, `g_g__Rhodotorula` …

## `metadata/clinical_data/03_sensitive_clinical.tsv` (42행 × 35컬럼)

**출처**: Table S2 (xlsx) · EuropePMC supplementaryFiles

⚠ **두 파일의 `sample_id` 표기가 다르다.** sample_info는 `Non.03_bac`처럼 마커 접미사가 붙어 있고, 이 표는 `Non.03`이다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`subject`**, 이 표에서 **`sample_id`** 다.

- `03_sensitive_16S`: 42행과 매칭
- `03_sensitive_ITS`: 42행과 매칭

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 42/42 | 42종 (예: Non.03, Non.19, Non.28 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `paper_sample_id` | 42/42 | 42종 (예: NS.03, NS.19, NS.28 …) | 논문 표기 샘플 ID (데이터 표기와 다를 수 있음) |
| `group` | 42/42 | Non-sensitive / Sensitive | 비교군 라벨 |
| `perceived_skin_type` | 42/42 | Combination / Dry / Dry (severe) / Normal / Oil | 자각 피부타입 (Dry / Combination / Normal / Oil) |
| `perceived_facial_skin_thickness` | 42/42 | 1 / 2 / 3 | 자각 피부 두께 (1–3) |
| `perceived_skin_pores` | 42/42 | 1 / 2 / 3 / 4 | 자각 모공 크기 (1–4) |
| `degree_of_pimple_or_acne` | 42/42 | 1 / 2 / 3 | 자각 여드름 정도 (1–3) |
| `skin_trouble_1st_rank` | 42/42 | 11종 (예: Blackhead/Whitehead, Dry skin, Enlarged pores …) | 가장 신경 쓰이는 피부 고민 1순위 |
| `skin_trouble_2nd_rank` | 42/42 | 12종 (예: Blackhead/Whitehead, Dark circles, Dry skin …) | 피부 고민 2순위 |
| `skin_trouble_3rd_rank` | 42/42 | 11종 (예: Blackhead/Whitehead, Dark circles, Dry skin …) | 피부 고민 3순위 |
| `perceived_skin_sensitivity` | 42/42 | 1 ~ 7 | **자각 민감도 (1–7)** — 군 라벨보다 세밀한 연속값 |
| `sensitive_skin_cognitive_cause` | 20/42 | 11종 (예: Affect of childbirth, After starting makeup, After starting makeup/In-between seasons …) | 민감성을 느끼게 된 계기 (자유응답) |
| `recognizing_truble_when_using_cosmetics` | 42/42 | 1 / 2 / 3 | 화장품 사용 시 트러블 인지 (1–3). 원본 오타 `truble` |
| `experience_of_sun_allergy_inflammation_burn` | 42/42 | 1 / 2 / 3 | 햇빛 알레르기·염증·화상 경험 (1–3) |
| `experience_of_skin_allergy` | 42/42 | 1 / 2 / 3 | 피부 알레르기 경험 (1–3) |
| `recognition_of_skin_condition_change` | 42/42 | 1 / 2 / 3 | 피부 상태 변화 인지 (1–3) |
| `unpleasant_sensation_on_skin` | 42/42 | 1 / 2 / 3 | 피부 불쾌감 (1–3) |
| `embarrassment_due_to_skin_problems` | 42/42 | 1 / 2 / 3 / 4 | 피부 문제로 인한 당혹감 (1–4) |
| `difficylties_in_daily_life_due_to_skin_probl` | 42/42 | 1 / 2 / 3 | 일상생활 어려움 (1–3). 원본 오타 `difficylties` |
| `effects_of_skin_problems_when_choosing_cloth` | 42/42 | 1 / 2 / 3 / 4 | 옷 선택에 미치는 영향 (1–4) |
| `effects_of_skin_problems_on_social_life_and_` | 42/42 | 1 / 2 / 3 | 사회생활·여가에 미치는 영향 (1–3) |
| `effects_of_skin_problems_on_work_or_study` | 37/42 | No / Yes | 업무·학업에 미치는 영향 (Yes/No) — 이 항목만 형식이 다름 |
| `effects_of_skin_problems_on_human_relationsh` | 42/42 | 1 / 2 / 3 | 대인관계에 미치는 영향 (1–3) |
| `skin_treatment_problems_time_cost_etc` | 42/42 | 1 / 2 / 3 | 치료 부담 (시간·비용 등) (1–3) |
| `maximum_temperature` | 41/42 | 35.7 ~ 37.4 | 피부 표면 최고 온도 (°C) |
| `minimum_temperature` | 41/42 | 22.1 ~ 32.8 | 피부 표면 최저 온도 (°C) |
| `average_temperature` | 41/42 | 32.3 ~ 36 | 피부 표면 평균 온도 (°C) |
| `melanin_right` | 42/42 | 0.439 ~ 0.676 | 멜라닌 지수 |
| `dullness_right` | 42/42 | 0.0227 ~ 0.0825 | 칙칙함 지수 |
| `corneometer_hydration_right_1` | 42/42 | 14.4 ~ 84.7 | 수분 1회차 (Corneometer, 오른쪽 볼) |
| `corneometer_hydration_right_2` | 42/42 | 12 ~ 84.3 | 수분 2회차 |
| `corneometer_hydration_right_3` | 42/42 | 11.9 ~ 78.4 | 수분 3회차 — 3회 평균을 쓰는 것이 안정적 |
| `skintouch_elasticity_right` | 42/42 | 43 ~ 90 | 피부 탄력 (Skintouch) |
| `sebumeter_sebum_rigth` | 42/42 | 0 ~ 87 | 피지 (Sebumeter, 오른쪽 볼). 원본 오타 `rigth` 그대로 |
| `age` | 42/42 | 22 ~ 52 | 나이 (세) |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
