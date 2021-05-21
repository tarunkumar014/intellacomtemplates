FROM wordpress:php7.4-fpm-alpine

MAINTAINER tarun@lsnsoft.com

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN rm /usr/local/bin/docker-entrypoint.sh

#ADD   composer.json /var/www/composer.json

COPY docker-entrypoint.sh /usr/local/bin/

ENV custom_php_conf /usr/local/etc/php/php.ini

RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini

RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" ${custom_php_conf} && \
    sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 90M/g" ${custom_php_conf} && \
    sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" ${custom_php_conf} && \
    sed -i -e "s/memory_limit\s*=\s*128M/memory_limit = 196M/g" ${custom_php_conf} && \
    sed -i -e "s/max_execution_time\s*=\s*30/max_execution_time = 60/g" ${custom_php_conf} && \
    sed -i -e "s/variables_order = \"GPCS\"/variables_order = \"EGPCS\"/g" ${custom_php_conf} && \
    sed -i -e "s/;opcache.enable=1/opcache.enable=1/g" ${custom_php_conf} && \
    sed -i -e "s/;opcache.memory_consumption=128/opcache.memory_consumption=128/g" ${custom_php_conf} && \
    sed -i -e "s/;opcache.max_accelerated_files=10000/opcache.max_accelerated_files=10000/g" ${custom_php_conf} && \
    sed -i -e "s/;opcache.revalidate_freq=2/opcache.revalidate_freq=240/g" ${custom_php_conf}

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["php-fpm"]


