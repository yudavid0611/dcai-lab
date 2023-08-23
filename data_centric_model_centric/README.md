# TIL
> coures link: https://dcai.csail.mit.edu/lectures/data-centric-model-centric/

<br>

- data centric ai의 중요성
    > Deep neural networks easily fit random labels
    Zhang et al. (ICLR, 2017)
    > 
    - 에러가 있는 데이터로 학습한 알고리즘은 문제를 발생시킨다.
    - real-world 데이터는 학교 수업에서 제공하는 깔끔한 데이터셋과는 다르다.

<br>

- data centric AI의 형태
    1. AI algorithms that understand data and use that information to improve models.
        -  예시: curriculum learning: 쉬운 데이터 먼저 학습시키기
    2. AI algorithms that modify data to improve AI models.
        -  예시: confident learning: wrong labeled data 삭제
    
<br>

- model centric AI vs data centric AI
    - model centric AI
        - 데이터셋이 주어지면, best model을 만들기 위해 노력한다.
        - 모델을 바꾸어 performance를 개선한다.
    - data centric AI
        - 어떤 모델이 주어지든, training dataset을 개선하기 위해 노력한다.
        - `systematically/algorithmically` dataset을 바꾸어 performance를 개선한다.

<br>

- data centric AI examples 
    - Outlier detection and removal (handling abnormal examples in dataset)
    - Error detection and correction (handling incorrect values/labels in dataset)
    - Establishing consensus (determining truth from many crowdsourced annotations)
    - Data augmentation (adding examples to data to encode prior knowledge)
    - Feature engineering and selection (manipulating how data are represented)
    - Active learning (selecting the most informative data to label next)
    - Curriculum learning (ordering the examples in dataset from easiest to hardest)