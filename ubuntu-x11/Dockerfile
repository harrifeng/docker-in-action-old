FROM ubuntu:15.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN sed -i 's/archive.ubuntu/mirrors.163/g'  /etc/apt/sources.list

RUN apt-get update

# /etc/sudoers is needed this
RUN apt-get install -y sudo

RUN useradd -m hfeng
RUN echo "hfeng:hfeng" | chpasswd
RUN echo "hfeng   ALL=(ALL)       ALL" >> /etc/sudoers


RUN apt-get install -y x-window-system
RUN apt-get install -y xfce4

RUN apt-get install -y openssh-server
RUN /etc/init.d/ssh restart
