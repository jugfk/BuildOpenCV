# OpenCV4.1을 빌드하기
***
OpenCV4 를 젯슨 나노에 설치해봅시다.

(0) 설치 스크립트를 다운로드하기
```
wget https://raw.githubusercontent.com/jetsonworld/BuildOpenCV/master/18_How_To_Install_OpenCV_On_Jetson_Nano.txt
cat 18_How_To_Install_OpenCV_On_Jetson_Nano.txt
```

(1) 패키지 설치 및 업데이트하기
```
sudo apt update
sudo apt install -y build-essential cmake git libgtk2.0-dev pkg-config  libswscale-dev libtbb2 libtbb-dev
sudo apt install -y python-dev python3-dev python-numpy python3-numpy
sudo apt install -y curl
```

(2) 비디오 및 이미지포맷 관련 패키지를 설치하기
```
sudo apt install -y  libjpeg-dev libpng-dev libtiff-dev 
sudo apt install -y libavcodec-dev libavformat-dev
sudo apt install -y libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
sudo apt install -y libv4l-dev v4l-utils qv4l2 v4l2ucp libdc1394-22-dev
```

(3) OpenCV와 컨튜리뷰션 패키지를 다운로드하기
```
curl -L https://github.com/opencv/opencv/archive/4.1.0.zip -o opencv-4.1.0.zip
curl -L https://github.com/opencv/opencv_contrib/archive/4.1.0.zip -o opencv_contrib-4.1.0.zip
```

(4) 패키지 압축풀기
```
unzip opencv-4.1.0.zip 
unzip opencv_contrib-4.1.0.zip 
cd opencv-4.1.0/
```

(5) 빌드할 곳의 디렉토리 만들기
```
mkdir build
cd build
```

(6) cmake를 이용햇 빌드하기
```
cmake     -D WITH_CUDA=ON \
        -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-4.1.0/modules \
        -D WITH_GSTREAMER=ON \
        -D WITH_LIBV4L=ON \
        -D BUILD_opencv_python2=ON \
        -D BUILD_opencv_python3=ON \
        -D BUILD_TESTS=OFF \
        -D BUILD_PERF_TESTS=OFF \
        -D BUILD_EXAMPLES=OFF \
        -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local ..
```

(7) OpenCV와 컨트리뷰션 모듈을 컴파일하기 (약 2시간 소요)
```
make -j4
sudo make install
```
