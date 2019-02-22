## 2.1 An introduction to Bayesian statistics   

> 2.1 Overview BS MED INTRO V2-en


정의 
- A statistical inference framework
- Can be used for estimation, classification, detection, model selection, etc.

특징 
- unknown quantities are described as **random**.


활용 예 #1 : 병원 

- Quantity of interest: the disease
- Observations: blood samples, temperature, comments by patient, etc
- 결과 : based on our observations, patient has disease X with 97% probability

활용 예 #2 : 자율 주행 차 

- Quantity of interest: relative position and velocity of other vehicles at the current time.
- Observations: wheel speeds, INS measurements, radar detections (distance and angle), Lidar point clouds, camera images, etc.
- 결과 : vehicle motions are modelled statistically


기존 통계학과의 차이점 `COMPARISON: BAYES VS FREQUENTIST`

- We wish to estimate the height of the Eiffel tower. 
    - Frequentist perspective: the tower has a certain height and is therefore not random.
    - Bayesian perspective: we describe our uncertainties in the height stochastically -> height is described as random!
    
OVERVIEW OF THE BAYESIAN STRATEG
- Modeling.
- Measurement update (본 강의에서 주로 다룸) 
- Decision making