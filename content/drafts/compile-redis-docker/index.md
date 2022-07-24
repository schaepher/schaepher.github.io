---
title: 编译 Redis 源码
date: 2020-03-27 01:05:00
updated: 2020-03-27 01:05:00
tags: 
- 
---



```yml
FROM centos:7

COPY ./CentOS-Base.repo /etc/yum.repo.d/CentOS-Base.repo

RUN groupadd -r redis && useradd -r -g redis redis

ENV REDIS_VERSION 5.0.3
ENV BUILD_DEPS=' \
        gcc \
        make \
    '

ADD ./redis-${REDIS_VERSION}.tar.gz /usr/src/

RUN yum install -y ${BUILD_DEPS} \
    && mv /usr/src/redis-${REDIS_VERSION} /usr/src/redis \
	&& grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 1$' /usr/src/redis/src/server.h \
	&& sed -ri 's!^(#define CONFIG_DEFAULT_PROTECTED_MODE) 1$!\1 0!' /usr/src/redis/src/server.h \
	&& grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 0$' /usr/src/redis/src/server.h \
    && make -C /usr/src/redis -j "$(nproc)" \
	&& make -C /usr/src/redis install \
	&& rm -r /usr/src/redis

RUN mkdir /data && chown redis:redis /data
VOLUME /data
WORKDIR /data

COPY docker-entrypoint.sh /
RUN chmod a+x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 6379

USER redis

CMD ["redis-server"]
```