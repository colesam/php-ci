FROM nginx:1.10

ADD nginx.conf /etc/nginx/nginx.conf
ADD sites-enabled /etc/nginx/sites-enabled
WORKDIR /var/www

EXPOSE 80
EXPOSE 443

CMD ["nginx"]