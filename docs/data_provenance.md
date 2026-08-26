# 데이터 출처

이 저장소의 데이터는 **공개 시퀀싱 데이터 + 논문 보충자료**에서 만들었다.
새로 생성한 실험 데이터는 없다.

## 원 논문과 accession

| # | 스터디 | 논문 | DOI | BioProject |
|---|---|---|---|---|
| 01 | 노화 | *Aged related human skin microbiome and mycobiome in Korean women*<br>Sci Rep 12:2500 (2022) | [10.1038/s41598-022-06189-5](https://doi.org/10.1038/s41598-022-06189-5) | `PRJNA613934` + `PRJNA614620` |
| 02 | 건강한 한국인 | *Taxonomic profiling of skin microbiome and correlation with clinical skin parameters in healthy Koreans*<br>Sci Rep 11:16269 (2021) | [10.1038/s41598-021-95734-9](https://doi.org/10.1038/s41598-021-95734-9) | `PRJNA723064` |
| 03 | 민감성 피부 | *Structures of the Skin Microbiome and Mycobiome Depending on Skin Sensitivity*<br>Microorganisms 8(7):1032 (2020) | [10.3390/microorganisms8071032](https://doi.org/10.3390/microorganisms8071032) | `PRJNA627788`(세균) + `PRJNA627798`(진균) |
| 04 | 여드름 | *Inferences in microbial structural signatures of acne microbiome and mycobiome*<br>J Microbiol 59(4):369–375 (2021) | [10.1007/s12275-021-0647-1](https://doi.org/10.1007/s12275-021-0647-1) | `PRJNA669317`(세균) + `PRJNA673754`(진균) |

01·03·04는 중앙대 + 아모레퍼시픽, 02는 서울대 연구다.

## 원시데이터 내려받기

- **출처**: ENA (European Nucleotide Archive) FTP
- **시점**: 2026-08-25
- **규모**: 7 accession · 429 run · 1,802 파일 · 7.1 GB
- **검증**: 모든 파일을 **ENA 등록 md5와 대조**해 일치 확인 (실패 0건)

원시 FASTQ는 이 저장소에 넣지 않았다 (`example_fastq/`의 예제 1쌍만 포함).
필요하면 accession으로 ENA/SRA에서 직접 받을 수 있다.

## 임상 메타데이터 출처

**BioSample·SRA에는 임상정보가 거의 없다.** 아래는 전부 논문 보충자료에서 추출한 것이다.

| 스터디 | 보충자료 | 받은 경로 |
|---|---|---|
| 01 노화 | Supplementary Table S1 (xlsx) | `static-content.springer.com` (Springer ESM) |
| 02 건강 | Supplementary Data 1(설문) + 2(생물물리) (xlsx) | `static-content.springer.com` |
| 03 민감성 | Table S2 (xlsx) | EuropePMC `supplementaryFiles` (PMC7409107) |
| 04 여드름 | Supplementary Table S1 (**PDF 2단 표**) | `static-content.springer.com` |

### 추출하면서 확인한 것

- **02 건강** — 논문 피험자 ID(`1902-003-007`)와 BioSample 이름(`YC7`)이 다르다.
  `-003-`=젊은군 / `-004-`=고령군 + 피험자 번호로 대응시키고,
  BioSample 채취일(2019-02-11 / 2019-11-15)로 **102/102 일치**를 확인했다.
- **04 여드름** — 여드름/건강 **군 라벨이 BioSample·샘플명 어디에도 없고** 보충자료 PDF에만 있다.
  33명 전원 복원, 군 충돌 0건, 논문 보고치(여드름 17 / 건강 16)와 일치.
- **01 노화** — 16S 51건 / ITS 60건의 QC 통과 수가 **등록 run 수와 정확히 일치**한다.

## 이 저장소에 없는 것과 그 이유

- **`PRJNA613934`** — `PRJNA614620`과 50개 샘플이 리드까지 동일한 중복 등록이라 제외했다.
- **`PRJNA673754`** — `PRJNA669317`과 66개 중 58개가 동일 파일이라 제외했다.
- 조사 대상이었던 나머지 9개 스터디(두피 AGA, 화상, 쌍둥이, 식이 등)는
  **샘플별 임상정보를 얻지 못해** 대상에서 뺐다. 논문이 변수를 보고하더라도
  보충표가 군 요약(mean±SD)뿐이면 샘플에 붙일 수 없다.

## ⚠ 스터디 1과 4는 데이터가 겹친다

같은 연구실이 같은 시퀀싱 데이터를 여러 BioProject에 나눠 등록했다.
리드 내용을 직접 대조한 결과 **`01_aging`과 `04_acne` 사이에 27개 run이 완전히 동일**하고,
배포 파일 기준으로 `sample_id`가 **13개 겹친다** (`Ca.23`, `Ca.25`, `Fa.23` …).

**두 스터디를 합쳐 표본 수를 늘리면 안 된다.**
파일 md5로는 잡히지 않는다 — 재압축 때문에 md5가 달라진다. 리드 내용으로 대조해야 한다.

## 라이선스·인용

원 데이터는 각 논문 저자의 것이고 ENA/SRA에 공개되어 있다.
이 자료를 쓴 결과를 발표할 때는 **위 표의 원 논문 4편을 인용**해야 한다.
이 저장소는 수업 목적의 재가공물이다.
