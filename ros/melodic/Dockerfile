FROM ros:melodic-ros-base-bionic

ARG DEBIAN_FRONTEND=noninteractive

# Needed to set keys
RUN apt-get update && apt-get install software-properties-common -y

RUN  apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
RUN add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo bionic main" -u

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
    && apt-get autoremove -y

# Ugly hack, otherwise librealsense2 installation fails.
RUN apt-get update && apt-get install -y \
    librealsense2-dkms \
   && apt-get autoremove -y

RUN apt-get update && apt-get install -y \
    librealsense2-utils \
   && apt-get autoremove -y

RUN apt-get update && apt-get install -y \
librealsense2-dev \
&& apt-get autoremove -y

RUN apt-get update && apt-get install -y \
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


# Installing a more recent cmake since ubuntu is out of date
RUN pip3 install cmake

RUN rosdep update

CMD [ "/bin/bash" ]
