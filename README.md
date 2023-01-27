# catholic_university

- - -
## 2023_1_25
- - -

* intel realsense depth camera D415 setting
    * 윈도우 에서 작동.
    * https://verilog-119b.tistory.com/17
    * 라즈베리파이 4B 세팅.
    * ROS2 라이브러리 적용.
    * https://intel.github.io/robot_devkit_doc/pages/rs.html --> 리눅스 18.04 가 아니라서 안됨
    * 아래 링크로 다시 시도.
    * https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md
    * 끝까지 따라한 후에 realsence-viewer 를 실행하고 펌웨어 업데이트를 해야 함.
    * USB 3.0 port 를 사용해야만 작동이 됨.
    * ubuntu 20.04 에서 작동 확인.

- - -
## 2023_1_26
- - -

* 라즈베리파이4 ubuntu 20.04 에서 같은 작업을 진행
* N: Skipping acquire of configured file 'main/binary-armhf/Packages' as repository 'https://librealsense.intel.com/Debian/apt-repo focal InRelease' doesn't support architecture 'armhf'
  armhf 는 지원하지 않는다면서 애러가 남.
* sudo apt-get install ros-foxy-realsense2-camera
* 설치 후 realsense 카메라 실행 -> 토픽 정상적으로 발행 확인. 하지만 이미지를 받는 것은 느림.
* pinkwink.kr/1277 post 참고

- - -
## 2023_1_27
- - -

* 어제와 같은 세팅으로 랜선을 연결해서 실행
  ![이미지 토픽](./images/Screenshot%20from%202023-01-27%2009-13-45.png "스크린샷")

  ![뎁스 토픽](./images/Screenshot%20from%202023-01-27%2009-14-23.png "스크린샷")

  * 초당 프레임 6~7 수준 으로 작동.
* opt/ros/share/realsense 에 있는 런치 파일 실행 rs_d400, rs_launch 는 실행 확인 함.
* realsense ROS2 param 적용 후 실행
  * point cloud 적용 후 rViz2 에서 실행 시켜 봄.
  * ros2 launch realsense2_camera rs_launch.py depth_module.profile:=1280x720x30 pointcloud.enable:=true
  * 참고: https://github.com/IntelRealSense/realsense-ros
  * 프로젝트에 활용한 코드가 필요.
    * depth_map 의 중앙에서 데이터를 얻어서 거리를 구해서 출력하는 demo 노드를 파이썬으로 만듬.
    * 참고: https://github.com/stereolabs/zed-ros2-examples/blob/master/tutorials/zed_depth_tutorial/src/zed_depth_sub_tutorial.cpp
    * 거리 데이터만 토픽으로 보내서 라즈베리파이의 hz 확인 30 hz 가능?
      * 얼라인 뎁스 토픽이 필요한듯?
      * ros2 launch realsense2_camera rs_launch.py align_depth.enable:=true
      * 얼라인 뎁스 토픽 파라미터를 다른 토픽이 발행 되지 않음.
      * m_pubsub 패키지에 image_center_depth_pub.py 만듬
        * data 의 크기가 해상도의 두배가 됨. uint8 두개가 연결되어서 float data가 되는거 같음.
        * cv_bridge 를 통해서 data를 변환 하고 접근 하거나 따로 코드를 만들어서 거리를 얻어야 함.
        * data test : width 먼저 증가하고 height 가 나중에 증가하는 1차원 배열임.
        * rviz2 에서 image가 제대로 디스플레이 되는데 여기서는 어떤 모듈이 쓰이는거지?
        *
