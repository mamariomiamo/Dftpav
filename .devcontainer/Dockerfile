# docker build -t noetic_from_file_try_v1 .

FROM osrf/ros:noetic-desktop-full
RUN apt-get update && apt-get install -y git \
    && apt-get install -y python3-pip \
    && apt-get install -y nano \
    && apt-get install -y tmux \
    && apt-get install -y bash-completion \
    && apt-get install -y wget

ADD .tmux.conf /root/
ADD cmake-3.26.3-linux-x86_64.tar.gz /root/
# export PATH=/root/cmake-3.26.3-linux-x86_64/bin:$PATH
# export CMAKE_PREFIX_PATH=/root/cmake-3.26.3-linux-x86_64:$CMAKE_PREFIX_PATH


# Install Protocal Buffer

# compile protobuf with -fPIC
# cmake . -DCMAKE_CXX_STANDARD=17  -DCMAKE_POSITION_INDEPENDENT_CODE=ON
#  cmake --build . --parallel 10 
# make VERBOSE=1 test
# sudo make install
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc


RUN cd ~/ \
    # && git clone https://github.com/protocolbuffers/protobuf.git -b v22.3 --recurse-submodules -j8 \
    && git clone https://github.com/protocolbuffers/protobuf.git -b v3.16.1 --recurse-submodules \
    && cd ~/protobuf/cmake \
    && cmake . -DCMAKE_CXX_STANDARD=17  -DCMAKE_POSITION_INDEPENDENT_CODE=ON \
    && cmake --build . --parallel 10 \
    && sudo make install

# Clone repository

# Install repo dependencies
## Install ompl

## Install geographic_msgs
RUN apt-get install -y ros-noetic-geographic-msgs \
    && apt-get install -y ros-noetic-tf2-sensor-msgs \
    && apt-get install -y libompl-dev ompl-demos \
    && apt-get install -y libgoogle-glog-dev libdw-dev libopenblas-dev gfortran

RUN mkdir -p ~/catkin_ws/src \
    && cd ~/catkin_ws/src \
    && git clone https://github.com/ZJU-FAST-Lab/Dftpav

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN cd ~/catkin_ws \
    && source /opt/ros/noetic/setup.bash \
    && catkin_make -DCMAKE_BUILD_TYPE=Release
