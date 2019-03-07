# Sensor Fusion and Object Tracking using an Extended Kalman Filter Algorithm

> ex-kalman은 H, F만 빼고는 기본 칼만과 같다. 본 예시에서는 고정 속도 모델을 사용하였기 때문에 F도 같다. `The extended Kalman filter is almost the same as a basic Kalman filter except the H, and F are different. However, in this case, since I‘m assuming a constant velocity model which is linear, the F is the same.`

## [Part 1](https://medium.com/@mithi/object-tracking-and-fusing-sensor-measurements-using-the-extended-kalman-filter-algorithm-part-1-f2158ef1e4f0)

This algorithm is a recursive two-step process: 

- prediction step 
    - produces estimates of the current variables along with their uncertainties. 
    - These estimates are based on the assumed model of how the estimates change over time. 
- The update step is done when the next measurements (subject to noise) is observed. 
    - In this step, the estimates (let’s call it state from here on) are updated based on the weighted average of the predicted state and the state based on the current measurement. 
    - A lower weight is given to that with a higher uncertainty.
    

퓨전 대상 
- liar : x,y
- Radar : rho, phi, speed(drho)

가정 : 동일한 속도로 움직인다. 

```c
// x - state vector
// P - uncertainty covariance matrix of state x (process covariance)
// z - measurement vector 
// R - uncertainty covariance matrix of sensor that produces z (measurement covariance)
// F - update matrix - used to get predicted x - based on time elapsed and assumed dynamic model being tracked
// H - extraction matrix - used to extract the hypothetical measurement if state x is correct and the sensor is perfect
// Q - noise covariance matrix - adds uncertainty to the process covariance
// S - 'innovation' covariance that combines process covariance and measurement covariance
// y - difference between the actual measurement and the predicted measurement 
// K - Kalman gain - contains information on how much weight to place on the current prediction and current observed measurement 
//   - that will result the final fused updated state vector and process covariance matrix
//   - computed from P (process covariance), H (extraction), R (measurement covariance)

void KalmanFilter::predict(){
  this->x = this->F * this->x;
  this->P = this->F * this->P * this->F.transpose() + this->Q;
}

void KalmanFilter::update(
  const VectorXd& z, const MatrixXd& H, const VectorXd& Hx, const MatrixXd& R){

  const MatrixXd PHt = this->P * H.transpose();
  const MatrixXd S = H * PHt + R;
  const MatrixXd K = PHt * S.inverse();
  VectorXd y = z - Hx;

  if (y.size() == 3) y(1) = atan2(sin(y(1)), cos(y(1))); //if radar measurement, normalize angle

  this->x = this->x + K * y;
  this->P = (this->I - K * H) * this->P;
 ```
 
 ![](https://cdn-images-1.medium.com/max/800/1*LcP_LQkH66uy6pg0BzogPQ.png)
 
 ### 1.1 predict 
 
 #### A.  Estimate of the state X
 
 - 현 상태 
 
 - x,y,vx,vy
 
 
 #### B. process or state covariance matrix P
 
 - 현 상태의 불확실성 
  - 현 상태가 n=4이므로 p = nxn = 4x4 
 - 값(위치) 변화가 크면 불확실성이 높고, 값 변화가 없으면 covariance=0 

![](https://cdn-images-1.medium.com/max/800/1*VZnRCoyB1GODH_sV6HArdg.png)
 
 ### 2.2 Update 
 
 #### A. measurements z
 
 - 측정 정보(Sensor measurement)
 
 
 #### B. covariance matrix of these measurements R

 - 측정 정보의 불확실성 
     - R_{lidar} : 측정 정보가 m=2 이므로 2x2
     - R_{radar} : 측정정보가 m=3 이므로 3x3
     
#### C. update matrix (aka state transition matrix) F
 
 - used to predict the value of the next x and P
 - It’s an n x n = 4 x 4 matrix
 - need a model of how the system behaves (고정 속도)
 - I use this model to get the updated x given the elapsed time dt .
 
 ```c
 /*
  px` = px + vx * dt
  py` = py + vy * dt
  vx` = vx 
  vy` = vy 

  |px`|     | 1  0 dt  0 |   | px |
  |py`|  =  | 0  1  0 dt | * | py |
  |vx`|     | 0  0  1  0 |   | vx |
  |vy`|     | 0  0  0  1 |   | yz |

   x` = F * x
*/

void KalmanFilter::updateF(const double dt){
  // this->F = MatrixXd::Identity(this->n, this->n);
  this->F(0, 2) = dt;
  this->F(1, 3) = dt;
}

void KalmanFilter::setQ(const MatrixXd& Qin){
  this->Q = Qin;
}
```
 
 
#### D. process noise covariance matrix Q



#### E.  acceleration noise (ax, ay)


#### F.  extraction matrix H 

- used to extract the theoretical sensor readings `Hx`

- The extraction matrix has 
 - m = 2 rows which is the number of **sensor measurements** and 
 - n = 4 columns which is the number of **state elements**
 
 ```python 
 Hx = H * predicted_x = predicted_z 

lidar_px = px = 1 * px + 0 * py + 0 * vx + 0 * vy
lidar_py = py = 0 * px + 1 * py + 0 * vx + 0 * vy 

"""
| lidar_px | = | 1 0 0 0 | * | px |
| lidar_py |   | 0 1 0 0 |   | py |
                             | vx |
                             | vy |
lidar_H =  | 1 0 0 0 |
           | 0 1 0 0 |
 """
 ```
 
 위 h는 polar corrd인 radar에 적용 할순 없다. 이 때문에 비선형이고 ex-kalman을 사용한다. `Unfortunately, it’s not as straightforward for the radar sensor since it is in polar coordinates. This makes the extraction non-linear (which is why this project is an extended Kalman filter as opposed to a simple Kalman filter). `
 
비 선형성을 선형선으로 하기 위해 `Jacobian`을 사용하여 H를 estimate한다. 

##### G. Innovation Covariance S

combines the covariance of 
- the state P, 
- the covariance of the measurements R 
- taking into account the extraction matrix H


This seems to be the covariance for vector y which is just the difference between the predicted measurement and actual measurement.

  
S is factored in to compute the optimal Kalman gain K 

Kalman gain K contains information on 
- how much weight to place on the current `prediction x` and current `observed measurement z`
- that will **result the final fused updated** `state vector x` and `process covariance matrix P`.



This K is the weight given to vector y. 

The intuition for the Kalman gain K here is that the state is updated based on a weighted average of the predicted state and the state based on the current measurement, a lower weight is given to that with a higher uncertainty.











