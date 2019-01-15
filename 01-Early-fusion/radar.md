Obserables
- range
- Angle (azimuth, Elevation)
- velocity
- Size


종류
- Long Range Radar : 76-78 GHz, 1~250m
- Short Range Radar : 24-26 GHz, 77-81GHz, 0.2m~80m

제일 많이 쓰는게 Delphi/Continental 입니다. 요즘은 대부분 77GHz 를 쓰구요, 전방을 보느냐 측방 또는 후방을 보느냐에 따라서 탐지 거리나 FOV가 조금씩 차이가 나는데.. 가격은 양산이 아니고 연구용 샘플을 산다면 (미국기준으로) 약 5000-7000불 정도입니다. 아래 링크 참고하세요
https://autonomoustuff.com/product-category/radar/


Delphi의 경우 ethernet/can 둘다 지원이 될텐데, can의 경우 usb2can 이 되는 kvaser 제품을 쓰시면 ros로 구동이 가능하죠. ^^;

ㅋㅋㅋ 한국 대기업은 델파이가 지원해줘서 이더넷도 되고 멀티 센서 트랙킹도 됩니다 ㅎㅎ 저희 같은 영세업채에겐 안 해줍니다 ㅋㅋㅋ


Delphi ESR 2.5 : https://docs.polysync.io/sensors/delphi-esr-2-5/


https://autonomoustuff.atlassian.net/wiki/spaces/RW/pages/17509820/Delphi+ESR


https://github.com/diyjac/Udacity-SDC-Radar-Driver-Micro-Challenge


rosbag : https://vision.eng.au.dk/fieldsafe/


rosbag store : https://rosbag.tier4.jp/index/ , 13page



Delphi ESR 9.21.21 구매 사이트 : http://www.unmanshop.com/goods/view.php?seq=83 , 700만


https://www.youtube.com/watch?v=NySMRVElhdY 2016 03 07 Delphi ESR Sensor Video


point cloud : https://www.youtube.com/watch?v=QAqgY1AcLhM


ROS radar_omnipresense : http://wiki.ros.org/radar_omnipresense

ROS sick_scan : http://wiki.ros.org/sick_scan


RVIZ : Select laser as fixed frame. And add a new PointCloud decoder subscribed at topic cloud.

Radar raw data - Automation with radar : https://www.youtube.com/watch?v=ZlA88IHimkw

https://mrsdprojects.ri.cmu.edu/2016teama/system-implementation/radar/


## InnoSenT 제품군

- ISYS-5010

![](https://i.imgur.com/129elrY.png)

- nrOfTargets : Number of detected targets

## Delphi 제품군

- [Delphi Electronically Scanning RADAR](https://www.autonomoustuff.com/wp-content/uploads/2016/08/delphi-esr.pdf): pdf


---
## SICK 제품군

- Radar : [RMS3xx](https://cdn.sick.com/media/docs/2/72/472/Telegram_listing_Radar_sensor_RMS320_en_IM0080472.PDF), RMS4xx

![](https://i.imgur.com/5Etrw1e.png)
https://cdn.sick.com/media/docs/0/30/930/Product_overview_Detection_and_Ranging_Solutions_2D_laser_scanners_3D_laser_scanners_radar_sensors_en_IM0063930.PDF


![](https://i.imgur.com/xDqYY0U.png)

