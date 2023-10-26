FROM php:8.0-apache
RUN apt-get update && \
    apt-get install -y
RUN apt-get install -y curl
RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev
#php ini
COPY php.ini /usr/local/etc/php/php.ini
#apache
RUN rm -rf /var/www/html
RUN mkdir /var/www/html
RUN chown -R www-data:www-data /var/www/html
#install codeigniter from oficial page
WORKDIR /var/www/html
RUN curl -O https://codeigniter.com/downloads/project/version4.zip
RUN unzip version4.zip
RUN rm version4.zip
RUN mv codeigniter4/ /var/www/html/
COPY sites-available/ci4.conf /etc/apache2/sites-enabled/sitio.conf
RUN docker-php-ext-install mysqli pdo pdo_mysql zip mbstring
RUN a2enmod rewrite
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd
RUN service apache2 restart
