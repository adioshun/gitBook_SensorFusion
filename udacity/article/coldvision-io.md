# [Object tracking with LIDAR, Radar, sensor fusion and Extended Kalman Filter](http://www.coldvision.io/2017/04/15/object-tracking-with-lidar-radar-sensor-fusion-and-extended-kalman-filter/)

> 원문 1~3은 칼만필터 깃북에 기록

## 4. Object motion tracking in 2D by fusing noisy measurements from LIDAR and Radar sensors

This part uses noisy measurements from Lidar and Radar sensors and the Extended Kalman Filter to estimate the 2D motion of bicycles

### 4.1 State Vector X & motion model 

The state has four elements: position in x and y, and the velocity in x and y.

![](http://www.coldvision.io/wp-content/uploads/2017/04/object_tracking_state_prediction.png)

The linear motion model in the matrix form:

![](http://www.coldvision.io/wp-content/uploads/2017/04/object_tracking_state_tranzition_matrix.png)


Motion noise and process noise refer to the same case: uncertainty in the object’s position when predicting location. 

위 모델에서 속도는 고정상수로 가정한다. 하지만 가속도로 인해서 속도는 변할수 있다. 따라서 process noise에서 이러한 불확실성을 포함하고 있다. `The model assumes velocity is constant between time intervals, but in reality we know that an object’s velocity can change due to acceleration. The model includes this uncertainty via the process noise.`

### 4.2 Laser Measurements

Lidar의 출력은 (x,y)이다. `The LIDAR sensor output is a point cloud but in this project, the point cloud is pre-processed and the x,y state of the bicycle is already extracted.`

![](http://www.coldvision.io/wp-content/uploads/2017/04/object_tracking_laser_measurements.png)


#### Definition of LIDAR variables:

- z는 측정 벡터 이다. 라이다의 경우 z는 x,y를 포함 하고 있다. `z is the measurement vector. For a lidar sensor, the z vector contains the position−x and position−y measurements.`

- H is the matrix that projects your belief about the object’s current state into the measurement space of the sensor. 
    - For lidar, this is a fancy way of saying that we discard velocity information from the state variable since the lidar sensor only measures position: 
    - 상태 벡터 X는 4개의 값을, 벡터 z는 2개의 값을 가지고 있다. `The state vector x contains information about [px,py,vx,vy] whereas the z vector will only contain [px,py]. `
    - Multiplying Hx allows us to compare x, our belief, with z, the sensor measurement.


- What does the prime notation in the x vector represent? 
    - The prime notation like px′ means you have already done the update step but have not done the measurement step yet. 
    - In other words, the object was at px. After time Δt, you calculate where you believe the object will be based on the motion model and get px′.


### 4.3 Radar Measurements

Radar의 출력은 거리, angle, 속도 이다. `The Radar sensor output is defined by the measured distance to the object, orientation and its speed.`

![](http://www.coldvision.io/wp-content/uploads/2017/04/object_tracking_radar_measurements.png)

#### Definition of Radar variables:

- The range, (ρ), is the distance to the pedestrian. 
    - The range is basically the magnitude of the position vector ρ which can be defined as ρ=sqrt(px2+py2).

- φ=atan(py/px). Note that φ is referenced counter-clockwise from the x-axis, so φ from the video clip above in that situation would actually be negative.

- The range rate, ρ˙, is the projection of the velocity, v, onto the line, L.


퓨전을 

To be able to fuse Radar measurements defined in the polar coordinate system with the LIDAR measurements defined in the cartesian coordinate system, one of the measurements must be transformed.






