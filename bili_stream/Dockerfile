FROM ubuntu:18.04

RUN apt-get update && apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev wget unzip
RUN wget https://nginx.org/download/nginx-1.19.9.tar.gz
RUN tar -zxvf nginx-1.19.9.tar.gz

WORKDIR nginx-1.19.9

RUN ./configure --with-stream --with-http_ssl_module --without-http_gzip_module
RUN make
RUN make install

COPY nginx.conf /
RUN cp /nginx.conf /usr/local/nginx/conf/nginx.conf

EXPOSE 1935

CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
