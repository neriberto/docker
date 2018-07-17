FROM ubuntu:18.04
LABEL maintainer="neriberto@gmail.com"
LABEL version="2.0-dev"

RUN apt-get update -qq && \
    apt-get --no-install-recommends -yq install \
    build-essential automake libtool make gcc autoconf \
    python3-dev python3-pip python3-setuptools git \
    libssl-dev swig libffi-dev ssdeep libfuzzy-dev \
    flex bison libssl-dev libmagic-dev valabind valac \
    p7zip-full unrar

WORKDIR /opt
RUN git clone https://github.com/viper-framework/viper
WORKDIR /opt/viper
RUN git submodule init && \
    git submodule update && \
    pip3 install -r requirements.txt && \
    make install

WORKDIR /src/
RUN git clone https://github.com/VirusTotal/yara.git
WORKDIR /src/yara
RUN ./bootstrap.sh && \
    ./configure --enable-magic --with-crypto && \
    make && \
    make install && \
    echo "/usr/local/lib" >> /etc/ld.so.conf && \
    ldconfig

# Install Yara python
WORKDIR /src/
RUN git clone --recursive https://github.com/VirusTotal/yara-python
WORKDIR /src/yara-python
RUN python3 setup.py build && python3 setup.py install

WORKDIR /src/
RUN git clone https://github.com/radare/radare2.git
WORKDIR /src/radare2
RUN sys/install.sh && r2pm init
#RUN r2pm install lang-python3 && \
#    r2pm install r2api-python && \
#    r2pm install r2pipe-py

# RUN pip install pyclamd

RUN apt-get autoremove && \
    apt-get -y purge python-dev libmagic-dev libssl-dev libffi-dev libfuzzy-dev git gcc autoconf automake make && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /src/*
