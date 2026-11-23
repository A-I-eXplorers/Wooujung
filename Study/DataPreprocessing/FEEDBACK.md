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

Iris

Wine

## 이충희
Titanic

Iris

Wine




각 데이터셋별 피드백이 아니라 전체 내용에 대한 피드백이면 지우고 작성해주셔도 됩니다.
