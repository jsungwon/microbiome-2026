# 01_aging — 노화

> *Aged related human skin microbiome and mycobiome in Korean women*  
> Sci Rep 12:2500 (2022) · doi:10.1038/s41598-022-06189-5

## 연구 설계

- **코호트**: 한국인 여성 61명 · 젊은군 19–28세 29명 / 고령군 60–63세 32명
- **채취 부위**: 볼(Ca) · 이마(Fa) — 부위별로 서로 다른 피험자
- **마커**: 16S V4–V5 (518F–926R) + ITS1 · 한 run에 두 앰플리콘 혼재

## 이 스터디의 파일

각 파일이 어떻게 생겼는지는 `figures/` 의 표 스크린샷 7장으로 볼 수 있다
(이 스터디를 예제로 만든 것이다 — `figures/README.md`).


| 파일 | 위치 | 내용 |
|---|---|---|
| `01_aging_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `01_aging_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `01_aging_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `01_aging_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `01_aging_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `01_aging_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `01_aging_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `01_aging_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `01_aging_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `01_aging_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `01_aging_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `01_aging_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `01_aging_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `01_aging_16S_sample_info.tsv` 컬럼 (55행 × 56컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 55/55 | 55종 (예: SRR11426354, SRR11426355, SRR11426356 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 55/55 | PRJNA614620 | BioProject accession |
| `sample_id` | 55/55 | 55종 (예: Ca.10R, Ca.12R, Ca.13R …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 55/55 | 55종 (예: Ca.10R, Ca.12R, Ca.13R …) | 피험자 식별자. 같은 사람의 여러 부위를 묶는 키 |
| `body_site` | 55/55 | Cheek / Forehead | 채취 부위 |
| `assay` | 55/55 | 16S+ITS_pooled | 마커 종류 |
| `region` | 55/55 | V4-V5+ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 55/55 | O / Y | 비교군 라벨 |
| `group_type` | 55/55 | age | group이 무슨 축인지 (age / sensitivity / acne) |
| `age` | 55/55 | 19 ~ 63 | 나이 (세) |
| `age_group` | 55/55 | O / Y | 연령군 코드 |
| `sex` | 55/55 | female | 성별 |
| `read_count` | 55/55 | 5748 ~ 245516 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 55/55 | 13 ~ 187 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 55/55 | 0.255316 ~ 3.95646 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 55/55 | 0.0920702 ~ 0.960534 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 55/55 | 1.10141 ~ 25.338 | 역 Simpson 지수 |
| `read_depth_final` | 55/55 | 1173 ~ 123957 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 55/55 | 6종 (예: Burkholderia-Caballeronia-Paraburkholderia, Cutibacterium, Micrococcus …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 55/55 | 13.16 ~ 98.89 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 55/55 | 27 ~ 186 | 검출된 속의 개수 (리드 1개 이상) |
| `paper_id` | 55/55 | 55종 (예: C1, C10, C11 …) | 논문 보충표의 샘플 번호 |
| `moisture` | 55/55 | 49.4 ~ 74 | 피부 수분 (Corneometer, AU) |
| `sebum` | 55/55 | 0.5 ~ 94.5 | 피지 (Sebumeter) |
| `pH` | 55/55 | 4.295 ~ 6.95 | 피부 표면 pH |
| `TEWL` | 55/55 | 13.25 ~ 33 | 경피수분손실 (g/m²h). 피부 장벽 기능 지표 |
| `shannon_16S` | 47/55 | 1.68592 ~ 6.10923 | **논문이 보고한** 세균 Shannon 값 (우리 `Shannon`과 대조용) |
| `faith_pd_16S` | 47/55 | 22.8463 ~ 84.5084 | 논문이 보고한 세균 Faith's PD |
| `simpson_even_16S` | 47/55 | 0.38002 ~ 0.959419 | 논문이 보고한 세균 Simpson evenness |
| `n_asv_16S` | 47/55 | 72 ~ 529 | 논문이 보고한 세균 ASV 수 |
| `qc_pass_16S` | 55/55 | no / yes | 논문의 세균 분석에 포함됐는지 (yes/no) |
| `shannon_ITS` | 55/55 | 0.674313 ~ 4.66884 | **논문이 보고한** 진균 Shannon 값 |
| `simpson_even_ITS` | 55/55 | 0.169478 ~ 0.90264 | 논문이 보고한 진균 Simpson evenness |
| `n_asv_ITS` | 55/55 | 7 ~ 103 | 논문이 보고한 진균 ASV 수 |
| `qc_pass_ITS` | 55/55 | yes | 논문의 진균 분석에 포함됐는지 (yes/no) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `01_aging_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Burkholderia-Caballeronia-Paraburkholderia`, `g_Staphylococcus`, `g_Unassigned`, `g_Streptococcus`, `g_Corynebacterium`, `g_Enhydrobacter`, `g_Brevundimonas` …

## `01_aging_ITS_sample_info.tsv` 컬럼 (58행 × 56컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 58/58 | 58종 (예: SRR11426354, SRR11426355, SRR11426356 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 58/58 | PRJNA614620 | BioProject accession |
| `sample_id` | 58/58 | 58종 (예: Ca.10R, Ca.12R, Ca.13R …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 58/58 | 58종 (예: Ca.10R, Ca.12R, Ca.13R …) | 피험자 식별자. 같은 사람의 여러 부위를 묶는 키 |
| `body_site` | 58/58 | Cheek / Forehead | 채취 부위 |
| `assay` | 58/58 | 16S+ITS_pooled | 마커 종류 |
| `region` | 58/58 | V4-V5+ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 58/58 | O / Y | 비교군 라벨 |
| `group_type` | 58/58 | age | group이 무슨 축인지 (age / sensitivity / acne) |
| `age` | 58/58 | 19 ~ 63 | 나이 (세) |
| `age_group` | 58/58 | O / Y | 연령군 코드 |
| `sex` | 58/58 | female | 성별 |
| `read_count` | 58/58 | 3700 ~ 245516 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 58/58 | 22 ~ 121 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 58/58 | 0.323858 ~ 3.2098 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 58/58 | 0.0933485 ~ 0.89271 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 58/58 | 1.10296 ~ 9.32051 | 역 Simpson 지수 |
| `read_depth_final` | 58/58 | 1273 ~ 99416 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 58/58 | g__Lentinula / g__Malassezia | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 58/58 | 39.92 ~ 98.03 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 58/58 | 14 ~ 86 | 검출된 속의 개수 (리드 1개 이상) |
| `paper_id` | 58/58 | 58종 (예: C1, C10, C11 …) | 논문 보충표의 샘플 번호 |
| `moisture` | 58/58 | 49.4 ~ 74 | 피부 수분 (Corneometer, AU) |
| `sebum` | 58/58 | 0.5 ~ 94.5 | 피지 (Sebumeter) |
| `pH` | 58/58 | 4.295 ~ 6.95 | 피부 표면 pH |
| `TEWL` | 58/58 | 13.25 ~ 33 | 경피수분손실 (g/m²h). 피부 장벽 기능 지표 |
| `shannon_16S` | 48/58 | 1.68592 ~ 7.90633 | **논문이 보고한** 세균 Shannon 값 (우리 `Shannon`과 대조용) |
| `faith_pd_16S` | 48/58 | 22.8463 ~ 84.5084 | 논문이 보고한 세균 Faith's PD |
| `simpson_even_16S` | 48/58 | 0.38002 ~ 0.983884 | 논문이 보고한 세균 Simpson evenness |
| `n_asv_16S` | 48/58 | 72 ~ 660 | 논문이 보고한 세균 ASV 수 |
| `qc_pass_16S` | 58/58 | no / yes | 논문의 세균 분석에 포함됐는지 (yes/no) |
| `shannon_ITS` | 58/58 | 0.674313 ~ 4.66884 | **논문이 보고한** 진균 Shannon 값 |
| `simpson_even_ITS` | 58/58 | 0.169478 ~ 0.90264 | 논문이 보고한 진균 Simpson evenness |
| `n_asv_ITS` | 58/58 | 7 ~ 103 | 논문이 보고한 진균 ASV 수 |
| `qc_pass_ITS` | 58/58 | yes | 논문의 진균 분석에 포함됐는지 (yes/no) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `01_aging_ITS_genus_pct.tsv`를 쓴다.

우점 속: `g_g__Malassezia`, `g_g__Rhodotorula`, `g_g__Lentinula`, `g_g__Mucor`, `g_g__Candida`, `g_g__Naganishia`, `g_Unassigned`, `g_g__Lasiobolus` …

## `metadata/clinical_data/01_aging_clinical.tsv` (61행 × 20컬럼)

**출처**: Supplementary Table S1 (xlsx) · Springer ESM

61개 샘플 전부. 시트 2개(Cheeks/Forehead) × 연령군 2블록 × 좌우 2단(왼쪽 Bacteria / 오른쪽 Fungi) 구조를 파싱했다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`sample_id`**, 이 표에서 **`sample_id`** 다.

- `01_aging_16S`: 55행과 매칭 · 임상표에만 있는 샘플 6개(전처리에서 탈락)
- `01_aging_ITS`: 58행과 매칭 · 임상표에만 있는 샘플 3개(전처리에서 탈락)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 61/61 | 61종 (예: Ca.10R, Ca.12R, Ca.13R …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `paper_id` | 61/61 | 61종 (예: C1, C10, C11 …) | 논문 보충표의 샘플 번호 |
| `body_site` | 61/61 | Cheek / Forehead | 채취 부위 |
| `group` | 61/61 | Old / Young | 비교군 라벨 |
| `age_group` | 61/61 | O / Y | 연령군 코드 |
| `sex` | 61/61 | female | 성별 |
| `age` | 61/61 | 19 ~ 63 | 나이 (세) |
| `moisture` | 61/61 | 49.4 ~ 74 | 피부 수분 (Corneometer, AU) |
| `sebum` | 61/61 | 0.5 ~ 94.5 | 피지 (Sebumeter) |
| `pH` | 61/61 | 4.295 ~ 6.95 | 피부 표면 pH |
| `TEWL` | 61/61 | 13.25 ~ 33 | 경피수분손실 (g/m²h). 피부 장벽 기능 지표 |
| `shannon_16S` | 51/61 | 1.68592 ~ 7.90633 | **논문이 보고한** 세균 Shannon 값 (우리 `Shannon`과 대조용) |
| `faith_pd_16S` | 51/61 | 22.8463 ~ 84.5084 | 논문이 보고한 세균 Faith's PD |
| `simpson_even_16S` | 51/61 | 0.38002 ~ 0.983884 | 논문이 보고한 세균 Simpson evenness |
| `n_asv_16S` | 51/61 | 72 ~ 833 | 논문이 보고한 세균 ASV 수 |
| `qc_pass_16S` | 61/61 | no / yes | 논문의 세균 분석에 포함됐는지 (yes/no) |
| `shannon_ITS` | 60/61 | 0.674313 ~ 4.66884 | **논문이 보고한** 진균 Shannon 값 |
| `simpson_even_ITS` | 60/61 | 0.169478 ~ 0.90264 | 논문이 보고한 진균 Simpson evenness |
| `n_asv_ITS` | 60/61 | 7 ~ 103 | 논문이 보고한 진균 ASV 수 |
| `qc_pass_ITS` | 61/61 | no / yes | 논문의 진균 분석에 포함됐는지 (yes/no) |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
