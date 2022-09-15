<img width="700" alt="스크린샷 2022-09-14 오후 3 09 49" src="https://user-images.githubusercontent.com/97447841/190073314-b827ea68-d503-4b9c-b803-97aa514f3723.png">

Date : 2022.3.17~2022.3.22

Tags : `sklearn` `Regression` 

Link : [https://github.com/heezzing/project2.git](https://github.com/heezzing/project2.git) 

발표영상 : [https://youtu.be/zvVHcPlQEOk](https://youtu.be/zvVHcPlQEOk)

## 개요

- 주제 : 국방비 예측 데이터 (나라별 군사비 규모를 예측하기 위해 선정)
- 베이스라인 : 단순선형회귀
    - 국방비 규모라 분류보단 회귀가 맞다고 생각하여 회귀를 선택함
- 평가지표 : • 회귀 평가지표(evaluation metrics): MAE,MSE,RMSE,R^2
- 데이터 출처  :  Kaggle
    
    [Military expenditure by country from 1970-2020](https://www.kaggle.com/datasets/prasertk/military-expenditure-by-country-from-19702020)
    
- 기여 내용 : 주제도출, 스토리텔링, 데이터 분석, 발표자료
- 종속변수 : M_USD
- 독립변수 : **M_of_gov,M_of_GDP**
-----------
## 프로젝트 내용

<img width="700" alt="스크린샷 2022-09-14 오후 3 10 32" src="https://user-images.githubusercontent.com/97447841/190073426-c7936889-4d25-484c-a3b9-e1a9070bad9b.png">

- 주제는 국방비 예측 데이터입니다.
- 주제를 선택한 이유 :
    - 우크라이나와 러시아의 전쟁을 보며 내가 누리고 있는 안전이 언제든이 없어질 수 있다고 느끼게 되었고 국가와 국민을 지키기 위해 각 나라별 국방비에 어느정도 투자하는지 궁금하여 선정하게 되었습니다.
- 가설은 GDP대비 국방비 비율과 국가지출 대비  국방비 비율이 국방비에 큰 영향을 미친다 입니다.

<img width="700" alt="스크린샷 2022-09-14 오후 3 11 02" src="https://user-images.githubusercontent.com/97447841/190073503-5d090f7d-3d25-4252-8912-cd48de11daa6.png">
<img width="700" alt="스크린샷 2022-09-14 오후 3 11 17" src="https://user-images.githubusercontent.com/97447841/190073547-e5393153-12da-4ab3-8e14-72234a9dcdd5.png">

- 데이터 수집은 kaggle에서 ****military expenditure.csv****를 다운받았습니다.
- pandas를 이용하여 데이터 전처리를 해주었습니다.
    - 결츨값 처리,불필요한 컬럼 처리
-------
### 단순선형회귀(베이스 모델)
<img width="700" alt="스크린샷 2022-09-14 오후 3 13 50" src="https://user-images.githubusercontent.com/97447841/190074002-d8eca87a-2b7b-415e-ba26-01961c4f4743.png">

- 베이스라인을 회귀로 잡고 선형회귀를 이용하였고 평가지표는 mse,rmse,mae,R^2를 이용하였습니다.
- 왼쪽은 GDP 대비 국방비 비율(M_of_GDP)과 국방비규모(USD)의 선형회귀선입니다.
- 오른쪽은 정부지출 대비 비율(M_of_gov)과 국방비규모(USD)의 선형회귀선입니다.
- 왼쪽의 그래프 기울기와 R^2값이 더 크므로 GDP대비 국방비 비율이 정부지출 대비 국방비 비율보다 국방비에 더 영향을 미치는걸 알 수 있습니다.
------
### 다중선형회귀
<img width="700" alt="스크린샷 2022-09-14 오후 3 22 08" src="https://user-images.githubusercontent.com/97447841/190075427-552b723e-af67-443b-b392-524303f56af3.png">

- 다중선형회귀모델의 R^2값이 단순선형회귀 모델보다 더 높은걸 알 수 있습니다.
- 하나의 특성을 사용한 단순선형회귀보다  테스트 오류가 더 줄어든걸 알 수 있습니다.
------
### 결정트리 ( DecisionTreeRegresor)
<img width="700" alt="스크린샷 2022-09-14 오후 3 24 13" src="https://user-images.githubusercontent.com/97447841/190075756-d4b8c7aa-87f9-4200-b460-367ebf151662.png">
<img width="700" alt="스크린샷 2022-09-14 오후 3 24 34" src="https://user-images.githubusercontent.com/97447841/190075815-26ac05e0-ec15-4849-a3f9-ba8b0e95ff19.png">

- 결정트리 : 스무고개 하듯 특성들으 ㅣ수치를 가지고 질문을 통해 정답크랠스를 찾아가는 과정입니다.
- 데이터의 과적합 제어를 위하여 Min_samples_split을 이용하였습니다
- 훈련 정확도가 테스트 데이터 정확도보다 높은걸 보면 이상치(미국의 데이터) 때문에 정확도가 낮다고 생각합니다.
- DecisionTreeRegresor가 단순선형회귀모델에 비해 정확도가 낮은걸 알 수 있습니다.
- 특성중요도 확인을 해보니 GDP 대비 국방비 비율(M_of_GDP)이 국가지출 대비 국방비 비율(M_of_gov)보다 국방비에 더 영향을 미치는걸 알 수 있습니다.
------
### 랜덤포레스트(RandomForestRegressor)
- <img width="700" alt="스크린샷 2022-09-14 오후 3 25 15" src="https://user-images.githubusercontent.com/97447841/190075933-0dd604a3-d10d-48e4-85a1-7e0ec3544e93.png">

- 랜덤포레스트 : 훈련과정에서 구성한 다수의 결정트리로부터 분류,평균 예측치를 출력합니다.
- 데이터의 과적합 제어를 위하여 Min_samples_split을 이용하였습니다
- 훈련 정확도가 테스트 데이터 정확도보다 높은걸 보면 이상치(미국의 데이터) 때문에 정확도가 낮다고 생각합니다.
- RandomForestRegressor가 단순선형회귀모델에 비해 정확도가 낮은걸 알 수 있습니다.
------
### 하이퍼파라미터 튜닝
<img width="700" alt="스크린샷 2022-09-14 오후 3 26 01" src="https://user-images.githubusercontent.com/97447841/190076076-3a98b7fa-87a8-40aa-af7a-ef12647acb78.png">

- 하이퍼파라미터 튜닝 : 모델의 성능을 확보하기 위해 조절하는 주요 설정값입니다.
- 하이퍼파라미터 튜닝을 이용한 모델의 회귀값 R^2는 0~1 사이의 값으로 표현되는데 -1.3 이므로 성능이 아주낮은 비정상적인 모델입니다.
- 오른쪽 모델을 보아도 실제값을 잘 예측하지 못하는걸 알 수 있습니다.
------
### 머신러닝 모델 해석 (PDP)
<img width="700" alt="스크린샷 2022-09-14 오후 3 26 49" src="https://user-images.githubusercontent.com/97447841/190076209-874ab3ac-5741-49ac-a00c-1b2ebfd551e7.png">

- PDP :  모델의 예측값이 특정 피쳐의 변화에 따라 평균적으로 어떻게 변화하는지 보여줍니다.
- PDP를 이용하여 그래프를 확인해 보니 변화가 매우 불규칙적입니다.
- 값을 예측하기 힘든 모델인걸 알 수 있습니다.
------
### 머신러닝 모델 해석 (SHAP)
<img width="700" alt="스크린샷 2022-09-14 오후 3 27 42" src="https://user-images.githubusercontent.com/97447841/190076352-e9fb9523-67c4-4f4b-b4ae-365d959e580b.png">

- SHAP : 특정 데이터에 대해 모델의 예측값에 각 지표들이 얼마나 기여하는지 보여줍니다.
- Shap value가 커야 예측값에 영향을 많이 줍니다.
- value 분포가 작으므로 예측값에 영향을 작게 주는걸 알 수 있습니다.
------
### 종합 결론
<img width="700" alt="스크린샷 2022-09-14 오후 3 32 54" src="https://user-images.githubusercontent.com/97447841/190077317-f68a5184-68d9-453b-b1d5-0c2347676a4c.png">

- 결론
    - GDP 대비 국방비 비율(M_of_GDP)과 국가 지출 대비 국방비 비율(M_of_gov)은 국방비에 큰 영향을 주지않습니다.
    - 예측 성능이 낮은 모델이므로 성능이 좋은 모델은 아닙니다.
    - 반성
        - 이상치 제거를 하면 좀 정확도가 올라갈 것이라고 생각합니다.
            - 미국이란 나라도 중요하지만, 전체적인 정확도를 위해선 제거가 필수인것 같습니다.
        - 독립변수(M_of_GDP,M_of_gov)를 이용하여 국방비(USD)단위로 맞췄다면 더 좋은 성능이 나왔을거라고 생각합니다.
        - 데이터가 부족했고 독립변수 설정과 가설에 문제가 있었던 거 같습니다.
        - 데이터를 선정할 때 주제도 중요하지만, 다양한 정보가 있는 데이터를 선정하고 EDA와 전처리를 잘 하는 것이 중요합니다.
       
