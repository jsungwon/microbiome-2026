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
| 05 | 메트포르민 **장내** | *Association of metformin administration with gut microbiome dysbiosis in healthy volunteers*<br>PLoS One 13(9):e0204317 (2018) | [10.1371/journal.pone.0204317](https://doi.org/10.1371/journal.pone.0204317) | `PRJEB24497` |
| 07 | 화장품 중재 | *Effect of the skincare product on facial skin microbial structure and biophysical parameters*<br>MicrobiologyOpen 10(5):e1236 (2021) | [10.1002/mbo3.1236](https://doi.org/10.1002/mbo3.1236) | `PRJEB44885` |
| 06 | 화장품·피부수분 | *Effects of cosmetics on the skin microbiome of facial cheeks with different hydration levels*<br>MicrobiologyOpen 7(2):e00557 (2018) | [10.1002/mbo3.557](https://doi.org/10.1002/mbo3.557) | `PRJNA345237` / `SRP090974` |
| 08 | 아토피 피부염 | *Staphylococcal Communities on Skin Are Associated with Atopic Dermatitis and Disease Severity*<br>Microorganisms 9(2):432 (2021) | [10.3390/microorganisms9020432](https://doi.org/10.3390/microorganisms9020432) | `PRJEB42898` |
| 09 | 여드름·이소트레티노인 | *Cutibacterium and Staphylococcus dysbiosis of the skin microbiome in acne and its decline after isotretinoin treatment*<br>JEADV Clin Pract 3(5):1454–1466 (2024) | [10.1002/jvc2.487](https://doi.org/10.1002/jvc2.487) | `PRJNA1044749` |
| 10 | 건선 다부위 | *Alteration of the cutaneous microbiome in psoriasis and potential role in Th17 polarization*<br>Microbiome 6:154 (2018) | [10.1186/s40168-018-0533-1](https://doi.org/10.1186/s40168-018-0533-1) | `PRJEB25915` |
| 11 | 두피 건선·지루피부염 | *Skin microbiome signatures associated with psoriasis and seborrheic dermatitis*<br>Exp Dermatol 31(7):1116–1118 (2022) | [10.1111/exd.14618](https://doi.org/10.1111/exd.14618) | `PRJNA788988` |
| 12 | 주사 — 피부·장·혈액 | *Characteristics of the Stool, Blood and Skin Microbiome in Rosacea Patients*<br>Microorganisms 12(12):2667 (2024) | [10.3390/microorganisms12122667](https://doi.org/10.3390/microorganisms12122667) | `PRJNA1189573` |
| 13 | 지질–미생물 (여드름·아토피) | *Shotgun-lipidomics reveals disease specific microbiome-lipid correlations in acne vulgaris and atopic dermatitis*<br>미게재 데이터셋 (Helmholtz Munich) | — | `PRJEB66070` |

**01–07은 한국인 코호트**(01·03·04 중앙대+아모레퍼시픽, 02 서울대, 07 LG생활건강)이고,
**08–13은 질환 코호트**로 덴마크·미국·중국·헝가리·독일에서 왔다.
피부가 아닌 검체가 둘 있다 — **05는 장내(분변)**, **12는 피부·대변·혈액 세 가지**다.
집단·부위·플랫폼이 다르므로 스터디를 가로질러 합칠 때는 반드시 배치 효과를 의심할 것.

## 원시데이터 내려받기

- **출처**: ENA (European Nucleotide Archive) FTP
- **시점**: 2026-08-25 (01–07) · 2026-08-30 (08–13)
- **규모**: 15 accession · 2,012 run · 3,784 파일 · 54.6 GB
  (01–07 9 accession 557 run 11.7 GB + 08–13 6 accession 1,455 run 42.9 GB)
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
| 05 메트포르민 | **S1.2 Table (docx) — 셀 배경색 인코딩** | journals.plos.org |
| 06 화장품 | Supplementary Table 1 (docx) | EuropePMC (PMC5911989) |
| 07 화장품 중재 | Table A2 (본문 부록) | EuropePMC (PMC8494714) |
| 08 아토피 | **저자 GitHub 저장소의 ENA 제출 시트 (xls)** | `github.com/ssi-dk/AD_staphylome_project` |
| 09 여드름 DK | (미확보 — Wiley 403) | 샘플명에서 군·부위만 복원 |
| 10 건선 | **BioSample 속성** — 논문 보충자료가 아니다 | ENA `browser/api/xml` |
| 11 두피 | (없음 — 2쪽 연구서한) | 샘플명에서 복원 |
| 12 주사 | 논문 Table 1 (**군 단위만**) | PMC11728485 |
| 13 지질–미생물 | (없음 — 미게재) | 샘플명에서 복원 |

### 추출하면서 확인한 것

- **02 건강** — 논문 피험자 ID(`1902-003-007`)와 BioSample 이름(`YC7`)이 다르다.
  `-003-`=젊은군 / `-004-`=고령군 + 피험자 번호로 대응시키고,
  BioSample 채취일(2019-02-11 / 2019-11-15)로 **102/102 일치**를 확인했다.
- **04 여드름** — 여드름/건강 **군 라벨이 BioSample·샘플명 어디에도 없고** 보충자료 PDF에만 있다.
  33명 전원 복원, 군 충돌 0건, 논문 보고치(여드름 17 / 건강 16)와 일치.
- **01 노화** — 16S 51건 / ITS 60건의 QC 통과 수가 **등록 run 수와 정확히 일치**한다.
- **05 메트포르민** — 위장관 부작용 중증도가 보충자료 **S1.2 Table**에 피험자별로 있는데,
  **셀 배경색으로만 표시**돼 있어 텍스트 추출로는 빈 표로 보인다.
  docx의 셀 음영(`w:shd/@w:fill`)을 읽어 복원했다: 초록=없음 / 노랑=경증 / 빨강=중증.
  피험자의 군은 관측된 날들 중 최중증도로 정했고, 결과가 **없음 3 / 경증 6 / 중증 9** 로
  논문 보고치와 정확히 일치한다.
  ⚠ `Subject_N` → ENA `S{N}` 대응은 **추론**이다(둘 다 1–18, 같은 논문·같은 순서).
  나이·성별·BMI는 중앙값만 보고돼 피험자별로는 붙일 수 없다.

## 08–13 처리에서 걸러낸 함정

이 여섯 데이터셋은 등록된 그대로 파이프라인에 넣으면 **오류 없이 끝나면서 조용히 틀린다.**
실제로 실측해서 잡아낸 것들이다.

| # | 함정 | 그냥 돌렸다면 |
|---|---|---|
| 08 | 프라이머 앞에 **0/2/7bp 가변 스페이서**(phased primer). 앵커(`^`) 매칭은 34%만 잡고, `--discard-untrimmed`가 양쪽을 요구해 손실이 곱해진다 | 리드 **80% 손실** |
| 08 | 스페이서 때문에 트리밍 후 길이가 276–284bp인데 `truncLen 280`. DADA2는 짧은 리드를 자르는 게 아니라 **버린다** | 리드 **22% 추가 손실** |
| 09 | 품질값이 전 염기 `?`(Q30) **단일 상수**. loess 적합 불가 | `Error matrix is NULL`로 **즉시 중단** |
| 10 | 샘플명 접미 `B`는 등(Back)이 아니라 **둔부 주름** | 67샘플 **부위 오분류** |
| 10 | 인서트 465–497bp인데 품질만 보면 260/220이 자연스럽다 | 병합 **55%**, 긴 분류군 소실 |
| 11 | 제출물이 원시 리드가 아니라 **이미 병합된 서열**(409/429bp) | paired 처리 시 전량 실패 |
| 11 | BioProject 설명의 **환자 수가 논문과 뒤바뀜** | 건선/지루피부염 **라벨 교체** |
| 12 | 혈액이 **저바이오매스** | 시약 오염을 실제 신호로 해석 |
| 13 | **파일 단위로 R1/R2가 뒤집힘** (111런 중 58런) | 같은 균이 **두 ASV로 분리** |
| 13 | `S1` 같은 앞 번호가 피험자가 아니라 **매칭 세트** | 서로 다른 두 사람이 **한 명으로 합쳐짐** |

교훈은 하나다 — **요약 지표(병합률·다양성)는 이 함정들을 거의 다 통과시킨다.**
새 데이터를 넣을 때는 프라이머 시작 위치, 트리밍 후 길이 분포, 앰플리콘 전장 분포를
직접 재고 `track_reads.tsv`의 단계별 보존율을 확인해야 한다.

### 09번 임상정보는 절반만 있다

논문 Table S1A/S1B에 개인별 연령·성별·IGA 중증도가 있지만
Wiley가 보충자료 내려받기를 403으로 막아 확보하지 못했다.
군(여드름/건강)·부위(볼/등/이마)·피험자는 샘플명에서 전부 복원했다.
기관 구독이 있으면 `jvc2487-sup-0003-Table_S1_rev.xlsx`를 받아 `sample_id`로 붙이면 된다.

### 11번 군 라벨을 논문 쪽으로 정한 근거

BioProject 설명은 "건선 45 / 지루피부염 37"이라고 적었지만 논문은 그 반대다.
등록된 샘플의 **고유 피험자 수가 `SD` 45명 / `P` 37명 / `HC` 30명**으로
**논문과 정확히 일치**하므로 논문을 따랐다 (SD=지루피부염, P=건선).

## ⚠ 06 화장품 — 시퀀스를 샘플별로 나눌 수 없다

논문은 30명 × 3시점 = **90개 시료를 바코드로 다중화**해 454로 시퀀싱했다고 밝히지만,
SRA에 올라온 것은 **run 2개**뿐이고 확인 결과:

- 두 run(`SRR4379959`, `SRR4381489`)이 **완전히 동일한 파일**이다 (리드 서열 해시 일치, 둘 다 1,253,852 리드)
- 리드가 바코드가 아니라 **프라이머(Bac541R)로 시작**한다 — 상위 2종 서열이 97%를 차지
- FASTQ 헤더는 454 웰 ID(`JKQJY0V01CW22C`)뿐으로 시료 정보가 없다

즉 **바코드가 이미 제거된 채로 하나로 합쳐져** 올라왔다. 어떤 리드가 어느 시료인지 복원할 수 없어
속(genus)·ASV 테이블을 만들지 못했다. 대신 보충자료 Supplementary Table 1에
**90개 시료의 논문 보고 다양성 지표**가 있어 그것만 정제했다.

## 이 저장소에 없는 것과 그 이유

- **`PRJNA613934`** — `PRJNA614620`과 50개 샘플이 리드까지 동일한 중복 등록이라 제외했다.
- **`PRJNA673754`** — `PRJNA669317`과 66개 중 58개가 동일 파일이라 제외했다.
- **08번의 `tuf` 466런, 09번의 `SLST` 151런·`tuf2` 85런** — 같은 프로젝트에 함께 등록돼 있지만
  단일유전자 타이핑이라 SILVA로 분류할 수 없다. 16S 런만 골라 처리했다.
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
이 자료를 쓴 결과를 발표할 때는 **위 표의 원 논문을 인용**해야 한다.
이 저장소는 수업 목적의 재가공물이다.
