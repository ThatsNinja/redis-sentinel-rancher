FROM centos:latest
MAINTAINER Jonah Sullivan <jonah@thats.ninja>

RUN yum -y install make gcc cc tar

RUN \
  cd /tmp && \
  curl -O http://download.redis.io/redis-stable.tar.gz && \
  tar xvzf redis-stable.tar.gz && \
  cd redis-stable && \
  make && \
  make install && \
  cp -f src/redis-sentinel /usr/local/bin && \
  mkdir -p /etc/redis && \
  cp -f *.conf /etc/redis && \
  rm -rf /tmp/redis-stable* && \
  sed -i 's/^\(bind .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(daemonize .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(dir .*\)$/# \1\ndir \/data/' /etc/redis/redis.conf && \
  sed -i 's/^\(logfile .*\)$/# \1/' /etc/redis/redis.conf

RUN yum -y erase gcc cc tar

VOLUME ["/data"]

WORKDIR /data

EXPOSE 26379

ADD giddyup /usr/local/bin/giddyup
RUN chmod 777 /usr/local/bin/giddyup

ADD sentinel.conf /etc/redis/sentinel.conf

ADD start-sentinel.sh /start-sentinel.sh
RUN chmod 777 /start-sentinel.sh
ENTRYPOINT [ "/start-sentinel.sh"]
