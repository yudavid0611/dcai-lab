# TIL
> coures link: https://dcai.csail.mit.edu/lectures/label-errors/

<br>

- 강의 목표
    - Improve ML models trained on data with label issues.

<br>

- confident learning
    - a framework of theory and algorithms for
        - finding label errors in a dataset.
        - ranking data by likelihood of being a label issue.
        - learning with noisy labels.
        - complete characterization of label noise in a dataset.
        - dataset curation
    - confident learning을 통해 label errors를 찾기 위해 **어떠한 모델의 predicted probabilities도 사용할 수 있다.**

<br>

- noisy labels는 어떻게 발생하는가?
    - clicked the wrong button(upvote/downvote, 1 star instead of 5 stars)
    - mistakes(즐겨찾기 버튼을 실수로 누름)
    - mismeasurement
    - incompetence(능력 부족)
    - another  ML model’s bad predictions
    - corruption and a million other places.

<br>

- 가정
    - true label이 주어지면, 모든 다른 클래스에 대한 constant flipping rate이 존재한다.
    - real-world 이미지에서 많은 boars 이미지들은 pigs로 잘못 라벨링 된다.
    - 그러나 missiles나 keyboard는 pigs로 잘못 라벨링되지 않는다.
    - `class-conditional` label noise는 클래스에 의존적이다.
        - 이미지 데이터 x(돼지가 어떻게 생겼는가)에 의존적이지 않다.

<br>

- confident learning
    1. thresholds 구하기
        - if j=dog, tj = 1 → dog로 labeled된 이미지에 대해 해당 이미지가 dog인 confidence는 100%
        - 모든 클래스에 대해 thresholds를 구한다.
    2. matrix 만들기
        - creating a matrix of counts to estimate the unnormalized joint distribution
            - 모델의 predicted probabilities와 tj(thresholds)를 비교하여 tj 이상일 경우 해당 label의 예측은 맞은 것으로 판단.
            - 예측 결과와 label을 고려하여 matrix 채우기
    3. noisy examples를 찾아 제거하고, 다시 학습한다.

<br>

- Ranking label errors
    - self-confidence: i로 labeled된 데이터에 대한 모델의 predicted probability를 바탕으로 정렬
    - normalized margin: i로 labeled된 데이터에 대한 모델의 predicted probability를 다른 클래스들 중 predicted probability가 큰 값으로 뺀 후 정렬