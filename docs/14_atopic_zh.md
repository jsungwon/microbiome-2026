# 14_atopic_zh — 아토피 종단 (취리히)

> *Skin microbiome and mycobiome of atopic dermatitis patients (Zurich cohort)*  
> 미게재 데이터셋 (ENA PRJEB44392) · doi:

## 연구 설계

- **코호트**: 스위스 성인 32명 · 아토피 / 건강 대조 · 취리히대학병원
- **채취 부위**: 팔오금 · 목뒤 · 미간 · 정수리 4부위 — 병변/비병변 구분 · t1/t2/t3 종단
- **마커**: 16S V1–V3 (27F–534R) + ITS1 · 한 프로젝트에 두 마커

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `14_atopic_zh_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `14_atopic_zh_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `14_atopic_zh_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `14_atopic_zh_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `14_atopic_zh_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `14_atopic_zh_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `14_atopic_zh_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `14_atopic_zh_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `14_atopic_zh_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `14_atopic_zh_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `14_atopic_zh_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `14_atopic_zh_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `14_atopic_zh_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `14_atopic_zh_16S_sample_info.tsv` 컬럼 (322행 × 49컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 322/322 | 322종 (예: ERR6650268, ERR6650269, ERR6650270 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 322/322 | PRJEB44392_16S | BioProject accession |
| `sample_id` | 322/322 | 322종 (예: B04, B05, B06 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 320/322 | 32종 (예: HC1, HC10, HC11 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 320/322 | Antecubital / Dorsal neck / Glabella / Vertex | 채취 부위 |
| `assay` | 322/322 | 16S | 마커 종류 |
| `region` | 322/322 | V1-V3 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 322/322 | Atopic dermatitis / Atopic dermatitis lesional / Atopic dermatitis non-lesional / Healthy | 비교군 라벨 |
| `group_type` | 322/322 | atopic_dermatitis | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/322 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/322 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 320/322 | F / M | 성별 |
| `read_count` | 322/322 | 21314 ~ 371540 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 322/322 | 13 ~ 389 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 322/322 | 0.433236 ~ 5.18474 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 322/322 | 0.137415 ~ 0.987731 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 322/322 | 1.15931 ~ 81.505 | 역 Simpson 지수 |
| `read_depth_final` | 322/322 | 1242 ~ 132107 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 322/322 | 8종 (예: Brevundimonas, Chryseobacterium, Corynebacterium …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 322/322 | 15 ~ 97.58 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 322/322 | 22 ~ 323 | 검출된 속의 개수 (리드 1개 이상) |
| `scorad` | 320/322 | 0 ~ 79.1 | **SCORAD** — 아토피 중증도 종합점수(0~103). **이 저장소에서 유일한 연속형 중증도**라 군 비교가 아니라 회귀·상관 분석을 할 수 있다 |
| `ad_severity` | 320/322 | HC / mild to moderate AD / severe AD | 중증도 범주 (mild to moderate AD / severe AD / HC) |
| `skin_condition` | 319/322 | Healthy / Lesion / Unaffected | 채취 피부 상태 (Lesion 병변 / Unaffected 비병변 / Healthy 건강) |
| `sampling_season` | 320/322 | autumn / spring / summer / winter | 채취 계절 (spring/summer/autumn/winter). 피부 미생물은 계절을 탄다 |
| `dupilumab` | 192/322 | no / yes | **두필루맙(생물학제제) 치료 여부** (yes/no). 치료가 미생물총을 바꾸므로 교란변수로 다룰 것 |
| `subject_plot` | 320/322 | 32종 (예: HC1, HC10, HC11 …) | 논문 그림에 쓰인 피험자 라벨 (HC1, AD3 …) |
| `author_discard` | 2/322 | yes | **저자가 제외 표시한 샘플** (`yes`). 분석에서 빼는 것을 권한다 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `14_atopic_zh_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Staphylococcus`, `g_Cutibacterium`, `g_Corynebacterium`, `g_Unassigned`, `g_Streptococcus`, `g_Enhydrobacter`, `g_Pseudomonas`, `g_Anaerococcus` …

## `14_atopic_zh_ITS_sample_info.tsv` 컬럼 (321행 × 47컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 321/321 | 321종 (예: ERR6650592, ERR6650593, ERR6650594 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 321/321 | PRJEB44392_ITS | BioProject accession |
| `sample_id` | 321/321 | 321종 (예: A02, A03, A04 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 0/321 | (전부 빈 칸) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 320/321 | Antecubital / Dorsal neck / Glabella / Vertex | 채취 부위 |
| `assay` | 321/321 | ITS | 마커 종류 |
| `region` | 321/321 | ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 321/321 | Atopic dermatitis / Atopic dermatitis lesional / Atopic dermatitis non-lesional / Healthy | 비교군 라벨 |
| `group_type` | 321/321 | atopic_dermatitis | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/321 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/321 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 320/321 | F / M | 성별 |
| `read_count` | 321/321 | 7082 ~ 359052 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 321/321 | 6 ~ 160 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 321/321 | 0.225055 ~ 4.14407 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 321/321 | 0.0809575 ~ 0.969484 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 321/321 | 1.08809 ~ 32.7696 | 역 Simpson 지수 |
| `read_depth_final` | 321/321 | 1786 ~ 117377 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 321/321 | 8종 (예: g__Ampelomyces, g__Aureobasidium, g__Candida …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 321/321 | 24.47 ~ 100 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 321/321 | 1 ~ 108 | 검출된 속의 개수 (리드 1개 이상) |
| `scorad` | 320/321 | 0 ~ 79.1 | **SCORAD** — 아토피 중증도 종합점수(0~103). **이 저장소에서 유일한 연속형 중증도**라 군 비교가 아니라 회귀·상관 분석을 할 수 있다 |
| `ad_severity` | 320/321 | HC / mild to moderate AD / severe AD | 중증도 범주 (mild to moderate AD / severe AD / HC) |
| `skin_condition` | 318/321 | Healthy / Lesion / Unaffected | 채취 피부 상태 (Lesion 병변 / Unaffected 비병변 / Healthy 건강) |
| `sampling_season` | 320/321 | autumn / spring / summer / winter | 채취 계절 (spring/summer/autumn/winter). 피부 미생물은 계절을 탄다 |
| `dupilumab` | 192/321 | no / yes | **두필루맙(생물학제제) 치료 여부** (yes/no). 치료가 미생물총을 바꾸므로 교란변수로 다룰 것 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `14_atopic_zh_ITS_genus_pct.tsv`를 쓴다.

우점 속: `g_g__Malassezia`, `g_g__Debaryomyces`, `g_Unassigned`, `g_g__Candida`, `g_g__Penicillium`, `g_g__Aureobasidium`, `g_g__Filobasidium`, `g_g__Rhodotorula` …

## 임상 데이터 — 없음

이 저장소에서 **임상정보가 가장 풍부한 스터디**다. 논문 없이 BioSample 만으로 완성된다:

| 변수 | 채움 | 값 |
|---|---|---|
| `scorad` | 641/652 | **연속형 중증도 0–76.1 (45단계)** |
| `skin condition` | 637/652 | 병변 / 비병변 / 건강 |
| `location` | 640/652 | 팔오금·목뒤·미간·정수리 |
| `visit new` | 640/652 | t1 / t2 / t3 종단 |
| `sampling season` | 640/652 | 봄·여름·가을·겨울 |
| `dupilumab` | 384/652 | 생물학제제 치료 여부 |

**SCORAD 가 연속형**이라 군 비교가 아니라 회귀·상관 분석을 할 수 있다. 이런 데이터는 이 저장소에서 여기뿐이다.

⚠ `discard=yes` 5건은 저자가 제외 표시한 샘플이다(note 에 남겨 뒀다). 16S 와 ITS 가 한 프로젝트에 섞여 있어 BioSample 의 `environmental package` 로 325/327 로 나눴다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
