# example_fastq — 수업용 예제 FASTQ (paired)

실제 데이터에서 **한 샘플의 paired FASTQ를 3만 쌍으로 서브샘플링**한 것이다. 총 7.3 MB라
내려받아 바로 돌려볼 수 있고, 전처리부터 분류까지 전체 워크플로를 몇 분 안에 완주한다.

```
example_SRR14277172_R1.fastq.gz   3.19 MB   30,144 reads
example_SRR14277172_R2.fastq.gz   4.10 MB   30,144 reads
example_metadata.tsv              이 샘플의 메타데이터·임상정보
md5sum.txt
```

## 어떤 샘플인가

| 항목 | 값 |
|---|---|
| 원본 run | `SRR14277172` (PRJNA723064) |
| 스터디 | Taxonomic profiling of skin microbiome in healthy Koreans (Sci Rep 2021) |
| 샘플 | `OF3` — 피험자 O3, **이마**, 54세 여성, 고령군(Old 49–67) |
| 마커 | 16S rRNA **V3–V4** (341F–805R) |
| 플랫폼 | Illumina MiSeq, 2×251 bp |
| 임상정보 | moisture 53.7 AU / sebum 34 µg·cm⁻² / TEWL 10.5 g·m⁻²h⁻¹ / 피부타입 1 + 주름·반점 등 20종 (`example_metadata.tsv`) |

**왜 이 샘플인가** — (1) 프라이머가 그대로 남아 있어 cutadapt 단계를 실습할 수 있고,
(2) 대상 4개 스터디 중 임상 항목이 가장 많은 스터디(20종)이며,
(3) 이마 샘플이라 피지(sebum) 측정치가 있고,
(4) 원본이 98,303쌍으로 깊어 3만 쌍 서브샘플이 편향 없는 무작위 부분집합이 된다.

## 만든 방법 (재현)

```bash
seqkit sample -s 42 -p 0.30518 -o R1.fastq.gz SRR14277172_1.fastq.gz
seqkit sample -s 42 -p 0.30518 -o R2.fastq.gz SRR14277172_2.fastq.gz
```

seed 고정이라 재현 가능하고, R1/R2의 read ID가 **순서까지 완전히 일치**함을 확인했다(페어 동기 보장).

## 검증 — 실제로 돌려봤다

파이프라인과 같은 파라미터(341F/805R 제거, truncLen 233/220)로 끝까지 돌린 결과다.

| 단계 | 리드 | 통과율 |
|---|---|---|
| 입력 | 30,144 쌍 | — |
| cutadapt (프라이머 제거) | 28,388 | 94.2% |
| filterAndTrim | 22,678 | 79.9% |
| 병합 | 22,127 | denoised 대비 98.3% |
| 키메라 제거 후 | 21,405 | 입력 대비 75.4% |
| ASV | 84 → **55** | |

**서브샘플이 전체 파일 결과를 그대로 재현한다:**

| genus | 전체 98,303쌍 | 서브샘플 30,144쌍 |
|---|---|---|
| Cutibacterium | 90.20% | **90.32%** |
| Lawsonella | 4.80% | **5.05%** |
| Staphylococcus | 1.35% | **1.49%** |
| Corynebacterium | 0.73% | **0.84%** |

우점 조성은 거의 동일하지만 **검출 ASV 수는 55개로 전체(151개)보다 적다.**
희귀 분류군은 심도가 있어야 잡힌다는 걸 보여주는 지점이라 수업에서 다루기 좋다.

## 병합 길이 분포 — 이 데이터의 함정

```
402 404 405 407 408 409 410 414 419 421 422 424 426 427 428
  5   3   1   6   2   2   1   1   1   1   4   1   1  23   3
```

**V3–V4 앰플리콘이 407 bp와 427 bp 이중 분포**를 이룬다. 리드가 251 bp뿐이라
truncLen을 조금만 크게 잡아도(예: 230/200 → 합 430) 427 bp급의 오버랩이 3 bp로 줄어
**그 분류군이 통째로 사라진다**. 여기서 쓴 233/220은 실측으로 고른 값이고,
위 분포에서 427 bp ASV 23개가 살아 있는 것이 그 결과다.

품질 그래프만 보고 truncLen을 정하면 안 된다는 사례로 쓸 수 있다.

## 바로 해보기

```bash
# 1. 프라이머 제거
cutadapt -g CCTACGGGNGGCWGCAG -G GACTACHVGGGTATCTAATCC \
         --discard-untrimmed -m 50 \
         -o trim_R1.fastq.gz -p trim_R2.fastq.gz \
         example_SRR14277172_R1.fastq.gz example_SRR14277172_R2.fastq.gz
```

```r
# 2. DADA2
library(dada2)
plotQualityProfile(c("trim_R1.fastq.gz","trim_R2.fastq.gz"))   # truncLen 정하기 전에 확인
filterAndTrim("trim_R1.fastq.gz","filt_R1.fastq.gz",
              "trim_R2.fastq.gz","filt_R2.fastq.gz",
              truncLen=c(233,220), maxEE=c(2,5), truncQ=2, maxN=0, compress=TRUE)
eF <- learnErrors("filt_R1.fastq.gz"); eR <- learnErrors("filt_R2.fastq.gz")
dF <- dada("filt_R1.fastq.gz", err=eF); dR <- dada("filt_R2.fastq.gz", err=eR)
mg <- mergePairs(dF, derepFastq("filt_R1.fastq.gz"), dR, derepFastq("filt_R2.fastq.gz"))
st <- removeBimeraDenovo(makeSequenceTable(mg), method="consensus")
table(nchar(colnames(st)))          # 407 / 427 이중 분포 확인
tax <- assignTaxonomy(st, "../../resources/silva_nr99_v138.2_toGenus_trainset.fa.gz")
```

참조 DB는 `release/../resources/`에 있다 (SILVA 138.2, UNITE).

전체 스터디의 결과 테이블은 `../data/analysis_ready/`, 파이프라인 설명은 `../docs/pipeline_results.md`.
