FROM ubuntu:15.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN sed -i 's/archive.ubuntu/mirrors.163/g'  /etc/apt/sources.list

RUN apt-get update

# /etc/sudoers is needed this
RUN apt-get install -y sudo

RUN useradd -s /bin/bash -m hfeng
RUN echo "hfeng:hfeng" | chpasswd
RUN echo "hfeng   ALL=(ALL)       ALL" >> /etc/sudoers

# X-windows support
RUN apt-get install -y x-window-system xfce4

RUN apt-get install -y git
RUN git clone https://github.com/harrifeng/.emacs.d.git /home/hfeng/.emacs.d
RUN chown -hR hfeng /home/hfeng/.emacs.d
RUN chgrp -hR hfeng /home/hfeng/.emacs.d

# language suport
RUN apt-get install -y g++ default-jdk maven

# Network utility
RUN apt-get install -y net-tools iputils-ping curl

RUN apt-get install -y emacs24

RUN apt-get install -y openssh-server
EXPOSE 22
CMD ["/etc/init.d/ssh", "start", "-D"]
