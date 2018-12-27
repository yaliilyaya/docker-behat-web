#FROM php:7.1-fpm
#
#RUN apt-get update && apt-get install -y wget git unzip openssh-server php php-dev php-pear \
#    && pecl install xdebug-2.6.1 \
#    && docker-php-ext-enable xdebug
#
#ADD ./php.ini /usr/local/etc/php/php.ini
#
#

FROM ubuntu:16.04

RUN apt-get update && apt-get install -y wget git unzip openssh-server php php-dev php-pear php-mbstring
RUN mkdir /var/run/sshd
RUN echo 'root:developer' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22

#xdebug install =( не работат
RUN pecl install xdebug-2.6.1
#RUN yes | pecl install xdebug \
#    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
#    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
#    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

ADD ./php.ini /usr/local/etc/php/php.ini
#composer install
RUN wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet

RUN mkdir -p /var/www/composer
ADD ./composer.json /var/www/composer/composer.json

WORKDIR /var/www/behat

CMD ["/usr/sbin/sshd", "-D"]