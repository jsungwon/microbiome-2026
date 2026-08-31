# 17_ad_myco — 아토피 마이코바이옴

> *The Skin Mycobiome of Patients With Atopic Dermatitis and Healthy Volunteers: A Case-Control Study*  
> Exp Dermatol 34(3):e70085 (2025) · doi:10.1111/exd.70085

## 연구 설계

- **코호트**: 폴란드 성인 100명 · 아토피 50명 / 건강 대조 50명 · 브로츠와프
- **채취 부위**: 병변 피부(주로 팔오금) — 대조군은 건강 피부
- **마커**: ITS1 (ITS1–ITS2) · 배양 검사 병행

## 이 스터디의 파일

| 파일 | 위치 | 내용 |
|---|---|---|
| `17_ad_myco_ITS_sample_info.tsv` | `metadata/sample_info/` | 샘플 1행 = 설계·메타데이터·다양성·상위 20속 |
| `17_ad_myco_ITS_genus_count.tsv` | `ITS_count/` | 샘플 × 속 **원시 리드 수(정수)** |
| `17_ad_myco_ITS_genus_pct.tsv` | `ITS_count/` | 샘플 × 속 **상대풍부도(%)**, 행 합 = 100 |
| `17_ad_myco_ITS_genus_long.tsv` | `ITS_count/` | 롱 포맷 (ggplot/seaborn용) |
| `17_ad_myco_ITS_genus_taxonomy.tsv` | `ITS_count/` | 속 → 문·강·목·과 계보 |
| `17_ad_myco_ITS_asv_count.tsv` | `asv/` | ASV 수준 카운트 (속보다 세밀) |
| `17_ad_myco_clinical.tsv` | `metadata/clinical_data/` | 논문 보충자료 원본 임상표 |

## 임상 데이터 — 없음

군은 `AZS_`(atopowe zapalenie skory = 아토피) / `Control_` 로 **50 / 50** 이며 논문 보고치와 정확히 일치한다.

⚠ 접미 코드(ZL / K / ZLK)는 부위로 보이지만 **확정하지 못했다.** 논문은 아토피 검체를 팔오금 44 / 목 6 으로 보고하는데 이름은 ZL 46 / K 4 이고, 대조군은 전부 팔오금이라는데 이름은 ZLK 31 / K 19 로 갈린다. 추정(ZL=zgiecie lokciowe 팔오금, K=kark 목)을 값으로 쓰지 않고 원문 코드만 note 에 남겼다.

⚠ 품질값이 전 염기 단일 상수라 DADA2 오류모델을 품질 무시 방식(`noqualErrfun`)으로 학습했고, 리드의 21%가 38bp 프라이머 다이머라 `min_len 50` 에서 걸러진다. 통과율 ~50%는 정상 제거다.

논문 Table 1 에 SCORAD·DLQI·IgE·호산구 등이 있지만 **군 요약**이라 샘플에 붙일 수 없다.

이 스터디에는 `metadata/clinical_data/` 파일이 없다. 샘플에 붙는 정보는 **피험자 ID와 시점뿐**이다.

## 주의

- **`g_*`와 `_genus_pct.tsv` 단위는 %다** (0–100). 비율이 필요하면 100으로 나눌 것.
- 상대풍부도는 합이 100으로 고정돼 **한 속이 늘면 나머지가 기계적으로 줄어든다.** 속별 비교는 CLR 변환 후 하거나 카운트 기반 방법을 쓸 것.
- 다양성 지표(`Observed`·`Shannon`·`Simpson`)는 심도 1,000 리드로 rarefy한 뒤 계산했다. 그 미만 샘플은 빈 칸이다.
- 절대 균수가 아니라 **구성 비율**이다. "균이 더 많다"가 아니라 "비율이 다르다"까지만 말할 수 있다.
