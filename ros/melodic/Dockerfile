FROM ros:melodic-ros-base-bionic

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    apt-utils \
    ca-certificates \
    curl \
    make \
    python3 \
    python3-pip \
    unzip \
    wget \
    zip \
    cmake \
    protobuf-compiler \
    python3-protobuf \
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



CMD [ "/bin/bash" ]
