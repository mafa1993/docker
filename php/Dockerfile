FROM ubuntu18.04

#php版本
ARG version=7.3
# 扩展目录，挂载扩展目录，不在docker内部安装扩展
ARG extension_dir

RUN apt update --fix-missing

#安装必要的包
RUN apt install -y libmcrypt-dev \
    software-properties-common \
    apt-transport-https \
    lsb-release \
    ca-certificates \
    # xml
    libxml2-dev \
    # pcre
    libpcre3-dev \
    build-essential \
    # jpeg
    libjpeg62-dev \
    # freetype
    libfreetype6-dev \  
    # png
    libpng12-dev \
    libpng3 \
    libpnglite-dev \
    # iconv
    libiconv-hook-dev \ 
    libiconv-hook1 \
    # mycrypt
    libmcrypt-dev \
    libmcrypt4 \
    # mhash
    libmhash-dev \
    libmhash2 \
    # openssl
    libltdl-dev \
    libssl-dev \
    # curl
    libcurl4-openssl-dev \
    # mysql
    libmysqlclient-dev

# 增加php源，防止要安装的版本不存在
RUN apt-get install language-pack-en -y
RUN apt-get install -y python-software-properties && export LANG=en_US.UTF-8 && LC_ALL=en_US.UTF-8 apt-add-repository ppa:ondrej/php && apt update 

# 由于apt-add-respository时有特殊字符返回，导致出错，改为将原copy到源目录
# 含有特殊字符的信息 key E5267A6C: public key "Launchpad PPA for Ondřej Surý" imported
# COPY ondrej-ubuntu-php-xenial.list /etc/apt/sources.list.d
# RUN apt update

RUN apt install -y php${version} \
    php-pear \
    php${version}-dev \
    php${version}-fpm


# 清除安装包
RUN apt clean && rm -fr /var/cache/apt/archives

# 扩展目录放在宿主机，在宿主机安装扩展即可实现扩展的安装，不必在docker内安装
#RUN pecl instll -y swoole \
#    redis
# RUN systemctl enable php${version}_fpm && systemctl start ${version}_fpm
RUN ln -s '/usr/lib/systemd/system/postfix.service' '/etc/systemd/system/multi-user.target.wants/test.service'
ENTRYPOINT service start php${version}-fpm start 

# 可以直接挂载扩展目录，共享扩展目录，在宿主机安装，docker里就安装了，apt get install的配置目录默认在/etc/php中
VOLUME ["/etc/php/","/dev/shm/php_fpm.sock","${extension_dir}"]

# docker build -t php7.3  --build-arg version=7.3 --build-arg extension_dir=/usr/local/lib/php/extensions/no-debug-non-zts-20170718 . -t代表指定名字
# docker run  -v /etc/php/:/etc/php/  /dev/shm/php-fpm.sock:/dev/shm/php-fpm.sock --name php  --privileged -itd php7.3 /bin/bash