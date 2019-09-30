FROM scratch

RUN useradd www -m

ADD ubuntu18.04-i386.tar.gz /

RUN apt update

#基础环境构建，只安装基础包
RUN apt install -y curl \
    wget \
    unzip \
    zip \
    jq \
    lrzsz \
    vim \
    libreoffice \
    gcc \
    gcc-c++ \
    #编译使用
    build-essential \
    nmap \
    sqlite3-pcre \
    ssh \
    autoconf \
    automake

#清安装包
RUN apt autoclean && rm -fr /var/cache/apt/archives/ 