# 🏰 에버랜드 방문객 경험 데이터 분석

## 1. 개요

### 🔎 핵심 결론 요약
본 분석을 통해 에버랜드의 고객 만족도 하락은  
**1) 대기 중심의 운영 비효율, 2) 지속 가능한 IP 부족, 3) 시설 노후화**라는 세 가지 구조적 요인이 핵심임을 확인했다.

구글·네이버 리뷰 및 글로벌 테마파크 벤치마킹 결과,
- **대기시간의 체감 피로**
- **콘텐츠/IP 경쟁력 약화**
- **구역별 시설 노후화**

가 부정 경험을 유발하는 주요 요인으로 나타났다.

→ 따라서 에버랜드는 **스마트 예약 시스템 도입**, **IP 플랫폼 확대**, **시설 리뉴얼**을 통해  
체류가치(Value of Stay)를 강화하고 글로벌 경쟁력을 확보해야 한다.

### 🎯 분석 목적과 기대효과
본 분석은 에버랜드의 **체감 만족도 하락 원인**을 정량적으로 규명하고  
이를 기반으로 **운영·콘텐츠·시설 개선 전략**을 제안하는 것을 목표로 한다.

이를 통해,
- 재방문율 상승  
- 평균 대기시간 감소  
- 글로벌 TOP 10 진입  

등의 장기적 성장을 위한 의사결정을 지원한다.

---

## 3. 분석 배경 및 목적

### 🧩 문제 정의
- 2019년 대비 2024년 방문객 수는 **84% 회복**,  
  그러나 **2025년 상반기 방문객 수는 전년 대비 37% 감소**
- 운영·콘텐츠·시설 전반에서 **체감 만족도가 회복되지 못함**
- 리뷰 데이터에서 **대기·시설·운영 관련 불만 증가**

### 분석 목적
1. 방문객의 부정 경험을 유발하는 핵심 요인 규명  
2. 도쿄·상하이 디즈니랜드 대비 방문객 수 부족 원인 진단  
3. 운영 효율·콘텐츠·시설 개선 전략 제안  
4. 데이터 기반 **체류 가치(Experience Value)** 강화 방안 도출  

---

## 4. 데이터 개요

### 📊 데이터 출처
- 구글맵 리뷰  
- 네이버 방문자 리뷰  
- 한국관광공사 방문객 통계  
- 통계청 이동 데이터  
- 기상청 날씨 데이터  
- Kaggle 글로벌 테마파크 대기시간 데이터  

### 📏 데이터 범위
- 총 리뷰 데이터: **6,290개**
- 사용 컬럼: 리뷰 텍스트, 평점 라벨(5점↑=1, 4점↓=0)
- 글로벌 대기시간 비교 데이터 포함

### 데이터 정제
- 네이버 리뷰 평점 미존재 → **KoELECTRA로 자동 감정 라벨링**
- 3개 감정분석 모델 비교 후 가장 안정적인 모델 채택
- 전체 데이터 약 30% 수작업 검수
- 불용어 제거 → 형태소 분석 → 키워드 추출
- TF-IDF 벡터화 + 로지스틱 회귀로 영향도 분석

### 용어 정의
- **오즈비(OR)**: 긍정 리뷰 가능성에 대한 상대적 영향  
- **체류가치(Value of Stay)**: 대기·경험·IP로 형성되는 만족 지표  
- **콘텐츠/IP 경쟁력**: 테마·캐릭터·세계관이 재방문을 유도하는 정도  

### 분석 도구
- Python (pandas, sklearn, matplotlib, transformers)  
- Google Colab  
- 딥러닝 모델: KoELECTRA, KcELECTRA, KLUE-roberta  
- 머신러닝: Logistic Regression, SVM, XGBoost  
- 시각화: seaborn, wordcloud  

---

## 5. 분석 방법론

### 기술통계
- 리뷰 평점 분포 분석  
- 키워드 출현 빈도 분석  

### EDA
- 워드클라우드 기반 부정 키워드 탐색  
- '대기/아이/운영/시설' 언급 증가 패턴  
- 글로벌 디즈니/유니버설 대기시간 비교  

### 가설 설정
- 가설 1: 운영 효율성 저하 → 불만 증가  
- 가설 2: 지속 가능한 콘텐츠/IP 부족 → 재방문 저하  
- 가설 3: 시설 노후화 → 경험 품질 저하  

### ML/통계 분석
- TF-IDF + 로지스틱 회귀로 영향도(OR, p-value) 분석  
- 딥러닝 감정분석으로 리뷰 자동 라벨링  

### 모델 검증
- F1-score로 모델 성능 평가  
- 유의수준 p < 0.05 변수만 채택  

---

## 6. 분석 결과

### 6-1. 부정 리뷰 분석 주요 발견
<img width="400" height="250" alt="image" src="https://github.com/user-attachments/assets/a052faf3-c178-4cdd-a7f1-58af41fd562a" />

- 최빈 부정 키워드: **대기, 아이**  
- 가족 방문 비중이 높아 **긴 대기시간 + 비효율적 운영**이 피로도 상승

  <img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/17478d1d-8ad7-48d9-a86d-26d620922538" />

- '시설' 관련 부정 비율은 **56%**, 운영(71%) 다음으로 높은 불만 비중  
- 시설 노후화는 체험 품질 전반을 떨어뜨리는 핵심 요인  

### 6-2. ML 기반 영향도 분석(오즈비)
<img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/78fbd3bc-8e8a-400e-bf51-6594e20e768f" />


<img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/c7c045eb-51b0-4963-b917-a49878e0f8c6" />

- **운영 관련 OR = 0.49**  
  → 긍정 리뷰 가능성을 절반 수준으로 감소  
- **시설 관련 OR = 0.41**  
  → 시설 노후화의 강한 부정 효과  
- **콘텐츠/IP OR = 1.21**  
  → 콘텐츠/IP는 긍정 경험을 만드는 핵심 요인  

→ 운영·시설 문제는 즉각적인 불만 요인,  
→ 콘텐츠/IP는 장기적 만족 자산임.

### 6-3. 글로벌 벤치마킹 결과 요약
<img width="1752" height="564" alt="image" src="https://github.com/user-attachments/assets/c3455189-89db-4026-ba10-2a4b06521277" />
<img width="1978" height="634" alt="image" src="https://github.com/user-attachments/assets/4c3020b5-e93d-4a37-a32c-23eaa5c65ea6" />

- 디즈니는 방문객이 2~3배 많아도  
  평균 대기시간 **20~35분** 유지  
- 대기공간에 **스토리·체험 요소** 강화  
- FastPass·Virtual Queue로 혼잡 완화  
- 에버랜드는 부지가 더 넓음에도  
  **대기시간이 더 길고**, 줄서기 중심 대기공간 구성  

→ 운영 체계 차이가 대기 피로도를 좌우하는 핵심 요인.

### 6-4. 가설 검증 결과
| 가설 | 결과 | 근거 |
|------|------|------|
| 운영 비효율 → 불만 증가 | 수용 | OR=0.49, 부정 비중 가장 높음 |
| IP 부족 → 재방문 저하 | 수용 | 콘텐츠 OR=1.21 |
| 시설 노후화 → 경험 저하 | 수용 | 시설 부정 56% |

### 6-5. 핵심 인사이트 요약
1. 대기시간 '체감 경험'이 만족도를 결정  
2. 콘텐츠/IP는 긍정 경험의 핵심 레버  
3. 시설 노후화는 재방문 의도 약화  

---

## 7. 결론 및 시사점

### 핵심 인사이트
1. 운영·시설·콘텐츠 **3개 축에서 구조적 개선 필요**  
2. 대기는 **시간 문제가 아닌 경험 품질 문제**  
3. IP 경쟁력이 파크의 **장기 생명력**을 좌우  

### 전략 제안

#### 전략 1. 스마트 예약 시스템 & 큐라인 혁신
- FastPass/Virtual Queue 도입  
- 대기시간 25~30% 감소  
- AR·스토리 기반 큐라인으로 “기다림을 콘텐츠로” 전환  

#### 전략 2. 콘텐츠/IP 플랫폼 강화
- K-POP, 드라마 등과 협업해 국내형 장기 IP 구축  
- 시즌 이벤트 → 상시 체험 콘텐츠화  
- 캐릭터/IP 기반 구역 설계  

#### 전략 3. 시설 리노베이션 & 첨단 어트랙션 도입
- 20년 이상 된 구역 전면 개편  
- AR/VR 기반 몰입형 어트랙션  
- 글로벌 TOP 10 수준 라인업 확보  

---

## 7-3. 한계점 및 향후 과제
- 에버랜드 내부 정량 데이터 부족 → 디즈니/유니버설로 대체  
- 실제 운영 로그 확보 시 M/M/1 기반 시뮬레이션 가능  
- 추가 사용자 인터뷰·AB 테스트 필요  

---

## 8. 부록

### 딥러닝 모델 평가표
<img width="500" height="600" alt="image" src="https://github.com/user-attachments/assets/5b4cb59e-1dba-474b-a38c-5941e839245c" />
  

### 머신러닝 모델 평가표
<img width="500" height="600" alt="image" src="https://github.com/user-attachments/assets/bdd4c994-3c7f-47c5-a1e0-227a1e13c6b5" />


### 참고 문헌
- Li J., Li Q. *Analysis of queue management in theme parks introducing the Fast Pass system.* Heliyon, 2023.  
- Rustad C. *Designing The Perfect Queue Line.* Journal of Student Research.  
- Zhang X. *Exploring the Success of Disney Parks through Intellectual Properties and Operation Strategies.*  
- Desai H., Pearlman D. *Determinants of Capital Expenditures Among Theme Parks.* European Business Review, 2024.
