# 10_psoriasis — 건선 다부위

> *Alteration of the cutaneous microbiome in psoriasis and potential role in Th17 polarization*  
> Microbiome 6:154 (2018) · doi:10.1186/s40168-018-0533-1

## 연구 설계

- **코호트**: 미국 성인 54명 · 건선 28명 / 건강 26명 · UCSF
- **채취 부위**: 두피·몸통·팔·다리·겨드랑이·둔부주름 6부위 — 환자는 병변/비병변 짝
- **마커**: 16S V1–V3 · 프라이머가 제거된 상태로 등록

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `10_psoriasis_16S_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `10_psoriasis_16S_genus_count.tsv` | `16S_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `10_psoriasis_16S_genus_pct.tsv` | `16S_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `10_psoriasis_16S_genus_long.tsv` | `16S_count/` | 롱 포맷 (ggplot/seaborn용) |
| `10_psoriasis_16S_genus_taxonomy.tsv` | `16S_count/` | 속 → 문·강·목·과 계보 |
| `10_psoriasis_16S_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `10_psoriasis_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `10_psoriasis_16S_sample_info.tsv` 컬럼 (417행 × 45컬럼)

| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `run` | 417/417 | 417종 (예: ERR2703303, ERR2703304, ERR2703305 …) | ENA/SRA run accession. 이 표의 고유 키 |
| `project` | 417/417 | PRJEB25915 | BioProject accession |
| `sample_id` | 417/417 | 417종 (예: X7300.ArL, X7300.ArN, X7300.AxN …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 417/417 | 54종 (예: X7300, X7301, X7302 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `body_site` | 417/417 | 6종 (예: Arm, Axilla, Gluteal fold …) | 채취 부위 |
| `assay` | 417/417 | 16S | 마커 종류 |
| `region` | 417/417 | V1-V3 | 증폭 영역. **다르면 ASV 수준 병합 불가** |
| `group` | 417/417 | Healthy / Psoriasis lesional / Psoriasis non-lesional | 비교군 라벨 |
| `group_type` | 417/417 | psoriasis | group이 무슨 축인지 (age / sensitivity / acne / metformin_time / atopic_dermatitis / psoriasis / scalp_disease / rosacea_sampletype / ad_acne) |
| `age` | 0/417 | (전부 빈 칸) | 나이 (세) |
| `age_group` | 0/417 | (전부 빈 칸) | 연령군 코드 |
| `sex` | 0/417 | (전부 빈 칸) | 성별 |
| `read_count` | 417/417 | 21249 ~ 606516 | ENA에 등록된 원시 리드 수 (전처리 전) |
| `Observed` | 417/417 | 16 ~ 2133 | 관측된 ASV 수 (rarefy 후). 심도에 민감 |
| `Shannon` | 417/417 | 0.209768 ~ 6.56795 | Shannon 다양성 지수 (rarefy 후) |
| `Simpson` | 417/417 | 0.0479936 ~ 0.994059 | Simpson 지수 (rarefy 후). 1에 가까울수록 다양 |
| `InvSimpson` | 417/417 | 1.05041 ~ 168.311 | 역 Simpson 지수 |
| `read_depth_final` | 417/417 | 15017 ~ 327855 | 전처리·키메라 제거 후 최종 리드 수. **심도 보정 시 이 값을 쓸 것** |
| `dominant_genus` | 417/417 | 16종 (예: Anaerococcus, Bacteroides, Brevundimonas …) | 이 샘플에서 가장 우세한 속 |
| `dominant_pct` | 417/417 | 10.06 ~ 97.87 | 우점 속의 상대풍부도 (%) |
| `n_genus_detected` | 417/417 | 7 ~ 432 | 검출된 속의 개수 (리드 1개 이상) |
| `host_phenotype` | 417/417 | Healthy / Psoriasis lesion / Psoriasis unaffected | BioSample의 숙주 표현형 (Psoriasis lesion / Psoriasis unaffected / Healthy) |
| `collection_date` | 417/417 | 2017 | 채취일 (BioSample 기록). 계절·배치 효과를 볼 때 쓴다 |
| `sequencing_method` | 417/417 | 417종 (예: Illumina MiSeq PE300, Illumina MiSeq PE301, Illumina MiSeq PE302 …) | 시퀀싱 방법 문자열 (BioSample 기록 그대로) |

미생물 컬럼 `g_*` 21개 — 상위 20속 상대풍부도(%) + `g_Other`. **합이 정확히 100**이다. 전체 속이 필요하면 `10_psoriasis_16S_genus_pct.tsv`를 쓴다.

우점 속: `g_Cutibacterium`, `g_Corynebacterium`, `g_Staphylococcus`, `g_Unassigned`, `g_Anaerococcus`, `g_Streptococcus`, `g_Finegoldia`, `g_Peptoniphilus` …

## 임상 데이터 — 없음

이 스터디는 드물게 **BioSample 자체에 임상 필드가 있다**. `host phenotype`(Psoriasis lesion / Psoriasis unaffected / Healthy)과 `environment (feature)`(6부위)가 417개 전부에 채워져 있다.

⚠ **샘플명만 믿으면 안 된다.** 접미 `B` 는 등(Back)이 아니라 **둔부 주름(Butt_Crease)** 이다 — 이름으로 읽으면 67샘플이 틀린다. 군 라벨은 이름 기반 복원과 BioSample이 417/417 일치했다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
