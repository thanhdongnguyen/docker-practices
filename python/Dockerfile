FROM centos:7

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum -y install epel-release && \
    yum install -y git wget vim tmux python-pip net-tools java-1.8.0-openjdk zlib-devel libffi-devel

RUN wget https://github.com/prometheus/prometheus/releases/download/v2.11.1/prometheus-2.11.1.linux-amd64.tar.gz && \
    tar -xvzf prometheus-2.11.1.linux-amd64.tar.gz

ENV PYTHON_VER=3.7.4
RUN yum groupinstall -y "Development Tools"
RUN wget https://www.python.org/ftp/python/${PYTHON_VER}/Python-${PYTHON_VER}.tar.xz
RUN tar -xJf Python-${PYTHON_VER}.tar.xz
RUN cd Python-${PYTHON_VER} && ./configure --enable-optimizations  && make altinstall

RUN pip install --upgrade pip && \
	pip install supervisor flask django prometheus_client gunicorn

COPY supervisord.conf /etc/supervisord.conf

CMD /usr/bin/supervisord -c /etc/supervisord.conf