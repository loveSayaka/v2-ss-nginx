FROM nginx:1.16-alpine
LABEL maintainer="ss over v2ray_plugin wtih a default site by nginx"
RUN rm /etc/nginx/conf.d/* \
     && mkdir ~/vps
COPY home /usr/share/nginx/html
COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/my.conf /etc/nginx/default.d/
COPY pem/* /root/cfpem/ 
