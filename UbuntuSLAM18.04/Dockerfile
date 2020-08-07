FROM ubuntu:18.04
LABEL maintainer "chengcheng0829@gmail.com"

# 1. Update source list and basic tools
RUN apt-get update -y \
    && apt-get install -y ca-certificates apt-utils \
    && echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse" > /etc/apt/sources.list \
    && echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list \
    && echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get dist-upgrade -y \
    && apt-get autoremove -y \
    # basic tools
    && apt-get install -y software-properties-common tree vim wget p7zip zip unzip curl build-essential \
    # install git
    && add-apt-repository -y ppa:git-core/ppa \
    && apt update \
    && apt install -y git

# 2. anaconda
# RUN  wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-2020.07-Linux-x86_64.sh -O ~/anaconda.sh \
#     && /bin/bash ~/anaconda.sh -b -p /opt/anaconda3 \
#     && rm -rf ~/anaconda.sh \
#     # Add by Anaconda
#     echo "export PATH=\"/opt/anaconda3/bin:\$PATH\"" >> ~/.bashrc

# 3. C++ tools
RUN apt-get install -y cmake doxygen clang-format-10 qt5-default libgoogle-glog-dev libgflags-dev libboost-all-dev \
    && apt-get install -y libsuitesparse-dev libtbb-dev nasm libatlas-base-dev \
    # 3.0 init
    && mkdir /home/code \
    && cd /home/code \
    # 3.1 gtest
    && wget https://github.com/google/googletest/archive/release-1.10.0.tar.gz -O /home/code/gtest.tar.gz \
    && tar -zxvf ./gtest.tar.gz \
    && cd ./googletest-release-1.10.0 \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON ..\
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.2 Eigen
    && wget https://gitlab.com/libeigen/eigen/-/archive/3.3.7/eigen-3.3.7.tar.gz -O /home/code/eigen.tar.gz \
    && tar -zxvf ./eigen.tar.gz \
    && cd ./eigen-3.3.7 \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF .. \
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.3 ceres
    && wget https://github.com/ceres-solver/ceres-solver/archive/1.14.0.tar.gz -O /home/code/ceres.tar.gz \
    && tar -zxvf ./ceres.tar.gz \
    && cd ./ceres-solver-1.14.0 \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF -DCXX11=ON -DBUILD_SHARED_LIBS=ON -DBUILD_EXAMPLES=OFF .. \
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.4 Sophus
    && wget https://codeload.github.com/strasdat/Sophus/zip/master -O /home/code/Sophus.zip \
    && unzip ./Sophus.zip \
    && cd ./Sophus-master \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTS=OFF -DBUILD_EXAMPLES=OFF .. \
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.5 fmt
    && wget https://github.com/fmtlib/fmt/archive/7.0.2.tar.gz -O /home/code/fmt.tar.gz \
    && tar -zxvf ./fmt.tar.gz \
    && cd ./fmt-7.0.2 \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DFMT_TEST=OFF -DFMT_DOC=OFF .. \
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.6 json
    && wget https://github.com/nlohmann/json/archive/v3.9.0.tar.gz -O /home/code/json.tar.gz \
    && tar -zxvf ./json.tar.gz \
    && cd ./json-3.9.0 \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF .. \
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.7 jpeg-turbo
    && wget https://github.com/libjpeg-turbo/libjpeg-turbo/archive/2.0.5.tar.gz -O /home/code/jpeg-turbo.tar.gz \
    && tar -zxvf ./jpeg-turbo.tar.gz \
    && cd ./libjpeg-turbo-2.0.5 \
    && mkdir build \
    && cd ./build \
    && cmake -DWITH_JPEG7=ON -DWITH_JPEG8=ON -DCMAKE_INSTALL_PREFIX:PATH="/usr/local" -DCMAKE_INSTALL_LIBDIR:PATH="lib" \
    -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_MANDIR:PATH="<CMAKE_INSTALL_DATAROOTDIR>/man/turbojpeg" \
    -DCMAKE_INSTALL_DOCDIR:PATH="<CMAKE_INSTALL_DATAROOTDIR>/doc/turbojpeg" .. \
    && make -j4 \
    && make install \
    && cd /home/code \
    # 3.8 OpenCV
    && apt-get install -y libgtk-3-dev pkg-config libavcodec-dev libavformat-dev libavresample-dev libswscale-dev \
    libtbb-dev libtbb2 libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev libopenblas-dev libatlas-cpp-0.6-dev \
    liblapacke-dev libfreetype6-dev libharfbuzz-dev \
    # install jasper
    && echo "deb http://security.ubuntu.com/ubuntu xenial-security main" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y libjasper-dev \
    # contrib modules dependency
    && apt-get install -y libhdf5-dev libtesseract-dev libleptonica-dev \
    && wget https://github.com/opencv/opencv/archive/4.4.0.tar.gz -O /home/code/OpenCV.tar.gz \
    && wget https://github.com/opencv/opencv_contrib/archive/4.4.0.tar.gz -O /home/code/OpenCVContrib.tar.gz \
    && tar -zxvf ./OpenCV.tar.gz \
    && tar -zxvf ./OpenCVContrib.tar.gz \
    && cd ./opencv-4.4.0 \
    && mkdir build \
    && cd ./build \
    && cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_DOCS=ON -DWITH_QT=ON -DBUILD_PERF_TESTS=OFF -DBUILD_TESTS=OFF \
    -DJPEG_INCLUDE_DIR:PATH="/usr/local/include" -DJPEG_LIBRARY_RELEASE:FILEPATH="/usr/local/lib/libjpeg.so" \
    -DOPENCV_EXTRA_MODULES_PATH:PATH="../../opencv_contrib-4.4.0/modules" \
    -DOPENCV_ENABLE_NONFREE=ON .. \
    && make -j4 \
    && make -j4 doxygen \
    && make install \
    && cd /home/code \
    # 3.x End
    && cd / \
    && rm -rf /home/code

