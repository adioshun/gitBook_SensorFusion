# Sensor Fusion and Object Tracking using an Extended Kalman Filter Algorithm

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
 
 - x : 현 상태 (x,y,vx,vy)
 - P : 현 상태의 불확실성 
     - 현 상태가 n=4이므로 p = nxn = 4x4 
     - 값(위치) 변화가 크면 불확실성이 높고, 값 변화가 없으면 covariance=0 

![](https://cdn-images-1.medium.com/max/800/1*VZnRCoyB1GODH_sV6HArdg.png)
 
 
 - z : 측정 정보(Sensor measurement)
 - R : 측정 정보의 불확실성 
     - R_{lidar} : 측정 정보가 m=2 이므로 
 
 
 
 