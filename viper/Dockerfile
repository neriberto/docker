FROM ubuntu:18.04
LABEL maintainer="neriberto@gmail.com"
LABEL version="2.0-dev"

# Install requirements
RUN apt-get update -qq && \
    apt-get --no-install-recommends -yq install \
    build-essential automake libtool make gcc autoconf \
    python3-dev python3-pip python3-setuptools git \
    libssl-dev swig libffi-dev ssdeep libfuzzy-dev \
    flex bison libssl-dev libmagic-dev valabind valac \
    p7zip-full unrar exiftool bsdmainutils git

# Download all sources
WORKDIR /src
RUN git clone https://github.com/viper-framework/viper && \
    git clone https://github.com/VirusTotal/yara.git && \
    git clone --recursive https://github.com/VirusTotal/yara-python && \
    git clone https://github.com/radare/radare2.git

WORKDIR /src/viper
RUN git checkout 5cf700761d904d9002a272164735c2ed2b4e0df9 && \
    git submodule init && \
    git submodule update && \
    sed -i -e s/Django/Django==2.0.2/g requirements-web.txt && \
    pip3 install -r requirements.txt && \
    make install

WORKDIR /src/yara
RUN git checkout v3.8.0 && \
    ./bootstrap.sh && \
    ./configure --enable-magic --enable-dotnet --with-crypto && \
    make && \
    make install && \
    echo "/usr/local/lib" >> /etc/ld.so.conf && \
    ldconfig

# Install Yara python
WORKDIR /src/yara-python
RUN git checkout . && \
    python3 setup.py build && \
    python3 setup.py install

WORKDIR /src/radare2
RUN git checkout 2.8.0 && \
    sys/install.sh && \
    r2pm init

# RUN pip install pyclamd

WORKDIR /root
RUN apt-get autoremove && \
    apt-get -y purge python-dev libmagic-dev libssl-dev libffi-dev libfuzzy-dev git gcc autoconf automake make && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 8080/tcp
VOLUME ["/root/.viper/"]
CMD ["viper-web", "-H", "0.0.0.0"]
