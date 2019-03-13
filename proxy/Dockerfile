FROM jmferrer/apache2-reverse-proxy

COPY ./conf/proxy.conf /etc/apache2/sites-enabled

COPY ./index.html /var/www/html/

CMD ["apache2-reverse-proxy"]
