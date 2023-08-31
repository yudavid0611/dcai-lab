# TIL
> coures link: https://dcai.csail.mit.edu/lectures/dataset-creation-curation/

<br>

- training data를 얻을 때 물어야 하는 질문
    - ML model이 어떻게 쓰일 것인가?
        - On what population will model be making predictions and when
    - Hypothetical edge cases
        - high stakes scenarios, rare events

<br>

- spurious correlation
    - 학습 데이터에서는 나타나지만 모델이 배포되는 real-world 데이터에서는 나타나지 않는 상관관계

<br>

- selection bias
    - training data distribution ≠ distribution in deployment
    - 발생 원인
        - (time series data) 과거 데이터로 학습된 모델로 미래를 예측할 때
        - over-filtering
        - rare events
        - convenience(get data only from close friends)
        - location
            - 특정 지역에서 데이터만 학습에 활용
    - 해결책
        - (data distribution) validation data를 deployment distribution과 최대한 비슷한 data로 구성하기(전체 dataset에서 randomly split하지 않고)
        - (time series) 가장 최근 data를 validation data로 사용하기
        - (location) hold out all data from some locations
        - (rare events) validation data 구축 시 over-sample

<br>
    
- Curating a dataset labeled by multiple annotators
    - 배경
        - 여러 명의 annotators가 라벨링을 한 많은 데이터셋들은 quality control examples를 포함하지 않는다.
        - 따라서 그러한 데이터셋이 주어지면 세 가지 quantities를 어떻게 추정할 것인지 고민해야 한다.
    - The three quantities
        1. A **consensus label** for each example that aggregates the individual annotations.
        2. A **quality score for each consensus label** which measures our confidence that this label is correct.
        3. A **quality score for each annotator** which estimates the overall correctness of their labels.
    - 세 가지 quantities를 추정하기 위해 다음 세 가지 알고리즘을 사용할 수 있다.
        1. ****Majority Vote and Inter-Annotator Agreement****
            - Agreement: example i label에 대해 labeling을 수행한 annotators 중 consensus label과 동일한 labeling을 수행한 annotators의 비율
            - Quality: annotator j의 overall quality를 추정한다.
            - 두 가지 downsides
                1. Resolving ties is ambiguous in majority vote.
                2. A bad annotator and good annotator have equal impact on the estimates.
        2. ****Dawid-Skene****
        3. ****CROWDLAB (Classifier Refinement Of croWDsourced LABels)****