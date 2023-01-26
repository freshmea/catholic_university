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
