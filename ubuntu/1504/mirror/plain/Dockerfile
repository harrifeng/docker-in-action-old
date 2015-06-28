FROM ubuntu:15.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN rm /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
    sudo \
    netcat \
    iputils-ping \
    supervisor \
    openssh-server

RUN useradd -s /bin/bash -m hfeng
RUN echo "hfeng:hfeng" | chpasswd
RUN echo "root:wyyzmwy" | chpasswd
RUN echo "hfeng   ALL=(ALL)       ALL" >> /etc/sudoers

RUN mkdir -p /var/run/sshd
RUN mkdir -p /var/log/supervisor

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 22 5001 5002 5003
CMD ["/usr/bin/supervisord"]
