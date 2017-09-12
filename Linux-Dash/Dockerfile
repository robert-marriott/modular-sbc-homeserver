
###############################################################################
# Linux-Dash is a supposedly lightweight, simple webui for monitoring Linux
# system information. It runs on whatever arbitrary webserver.
###############################################################################
FROM armhf/alpine

# Add dependencies for Linux-Dash to work
RUN  apk update && apk upgrade && \
     apk add  bash \
              apache2 \
              apache2-utils \
              curl \
              php5 \
              php5-curl \
              php5-json \
              git && \
              rm -rf /var/cache/apk/*

# Create config file with sed for simple deployment
RUN sed -i 's#^DocumentRoot ".*#DocumentRoot "/web/html"#g' /etc/apache2/httpd.conf && \
    sed -i 's#AllowOverride [Nn]one#AllowOverride All#' /etc/apache2/httpd.conf && \
    sed -i 's#^ServerRoot .*#ServerRoot /web#g'  /etc/apache2/httpd.conf && \
    sed -i 's/^#ServerName.*/ServerName webproxy/' /etc/apache2/httpd.conf && \
    sed -i 's#^IncludeOptional /etc/apache2/conf#IncludeOptional /web/config/conf#g' /etc/apache2/httpd.conf && \
    sed -i 's#PidFile "/run/.*#Pidfile "/web/run/httpd.pid"#g'  /etc/apache2/conf.d/mpm.conf && \
    sed -i 's#Directory "/var/www/localhost/htdocs.*#Directory "/web/html" >#g' /etc/apache2/httpd.conf && \
    sed -i 's#Directory "/var/www/localhost/cgi-bin.*#Directory "/web/cgi-bin" >#g' /etc/apache2/httpd.conf && \

    sed -i 's#/var/log/apache2/#/web/logs/#g' /etc/logrotate.d/apache2 && \
    sed -i 's/Options Indexes/Options /g' /etc/apache2/httpd.conf && \

    mkdir /web/ && chown -R apache.www-data /web && \
    git clone https://github.com/afaqurk/linux-dash.git /web

EXPOSE 80 443

VOLUME /web

CMD exec /usr/sbin/apachectl -DFOREGROUND
