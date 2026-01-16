# credit-delinquency-ML-XAI

**머신러닝 + XAI(SHAP) 기반 신용카드 연체 예측 프로젝트**
---

## 🖥️ 프로젝트 소개

신용카드 연체 예측은 금융기관의 신용위험 관리에서 핵심 과제이다.
기존 신용평가 방식은 공적 기록·상환 이력 등 전통적 금융 변수와 로지스틱 회귀 기반 접근이 많았으나, 최근에는 **머신러닝과 비재무적 특성(인구통계·고용 형태 등)을 결합**하여 예측 정확도를 높이려는 연구가 확산되고 있다.
본 프로젝트는 Kaggle 신용카드 사용자 데이터(26,457명)를 활용해 **연체 여부 이진 분류 모델을 구축**하고, **SHAP 기반 XAI 분석**으로 주요 변수의 기여 방향과 크기를 해석 가능하게 제시한다.

---

## 🕰️ 개발 기간

* 2025.9.11 - 2025.2.9

---

## 🧑‍🤝‍🧑 멤버 구성

* 유지현
* 김**
* 김**
* 정**

---

## 🏆 수상

**한국디지털콘텐츠학회 하계종합학술대회 대학생 논문경진대회 동상**

---

## 🧩 연구 / 시스템 구조 (Workflow)

1. **데이터 수집 및 전처리**

* Kaggle 플랫폼에서 26,457건 신용카드 사용자 데이터 수집
* 범주형 변수(교육수준/결혼여부/주거형태/소득유형/직업유형 등) **원-핫 인코딩**
* `days_employed`는 고용 이력이 없는 경우 0으로 치환

2. **타겟(라벨) 정의**

* `delinquency`: 0(안정), 1(주의), 2(위험)
* 본 연구 목적에 맞춰 **0 → 0**, **(1,2) → 1**로 통합하여 **이진 분류 문제로 재정의** fileciteturn0file0

3. **클래스 불균형 처리(SMOTE)**

* 클래스 분포가 심각하게 불균형하여 학습 편향 가능성 존재
* 학습 세트에 한해 **SMOTE 적용**, 최종적으로 두 클래스 모두 16,264건으로 균형화 fileciteturn0file0

4. **모델 학습 및 하이퍼파라미터 튜닝(Optuna)**

* RandomForest / XGBoost / LightGBM 모델 구축
* Optuna 기반 하이퍼파라미터 탐색으로 최적 조합 도출

5. **모델 성능 평가(교차검증)**

* **Stratified K-Fold 교차검증(K=5)** 적용
* Accuracy / Precision / Recall / F1-score로 성능 비교 fileciteturn0file0

6. **설명가능성 확보(XAI: SHAP)**

* LightGBM에 대해 변수중요도 및 SHAP 분석 수행
* 예측에 영향을 미치는 핵심 변수와 방향성을 시각화하여 **모델 투명성 및 해석 가능성 확보** fileciteturn0file0

---

## ⚙️ 개발 환경

* **Language**: Python
* **ML Models**: LightGBM, XGBoost, RandomForest 
* **Hyperparameter Tuning**: Optuna 
* **Validation**: Stratified K-Fold Cross Validation(K=5) 
* **Imbalanced Learning**: SMOTE 
* **XAI**: SHAP(Shapley Additive Explanations) 
* **Dataset**: Kaggle Credit Card Users Dataset (N=26,457) 

---

## 📁 프로젝트 구조


```bash
credit-delinquency-ML-XAI/
├─ data/
│  ├─ raw/
│  └─ processed/
├─ notebooks/
│  ├─ 01_eda.ipynb
│  ├─ 02_model_training.ipynb
│  └─ 03_shap_analysis.ipynb
├─ src/
│  ├─ preprocessing.py
│  ├─ train.py
│  ├─ tune_optuna.py
│  ├─ evaluate.py
│  └─ explain_shap.py
├─ results/
│  ├─ metrics/
│  └─ figures/
└─ README.md
```

---

## 📌 주요 기능

### 01 데이터 수집 및 전처리
[상세보기 · WIKI]()
* Kaggle 데이터 기반 인구통계·경제 변수 확보
* 범주형 변수 원-핫 인코딩 적용
* 학습/테스트 데이터 **7:3 분할** 및 층화추출(Stratified sampling) 적용 

### 02 클래스 불균형 처리 (SMOTE)
[상세보기 · WIKI]()
* 목표 변수의 심각한 불균형으로 인한 모델 편향 문제 개선
* 학습 데이터에서 SMOTE 적용 후 **양 클래스 균형(16,264건)** 확보

### 03 머신러닝 모델 학습 및 비교
[상세보기 · WIKI]()
* RandomForest / XGBoost / LightGBM 모델 구축
* 앙상블 기반 모델의 학습 방식 차이 비교(배깅 vs 부스팅)

### 04 Optuna 기반 하이퍼파라미터 최적화
[상세보기 · WIKI]()
* 모델별 탐색 공간 정의 후 최적 조합 도출
* 규제/샘플링/트리 깊이 등 파라미터를 함께 최적화 

### 05 성능 평가 및 최종 모델 선정
[상세보기 · WIKI]()
* Accuracy / Precision / Recall / F1-score로 성능 평가
* LightGBM이 **Recall 및 F1-score에서 최고 성능**으로 최종 선정 

### 06 XAI(SHAP) 기반 모델 해석
[상세보기 · WIKI]()
* 변수 중요도 + 예측 기여 방향을 함께 제시
* 단순 정확도뿐 아니라 **연체 위험 요인의 구조적 이해**를 지원

---

## 📊 모델 성능(결과 요약)

세 모델의 성능 비교 결과는 다음과 같습니다. fileciteturn0file0

| Model        | Accuracy | Precision | Recall   | F1       |
| ------------ | -------- | --------- | -------- | -------- |
| RandomForest | 0.85     | 0.90      | 0.94     | 0.92     |
| **LightGBM** | **0.88** | 0.89      | **0.98** | **0.94** |
| XGBoost      | 0.88     | 0.90      | 0.96     | 0.93     |

---

## 🔍 변수 중요도 및 SHAP 인사이트

변수 중요도 및 SHAP 분석을 통해 다음과 같은 핵심 요인을 확인했습니다. fileciteturn0file0

### ✅ 핵심 영향 변수(상위)

* `month_card_issued` (신용카드 발급 경과 월 수)
* `days_birth` (출생 후 경과 일 수)
* `days_employed` (취업 후 경과 일 수)
* `income_total` (총소득)
* `family_size` (가족 구성원 수)

### ✅ 해석 요약

* `month_card_issued`가 높을수록 **연체 위험 증가 경향**
* `income_total`은 값이 클수록 전반적으로 **연체 위험 감소 경향(음의 기여 우세)**
* 가족 관련 변수는 **규모(family_size)**와 **구조(기혼 여부)**가 서로 다른 방식으로 위험에 영향을 미침

  * 가족 규모가 커질수록 위험 증가 경향
  * 기혼(`family_type_married`)은 위험 감소(안정 효과) fileciteturn0file0

---

## ✍️ 결론 및 시사점

본 프로젝트는 머신러닝 기반 신용카드 연체 예측에서 **예측 성능**과 **설명가능성(XAI)**을 동시에 확보했습니다. 특히 SHAP을 활용해 주요 변수 기여도를 정량화하고 영향 방향을 제시함으로써, 금융기관의 정책·심사 과정에서 활용 가능한 형태의 근거 기반 해석을 제공합니다. fileciteturn0file0

---
