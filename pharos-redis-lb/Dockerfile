FROM ubuntu:14.04
MAINTAINER Jonah Sullivan <jonah@thats.ninja>

RUN apt-get update && apt-get install -y software-properties-common python-software-properties && \
    add-apt-repository ppa:vbernat/haproxy-1.5 && \
    apt-get update && \
    apt-get install -y haproxy socat && \
    rm -rf /var/lib/apt/lists/*

RUN echo 'EXTRAOPTS="-db"' >> /etc/default/haproxy

RUN mkdir -p /run/haproxy && touch /run/haproxy/admin.sock

ADD ./confd/conf.d /etc/confd/conf.d
ADD ./confd/templates /etc/confd/templates
ADD https://github.com/rancher/confd/releases/download/0.11.0-dev-rancher/confd-0.11.0-dev-rancher-linux-amd64 /confd
RUN chmod +x /confd

EXPOSE 6379

CMD ["haproxy", "-f", "/etc/haproxy/haproxy.cfg", "-p", "-/var/run/haproxy.pid"]