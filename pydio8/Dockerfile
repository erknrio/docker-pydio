FROM debian:jessie

LABEL maintainer Erknrio <erknrio@gmail.com>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget apache2 && \
    echo "deb https://download.pydio.com/pub/linux/debian/ jessie-backports main" > /etc/apt/sources.list.d/pydio.list && \
    wget -qO - https://download.pydio.com/pub/linux/debian/key/pubkey | apt-key add - && \
    apt-get install -y apt-transport-https && \
    apt-get update && \
    apt-get install -y pydio pydio-all && \
    wget https://download.pydio.com/pub/core/archives/pydio-core-8.0.0.tar.gz && \
    tar -xzf pydio-core-8.0.0.tar.gz && \
    mv pydio-core-8.0.0 /var/www/html/pydio/ && \
    chown -R www-data:www-data /var/www/html/pydio/ && \
    rm pydio-core-8.0.0.tar.gz
    
WORKDIR /var/www/
ENV TERM xterm

CMD apachectl -DFOREGROUND
