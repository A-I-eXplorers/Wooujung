# 📊 데이터 탐색적 분석(EDA) 및 전처리 프로젝트

이 저장소는 머신러닝 및 데이터 분석의 대표적인 벤치마크 데이터셋인 **Iris(붓꽃)**, **Titanic(타이타닉)**, **Wine(와인)** 데이터를 활용하여 데이터 구조 파악, 결측치 및 이상치 처리, 파생 변수 생성(Feature Engineering), 그리고 시각화를 통한 핵심 인사이트 도출 과정을 정리한 프로젝트입니다.

---

## 🛠️ 기술 스택 및 라이브러리
* **Language:** Python 3
* **Data Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`, `seaborn`
* **Datasets & Preprocessing:** `scikit-learn` (`load_iris`, `load_wine`, `StandardScaler`), `seaborn` (`titanic`)

---

## 📁 데이터셋별 분석 내용 및 핵심 인사이트

### 1. Iris (붓꽃) 데이터셋 EDA
* **데이터 개요:** 150개 샘플, 4개의 수치형 피처(`sepal length`, `sepal width`, `petal length`, `petal width`)와 3개 품종(`setosa`, `versicolor`, `virginica`)으로 구성.
* **전처리 진단:** 결측치 및 중복 데이터가 없으며, 품종별 각 50개씩(`1:1:1`) 완벽한 균형을 이루고 있어 별도의 리샘플링이 불필요함. `sepal width`의 일부 극단값은 자연적인 개체 차이로 판단하여 보존.
* **주요 분석 결과:**
  * **강한 상관관계:** `petal length`와 `petal width` 간 상관계수가 0.96으로 매우 높으며, `sepal length` 역시 꽃잎 크기와 강한 양의 상관관계($0.82 \sim 0.87$)를 보임.
  * **분류 변별력:** `Setosa` 품종은 꽃잎 크기가 현저히 작아(`petal width <= 0.6cm`) 선형 분리가 가능함. `Versicolor`와 `Virginica`는 꽃받침(Sepal)보다 **꽃잎(Petal) 변수**를 기준으로 명확히 구분됨.

---

### 2. Titanic (타이타닉) 데이터셋 전처리 및 피처 엔지니어링
* **데이터 개요:** 891명의 승객 데이터(15개 컬럼)를 대상으로 모델 학습을 위한 데이터 정제 및 파생 변수 생성 수행.
* **주요 전처리 기법:**
  * **결측치 대체:** `age`(177개 결측)는 이상치 영향을 줄이기 위해 객실 등급(`pclass`)과 성별(`sex`) 그룹별 **중앙값(Median)**으로 대체. `embarked`(2개 결측)는 최빈값(`S`)으로 대체.
  * **결측치의 정보화:** 결측 비율이 약 $77.2\%$에 달하는 `deck` 컬럼은 단순 삭제 대신 기록 유무를 나타내는 이진 변수(`has_deck`)로 변환.
  * **이상치 및 왜도 완화:** 극단적인 고가 티켓으로 인해 왜도(Skewness)가 4.79에 달하던 `fare` 변수에 로그 변환(`np.log1p`)을 적용하여 왜도를 0.39로 개선.
  * **인코딩:** 성별 이진 매핑(`sex_encoded`) 및 범주형 변수(`embarked`, `age_group`) 원-핫 인코딩(`drop_first=True`) 적용.
* **주요 분석 결과:**
  * **객실 정보 유무(`has_deck`):** 객실 기록 보유 그룹의 생존율(67.00\%$)이 미보유 그룹($29.94\%$)보다 약 $37\%p$ 높음.
  * **동반 가족 규모(`family_size`, `is_alone`):** 혼자 탑승한 경우($30.35\%$)보다 가족 동반 시($50.56\%$) 생존율이 높았으며, 특히 2~4인 소규모 가족의 생존율이 가장 높고 5인 이상 대가족은 급감하는 비선형적 패턴을 확인.

---

### 3. Wine (와인) 데이터셋 스케일링 및 다변량 분석
* **데이터 개요:** 178개 와인 샘플, 13개의 화학 성분 피처(실수형)와 3개 등급(`class_0`, `class_1`, `class_2`)으로 구성.
* **전처리 진단:** 결측치 및 중복 행이 전혀 없으나(`0개`), `proline`($278 \sim 1680$)와 `nonflavanoid_phenols`($0.13 \sim 0.66$) 등 변수 간 스케일 격차가 매우 크므로 `StandardScaler`를 통한 표준화 적용.
* **주요 분석 결과:**
  * **핵심 분류 변수:** 타겟(`wine_class`)과 강한 음의 상관관계를 보이는 `flavanoids`($-0.85$), `od280/od315`($-0.79$), `total_phenols`($-0.72$), `proline`($-0.63$)이 품종을 가르는 핵심 지표임. 반면 `ash`($-0.05$)는 영향력이 거의 없음.
  * **다중공선성 주의:** `flavanoids`와 `total_phenols`의 상관계수가 **$0.86$**으로 매우 높아 향후 모델링 시 변수 선택(Feature Selection) 또는 차원 축소(PCA)가 필요함.
  * **품종별 특징:** `proline`은 `class_0`을, `od280/od315`는 `class_2`를 단독으로 분리하는 데 매우 효과적이며, `alcohol`과 `color_intensity`를 조합하면 세 품종이 2차원 평면에서 뚜렷한 3개의 군집을 형성함.

---

## 🚀 실행 방법
1. 저장소를 클론하거나 `.ipynb` 노트북 파일을 다운로드합니다.
2. 필요한 패키지를 설치합니다.
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn
   ```
3. Jupyter Notebook 또는 Google Colab 환경에서 각 노트북 셀을 순차적으로 실행하여 통계 리포트와 시각화 결과를 확인합니다.
