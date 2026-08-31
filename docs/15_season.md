# 15_season — 사계절 가구 코호트

> *Individual and household attributes influence the dynamics of the personal skin microbiota / Neutral Processes Drive Seasonal Assembly of the Skin Mycobiome*  
> Microbiome 6:26 (2018) · mSystems 4:e00004-19 (2019) · doi:10.1186/s40168-018-0412-9

## 연구 설계

- **코호트**: 홍콩 성인 24명 · 가구 단위 모집 · 중국계
- **채취 부위**: 이마 · 좌우 팔뚝 · 좌우 손바닥 — 같은 사람을 **4계절 반복** 측정
- **마커**: 16S V4 (515F, 단일말단) + ITS1 · **음성대조 5건 포함**

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `15_season_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `15_season_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `15_season_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `15_season_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `15_season_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `15_season_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `15_season_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `15_season_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `15_season_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `15_season_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `15_season_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `15_season_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `15_season_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `15_season_16S_sample_info.tsv` 컬럼 (483행 × 47컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 483/483 | 483종 (예: SRR5709174, SRR5709175, SRR5709176 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 483/483 | PRJNA390040 | BioProject accession |
| `sample_id` | 483/483 | 483종 (예: ADMa3zFOHAUT, ADMa3zFOHSPR, ADMa3zFOHSUM …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 479/483 | 24종 (예: ADMa3z, FH3z, HFC3z …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 483/483 | 6종 (예: Forehead, Left Forearm, Left Palm …) | 채취 부위 |
| `assay` | 483/483 | 16S | 마커 종류 |
| `region` | 483/483 | V4 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 483/483 | Household cohort / 음성대조 | 비교군 라벨 |
| `group_type` | 483/483 | season_household | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/483 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/483 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/483 | (전부 빈 칸) | 성별 |
| `read_count` | 483/483 | 3694 ~ 170454 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 483/483 | 81 ~ 498 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 483/483 | 1.56055 ~ 5.27903 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 483/483 | 0.552375 ~ 0.9885 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 483/483 | 2.23401 ~ 86.9574 | 역 Simpson 지수 |
| `read_depth_final` | 483/483 | 1664 ~ 76166 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 483/483 | 28종 (예: Acinetobacter, Alkanindiges, Brevundimonas …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 483/483 | 8.21 ~ 79.19 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 483/483 | 79 ~ 396 | 검출된 속의 개수 (리드 1개 이상) |
| `collection_date` | 483/483 | 2014-01 / 2014-04 / 2014-08 / 2014-11 | 채취일 (BioSample 기록). 계절·배치 효과를 볼 때 쓴다 |
| `household` | 479/483 | 11종 (예: ADMa, FH, HFC …) | 가구 코드. 같은 가구 구성원은 미생물총이 닮으므로 **독립 표본이 아니다** |
| `dominant_hand` | 479/483 | left / right | 주로 쓰는 손 (left/right). 손바닥 시료 해석에 쓴다 |
| `ethnicity` | 479/483 | Chinese | 민족 (Chinese 등) |
| `urban_rural` | 483/483 | Urban/Rural / swab_control_1 / swab_control_2 / swab_control_3 / swab_control_4 | 거주 환경 구분 (Urban/Rural). 음성대조는 `swab_control_*`로 표시된다 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `15_season_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Unassigned`, `g_Cutibacterium`, `g_Acinetobacter`, `g_Halomonas`, `g_Staphylococcus`, `g_Enhydrobacter`, `g_Streptococcus`, `g_Micrococcus` …

## `15_season_ITS_sample_info.tsv` 컬럼 (474행 × 44컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 474/474 | 474종 (예: SRR6360565, SRR6360566, SRR6360567 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 474/474 | PRJNA421247 | BioProject accession |
| `sample_id` | 474/474 | 474종 (예: ADMA3zFOHWINT, ADMA3zLFWINT, ADMA3zLPWINT …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 473/474 | 24종 (예: ADMA3Z, FH3Z, HFC3Z …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 474/474 | 6종 (예: Forehead, Left Forearm, Left Palm …) | 채취 부위 |
| `assay` | 474/474 | ITS | 마커 종류 |
| `region` | 474/474 | ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 474/474 | Household cohort / 음성대조 | 비교군 라벨 |
| `group_type` | 474/474 | season_household | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/474 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/474 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/474 | (전부 빈 칸) | 성별 |
| `read_count` | 474/474 | 1839 ~ 198755 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 474/474 | 4 ~ 159 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 474/474 | 0.0367087 ~ 4.11097 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 474/474 | 0.00954007 ~ 0.974939 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 474/474 | 1.00963 ~ 39.903 | 역 Simpson 지수 |
| `read_depth_final` | 474/474 | 1045 ~ 150868 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 474/474 | 22종 (예: g__Allium, g__Aspergillus, g__Aureobasidium …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 474/474 | 15.06 ~ 99.96 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 474/474 | 3 ~ 117 | 검출된 속의 개수 (리드 1개 이상) |
| `collection_date` | 474/474 | 45종 (예: 2014, 2014-01-07, 2014-01-09 …) | 채취일 (BioSample 기록). 계절·배치 효과를 볼 때 쓴다 |
| `isolation_source` | 474/474 | 474종 (예: ADMA 3Z Forehead Autumn, ADMA 3Z Forehead Spring, ADMA 3Z Forehead Summer …) | BioSample의 채취원 문자열. 15번 진균은 `ADMA 3Z Forehead Winter`처럼 가구·구성원·부위·계절이 한 문자열에 들어 있다 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `15_season_ITS_genus_pct.tsv`를 쓴다.

우점 속: `g_g__Malassezia`, `g_g__Candida`, `g_Unassigned`, `g_g__Cladosporium`, `g_g__Brassica`, `g_g__Aspergillus`, `g_g__Cutaneotrichosporon`, `g_g__Manihot` …

## 임상 데이터 — 없음

같은 사람을 **4계절 반복** 측정한 드문 설계다. 가구 단위로 모집해서 `가구 > 개인 > 부위 > 계절` 4축으로 분산을 나눌 수 있다.

BioSample 에 `host_subject_id`·`dominant_hand`(주손)·`ethnicity`·도농 구분이 있고, 논문 보충표(Leung 2018 MOESM18)에는 484샘플 전부의 연령군·성별·채취일이, Tong 2019 Table S2 에는 **채취 시점의 기온·습도**가 있다.

✅ **음성대조 5건이 들어 있다**(세균 4 + 진균 1). 이 저장소의 다른 스터디에는 음성대조가 없어 오염 판정을 심도 상관 같은 약한 근사로만 했는데, 여기서는 `decontam` 의 prevalence 방법을 제대로 쓸 수 있다.

⚠ 세균 쪽은 한 파일에 정방향(515F)과 역방향(806R) 리드가 반반 섞여 있다. 두 방향이 V4 의 서로 다른 구간을 덮어 같은 균이 두 ASV 로 갈라지므로 정방향만 남겼다 — 통과율 ~50%는 손실이 아니라 의도된 선택이다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
