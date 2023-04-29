FROM php:8.0-apache
COPY ./source.zip /tmp/source.zip
RUN /usr/bin/apt-get update && \
    # Download the source code
    /usr/bin/apt-get install -y unzip && \
    /usr/bin/unzip /tmp/source.zip -d /var/www/html/ && \
    # Install and enable SQLite3
    /usr/bin/apt-get install -y sqlite3 libsqlite3-dev && \
    docker-php-ext-install pdo_sqlite && docker-php-ext-enable pdo_sqlite && \
    # Set the correct permissions
    /bin/chown -R www-data:www-data /var/www/html/ && \
    /bin/chmod -R 777 /var/www/html/ && \
    # Clean up
    /usr/bin/apt-get purge -y unzip && /usr/bin/apt-get clean && \
    /bin/rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
USER www-data
WORKDIR /var/www/html/
EXPOSE 80
ENTRYPOINT [ "/bin/sh", "-c", "/usr/local/bin/apache2-foreground" ]