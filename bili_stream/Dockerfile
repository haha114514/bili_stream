FROM ubuntu:16.04

RUN apt-get update && apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev wget unzip
RUN wget http://nginx.org/download/nginx-1.15.1.tar.gz
RUN wget https://github.com/sergey-dryabzhinsky/nginx-rtmp-module/archive/dev.zip
RUN tar -zxvf nginx-1.15.1.tar.gz
RUN unzip dev.zip

WORKDIR nginx-1.15.1

RUN ./configure --with-http_ssl_module --add-module=../nginx-rtmp-module-dev
RUN make
RUN make install

COPY nginx.conf /
RUN cat /nginx.conf >> /usr/local/nginx/conf/nginx.conf

EXPOSE 1935

CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]