# 02_healthy — 건강한 한국인

> *Taxonomic profiling of skin microbiome and correlation with clinical skin parameters in healthy Koreans*  
> Sci Rep 11:16269 (2021) · doi:10.1038/s41598-021-95734-9

## 연구 설계

- **코호트**: 건강한 한국인 51명 · 젊은군 21–36세 25명 / 고령군 49–67세 26명 · 남 25 / 여 26
- **채취 부위**: 볼 · 이마 — 같은 사람의 두 부위 (개체 내 짝 비교 가능)
- **마커**: 16S V3–V4 (341F–805R)

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `02_healthy_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `02_healthy_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `02_healthy_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `02_healthy_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `02_healthy_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `02_healthy_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `02_healthy_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `02_healthy_16S_sample_info.tsv` 컬럼 (102행 × 62컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 102/102 | 102종 (예: SRR14277118, SRR14277119, SRR14277120 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 102/102 | PRJNA723064 | BioProject accession |
| `sample_id` | 102/102 | 102종 (예: OC1, OC10, OC11 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 102/102 | 51종 (예: O1, O10, O11 …) | 피험자 식별자. 같은 사람의 여러 부위를 묶는 키 |
| `body_site` | 102/102 | Cheek / Forehead | 채취 부위 |
| `assay` | 102/102 | 16S | 마커 종류 |
| `region` | 102/102 | V3-V4 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 102/102 | O / Y | 비교군 라벨 |
| `group_type` | 102/102 | age | group이 무슨 축인지 (age / sensitivity / acne) |
| `age` | 102/102 | 21 ~ 67 | 나이 (세) |
| `age_group` | 102/102 | Old(49-67) / Young(21-36) | 연령군 코드 |
| `sex` | 102/102 | female / male | 성별 |
| `read_count` | 102/102 | 29104 ~ 144363 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 102/102 | 23 ~ 561 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 102/102 | 0.296184 ~ 4.82913 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 102/102 | 0.0761183 ~ 0.984224 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 102/102 | 1.08239 ~ 63.3858 | 역 Simpson 지수 |
| `read_depth_final` | 102/102 | 17755 ~ 81508 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 102/102 | 8종 (예: Corynebacterium, Cutibacterium, Elizabethkingia …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 102/102 | 12.31 ~ 96.44 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 102/102 | 13 ~ 187 | 검출된 속의 개수 (리드 1개 이상) |
| `skin_type` | 102/102 | 1 / 2 / 3 / 4 | 피부타입 1–4 (건성→복합성) |
| `irritation_environment` | 102/102 | No / Yes | 환경에 의한 피부 자극 경험 (Yes/No) |
| `irritation_cosmetics` | 102/102 | No / Yes | 화장품에 의한 피부 자극 경험 (Yes/No) |
| `cosmetic_side_effects` | 102/102 | No / Yes | 화장품 부작용 경험 (Yes/No) |
| `sunscreen_use` | 102/102 | 1 / 2 / 3 | 자외선차단제 사용 빈도 (1–3) |
| `moisture_AU` | 102/102 | 20.8333 ~ 88.7 | 피부 수분 (Corneometer, AU) · 부위별 값 |
| `TEWL_g_m2h` | 102/102 | 6.2 ~ 59 | 경피수분손실 (g/m²h) · 부위별 값 |
| `redness_a` | 102/102 | 5.66 ~ 17.17 | 홍조 (a* 값) · 부위별 |
| `skin_tone_mean` | 102/102 | 148.922 ~ 225.87 | 피부톤 평균 (VISIA) · 부위별 |
| `skin_tone_sd` | 102/102 | 3.06 ~ 18.3616 | 피부톤 표준편차 · 부위별 |
| `sebum_ug_cm2` | 51/102 | 18 ~ 213 | 피지 (µg/cm²) · **이마에서만 측정** — 볼 행은 빈 칸 |
| `mole_amount` | 51/102 | 63 ~ 334 | 점 개수 · **볼에서만 측정** |
| `uv_spot_n` | 51/102 | 5 ~ 663 | UV 반점 수 · **볼에서만 측정** |
| `brown_spot_n` | 51/102 | 250 ~ 714 | 갈색 반점 수 · **볼에서만 측정** |
| `porphyrin_amount` | 51/102 | 68 ~ 5593 | 포르피린 양 · **볼에서만 측정** |
| `texture_Ra_um` | 102/102 | 13.6 ~ 44.4 | 거칠기 Ra (µm, PRIMOS) · 얼굴 단위 |
| `texture_Rmax_um` | 102/102 | 41.7 ~ 327.9 | 거칠기 Rmax (µm) |
| `wrinkle_depth_um` | 102/102 | 25 ~ 137 | 눈가주름 평균 깊이 (µm) |
| `wrinkle_volume_mm3` | 102/102 | 0.4 ~ 7.1 | 눈가주름 부피 (mm³) |
| `wrinkle_area_mm2` | 102/102 | 15.97 ~ 56.36 | 눈가주름 면적 (mm²) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `02_healthy_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Staphylococcus`, `g_Unassigned`, `g_Lawsonella`, `g_Corynebacterium`, `g_Enhydrobacter`, `g_Streptococcus`, `g_Xanthomonas` …

## `metadata/clinical_data/02_healthy_clinical.tsv` (102행 × 26컬럼)

**출처**: Supplementary Data 1(설문) + 2(생물물리) (xlsx) · Springer ESM

논문 피험자 ID `1902-003-007`을 BioSample 이름 `YC7`에 대응시켰다. `-003-`=젊은군 / `-004-`=고령군 + 피험자 번호이며, BioSample 채취일로 102/102 일치를 확인했다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`sample_id`**, 이 표에서 **`sample_id`** 다.

- `02_healthy_16S`: 102행과 매칭

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 102/102 | 102종 (예: OC1, OC10, OC11 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `paper_subject_id` | 102/102 | 51종 (예: 1902-003-001, 1902-003-002, 1902-003-003 …) | 논문 표기 피험자 ID (`{연월}-{003=젊은군|004=고령군}-{번호}`) |
| `group` | 102/102 | O / Y | 비교군 라벨 |
| `body_site` | 102/102 | Cheek / Forehead | 채취 부위 |
| `sex` | 102/102 | female / male | 성별 |
| `age` | 102/102 | 21 ~ 67 | 나이 (세) |
| `skin_type` | 102/102 | 1 / 2 / 3 / 4 | 피부타입 1–4 (건성→복합성) |
| `irritation_environment` | 102/102 | No / Yes | 환경에 의한 피부 자극 경험 (Yes/No) |
| `irritation_cosmetics` | 102/102 | No / Yes | 화장품에 의한 피부 자극 경험 (Yes/No) |
| `cosmetic_side_effects` | 102/102 | No / Yes | 화장품 부작용 경험 (Yes/No) |
| `sunscreen_use` | 102/102 | 1 / 2 / 3 | 자외선차단제 사용 빈도 (1–3) |
| `moisture_AU` | 102/102 | 20.8333 ~ 88.7 | 피부 수분 (Corneometer, AU) · 부위별 값 |
| `TEWL_g_m2h` | 102/102 | 6.2 ~ 59 | 경피수분손실 (g/m²h) · 부위별 값 |
| `redness_a` | 102/102 | 5.66 ~ 17.17 | 홍조 (a* 값) · 부위별 |
| `skin_tone_mean` | 102/102 | 148.922 ~ 225.87 | 피부톤 평균 (VISIA) · 부위별 |
| `skin_tone_sd` | 102/102 | 3.06 ~ 18.3616 | 피부톤 표준편차 · 부위별 |
| `sebum_ug_cm2` | 51/102 | 18 ~ 213 | 피지 (µg/cm²) · **이마에서만 측정** — 볼 행은 빈 칸 |
| `mole_amount` | 51/102 | 63 ~ 334 | 점 개수 · **볼에서만 측정** |
| `uv_spot_n` | 51/102 | 5 ~ 663 | UV 반점 수 · **볼에서만 측정** |
| `brown_spot_n` | 51/102 | 250 ~ 714 | 갈색 반점 수 · **볼에서만 측정** |
| `porphyrin_amount` | 51/102 | 68 ~ 5593 | 포르피린 양 · **볼에서만 측정** |
| `texture_Ra_um` | 102/102 | 13.6 ~ 44.4 | 거칠기 Ra (µm, PRIMOS) · 얼굴 단위 |
| `texture_Rmax_um` | 102/102 | 41.7 ~ 327.9 | 거칠기 Rmax (µm) |
| `wrinkle_depth_um` | 102/102 | 25 ~ 137 | 눈가주름 평균 깊이 (µm) |
| `wrinkle_volume_mm3` | 102/102 | 0.4 ~ 7.1 | 눈가주름 부피 (mm³) |
| `wrinkle_area_mm2` | 102/102 | 15.97 ~ 56.36 | 눈가주름 면적 (mm²) |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
