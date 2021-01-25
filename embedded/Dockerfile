FROM ros:noetic-ros-base

ARG DEBIAN_FRONTEND=noninteractive

# Needed to set keys
RUN apt-get update && apt-get install software-properties-common -y

RUN  apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE ||  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
RUN add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo focal main" -u

# We need libpython2.7 due to GDB tools.
RUN apt-get update && apt-get install -y \
    apt-utils \
    bison \
    ca-certificates \
    ccache \
    check \
    curl \
    flex \
    git \
    gperf \
    lcov \
    libncurses-dev \
    libusb-1.0-0-dev \
    make \
    ninja-build \
    libpython2.7 \
    python3 \
    python3-pip \
    unzip \
    wget \
    xz-utils \
    zip \
    cmake \
    build-essential \
    clang-format \
    clang-tidy \
    doxygen \ 
    graphviz \
    gcc-arm-none-eabi \
    protobuf-compiler \
    python3-protobuf \
    python3-rosdep2 \
    librealsense2-dkms \
    librealsense2-utils \
    librealsense2-dev \
    librealsense2-dbg \
   && apt-get autoremove -y \
   && rm -rf /var/lib/apt/lists/* \
   && update-alternatives --install /usr/bin/python python /usr/bin/python3 10

RUN python -m pip install --upgrade pip virtualenv

# Install ROS requirements
RUN apt-get update && apt-get install -y \
  ros-noetic-rosdoc-lite

# To build the image for a branch or a tag of IDF, pass --build-arg IDF_CLONE_BRANCH_OR_TAG=name.
# To build the image with a specific commit ID of IDF, pass --build-arg IDF_CHECKOUT_REF=commit-id.
# It is possibe to combine both, e.g.:
#   IDF_CLONE_BRANCH_OR_TAG=release/vX.Y
#   IDF_CHECKOUT_REF=<some commit on release/vX.Y branch>.

ARG IDF_CLONE_URL=https://github.com/espressif/esp-idf.git
ARG IDF_CLONE_BRANCH_OR_TAG=v4.1
ARG IDF_CHECKOUT_REF=

ENV IDF_PATH=/opt/esp/idf
ENV IDF_TOOLS_PATH=/opt/esp

RUN echo IDF_CHECKOUT_REF=$IDF_CHECKOUT_REF IDF_CLONE_BRANCH_OR_TAG=$IDF_CLONE_BRANCH_OR_TAG && \
    git clone --recursive \
      ${IDF_CLONE_BRANCH_OR_TAG:+-b $IDF_CLONE_BRANCH_OR_TAG} \
      $IDF_CLONE_URL $IDF_PATH && \
    if [ -n "$IDF_CHECKOUT_REF" ]; then \
      cd $IDF_PATH && \
      git checkout $IDF_CHECKOUT_REF && \
      git submodule update --init --recursive; \
    fi

# Install esp-idf toolchain. Will need
#RUN $IDF_PATH/install.sh

# Ccache is installed, enable it by default
ENV IDF_CCACHE_ENABLE=1

# Install buzz
RUN git clone https://github.com/MISTLab/Buzz.git /tmp/buzz && \
    cd /tmp/buzz && \
    mkdir build && \
    cd build && \
    cmake ../src && \
    make && \
    make install && \
    ldconfig

RUN rosdep update



CMD [ "/bin/bash" ]

#Will need to souce esp-idf on entry to build.
