FROM    ubuntu:16.04

# add key
COPY nginx_signing.key /tmp/nginx_signing.key
RUN apt-key add /tmp/nginx_signing.key

RUN echo "deb http://nginx.org/packages/ubuntu/ xenial nginx" | tee /etc/apt/sources.list.d/nginx.list
RUN echo "deb-src http://nginx.org/packages/ubuntu/ xenial nginx" | tee /etc/apt/sources.list.d/nginx.list

RUN apt-get update
RUN apt-get install -y nginx nodejs npm
RUN npm  install -g bower
RUN ln -s /usr/bin/nodejs /usr/bin/node

EXPOSE 80

ENTRYPOINT nginx -g 'daemon off;'
