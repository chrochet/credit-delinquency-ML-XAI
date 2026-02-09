# credit-delinquency-ML-XAI

**머신러닝 + XAI(SHAP) 기반 신용카드 연체 예측 프로젝트**
---

## 🖥️ 프로젝트 소개

신용카드 연체 예측은 금융기관의 신용위험 관리에서 핵심 과제이다.
기존 신용평가 방식은 공적 기록·상환 이력 등 전통적 금융 변수와 로지스틱 회귀 기반 접근이 많았으나, 최근에는 **머신러닝과 비재무적 특성(인구통계·고용 형태 등)을 결합**하여 예측 정확도를 높이려는 연구가 확산되고 있다.
본 프로젝트는 Kaggle 신용카드 사용자 데이터(26,457명)를 활용해 **연체 여부 이진 분류 모델을 구축**하고, **SHAP 기반 XAI 분석**으로 주요 변수의 기여 방향과 크기를 해석 가능하게 제시한다.

---

## 🕰️ 개발 기간

* 2024.9.11 - 2025.2.9

---

## 🧑‍🤝‍🧑 멤버 구성

* 유지현
* 김**
* 김**
* 정**

---

## 🏆 수상

**한국디지털콘텐츠학회 하계종합학술대회 대학생 논문경진대회 동상**

KCI논문등재
https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART003284895
---



## 🧩 연구 / 시스템 구조 (Workflow)

1. **데이터 수집 및 전처리**

* Kaggle 플랫폼에서 26,457건 신용카드 사용자 데이터 수집
* 범주형 변수(교육수준/결혼여부/주거형태/소득유형/직업유형 등) **원-핫 인코딩**
* `days_employed`는 고용 이력이 없는 경우 0으로 치환

2. **타겟(라벨) 정의**

* `delinquency`: 0(안정), 1(주의), 2(위험)
* 본 연구 목적에 맞춰 **0 → 0**, **(1,2) → 1**로 통합하여 **이진 분류 문제로 재정의**

3. **클래스 불균형 처리(SMOTE)**

* 클래스 분포가 심각하게 불균형하여 학습 편향 가능성 존재
* 학습 세트에 한해 **SMOTE 적용**, 최종적으로 두 클래스 모두 16,264건으로 균형화 

4. **모델 성능 평가(교차검증)**

* **Stratified K-Fold 교차검증(K=5)** 적용
* Accuracy / Precision / Recall / F1-score로 성능 비교

5. **변수중요도 결과**

6. **설명가능성 확보(XAI: SHAP)**

* LightGBM에 대해 변수중요도 및 SHAP 분석 수행
* 예측에 영향을 미치는 핵심 변수와 방향성을 시각화하여 **모델 투명성 및 해석 가능성 확보** 

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

## 📌 주요 기능

### 01 데이터 수집 및 전처리
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/01.-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%88%98%EC%A7%91-%EC%A0%84%EC%B2%98%EB%A6%AC)
* Kaggle 데이터 기반 인구통계·경제 변수 확보
* 범주형 변수 원-핫 인코딩 적용
* 학습/테스트 데이터 **7:3 분할** 및 층화추출(Stratified sampling) 적용 

### 02 클래스 불균형 처리 (SMOTE)
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/02.-SMOTE-%EB%B6%88%EA%B7%A0%ED%98%95-%EC%B2%98%EB%A6%AC)
* 목표 변수의 심각한 불균형으로 인한 모델 편향 문제 개선
* 학습 데이터에서 SMOTE 적용 후 **양 클래스 균형(16,264건)** 확보

### 03 머신러닝 모델 학습 및 비교
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/03.-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%AA%A8%EB%8D%B8-%ED%95%99%EC%8A%B5-%EB%B0%8F-%EB%B9%84%EA%B5%90)
* RandomForest / XGBoost / LightGBM 모델 구축


### 04 성능 평가 및 최종 모델 선정
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/04.-%EC%84%B1%EB%8A%A5-%ED%8F%89%EA%B0%80-%EB%B0%8F-%EC%B5%9C%EC%A2%85-%EB%AA%A8%EB%8D%B8-%EC%84%A0%EC%A0%95)
* Accuracy / Precision / Recall / F1-score로 성능 평가
  

### 05 변수중요도 결과
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/05.-%EB%B3%80%EC%88%98%EC%A4%91%EC%9A%94%EB%8F%84)


### 06 XAI(SHAP) 기반 모델 해석
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/06.-XAI(SHAP)-%EA%B8%B0%EB%B0%98-%EB%AA%A8%EB%8D%B8-%ED%95%B4%EC%84%9D)
* 변수 중요도 + 예측 기여 방향을 함께 제시
* 단순 정확도뿐 아니라 **연체 위험 요인의 구조적 이해**를 지원


### extra) 기반 하이퍼파라미터 최적화
[상세보기 · WIKI](https://github.com/chrochet/credit-delinquency-ML-XAI/wiki/extra)-%ED%95%98%EC%9D%B4%ED%8D%BC%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0-%EC%B5%9C%EC%A0%81%ED%99%94).
* 모델별 탐색 공간 정의 후 최적 조합 도출
* 규제/샘플링/트리 깊이 등 파라미터를 함께 최적화 

