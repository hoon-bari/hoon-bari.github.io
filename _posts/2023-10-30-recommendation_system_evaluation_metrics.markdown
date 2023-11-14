---
title: "추천시스템 평가지표(Recommendation System Evaluation Metrics)"
excerpt:
  "머신러닝 분야는 모델 구축만큼이나 성능평가도 중요합니다. 추천시스템 또한 머신러닝의 비지도학습에 속하기 때문에, 성능평가가 중요합니다. 그래서 추천시스템에는 Recall/Precision@k, MAP@k, NDCG@k 등 다양한 성능평가지표가 존재합니다. 이번 포스팅에서는 이러한 추천시스템의 평가지표에 대해 살펴보도록 하겠습니다."

categories:
      - Recommender System

tags:
      - [Recommendation, Evaluation]

Permalink: /RS/Recomender_evaluation

toc: true
toc_sticky: true

date: 2023-10-30
last_modified_at: 2023-10-30

use_math : true
---
![추천시스템 썸네일](https://github.com/hoon-bari/DACON_Medicine/assets/121400054/49ac6907-8597-4413-b932-1bf061a40996)

추천시스템은 정보 필터링 기술의 일종으로,  
특정 사용자가 관심을 가질만한 정보(영화, 음악, 책, 뉴스, 이미지, 공고 등)을 추천하는 것입니다.  
이러한 추천시스템의 성능을 평가하기 위한 다양한 metrics가 있는데요. 오늘은 그러한 metrics들을 한 번 살펴보겠습니다.  
<br>

### 1. 들어가기 전에 - Confusion Matrix(Error Matrix)
---
오늘 살펴볼 평가지표에 대해 설명하기 전에 알고 가야할 개념에 대해서 간단히 짚고 넘어가보겠습니다.  
다들 한번쯤은 보셨을 Confusion Matrix입니다.  

![confusion matrix](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/2029147a-0bd2-4f66-876d-6af3db234d0c)
<br>

보통 한글로는 혼돈행렬이라고 부르는 이 표는,  
통계분석 혹은 머신러닝 분야에서 지도학습이나 비지도학습의 알고리즘 성능평가를 시각화할 수 있는 표입니다.   
Actual 부분은 실제값, Predict부분은 예측값을 의미하며, 그 아래에서 4가지 경우로 나눠집니다.  
__1. True Positive(TP)__ : 조건이나 특성의 존재를 올바르게 나타내는 검사결과(예 : 암이 있으면 있다고 나타내는 경우)  
__2. True Negative(TN)__ : 조건이나 특성의 부재를 올바르게 나타내는 검사결과(예 : 암이 없으면 없다고 나타내는 경우)  
__3. False Positive(FP)__ : 특정 조건이나 속성이 있다고 잘못된 결과를 나타내는 검사결과(예 : 암이 없는데 있다고 나타내는 경우),  
Type I error(1종 오류)라고도 합니다.  
__4. False Nagative(FN)__ : 특정 조건이나 속성이 없다고 잘못된 결과를 나타내는 검사결과(예 : 암이 있는데 없다고 나타내는 경우),  
Type II error(2종 오류)라고도 합니다.

<br>

### 2. Precision@k / Recall@k
---
#### 1\) Precision@k

위에서 살펴본 혼돈행렬의 개념을 토대로, Precision과 Recall을 계산할 수 있습니다.  
Precision은 아래와 같이 계산됩니다.

<br>

<style>
.math_1 {
    display: flex;
    justify-content: center;
    font-size: 32px; 
}
</style>

<div class="math_1">
    $Precision = \frac{TP}{TP + FP}$
</div>
<br>

위 혼돈행렬과 설명을 참고하면, 예측된 값들 중 (존재하는 값들이 존재한다고) 예측되는 경우의 비율을 Precision이라고 합니다.   
한글로는 정확도라고도 합니다.
추천시스템에서의 Precision은 모델이 추천한 아이템 중 사용자가 관심있는 아이템의 비율을 의미합니다.  
그리고 Precision@k는 k개 추천결과에 대한 Precision을 계산한 것으로,  
모델이 추천한 아이템 k개 중에 실제 사용자가 관심있어하는 아이템의 비율을 의미합니다.   

<br>

<style>
.math_2 {
    display: flex;
    justify-content: center;
    font-size: 32px; 
}
</style>

<div class="math_2">
    $\text{Precision@k} = \frac{\text{relevant recommend items}}{\text{total relevant items}}$
</div>
<br>

#### 2\) Recall@k

Recall은 아래와 같이 계산됩니다.

<br>

<style>
.math_3 {
    display: flex;
    justify-content: center;
    font-size: 32px; 
}
</style>

<div class="math_3">
    $Recall = \frac{TP}{TP + FN}$
</div>
<br>

Recall은 실제 (존재하는)값들 중 (존재한다고)예측되는 경우의 비율을 의미합니다.  
Precision이 예측값을 기준으로 둔다면, Recall은 실제값을 기준으로 두는 것이 차이입니다. 한글로는 재현율이라고 합니다.  
그래서 추천시스템에서 Recall은 사용자가 실제로 관심있는 아이템 중에 모델이 추천한 아이템의 비율을 의미합니다.  
또한 Recall@k는 k개 추천 결과에 대한 Recall을 계산한 것으로,  
사용자가 관심있는 모든 아이템 중에서 모델의 추천한 아이템 k개가 얼마나 포함되는지 비율을 의미합니다.

<br>

<style>
.math_4 {
    display: flex;
    justify-content: center;
    font-size: 32px; 
}
</style>

<div class="math_4">
    $\text{Recall@k} = \frac{\text{relevant recommend items}}{\text{all the possible relevant items}}$
</div>
<br>


#### 3\) Precision@k / Recall@k 예시

예를 들어 아래와 같은 예시가 있다면, Precision@5와 Recall@5는 아래와 같이 됩니다.

![푸바오](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/662caeee-eaa1-4009-af0a-793af22f1417)

<style>
.math_5 {
    display: flex;
    justify-content: center;
    font-size: 28px; 
}
</style>

<div class="math_5">
    <span style="margin-right: 50px;">$Precision@5 = \frac{3}{5}$</span>
    <span>$Recall@5 = \frac{3}{6}$</span>
</div>

<br>

### 3. Mean Average Precision@k
---
(객체탐지에서의 mAP와 용어가 같은데, 나중에 이 2개의 차이에 대해서도 설명해보겠습니다.)

앞에서 설명한 Precision@k, Recall@k는 모두 순서를 신경쓰지 않습니다.  
하지만 추천시스템에서는 사용자가 관심을 더 많이 가질만한 아이템을 상위에 추천해주는 것이 매우 중요합니다.  
이를 위해 성능 평가에 순서 개념을 도입한 것이 Mean Average Precision@k입니다.  
여기서 Mean과 Average가 모두 한국어로 번역하면 평균이므로, 혼란스러울 수 있습니다.  
정확하게는 Average Precision의 Mean으로 해석해야하는데, 이게 어떤 의미인지 먼저 그림을 띄워놓고 그 다음 설명하겠습니다.  

![푸바오 러바오](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/1b214d81-e68c-4630-8696-2124bd1e5a61)

<style>
.math_6 {
    display: flex;
    justify-content: center;
    font-size: 20px; 
}
</style>

<div class="math_6">
    $\text{User L's } AP@3 = \frac{1}{m} \sum\limits_{i=1}^{3} \text{precision@}i = \frac{1}{2} \left( \frac{1}{1} \times 1 + \frac{1}{2} \times 0 + \frac{1}{3} \times 0 \right) = 0.5$
</div>
  
<style>
.math_7 {
    display: flex;
    justify-content: center;
    font-size: 20px; 
}
</style>

<div class="math_7">
    $\text{User F's } AP@3 = \frac{1}{m} \sum\limits_{i=1}^{3} \text{precision@}i = \frac{1}{2} \left( \frac{0}{1} \times 0 + \frac{0}{2} \times 0 + \frac{1}{3} \times 1 \right) = 0.16$
</div>
<br>
<style>
.math_8 {
    display: flex;
    justify-content: center;
    font-size: 40px; 
}
</style>

<div class="math_8">
    $MAP@3 = \frac{0.5 + 0.16}{2}$
</div>
<br>
  
#### 1\) Average Precision@k

Precision@i는 추천한 아이템 개수 k중에서 해당 인덱스까지만 고려했을 때의 Precision값입니다.  
예를 들어, Precision@1은 가장 처음에 나오는 아이템을 하나만 추천했을 때의 Precision값입니다.  
위 그림의 예시를 보면,  
러바오는 가장 처음에 추천한 '설죽 2'를 좋아했으므로 Precision@1의 값은 1/1=1이고, Precision@2는 1/2입니다.

rel(i)는 relevence를 나타내는데, 해당 아이템을 사용자가 좋아했는지 여부를 나타냅니다.  
(좋아하면 1, 아니면 0의 값을 가집니다.)  
Precision에 relevence값을 곱해주는 이유는 정답 아이템이 추천 목록 중에서 딱 해당 순위에만 영향력을 주기 위함입니다.
정답이 1개 있는데 정답을 포함한 3개의 아이템을 추천했어도,  
정답을 첫 번째로 추천한 경우가 두 번째, 세 번째 추천한 것보다 AP 점수가 더 높아집니다.  

밑의 수식이 바로 Average Precision@k를 구하는 수식인데, **m은 모든 아이템 중에서 사용자가 좋아한 아이템 수**입니다.  
<br>
<style>
.math_9 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_9">
    $AP@k = \frac{1}{m} \sum\limits_{i=1}^{3} \text{precision@}i \times \text{rel(i)}$
</div>
<br>

위 그림을 다시 보면, 러바오와 푸바오 둘 다 전체 아이템 중 2개를 좋아했고, 하나가 추천 목록에 포함됩니다.  
하지만 사용자가 좋아한 아이템의 추천 순서가 높았는지 낮았는지에 따라 AP값이 크게 차이납니다.  
러바오는 첫 번째에 맞췄기 때문에, 푸바오에 비해 점수가 훨씬 높습니다.  
이렇듯 순서를 평가 지표에 반영한 것이 AP입니다.

#### 2\) Mean Average Precision@k

MAP@k는 모든 유저에 대한 Average Precision@k의 평균을 의미합니다.  
밑의 수식을 보면 U는 User의 집합을, |U|는 유저의 수를 나타냅니다.  
<style>
.math_10 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_10">
    $MAP@k = \frac{1}{|U|} \sum\limits_{u=1}^{|U|} (AP@k)_u$
</div>
<br>

위 그림처럼 총 사용자가 러바오, 푸바오 총 2명이라고 가정하면, 각 유저의 AP@k 값의 평균을 하면 MAP@k를 구할 수 있습니다.

<br>

### 4. NDCG@k(Normalized Discounted Cumulative Gain)
---

NDCG는 원래 검색분야에서 등장하는 지표이지만 추천 시스템에도 많이 사용되고 있습니다.  
위의 두 평가 지표와 마찬가지로 Top K개의 아이템을 추천하는 경우, 추천 순서에 가중치를 두어 평가합니다.  
**NDCG값은 1에 가까울수록 좋습니다.**   
또한 MAP는 사용자가 선호한 아이템이 추천 리스트 중 어떤 순서에 포함됐는지 여부에 대해서 1 or 0으로만 구분하지만,  
**NDCG@k는 순서별로 가중치 값(관련도, relevance)을 다르게 적용하여 계산합니다.**  

![푸바오2](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/13d48f4b-93d7-4aff-ac33-9a2e3b16ff6d)

<style>
.math_11 {
    display: flex;
    justify-content: center;
    font-size: 20px; 
}
</style>

<div class="math_11">
    $CG_3 = \sum\limits_{i=1}^{K} \text{rel}_i  = \text{rel}_1 + \text{rel}_2 + \text{rel}_3 = 3 + 2 + 1 = 6$
</div>

<style>
.math_12 {
    display: flex;
    justify-content: center;
    font-size: 20px; 
}
</style>

<div class="math_12">
    $DCG_3 = \sum\limits_{i=1}^{K} \frac{\text{rel}_i}{\log_2(i+1)} = \frac{3}{\log_2(1 + 1)} + \frac{2}{\log_2(2 + 1)} + \frac{1}{\log_2(3 + 1)} = \frac{3}{1} + \frac{2}{1.58} + \frac{1}{2} = 4.78$
</div>

<style>
.math_13 {
    display: flex;
    justify-content: center;
    font-size: 20px; 
}
</style>

<div class="math_13">
    $IDCG_3 = \frac{\text{rel}^{\text{opt}}_i}{\log_2(i+1)} = \frac{3}{\log_2(1 + 1)} + \frac{3}{\log_2(2 + 1)} + \frac{2}{\log_2(3 + 1)} = \frac{3}{1} + \frac{3}{1.58} + \frac{2}{2} = 5.89$
</div>
<br>
<style>
.math_14 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_14">
    $NDCG_3 = \frac{DCG}{IDCG} = \frac {4.78}{5.89} = 0.81$
</div>

<br>

#### 1\) Relevance

Relevance란, **사용자가 특정 아이템과 얼마나 관련이 있는지를 나타내는 값**입니다.  
Relevance 값은 정해진 것이 아니고 추천의 상황에 맞게 정해야합니다.  
예를 들어, 신발 추천인 경우 사용자가 해당 신발을 얼마나 클릭했는지, 혹은 클릭 여부(binary)등 다양한 방법으로 선정할 수 있습니다.  
위 그림에서는 전체 아이템에 대한 Relevance를 파란색으로 표시했습니다.  
<br>

#### 2\) Cumulative Gain(CG)

**CG는 추천한 아이템의 Relevance 합**입니다.  
두 추천 모델이 순서에 관계없이 동일한 아이템 셋을 추천하는 경우 두 모델의 CG는 같아집니다.
즉, 순서를 고려하지 않은 값입니다.

<style>
.math_15 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_15">
    $CG_K = \sum\limits_{i=1}^{K}\text{rel}_i$
</div>
<br>

#### 3\) Discounted Cumulative Gain(DCG)

**CG에 순서에 따른 discount개념을 도입한 것을 의미합니다.**  
추천 아이템의 순서가 뒤에 있을수록 분모가 커짐으로써 전체 DCG에 영향을 적게 주도록 합니다.  
**그러나 사용자별로 추천 아이템 수가 다른 경우 정확한 성능 평가가 어렵다는 한계가 있습니다.**  
예를 들어, 푸바오가 고른 대나무(혹은 죽순)종류가 5개인데 러바오가 고른 대나무(혹은 죽순)종류가 50개라면,  
둘에게 추천되는 아이템 수는 다를 수밖에 없습니다.  
추천 아이템의 수가 많아질수록 DCG값은 증가하기 때문에 정확한 평가를 위해서는 Scale을 맞출 필요가 있습니다.  

<style>
.math_16 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_16">
    $DCG_K = \sum\limits_{i=1}^{K} \frac{\text{rel}_i}{\log_2(i+1)}$
</div>
<br>

#### 4\) Normalized DCG(NDCG)

앞서 말한 DCG의 한계점을 보완하기 위해 **DCG에 정규화를 적용한 것**입니다.

<style>
.math_17 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_17">
    $NDCG_K = \frac{DCG}{IDCG}$
</div>
<br>
여기서 IDCG라는 값이 보이는데, 이는 최선의 추천을 했을 때 받는 DCG값입니다.  
IDCG는 모든 추천 아이템 조합 중에 최대 DCG값과 동일합니다.  
위에 있는 푸바오 그림에서 보면, 가장 이상적인 경우는 Relevance가 높은 순서대로 솜죽 1(3), 설죽 3(3), 설죽 1(2)... 입니다.  
이렇게 3개를 추천했을 때 DCG값을 구하면 5.89가 됩니다.  

<style>
.math_18 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_18">
    $IDCG_K = \frac{\text{rel}^{\text{opt}}_i}{\log_2(i+1)}$
</div>
<br>

**결국, NDCG@k는 가장 이상적인 추천 조합 대비 현재 모델의 추천 리스트가 얼마나 좋은지를 나타내는 지표입니다.**  
그리고 정규화를 함으로써 NDCG는 0~1사이의 값을 가지게 됩니다.  
아래 그림은 K(x축, Rank)가 증가함에 따라, DCG와 NDCG가 어떻게 달라지는지를 나타낸 그래프입니다.  
(왼쪽은 DCG@k, 오른쪽은 NDCG@k)  
좌측 그래프는 서로 다른 추천 모델(A~E, Ideal)의 DCG값이고, 우측은 NDCG값을 나타냅니다.  
**DCG는 K가 증가함에 따라 지속적으로 증가하는 반면 NDCG는 어느 정도 K에 독립적이기 때문에,**  
**어떤 K가 적절한지 판단이 가능합니다. 또한 NDCG가 작은 scale을 가지기 때문에 비교가 더 용이합니다.**  

![graph](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/8e705871-d0a1-48f4-8a6c-a5b1cf31298d)

<br>

### 4. Hit Rate@k
---

**Hit Rate는 전체 사용자 수 대비 적중한 사용자 수(적중률)를 의미합니다.**  
아래와 같은 단계를 거쳐 구합니다.  
1) 사용자가 선호한 아이템 중 1개를 제외합니다.  
2) 나머지 아이템들로 추천시스템을 학습합니다.  
3) 사용자별로 K개의 아이템을 추천하고, 앞서 제외한 아이템이 포함되면 Hit입니다.  
4) 전체 사용자 수 대비 Hit한 사용자 수 비율을 구하면 Hit Rate가 됩니다.  

<style>
.math_19 {
    display: flex;
    justify-content: center;
    font-size: 30px; 
}
</style>

<div class="math_19">
    $Hit Rate = \frac{\text{# of Hit User}}{\text{# of User}}$
</div>
<br>

그림으로 보면 아래와 같습니다. 아래의 경우, Hit Rate는 $\frac{1}{2}$입니다.

![푸바오 러바오2](https://github.com/hoon-bari/hoon-bari.github.io/assets/121400054/042c93a5-edeb-4b9e-aca5-2fe0ac9fb317)

<br>

### 5. 그 외 다른 추천시스템 평가지표
---
위에서 설명한 평가지표 이외에도 '추천 평점'을 예측하는 MAE, RMSE(보통 회귀 예측의 지표)가 있고,  
추천 결과가 얼마나 분산되어있는지를 평가하는 Entropy Diversity 지표도 있습니다.  
이런 지표들에 대해서는 나중에 시간이 된다면 따로 다뤄보도록 하겠습니다.  

<br>

### 6. 정리
---

이번에 참여하고 있는 대회의 평가지표가 Recall@5라,  
해당 부분에 대해 정리할 겸 Precision/Recall@k부터 시작하여 추천시스템의 다양한 평가지표에 대해 살펴보았습니다.  
다음엔 추천시스템의 여러가지 방법에 대해서 포스팅해보도록 하겠습니다.  

<br>

#### Reference
[① https://en.wikipedia.org/wiki/Confusion_matrix](https://en.wikipedia.org/wiki/Confusion_matrix)  
[② Alshammari, A., Kapetanakis, S. et al, Twitter User Modeling based on Indirect Explicit Relationships for Personalized Recommendations, Computational Collective Intelligence \(pp.93-105\), 2019](https://www.researchgate.net/publication/335439095_Twitter_User_Modeling_Based_on_Indirect_Explicit_Relationships_for_Personalized_Recommendations)  
[③ https://sungkee-book.tistory.com/11](https://sungkee-book.tistory.com/11)  
[④ https://yeomko.tistory.com/32](https://yeomko.tistory.com/32)  
[⑤ https://yamalab.tistory.com/119](https://yamalab.tistory.com/119)
