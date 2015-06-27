FROM ubuntu:15.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN rm /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list

RUN apt-get update && \
      supervisor \
      openssh-server \
      mysql-server

RUN useradd -s /bin/bash -m hfeng
RUN echo "hfeng:hfeng" | chpasswd
RUN echo "root:wyyzmwy" | chpasswd
RUN echo "hfeng   ALL=(ALL)       ALL" >> /etc/sudoers

RUN mkdir -p /var/run/sshd
RUN mkdir -p /var/log/supervisor

VOLUME ["/var/lib/mysql"]

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 22 3000
CMD ["/usr/bin/supervisord"]
