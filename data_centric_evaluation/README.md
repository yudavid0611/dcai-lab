# TIL
> coures link: https://dcai.csail.mit.edu/lectures/data-centric-evaluation/

<br>

- 일반적인 ML applications 개발 과정
    1. Collect data and define the appropriate ML task for your application.
    2. Explore the data to see if it exhibits any fundamental problems.
    3. Preprocess the data into a format suitable for ML modeling.
    4. Train a straightforward ML model that is expected to perform reasonably.
    5. **Investigate shortcomings of the model and the dataset.**
    6. Improve the dataset to address its shortcomings.
    7. Improve the model (architecture search, regularization, hyperparameter tuning, ensembling different models).
    8. Deploy model and monitor subsequent data for new issues.

<br>

- Model evaluation은 최종 application에 엄청난 영향을 미친다.
    - 예를 들어, Fraud vs Not-Fraud 분류 모델 학습 시 overall accuracy를 사용하는 것은 적절하지 않다. 왜냐하면 Not-Fraud 샘플이 데이터셋에 훨씬 많기 때문에 모델이 모든 입력에 대해 Not-Fraud로 예측할 것이기 때문이다.
    - Common pitfalls when evaluating models.
        - Data leakage
        - Misspecified metric: average loss만 보여주는 것은 rare examples/subpopulations에 대한 `severe failure cases`를 제대로 대표하지 못할 수 있다.
        - Selection bias: Validation data가 deployment setting을 대표하지 못함
        - Annotation error

<br>

- Underperforming subpopulations
    - 모델의 예측력은 데이터가 어느 slice에 속해있는지에 따라 달라지면 안 된다(즉 어떤 slice에서도 동일한 예측력을 가져야 한다).
    - data slice: 데이터셋에서 공통 특징을 공유하고 있는 부분 집합
        - ex. 특정 지역의 데이터, 하나의 특정 센서로부터 얻은 데이터, 성별, 인종 등
    - 특정 slice에서의 모델 performance를 개선하는 법
        1. Higher fitting capacity를 가진 ML 모델을 사용한다.
        2. 낮은 performance를 보이는 Minority subgroup을 over-sample(up-weight) 한다.
        3. 낮은 performance를 보이는 subgroup 데이터를 더 모은다.
        4. 추가적인 feature를 측정하거나 만든다.
            1. 상황:  Classifying if customer will purchase some product or not, based on
            customer & product features
            2. 문제: Predictions for young customers may be worse (less available history)
            3. 해결: Could add an extra feature to the dataset such as: “Popularity of this product among young customers
    - Underperforming subpopulations를 찾는 법
        1. Validation data의 examples를 loss value를 기준으로 정렬한다. High loss를 가진 examples를 확인한다(Error analysis).
        2. 이러한 examples에 클러스터링을 적용하여 공통점을 가지고 있는 클러스터를 찾는다.

<br>

- 모델 예측이 틀리는 이유
    1. 잘못된 라벨링
    2. 어떤 클래스에도 속할 수 없는 데이터
    3. 이상치
    4. 사용 중인 모델이 suboptimal임
    5. 동일한 특징을 갖지만 라벨이 다른 데이터가 존재