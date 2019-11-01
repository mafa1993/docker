
# php dockerFile介绍

1. 基于ubuntu18.04的镜像构建
2. 使用arg version指定安装php的版本
3. 配置文件路径/etc/php/已经挂载
4. 使用socket进行PHP的通信，/dev/shm/php_fpm.sock已经挂载到宿主
5. docker build -t php7.3  --build-arg version=7.3 --build-arg extension_dir=/usr/local/lib/php/extensions/no-debug-non-zts-20170718 .
6. 运行命令 docker run  -v /etc/php/:/etc/php/ -v /dev/shm/php_fpm.sock:/dev/shm/php_fpm.sock  --name php  --privileged -itd php7.3 /bin/bash
