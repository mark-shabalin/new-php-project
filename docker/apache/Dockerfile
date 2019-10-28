ARG APACHE_IMAGE

FROM ${APACHE_IMAGE}

RUN apk update;

RUN echo "Include /usr/local/apache2/conf/apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf
