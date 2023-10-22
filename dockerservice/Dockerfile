FROM webdevops/php-nginx:7.2

ENV COMPOSER_ALLOW_SUPERUSER=1

#ADD wkhtmltox_0.12.5-1.stretch_amd64.deb /tmp/

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
   #&& sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list.d/buster.list \
   #&& sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list.d/buster.list \
    && apt-get update \
    && cd /tmp \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && docker-service-enable ssh \
    && echo 'root:123456' | chpasswd \
    && pecl install http://pecl.php.net/get/yaf-3.0.8.tgz \
    && echo "[yaf]" >> /opt/docker/etc/php/php.ini \
    && echo "extension=yaf.so" >> /opt/docker/etc/php/php.ini \
    && echo "yaf.use_namespace=1" >> /opt/docker/etc/php/php.ini \
    && echo "yaf.cache_config=1" >> /opt/docker/etc/php/php.ini \
    && docker-run-bootstrap \
    && docker-image-cleanup

ENV WEB_DOCUMENT_ROOT=project
WORKDIR $WEB_DOCUMENT_ROOT
