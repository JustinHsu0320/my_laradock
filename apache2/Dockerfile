# FROM httpd:2.4

# LABEL maintainer="Lin Leo"

# RUN apk update; \
#     apk upgrade;
# # Copy apache vhost file to proxy php requests to php-fpm container
# COPY demo.apache.conf /usr/local/apache2/conf/demo.apache.conf
# RUN echo "Include /usr/local/apache2/conf/demo.apache.conf" \
#     >> /usr/local/apache2/conf/httpd.conf

# # rewrite

# RUN sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf

# # Include other conf
# RUN { \
#         echo 'IncludeOptional /usr/local/apache2/conf/sites-available/*.conf'; \
#     } >> /usr/local/apache2/conf/httpd.conf \
#     && mkdir /usr/local/apache2/conf/sites-available \ 
#     && chmod -R o+w /usr/local/apache2/conf/sites-available


FROM httpd:2.4

LABEL maintainer="Lin Leo"

ARG WEB_USER=www-data
ARG WEB_GROUP=www-data
ARG APACHE_ROOT_DIR=/usr/local/apache2

# COPY httpd-vhosts.conf ${APACHE_ROOT_DIR}/conf/extra/httpd-vhosts.conf
# COPY httpd.conf ${APACHE_ROOT_DIR}/conf/httpd.conf
RUN apt-get update
RUN apt-get -y install vim curl

# a2enmod rewrite

RUN chgrp -R ${WEB_GROUP} ${APACHE_ROOT_DIR}/conf/httpd.conf \
    && chgrp -R ${WEB_GROUP} ${APACHE_ROOT_DIR}/conf/extra/httpd-vhosts.conf

RUN usermod -u 1000 ${WEB_USER} \
    && groupmod -g 1000 ${WEB_GROUP} \
    && chgrp -R ${WEB_GROUP} ${APACHE_ROOT_DIR}