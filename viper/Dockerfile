#
# This file is part of Viper - https://github.com/viper-framework/viper
# See the file 'LICENSE' for copying permission.
#

FROM ubuntu:14.04
MAINTAINER Viper-Framework (https://github.com/viper-framework)

ENV YARA_VERSION       3.5.0
ENV PYEXIF_VERSION     0.2.0
ENV ANDROGUARD_VERSION 1.9

USER root
RUN apt-get update && apt-get install -y \
    git \
    gcc \
    python-dev \
    python-pip \
    curl \
    libtool \
    autoconf \
    python-socksipy \
    python-m2crypto \
    python-levenshtein \
    swig \
    libssl-dev \
    libffi-dev \
    libfuzzy-dev \
    pff-tools \
    libimage-exiftool-perl && \
  rm -rf /var/lib/apt/lists/*

# Make Tmp Dir
RUN mkdir ~/tmp_build

# Install Yara
RUN cd ~/tmp_build && \
  git clone -b v${YARA_VERSION} https://github.com/VirusTotal/yara.git && \
  cd yara && \
  bash build.sh && \
  make install && \
  rm -rf yara && \
  ldconfig

# Install Yara python
RUN git clone --recursive https://github.com/VirusTotal/yara-python && \
  cd yara-python && \
  python setup.py build && \
  sudo python setup.py install && \
  cd ~/tmp_build && \
  sudo rm -rf yara-python

# Install PyExif
RUN cd ~/tmp_build && \
  git clone -b v${PYEXIF_VERSION} git://github.com/smarnach/pyexiftool.git && \
  cd pyexiftool && \
  python setup.py install 
  
# Install AndroGuard
RUN cd ~/tmp_build && \
  curl -sSL https://github.com/androguard/androguard/archive/${ANDROGUARD_VERSION}.tar.gz | \
  tar -xzC .  && \
  cd androguard-${ANDROGUARD_VERSION} && \
  python setup.py install

# Create Viper User
RUN groupadd -r viper && \
  useradd -r -g viper -d /home/viper -s /sbin/nologin -c "Viper User" viper && \
  mkdir /home/viper && \
  chown -R viper:viper /home/viper

# Clean tmp_build
RUN rm -rf ~/tmp_build

USER viper
WORKDIR /home/viper
RUN git clone https://github.com/viper-framework/viper.git

USER root
WORKDIR /home/viper/viper
RUN pip install -r requirements.txt

USER viper
EXPOSE 9090
CMD python viper-web -H $HOSTNAME
