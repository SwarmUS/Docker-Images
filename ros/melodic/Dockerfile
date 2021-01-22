FROM ros:melodic-ros-base-bionic

ARG DEBIAN_FRONTEND=noninteractive

# Needed to set keys
RUN apt-get update && apt-get install software-properties-common -y

RUN  apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE ||  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
RUN add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo bionic main" -u

RUN apt-get update && apt-get install -y \
    apt-utils \
    ca-certificates \
    curl \
    make \
    python3 \
    python3-pip \
    unzip \
    zip \
    protobuf-compiler \
    python3-protobuf \
    wget \
    librealsense2-dkms \
    librealsense2-utils \
    librealsense2-dev \
    librealsense2-dbg \
   && apt-get autoremove -y

# Install buzz
RUN git clone https://github.com/MISTLab/Buzz.git /tmp/buzz && \
    cd /tmp/buzz && \
    mkdir build && \
    cd build && \
    cmake ../src && \
    make && \
    make install && \
    ldconfig

# Install I2Cdevlib
RUN mkdir -p /usr/share/arduino/libraries && \
    cd /usr/share/arduino/libraries && \
    git clone https://github.com/chrisspen/i2cdevlib.git

# Install Bcm2835
RUN cd /tmp && \
    wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.50.tar.gz && \
    tar zxvf bcm2835-1.50.tar.gz && \
    cd bcm2835-1.50 && \
    ./configure && \
    make && \
    make install

# Installing a more recent cmake since ubuntu is out of date
RUN pip3 install cmake



CMD [ "/bin/bash" ]
