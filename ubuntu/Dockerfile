FROM ubuntu:19.04

RUN apt-get update && \
      apt-get -y upgrade && \
      apt-get install -y build-essential && \
      apt-get install -y software-properties-common && \
      apt-get install -y libssl-dev libffi-dev python-dev && \
      apt-get install -y curl git htop man unzip vim tmux wget python-pip


CMD ["/usr/sbin/init"]
