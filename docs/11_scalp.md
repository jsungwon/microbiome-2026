# 11_scalp — 두피 건선·지루피부염

> *Skin microbiome signatures associated with psoriasis and seborrheic dermatitis*  
> Exp Dermatol 31(7):1116–1118 (2022) · doi:10.1111/exd.14618

## 연구 설계

- **코호트**: 중국 성인 112명 · 지루피부염 45명 / 건선 37명 / 건강 30명 · 베이징대 제1병원
- **채취 부위**: 두피 — 환자는 병변/비병변 짝, 대조는 1점
- **마커**: 16S V3–V4 · 이미 병합·프라이머 제거된 서열로 등록(길이 409/429bp)

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `11_scalp_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `11_scalp_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `11_scalp_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `11_scalp_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `11_scalp_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `11_scalp_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `11_scalp_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `11_scalp_16S_sample_info.tsv` 컬럼 (187행 × 42컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 187/187 | 187종 (예: SRR17243429, SRR17243430, SRR17243431 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 187/187 | PRJNA788988 | BioProject accession |
| `sample_id` | 187/187 | 187종 (예: HC.002, HC.004, HC.005 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 187/187 | 112종 (예: HC002, HC004, HC005 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 187/187 | Scalp | 채취 부위 |
| `assay` | 187/187 | 16S | 마커 종류 |
| `region` | 187/187 | V3-V4 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 187/187 | Healthy / Psoriasis lesional / Psoriasis non-lesional / Seborrheic dermatitis lesional / Seborrheic dermatitis non-lesional | 비교군 라벨 |
| `group_type` | 187/187 | scalp_disease | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/187 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/187 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/187 | (전부 빈 칸) | 성별 |
| `read_count` | 187/187 | 56186 ~ 113864 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 187/187 | 138 ~ 2235 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 187/187 | 0.707702 ~ 7.10103 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 187/187 | 0.214426 ~ 0.998352 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 187/187 | 1.27295 ~ 606.877 | 역 Simpson 지수 |
| `read_depth_final` | 187/187 | 47020 ~ 100196 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 187/187 | 10종 (예: Brachybacterium, Chryseobacterium, Corynebacterium …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 187/187 | 12.74 ~ 88.68 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 187/187 | 63 ~ 428 | 검출된 속의 개수 (리드 1개 이상) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `11_scalp_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Staphylococcus`, `g_Unassigned`, `g_Lawsonella`, `g_Corynebacterium`, `g_Paracoccus`, `g_Enhydrobacter`, `g_Kocuria` …

## 임상 데이터 — 없음

논문이 2쪽짜리 연구서한(research letter)이라 개인 단위 표가 없다. 군은 샘플명 `SD.070.L`(군.피험자.병변)에서 복원했다.

⚠ **등록 설명과 논문의 환자 수가 서로 뒤바뀌어 있다.** BioProject 설명은 "건선 45 / 지루피부염 37" 이라고 적었지만, 논문과 실제 샘플 수는 **지루피부염 45 / 건선 37** 이다. 접두사 `SD`=45명, `P`=37명으로 논문 쪽과 일치하므로 논문을 따랐다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
