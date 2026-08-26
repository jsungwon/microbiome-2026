# microbiome-2026 — 한국인 피부 마이크로바이옴 실습 데이터

논문 4편의 공개 데이터를 내려받아 앰플리콘 파이프라인(DADA2)으로 처리하고,
**논문 보충자료의 샘플별 임상정보와 결합**해 둔 수업용 자료다.
FASTQ를 다루지 않고 TSV만 읽어서 바로 분석할 수 있다.

## 스터디 4개

| 폴더 접두사 | 스터디 | 논문 | 비교군 | 샘플 |
|---|---|---|---|---|
| `01_aging` | 노화 | Sci Rep 2022 | 젊은(Y) / 고령(O) | 16S 55 · ITS 58 |
| `02_healthy` | 건강한 한국인 | Sci Rep 2021 | 젊은(Y) / 고령(O) | 16S 102 |
| `03_sensitive` | 민감성 피부 | Microorganisms 2020 | 민감 / 비민감 | 16S 42 · ITS 42 |
| `04_acne` | 여드름 | J Microbiol 2021 | 여드름 / 건강 | 16S 60 · ITS 53 |

상세 목록은 `metadata/study_index.tsv`.

## 폴더 구조

```
metadata/sample_info/   <스터디>_<마커>_sample_info.tsv   ← 여기서 시작
                        샘플 1행 = 설계 + 임상 메타데이터 + 다양성 + 상위 20속(%)
metadata/clinical_data/ <스터디>_clinical.tsv
                        논문 보충자료에서 추출한 원본 임상표 (샘플 단위 1행)
                        sample_info에 이미 병합돼 있음 — 원본이 필요할 때만 쓴다
16S_count/              세균 정량 — genus_count(정수) · genus_pct(%) · genus_long · genus_taxonomy
ITS_count/              진균 정량 — 동일 구성
asv/                    ASV 수준 원자료 (속보다 세밀) + 대표 서열 FASTA
example_fastq/          예제 paired FASTQ (7.3 MB) — 전처리 실습용
docs/                   스터디별 컬럼 설명
docs/figures/           데이터 표 예시 스크린샷 (PPT용, 01번 스터디 기준)
```

## 시작하기

```r
d <- read.delim("metadata/sample_info/01_aging_16S_sample_info.tsv")
boxplot(g_Cutibacterium ~ group, data = d)
cor.test(d$sebum, d$Shannon, method = "spearman")
```

```python
import pandas as pd
d = pd.read_csv("metadata/sample_info/01_aging_16S_sample_info.tsv", sep="\t")
d.groupby("group")["g_Cutibacterium"].describe()
```

**컬럼 뜻을 모르겠으면 `docs/<스터디>.md`를 보면 된다.**
`sample_info`와 `clinical_data` 두 파일의 컬럼마다 채움 개수·값 범위·설명이 있다.

> ⚠ `03_sensitive`는 두 파일의 샘플 식별 컬럼 표기가 다르다 —
> sample_info는 `Non.03_bac`(컬럼 `subject`는 `Non.03`), 임상표는 `Non.03`이다.

## 어떤 파일을 쓸까

| 하려는 것 | 쓸 파일 |
|---|---|
| 군 간 조성 비교, 시각화 | `metadata/sample_info/*_sample_info.tsv` |
| 상위 20속으로 부족할 때 | `16S_count/*_genus_pct.tsv` (전체 속, %) |
| rarefaction · CLR · 카운트 모델 | `16S_count/*_genus_count.tsv` (정수) |
| 막대그래프·박스플롯 (long 포맷) | `16S_count/*_genus_long.tsv` |
| 문(Phylum) 수준으로 묶기 | `16S_count/*_genus_taxonomy.tsv` 조인 |
| ASV 수준 정밀 분석 | `asv/*_asv_count.tsv` + `*_asv_taxonomy.tsv` |
| 전처리(프라이머 제거·DADA2) 실습 | `example_fastq/` |

## 분석 과제 예시

1. **연령과 미생물** — `01_aging_16S`에서 `g_Cutibacterium`을 `group`으로 비교하라.
   차이가 크다. 그런데 `sebum`도 함께 보면 원인을 무엇이라 말할 수 있는가?
2. **교란 찾기** — `sebum`과 `Shannon`의 상관을 구하고, `group`별로 나눠 다시 구하라.
   `01_aging_16S`와 `04_acne_16S` 둘 다에서 같은 패턴이 나온다.
3. **부위 효과** — `body_site`로 나눠 우점 속이 달라지는지 보라.
   `02_healthy`와 `04_acne`는 같은 사람의 두 부위가 있어 `subject`로 짝지을 수 있다.
4. **재현 검증** — `04_acne_16S`에서 `g_Staphylococcus`/`g_Cutibacterium` 비를 군 간 검정하라.
   논문은 여드름군이 높다고 했다. 유의한가?
5. **논문 값과 대조** — `01_aging_16S`·`04_acne_16S`에는 논문이 보고한 `shannon_16S`와
   우리가 계산한 `Shannon`이 나란히 있다. 산점도로 그려 보라. 같은 데이터인데 왜 다른가?
6. **설문과 미생물** — `03_sensitive_16S`의 `perceived_skin_sensitivity`(1–7)와 조성이
   관련 있는가? 이분법 군 라벨보다 연속값이 더 잘 설명하는가?

## 데이터를 다룰 때 반드시 알 것

- **상대풍부도(compositional)다. 절대 균수가 아니다.** qPCR·spike-in 없이 앰플리콘만
  시퀀싱했으므로 "균이 더 많다"가 아니라 **"구성 비율이 다르다"**까지만 말할 수 있다.
- **합이 100%로 고정** → 한 속이 늘면 나머지는 기계적으로 준다. 단순 t검정·Wilcoxon으로
  속별 비교하면 실제 변화가 없는 속도 유의하게 나온다. CLR 변환 후 검정할 것.
- **시퀀싱 심도가 샘플마다 크게 다르다.** 검출 속 수는 심도에 직접 영향을 받는다.
  `read_depth_final` 컬럼으로 확인하고, 다양성 비교 전에 보정할 것.
- **스터디를 가로질러 속을 합치지 말 것.** `02_healthy`만 V3–V4이고 나머지는 V4–V5라
  검출되는 속 구성이 다르다.
- **`01_aging`과 `04_acne`는 27개 샘플이 같은 시퀀싱 데이터**다. 두 스터디를 합쳐
  표본 수를 늘리면 안 된다.
- **물성치는 스터디마다 측정 기기와 단위가 다르다.** 스터디 내 비교는 괜찮지만
  절대값을 가로질러 비교하려면 표준화가 필요하다.
