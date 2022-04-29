FROM alpine:latest

LABEL MAINTAINER="me@monlor.com"

ENV LANG='zh_CN.UTF-8' LANGUAGE='zh_CN:zh' LC_ALL='zh_CN.UTF-8'

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk update && apk add --no-cache bash tzdata curl && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime