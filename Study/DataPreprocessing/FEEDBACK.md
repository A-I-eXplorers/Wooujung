# 피드백 남기는 곳

## 심소은
Titanic
 
 위에서 중복 의미 컬럼 제거했다고 했는데 encode된 값과 원본이 같이 들어가있고, alone과 is_alone도 같이 들어가있고 원본이랑 파생 변수들이 공존되어있어서 나중에 문제가 될 수 있지 않을까?

Iris
 
 마지막에 일부 극단값이 관측되나 자연적인 개체 차이 범위 내이므로 이상치를 제거하지 않고 보존한다고 했는데 나중에 이상치에 민감한 knn 같은 모델에 학습할 때도 그대로 두는게 나을까?

Wine

처음에 df.drop(columns=['target'], inplace=True) 했는데 In[21]에서 heatmap 그릴 때 target 컬럼이 없는데 괜찮을려나?

## 이도연
Titanic

log scale 변환 방식 채용, 가족 수별 생존율을 시각화하여 더 입체적인 정보를 알 수 있었으며 
is_alone 으로 개인/단체의 생존율 차이 직관적 분석도 가능했음

주석: sex, sex_encoded, alone, is_alone 의미적 중복칼럼 (처리 전 칼럼) drop_cols 추가하면 모델에 넣기 더 쉬워질 것으로 보임

Iris

boxplot 위에 stripplot을 겹쳐 개별 점까지 보이게 한 점과 분석 요약 주석이 좋았음

주석: sepal width만 약한 음의 상관이라고 했는데 품종별로 나눠서 보면 방향이 달라지는지(심슨의 역설) 확인해도 좋을 것 같음

Wine

Min/Max/Mean/Std/Skewness를 한 표로 정리해 스케일링 필요성을 보여준 점이 좋았음

주석: target은 순서 없는 품종 라벨이라 상관계수로 "번호가 커질수록 낮아진다"고 해석하는 건 조심해야 할 듯 (품종별 평균 비교가 더 적절)

## 이충희
Titanic
* 가족 수 분석에서 끝나지 않고 생존율이 4인까지 오르다가 5인 이상에서 떨어지는 비선형 패턴을 찾아내서 이를 바탕으로 Alone/Small/Large로 재구간화한 점이 좋았음

Iris
* boxplot 위에 stripplot을 겹쳐서 개별 점을 보이게 한 점이 좋았음 덕분에 표본이 50개씩인 데이터에 대해 분포를 직접 볼 수 있어서 많은 정보를 확인 가능할 수 있었음
* 스케일링 과정이 포함되면 좋을 것 같음

Wine
* Min, Max, Mean, Std, Skewness를 한 표로 묶어서, 스케일링이 필요한 이유를 정리한 것이 좋았음
* df.drop(columns=['target'], inplace=True)로 target을 지운 것 같은데 히트맵 셀은 df[numeric + ['target']]을 사용 중임 지금 실행하면 에러가 발생할 수 있을 것 같음



각 데이터셋별 피드백이 아니라 전체 내용에 대한 피드백이면 지우고 작성해주셔도 됩니다.
