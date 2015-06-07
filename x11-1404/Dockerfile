FROM ubuntu:14.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN sed -i 's/archive.ubuntu/mirrors.163/g'  /etc/apt/sources.list

RUN apt-get update

# X-windows support, may not needed any more
# RUN apt-get install -y x-window-system xfce4

# Font inconsolata
RUN apt-get install -y fonts-wqy-zenhei fonts-inconsolata

# language suport
RUN apt-get install -y g++ default-jdk maven

# Network utility
RUN apt-get install -y net-tools iputils-ping curl

RUN apt-get install -y emacs24

RUN apt-get install -y openssh-server

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
       software-properties-common python-software-properties
RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive apt-get -y install \
      build-essential \
      curl \
      git-core \
      libcurl4-openssl-dev \
      libreadline-dev \
      libssl-dev \
      libxml2-dev \
      libxslt1-dev \
      libyaml-dev \
      p7zip-full \
      zlib1g-dev \
      libmysqlclient-dev \
      mysql-client \
      mysql-server \
      imagemagick \
      libmagick++-dev \
      openjdk-7-jre-headless \
      poppler-utils \
      phantomjs \
      opensaml2-tools \
      libicu-dev \
      unixodbc-dev \
      libffi-dev

RUN curl -O http://192.168.59.3:8000/jsl-0.3.0-src.tar.gz && \
  tar -zxvf jsl-0.3.0-src.tar.gz && \
  cd jsl-0.3.0/src && \
  make -f Makefile.ref BUILD_OPT=1 && \
  cp Linux_All_OPT.OBJ/jsl /usr/local/bin && \
  cd - && \
  rm -r jsl-0.3.0 jsl-0.3.0-src.tar.gz

# Add user

# /etc/sudoers is needed this
RUN apt-get install -y sudo

RUN useradd -s /bin/bash -m hfeng
RUN echo "hfeng:hfeng" | chpasswd
RUN echo "hfeng   ALL=(ALL)       ALL" >> /etc/sudoers

RUN git clone https://git.coding.net/harrifeng/emacs.d.git /home/hfeng/.emacs.d
RUN chown -hR hfeng /home/hfeng/.emacs.d
RUN chgrp -hR hfeng /home/hfeng/.emacs.d

EXPOSE 22
CMD ["/etc/init.d/ssh", "start", "-D"]
