FROM redis:3.2.4
MAINTAINER Jonah Sullivan <jonah@thats.ninja>
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y curl sed 

ADD giddyup /usr/local/bin/giddyup
RUN chmod 777 /usr/local/bin/giddyup

ADD conf/redis.conf /usr/local/etc/redis/redis.conf
ADD  start-redis.sh /start-redis.sh
RUN chmod 777 /start-redis.sh
CMD [ "/start-redis.sh"]
