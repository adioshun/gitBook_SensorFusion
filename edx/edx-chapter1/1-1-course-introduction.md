## 1.1 Course Introduction 

### 1.1.1 Introduction to Sensor fusion and non-linear filtering

![](https://i.imgur.com/BhzKURp.png)

definition : we should use a sequence of noisy observations from one or more sensors.
- If we use one sensor, we call it filtering.
- And if we use more sensors, we call it sensor fusion.

goal : filter the sequence of noisy sensor observations to get a better **estimate** of some unknown quantity of interest(=state.)

However, we are not just content with an estimate.

We are also interested in finding the associated uncertainty measures, that is, how sure we are of our estimate.

CAMERA 
- 장점 : detecting and classifying, determining the relative angle
- 단점 : cannot be measured directly using a single camera.

radar
- 장점 : good at measuring the distance to an object, Doppler shift(=relative radial velocity)
- 단점 : not good at measuring the angle to an object.


### 1.1.2 Demonstrations

