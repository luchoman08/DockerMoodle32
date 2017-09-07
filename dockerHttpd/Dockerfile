 FROM php:5.6-apache
 RUN mkdir /var/www/moodle
 WORKDIR /var/www/html/moodle
 RUN mkdir /var/www/moodledata
 RUN chown -R root:www-data /var/www//moodledata
 RUN chmod -R 770  /var/www//moodledata
 RUN chown -R www-data:www-data /var/www/html/moodle
 RUN chmod -R 777 /var/www/html/moodle
 RUN apt-get update
 RUN cat ../requirements.txt | xargs apt-get install --assume-yes   
 RUN pecl install zip   
 COPY config/php.ini /usr/local/etc/php/php.ini

