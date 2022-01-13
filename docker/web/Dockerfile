FROM nginx:1.20

RUN apt-get update && apt-get install -y \
    nano
    
RUN rm /etc/nginx/conf.d/default.conf
COPY ./vhost /etc/nginx/conf.d
