# figures — 데이터 표 예시 (01_aging 기준)

PPT에 붙여 쓰는 표 스크린샷이다. **01번 노화 스터디**를 예로 각 파일이 어떻게 생겼는지 보여준다.
나머지 세 스터디도 파일 구조는 같고 컬럼 구성만 다르다.

| 그림 | 파일 | 이 그림으로 설명할 것 |
|---|---|---|
| `01_sample_info.png` | `metadata/sample_info/01_aging_16S_sample_info.tsv` | **분석의 시작점.** 한 행에 식별·비교군·다양성·임상·미생물이 모두 있다 |
| `02_genus_count.png` | `16S_count/01_aging_16S_genus_count.tsv` | 원시 리드 수(정수). 행 합 = `total_reads` |
| `03_genus_pct.png` | `16S_count/01_aging_16S_genus_pct.tsv` | 상대풍부도(%). 행 합 = 100 |
| `04_genus_long.png` | `16S_count/01_aging_16S_genus_long.tsv` | 롱 포맷 — 한 행 = (샘플 × 속) |
| `05_genus_taxonomy.png` | `16S_count/01_aging_16S_genus_taxonomy.tsv` | 속 → 문·강·목·과 계보 |
| `06_clinical.png` | `metadata/clinical_data/01_aging_clinical.tsv` | 논문 보충자료 원본 임상표 |
| `07_asv_count.png` | `asv/01_aging_16S_asv_count.tsv` | ASV 수준. 행이 ASV, 열이 샘플로 **방향이 반대** |

## 컬럼 색 (그림 안 범례와 동일)

| 색 | 뜻 |
|---|---|
| 파랑 | 식별 (run · sample_id · subject · body_site) |
| 초록 | 비교군 (group · age · sex) |
| 노랑 | 다양성 (Observed · Shannon) — 우리가 계산한 값 |
| 주황 | 임상 측정 (moisture · sebum · pH · TEWL) |
| 보라 | 미생물 (속 상대풍부도 %) |
| 청록 | 논문이 보고한 값 (shannon_16S · n_asv_16S · qc_pass_16S) |
| 진파랑 | 카운트 (total_reads · count) |

## 슬라이드에서 짚어주면 좋은 것

- **`01_sample_info.png`** — 비교군을 고르게 뽑아 놓았다. 고령군(O)은 `sebum` 8.5~20.5에
  `g_Cutibacterium` 2~20%, 젊은군(Y)은 `sebum` 27~61에 `g_Cutibacterium` 38~66%로
  **피지와 우점 속이 같이 움직이는 것**이 표에서 바로 보인다.
- **`02` vs `03`** — 같은 데이터의 카운트와 %다. 카운트는 심도가 제각각(3,625 ~ 59,400)이고
  %는 행 합이 100으로 고정된다. **왜 심도 보정이 필요한지** 두 그림으로 설명할 수 있다.
- **`06_clinical.png`** — `Ca.36`은 `qc_pass_16S = no`이고 논문 보고값이 `—`다.
  **임상표에는 있지만 전처리에서 탈락한 샘플**이 있다는 걸 보여준다.
- **`04_genus_long.png`** — 같은 `run`이 반복되고 `genus`만 바뀐다. 와이드와 롱의 차이를
  한 장으로 설명할 수 있다.

## 재생성

```bash
python3 release/workflow/scripts/make_table_figures.py /BiO/Live/jsungwon/microbiome-2026
```

headless Chrome으로 HTML 표를 캡처한다. 다른 스터디로 바꾸려면 스크립트의 `FIGS` 안
파일 경로를 `02_healthy` 등으로 바꾸면 된다.
