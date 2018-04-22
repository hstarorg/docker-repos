FROM php:7.2.4-apache

LABEL author="Jay.M.Hu" email="hm910705@163.com"

COPY config/php.ini /usr/local/etc/php/php.ini

# 默认拷贝到容器中
# COPY dist/ /var/www/html/

# 也可以直接创建映射
# VOLUME [ "/var/www/html" ]

RUN chmod -R 777 /var/www/html/

# 安装mysql扩展
RUN xz -d /usr/src/php.tar.xz && \
	tar -xf /usr/src/php.tar -C /usr/src/ && \
	cd /usr/src/php-7.2.4/ext/mysqli/ && \
	phpize && \
	./configure -with-php-config=/usr/local/bin/php-config && \
	make && \
	make install;
