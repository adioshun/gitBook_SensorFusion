# [Sensor Fusion Tutorial](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/)

- [깃허브](https://github.com/datascopeanalytics/sensor_fusion)

## 1. What is this sensor fusion thing?

자전거 타기를 예로 실생활에서 발생 하는 센서 퓨전 예시 언급 

## 2. Sensing the number of people in a train car

통근 시간 전철의 앉아 가기 위해서 필요한것 
- measure or estimate the number of people in each car, in real time
- occupancy estimate

## 3. Sensor models

기차내 CO2를 측정하여 number of people in each car를 예측 할수 있다. 

|![](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/experiment_plots/co_2.svg)|![](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/reading_plots/1_co2.svg)|
|-|-|

Co2가 1092ppm이라면 대략 46명이 있을수 있다. 


## 4. Multiple readings between stations



let’s actually get some data! Let’s start looking at what’s happening in the car between two stations, something we can determine easily, either from an accelerometer on the car or from the great train tracker app CTA provides. (??)

> 두 정거장 사이에 사람이 내릴수 없으니 이를 GT로 활용 하는건가? 

![](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/reading_plots/2_co2.svg)





Mathematically, we multiply the two blue distributions and normalize the result as needed. 
![](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/reading_plots/3_co2.svg)




Because our distributions are Gaussian this multiplication can be done analytically:

![](https://i.imgur.com/CQC4caB.png)

in code, it looks something like this:
```python
class Gaussian(object):
    ...
    def bayesian_update(self, other):
        sigma_sum = self.sigma**2 + other.sigma**2
        self.mu = ((self.sigma**2) * other.mu + (other.sigma**2) * self.mu) / sigma_sum
        self.sigma = np.sqrt(((self.sigma * other.sigma)**2) / sigma_sum)
```

## 5. Multiple sensors (+온도계)

온도계를 설치 하여서 변화에 따른 재실자 수를 예측 할수 있다. 

![](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/experiment_plots/Temperature.svg)

![](https://datascopeanalytics.com/blog/sensor-fusion-tutorial/reading_plots/4_co2.svg)


```python 

class Reading(Gaussian):

    def __init__(self, sensor, truth, timestamp=None):
        """Generate a reading from `sensor` at `timestamp`,
        given `truth` people"""
        ...

class Estimate(Gaussian):
    ...

    def add_reading(self, reading):
        self.reading_vector.append(reading)
        self.update(reading)

    def update(self, reading):
        ...
        self.bayesian_update(reading)

reading_1 = Reading(co2_sensor, 60)
reading_2 = Reading(temp_sensor, 60)

estimate = Estimate()
estimate.add_reading(reading_1)
estimate.add_reading(reading_2)

reading_3 = Reading(co2_sensor, 60)
estimate.add_reading(reading_3)
```

## 6. Moving targets


두 정거장 사이에서는 내릴수가 없기 때문에 재실자 수는 동일하다. 

하지만 전체 경로 상에서는 빈번하게 내리고 타는게 가능하다. 

In mathematical terms this means that, every time we stop at a station, the error on our estimate of the number of people in the car will have to widen, and since we don’t know how much we’ll just set its sigma to infinity. In code, this is done by either creating a brand new Estimate or setting its sigma to None:

```
estimate=Estimate()
# or
estimate.sigma = None
```


## 7. Better models


What we did in the previous sections is a well known and quite brilliant method called **Kalman filtering**.

A very similar approach, called **Kalman smoothing** can be taken if we do not need real time results, but instead can use the full data at once to determine the most likely outcome. 








