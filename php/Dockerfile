FROM ubuntu18.04

#php版本
ARG version=7.3
#增加php的源
RUN apt-add-repository ppa:ondrej/php
#安装必要的包
RUN apt insall -y libmcrypt-dev \
    software-properties-common \
    apt-transport-https \
    lsb-release \
    ca-certificates \
    libxml2*

RUN apt insall -y php7.3 \
    php-pear


VOLUME [ "/etc/php/" ]