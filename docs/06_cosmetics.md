# 06_cosmetics — 화장품·피부수분

> *Effects of cosmetics on the skin microbiome of facial cheeks with different hydration levels*  
> MicrobiologyOpen 7(2):e00557 (2018) · doi:10.1002/mbo3.557

## 연구 설계

- **코호트**: 건강한 한국인 여성 30명 · 평균 43.8세(26–53) · 고수분군 HHG 16 / 저수분군 LHG 14
- **채취 부위**: 볼(facial cheek) — 같은 사람을 3시점 추적 (사용 전 / 2주 / 4주)
- **마커**: 16S V1–V3 (Bac9F–Bac541R) · 454 GS FLX Titanium

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `06_cosmetics_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## `metadata/clinical_data/06_cosmetics_clinical.tsv` (90행 × 11컬럼)

**출처**: Supplementary Table 1 (docx) · MicrobiologyOpen 보충자료

⚠ **이 스터디는 원시 시퀀스를 샘플별로 나눌 수 없다.** SRA에 올라온 2개 run은 서로 완전히 동일한 파일이고(리드 서열 해시 일치), 90개 시료가 바코드로 다중화된 상태에서 **바코드가 이미 제거돼** 있다 — 리드에도 헤더에도 시료를 구분할 정보가 없다. 그래서 `16S_count/`·`asv/`·`sample_info/` 파일이 없고, **이 임상표가 샘플 단위로 얻을 수 있는 전부**다.

다양성 지표는 우리가 계산한 것이 아니라 **논문이 보고한 값**이다.

이 스터디는 이 파일 하나가 전부다 (샘플 단위 1행).


| 컬럼 | 채움 | 값 / 범위 | 설명 |
|---|---|---|---|
| `sample_id` | 90/90 | 90종 (예: HHG10_2weeks, HHG10_4weeks, HHG10_Beforeuse …) | 원본 샘플 식별자 (논문·BioSample 표기) |
| `subject` | 90/90 | 30종 (예: HHG1, HHG10, HHG11 …) | 피험자 식별자. 같은 사람의 여러 부위(또는 시점)를 묶는 키 |
| `hydration_group` | 90/90 | HHG / LHG | **피부 수분군** — HHG 고수분(≥50 A.U.) / LHG 저수분(<50) |
| `timepoint` | 90/90 | T0(사용 전) / T2w(2주) / T4w(4주) | 종단 설계의 시점. 스터디마다 값이 다르다 (예: M0/M24h/M7d, T0/T2w/T4w) |
| `paper_sampling_time` | 90/90 | 2 weeks / 4 weeks / Before use | 논문 표기 시점 (Before use / 2 weeks / 4 weeks) |
| `reads_total` | 90/90 | 4074 ~ 30750 | 논문이 보고한 총 리드 수 |
| `reads_high_quality` | 90/90 | 3184 ~ 16983 | 논문이 보고한 고품질 리드 수 |
| `otus_paper` | 90/90 | 113 ~ 1017 | **논문이 보고한** OTU 수 (97% 클러스터링) |
| `chao1_paper` | 90/90 | 191 ~ 2659 | 논문이 보고한 Chao1 (풍부도 추정치) |
| `shannon_paper` | 90/90 | 1.71 ~ 5.41 | **논문이 보고한** Shannon 지수 (우리 `Shannon`과 대조용) |
| `evenness_paper` | 90/90 | 0.35 ~ 0.83 | 논문이 보고한 균등도(evenness) |

## 주의

- 이 스터디에는 **미생물 정량 데이터가 없다.** 원시 시퀀스를 샘플별로 나눌 수 없어 속(genus)·ASV 테이블을 만들 수 없었다.
- 다양성 지표는 **논문이 보고한 값**이다. 다른 스터디의 `Shannon`은 우리가 계산한 값이라 **직접 비교하면 안 된다** (도구·참조DB·rarefaction이 다름).
- 대신 **종단 설계**(30명 × 3시점)와 **수분군**(HHG/LHG)이 온전해서, 다양성 지표만으로 반복측정 분석을 실습할 수 있다.
