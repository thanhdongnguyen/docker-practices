FROM alpine:3.10.1


ENV PROMETHEUS_VER=2.11.1

###################### Install Libraries ######################


RUN apk --update add curl ca-certificates tar && \
	curl -Ls https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk
    # apk add --allow-untrusted /tmp/glibc-2.21-r2.apk

RUN apk update  && \
	apk upgrade && \
	apk add wget vim tmux git make musl-dev git openssh make curl 

###################### Install Enviroment Languages ######################

RUN mkdir -p /source/php && \
	mkdir -p /source/python && \
	mkdir -p /source/node && \
	mkdir -p /source/java && \
	mkdir -p /source/go && \
	mkdir -p /go && \
	mkdir -p /source/c++ && \
	mkdir -p /source/ruby 

# Python
RUN apk add python3
RUN pip3.7 install --upgrade pip && \
	pip3.7 install supervisor flask django prometheus_client gunicorn setuptools jaeger-client	


# Nodejs
RUN apk add nodejs npm && \
	npm install -g tsc
# PHP
RUN apk add php7 php7-fpm php7-opcache php7-gd php7-mysqli php7-zlib php7-curl
# Java
# RUN mkdir /opt && \
# 	curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz | tar -xzf - -C /opt && \
# 	ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jdk && \
# 	rm -rf /opt/jdk/*src.zip /opt/jdk/lib/missioncontrol /opt/jdk/lib/visualvm  /opt/jdk/lib/*javafx* /opt/jdk/jre/lib/plugin.jar /opt/jdk/jre/lib/ext/jfxrt.jar /opt/jdk/jre/bin/javaws /opt/jdk/jre/lib/javaws.jar  /opt/jdk/jre/lib/desktop /opt/jdk/jre/plugin /opt/jdk/jre/lib/deploy*  /opt/jdk/jre/lib/*javafx* /opt/jdk/jre/lib/*jfx* /opt/jdk/jre/lib/amd64/libdecora_sse.so /opt/jdk/jre/lib/amd64/libprism_*.so /opt/jdk/jre/lib/amd64/libfxplugins.so /opt/jdk/jre/lib/amd64/libglass.so /opt/jdk/jre/lib/amd64/libgstreamer-lite.so /opt/jdk/jre/lib/amd64/libjavafx*.so /opt/jdk/jre/lib/amd64/libjfx*.so
RUN apk fetch openjdk8 && \
	apk add openjdk8
# ENV JAVA_HOME=/opt/jdk
# ENV PATH=${PATH}:${JAVA_HOME}/bin

# Go
RUN mkdir -p /root/go/bin
RUN apk --update add go 
ENV GOROOT=/source/go
ENV GOPATH=/go
ENV GOBIN=/root/go/bin
ENV PATH=/go/bin:${PATH}
# C++
# Ruby


###################### Install Monitering ######################

# Prometheus
RUN wget https://github.com/prometheus/prometheus/releases/download/v${PROMETHEUS_VER}/prometheus-${PROMETHEUS_VER}.linux-amd64.tar.gz && \
    tar -xvzf prometheus-${PROMETHEUS_VER}.linux-amd64.tar.gz
