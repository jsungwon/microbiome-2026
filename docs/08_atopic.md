# 08_atopic — 아토피 피부염

> *Staphylococcal Communities on Skin Are Associated with Atopic Dermatitis and Disease Severity*  
> Microorganisms 9(2):432 (2021) · doi:10.3390/microorganisms9020432

## 연구 설계

- **코호트**: 덴마크 성인 186명 · 아토피 환자 94명 / 건강 대조 92명 · Statens Serum Institut
- **채취 부위**: 병변 피부 · 비병변 피부 · 코(전비강) — 같은 사람의 여러 부위
- **마커**: 16S V3–V4 (341F–805R) · Illumina MiSeq

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `08_atopic_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `08_atopic_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `08_atopic_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `08_atopic_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `08_atopic_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `08_atopic_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `08_atopic_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `08_atopic_16S_sample_info.tsv` 컬럼 (466행 × 46컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 466/466 | 466종 (예: ERR5237550, ERR5237551, ERR5237552 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 466/466 | PRJEB42898 | BioProject accession |
| `sample_id` | 466/466 | 466종 (예: AD_LS_104_16Sv3v4, AD_LS_105_16Sv3v4, AD_LS_10_16Sv3v4 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 466/466 | 186종 (예: AD10, AD104, AD105 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 466/466 | Lesional skin / Non-lesional skin / Nose / Skin | 채취 부위 |
| `assay` | 466/466 | 16S | 마커 종류 |
| `region` | 466/466 | V3-V4 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 466/466 | AD / Control | 비교군 라벨 |
| `group_type` | 466/466 | atopic_dermatitis | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/466 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/466 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 466/466 | F / M | 성별 |
| `read_count` | 466/466 | 15274 ~ 486990 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 466/466 | 14 ~ 544 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 466/466 | 0.341052 ~ 5.30017 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 466/466 | 0.120118 ~ 0.988127 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 466/466 | 1.13652 ~ 84.225 | 역 Simpson 지수 |
| `read_depth_final` | 466/466 | 4090 ~ 199559 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 466/466 | 17종 (예: Corynebacterium, Cutibacterium, Dolosigranulum …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 466/466 | 10.67 ~ 98.86 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 466/466 | 12 ~ 220 | 검출된 속의 개수 (리드 1개 이상) |
| `skin_type` | 280/466 | dry / moist / sebaceous | 피부타입 1–4 (건성→복합성) |
| `sample_site` | 466/466 | AD_LS / AD_NLS / AD_nose / Control_nose / Control_skin | 채취 구분 코드 (AD_LS 병변 / AD_NLS 비병변 / AD_nose 코 / Control_skin / Control_nose) |
| `body_site_paper` | 466/466 | 13종 (예: antecubital_fossa, arm, back …) | 논문·저자시트가 기록한 **실제 해부학 부위** (arm, antecubital_fossa, nose 등). `body_site` 는 설계상 구분(병변/비병변)이라 서로 다르다 |
| `country` | 466/466 | Denmark | 채취 국가 |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `08_atopic_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Staphylococcus`, `g_Corynebacterium`, `g_Micrococcus`, `g_Dolosigranulum`, `g_Cutibacterium`, `g_Streptococcus`, `g_Unassigned`, `g_Moraxella` …

## `metadata/clinical_data/08_atopic_clinical.tsv` (466행 × 8컬럼)

**출처**: 저자 저장소 ENA 시트 (xls) · github.com/ssi-dk/AD_staphylome_project

논문 Table S1은 군 단위 치료력 요약뿐이라 개인 단위 값이 없다. 저자가 공개한 저장소의 `ENA_sample_data/data_file.xls` 가 932샘플(16S 466 + tuf 466) 전부에 대해 군·피험자·부위·성별을 준다. `SAMPLE` 열이 우리 `sample_id` 와 그대로 일치해 **466/466 성별**이 붙는다.

같은 저장소의 phyloseq 객체에서 `skin_type`(sebaceous/dry/moist)을 더 얻었는데, 피부 280샘플에만 있고 코 186샘플에는 없다.

⚠ **SCORAD 중증도는 공개본에 없다.** 덴마크 개인정보 규정 때문에 제외되었다고 논문이 명시한다. 군 단위로는 경증 25 / 중등증 48 / 중증 21명이다.

`sample_info`에 이미 병합돼 있지만, 논문 단위 원본 표가 필요할 때 쓴다 (샘플 단위 1행 — run 단위가 아니다).

샘플을 식별하는 컬럼은 `sample_info`에서 **`sample_id`**, 이 표에서 **`sample_id`** 다.

- `08_atopic_16S`: 466행과 매칭

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 466/466 | 466종 (예: AD_LS_104_16Sv3v4, AD_LS_105_16Sv3v4, AD_LS_10_16Sv3v4 …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 466/466 | 186종 (예: AD_10, AD_104, AD_105 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `group` | 466/466 | AD / Control | 비교군 라벨 |
| `sample_site` | 466/466 | AD_LS / AD_NLS / AD_nose / Control_nose / Control_skin | 채취 구분 코드 (AD_LS 병변 / AD_NLS 비병변 / AD_nose 코 / Control_skin / Control_nose) |
| `body_site_paper` | 466/466 | 13종 (예: antecubital_fossa, arm, back …) | 논문·저자시트가 기록한 **실제 해부학 부위** (arm, antecubital_fossa, nose 등). `body_site` 는 설계상 구분(병변/비병변)이라 서로 다르다 |
| `sex` | 466/466 | F / M | 성별 |
| `skin_type` | 280/466 | dry / moist / sebaceous | 피부타입 1–4 (건성→복합성) |
| `country` | 466/466 | Denmark | 채취 국가 |

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
