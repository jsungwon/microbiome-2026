# 04_acne — 여드름

> *Inferences in microbial structural signatures of acne microbiome and mycobiome*  
> J Microbiol 59(4):369–375 (2021) · doi:10.1007/s12275-021-0647-1

출처·accession → [`data_provenance.md`](data_provenance.md) · 처리 과정 → [`pipeline.md`](pipeline.md)

## 연구 설계

- **코호트**: 한국인 여성 33명 · 여드름 17명 / 건강 16명 · 19–28세
- **채취 부위**: 이마(Fa) · 오른쪽 볼(Ca) — 같은 사람의 두 부위 (개체 내 짝 비교 가능)
- **마커**: 16S V4–V5 + ITS1 · 한 run에 두 앰플리콘 혼재

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `04_acne_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `04_acne_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `04_acne_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `04_acne_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `04_acne_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `04_acne_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `04_acne_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `04_acne_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `04_acne_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `04_acne_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `04_acne_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `04_acne_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `04_acne_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `04_acne_16S_sample_info.tsv` 컬럼 (60행 × 52컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 60/60 | 60종 (예: SRR12968645, SRR12968646, SRR12968648 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 60/60 | PRJNA669317 | BioProject accession |
| `sample_id` | 60/60 | 60종 (예: Ca.01, Ca.02, Ca.03 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 60/60 | 1 ~ 33 | 피험자 식별자. 같은 사람의 여러 부위를 묶는 키 |
| `body_site` | 60/60 | Cheek / Forehead | 채취 부위 |
| `assay` | 60/60 | 16S+ITS_pooled | 마커 종류 |
| `region` | 60/60 | V4-V5+ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 60/60 | Acne / Healthy | 비교군 라벨 |
| `group_type` | 60/60 | acne | group이 무슨 축인지 (age / sensitivity / acne) |
| `age` | 60/60 | 19 ~ 28 | 나이 (세) |
| `age_group` | 0/60 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 60/60 | female | 성별 |
| `read_count` | 60/60 | 2911 ~ 354824 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 60/60 | 8 ~ 388 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 60/60 | 0.323568 ~ 5.07704 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 60/60 | 0.102226 ~ 0.984558 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 60/60 | 1.11387 ~ 64.7569 | 역 Simpson 지수 |
| `read_depth_final` | 60/60 | 1325 ~ 261994 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 60/60 | Burkholderia-Caballeronia-Paraburkholderia / Corynebacterium / Cutibacterium / Staphylococcus / Unassigned | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 60/60 | 15.54 ~ 98.92 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 60/60 | 9 ~ 271 | 검출된 속의 개수 (리드 1개 이상) |
| `moisture` | 60/60 | 50.3 ~ 75.9 | 피부 수분 (Corneometer, AU) |
| `sebum` | 60/60 | 13.5 ~ 124 | 피지 (Sebumeter) |
| `pH` | 60/60 | 4.36 ~ 6.95 | 피부 표면 pH |
| `TEWL` | 60/60 | 14 ~ 36.55 | 경피수분손실 (g/m²h). 피부 장벽 기능 지표 |
| `shannon_16S` | 59/60 | 0.111 ~ 6.468 | **논문이 보고한** 세균 Shannon 값 (우리 `Shannon`과 대조용) |
| `faith_pd_16S` | 59/60 | 3.684 ~ 23.579 | 논문이 보고한 세균 Faith's PD |
| `qc_pass_16S` | 60/60 | no / yes | 논문의 세균 분석에 포함됐는지 (yes/no) |
| `shannon_ITS` | 48/60 | 0.834 ~ 3.305 | **논문이 보고한** 진균 Shannon 값 |
| `qc_pass_ITS` | 60/60 | no / yes | 논문의 진균 분석에 포함됐는지 (yes/no) |
| `faith_pd_ITS` | 48/60 | 2.31 ~ 10.686 | 논문이 보고한 진균 Faith's PD |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `04_acne_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Staphylococcus`, `g_Burkholderia-Caballeronia-Paraburkholderia`, `g_Unassigned`, `g_Corynebacterium`, `g_Streptococcus`, `g_Enhydrobacter`, `g_Brevundimonas` …

## `04_acne_ITS_sample_info.tsv` 컬럼 (53행 × 52컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 53/53 | 53종 (예: SRR12968645, SRR12968646, SRR12968648 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 53/53 | PRJNA669317 | BioProject accession |
| `sample_id` | 53/53 | 53종 (예: Ca.01, Ca.02, Ca.03 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 53/53 | 1 ~ 33 | 피험자 식별자. 같은 사람의 여러 부위를 묶는 키 |
| `body_site` | 53/53 | Cheek / Forehead | 채취 부위 |
| `assay` | 53/53 | 16S+ITS_pooled | 마커 종류 |
| `region` | 53/53 | V4-V5+ITS1 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 52/53 | Acne / Healthy | 비교군 라벨 |
| `group_type` | 53/53 | acne | group이 무슨 축인지 (age / sensitivity / acne) |
| `age` | 52/53 | 19 ~ 28 | 나이 (세) |
| `age_group` | 0/53 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 53/53 | female | 성별 |
| `read_count` | 53/53 | 3700 ~ 354824 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 53/53 | 23 ~ 79 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 53/53 | 0.316235 ~ 2.3692 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 53/53 | 0.0855187 ~ 0.821975 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 53/53 | 1.09352 ~ 5.61718 | 역 Simpson 지수 |
| `read_depth_final` | 53/53 | 1051 ~ 62658 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 53/53 | g__Malassezia | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 53/53 | 39.97 ~ 98.12 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 53/53 | 12 ~ 52 | 검출된 속의 개수 (리드 1개 이상) |
| `moisture` | 52/53 | 50.3 ~ 72.7 | 피부 수분 (Corneometer, AU) |
| `sebum` | 52/53 | 23 ~ 124 | 피지 (Sebumeter) |
| `pH` | 52/53 | 4.36 ~ 6.95 | 피부 표면 pH |
| `TEWL` | 52/53 | 14 ~ 42.6 | 경피수분손실 (g/m²h). 피부 장벽 기능 지표 |
| `shannon_16S` | 49/53 | 0.111 ~ 4.279 | **논문이 보고한** 세균 Shannon 값 (우리 `Shannon`과 대조용) |
| `faith_pd_16S` | 49/53 | 3.684 ~ 12.744 | 논문이 보고한 세균 Faith's PD |
| `qc_pass_16S` | 52/53 | no / yes | 논문의 세균 분석에 포함됐는지 (yes/no) |
| `shannon_ITS` | 43/53 | 0.834 ~ 3.305 | **논문이 보고한** 진균 Shannon 값 |
| `qc_pass_ITS` | 52/53 | no / yes | 논문의 진균 분석에 포함됐는지 (yes/no) |
| `faith_pd_ITS` | 43/53 | 2.31 ~ 9.214 | 논문이 보고한 진균 Faith's PD |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `04_acne_ITS_genus_pct.tsv`를 쓴다.

우점 속: `g_g__Malassezia`, `g_g__Rhodotorula`, `g_g__Mucor`, `g_g__Naganishia`, `g_g__Lasiobolus`, `g_g__Debaryomycetaceae_gen_Incertae_sedis`, `g_g__Cladosporium`, `g_Unassigned` …

## `metadata/clinical_data/04_acne_clinical.tsv` (63행 × 16컬럼)

**출처**: Supplementary Table S1 (PDF 2단 표) · Springer ESM

여드름/건강 군 라벨이 BioSample·샘플명 어디에도 없고 이 표에만 있다. PDF 2단 레이아웃(왼쪽 Bacteria / 오른쪽 Fungi)을 잘라 파싱했다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`sample_id`**, 이 표에서 **`sample_id`** 다.

- `04_acne_16S`: 60행과 매칭 · 임상표에만 있는 샘플 3개(전처리에서 탈락)
- `04_acne_ITS`: 53행과 매칭 · 임상표에만 있는 샘플 11개(전처리에서 탈락) · **임상값이 없는 샘플 1개**

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 63/63 | 63종 (예: Ca.01, Ca.02, Ca.03 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `paper_sample_id` | 63/63 | 63종 (예: Ca.1, Ca.10, Ca.11 …) | 논문 표기 샘플 ID (데이터 표기와 다를 수 있음) |
| `subject` | 63/63 | 1 ~ 33 | 피험자 식별자. 같은 사람의 여러 부위를 묶는 키 |
| `body_site` | 63/63 | Cheek / Forehead | 채취 부위 |
| `group` | 63/63 | Acne / Healthy | 비교군 라벨 |
| `age` | 63/63 | 19 ~ 28 | 나이 (세) |
| `moisture` | 63/63 | 50.3 ~ 75.9 | 피부 수분 (Corneometer, AU) |
| `TEWL` | 63/63 | 14 ~ 42.6 | 경피수분손실 (g/m²h). 피부 장벽 기능 지표 |
| `pH` | 63/63 | 4.36 ~ 6.95 | 피부 표면 pH |
| `sebum` | 63/63 | 13.5 ~ 124 | 피지 (Sebumeter) |
| `shannon_16S` | 59/63 | 0.111 ~ 6.468 | **논문이 보고한** 세균 Shannon 값 (우리 `Shannon`과 대조용) |
| `faith_pd_16S` | 59/63 | 3.684 ~ 23.579 | 논문이 보고한 세균 Faith's PD |
| `qc_pass_16S` | 63/63 | no / yes | 논문의 세균 분석에 포함됐는지 (yes/no) |
| `shannon_ITS` | 51/63 | 0.834 ~ 3.305 | **논문이 보고한** 진균 Shannon 값 |
| `faith_pd_ITS` | 51/63 | 2.31 ~ 10.686 | 논문이 보고한 진균 Faith's PD |
| `qc_pass_ITS` | 63/63 | no / yes | 논문의 진균 분석에 포함됐는지 (yes/no) |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
