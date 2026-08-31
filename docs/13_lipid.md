# 13_lipid — 지질–미생물 (여드름·아토피)

> *Shotgun-lipidomics reveals disease specific microbiome-lipid correlations in acne vulgaris and atopic dermatitis*  
> ENA PRJEB66070 (Helmholtz Munich) · doi:

## 연구 설계

- **코호트**: 독일 성인 73명 · 여드름 21명 / 아토피 16명 / 건강 36명
- **채취 부위**: 테이프 스트립 — 환자의 병변·비병변과 **부위를 맞춘** 건강 대조가 한 세트
- **마커**: 16S V1–V3 (27F–534R) · 파일 단위로 R1/R2 방향이 뒤집혀 있어 정규화 필요

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `13_lipid_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `13_lipid_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `13_lipid_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `13_lipid_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `13_lipid_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `13_lipid_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `13_lipid_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `13_lipid_16S_sample_info.tsv` 컬럼 (111행 × 42컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 111/111 | 111종 (예: ERR12050112, ERR12050113, ERR12050114 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 111/111 | PRJEB66070 | BioProject accession |
| `sample_id` | 111/111 | 111종 (예: S10_AE_LS_LEG_SMi42, S10_AE_NL_LEG_SMi43, S10_HE_HE_LEG_JB85 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 111/111 | 73종 (예: AB, AD, ALT …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 111/111 | 7종 (예: Abdomen, Arm, Back …) | 채취 부위 |
| `assay` | 111/111 | 16S | 마커 종류 |
| `region` | 111/111 | V1-V3 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 111/111 | Acne vulgaris lesional / Acne vulgaris non-lesional / Atopic dermatitis lesional / Atopic dermatitis non-lesional / Healthy | 비교군 라벨 |
| `group_type` | 111/111 | ad_acne | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/111 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/111 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/111 | (전부 빈 칸) | 성별 |
| `read_count` | 111/111 | 23854 ~ 79120 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 111/111 | 21 ~ 220 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 111/111 | 0.635913 ~ 4.22902 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 111/111 | 0.197207 ~ 0.96733 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 111/111 | 1.24565 ~ 30.6093 | 역 Simpson 지수 |
| `read_depth_final` | 111/111 | 8735 ~ 31178 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 111/111 | Corynebacterium / Cutibacterium / Sphingomonas / Staphylococcus / Unassigned | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 111/111 | 18.72 ~ 92.62 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 111/111 | 12 ~ 73 | 검출된 속의 개수 (리드 1개 이상) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `13_lipid_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Sphingomonas`, `g_Staphylococcus`, `g_Methylobacterium`, `g_Corynebacterium`, `g_Renibacterium`, `g_Unassigned`, `g_Streptococcus` …

## 임상 데이터 — 없음

질환(HE/AE/AKNE)·병변 여부(LS/NL)·부위·개인코드가 전부 샘플명에 들어 있다.

⚠ **`S1` 같은 앞 번호는 피험자가 아니라 매칭 세트 번호다.** 한 세트 안에 환자의 병변·비병변과 **부위를 맞춘 건강 대조**가 함께 들어 있다. 실제 개인은 끝 코드의 알파벳(`BK1`/`BK2`=환자 BK, `LP111`=대조 LP)이고 73명(환자 37 + 건강 36)이 겹치지 않는다. S 번호로 묶으면 서로 다른 두 사람이 한 명으로 합쳐진다. 세트 번호는 `timepoint` 컬럼에 넣어 뒀다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
