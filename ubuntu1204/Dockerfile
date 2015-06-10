FROM ubuntu:12.04

MAINTAINER harrifeng "harrifeng@gmail.com"

# company  firewall
# ENV http_proxy http://proxy.sin.sap.corp:8080
# ENV https_proxy http://proxy.sin.sap.corp:8080
# For testcase
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV TZ US/Pacific

RUN sed -i 's/archive.ubuntu/mirrors.163/g'  /etc/apt/sources.list

RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive apt-get -y install \
      fonts-wqy-zenhei \
      fonts-inconsolata \
      g++ \
      supervisor \
      openssh-server \
      mysql-server \
      sudo \
      # default-jdk \
      # maven  \
      # golang \
      net-tools \
      iputils-ping \
      curl
      software-properties-common python-software-properties \
      build-essential \
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
      imagemagick \
      libmagick++-dev \
      openjdk-7-jre-headless \
      poppler-utils \
      phantomjs \
      opensaml2-tools \
      libicu-dev \
      unixodbc-dev \
      libffi-dev

RUN useradd -s /bin/bash -m hfeng
RUN echo "hfeng:hfeng" | chpasswd
RUN echo "root:wyyzmwy" | chpasswd
RUN echo "hfeng   ALL=(ALL)       ALL" >> /etc/sudoers

RUN echo "[supervisord]" >> /etc/supervisor/supervisord.conf && \
    echo "nodaemon=true" >> /etc/supervisor/supervisord.conf && \
    echo "" >> /etc/supervisor/supervisord.conf && \
    echo "[program:sshd]" >> /etc/supervisor/supervisord.conf && \
    echo "command=/etc/init.d/ssh start -D" >> /etc/supervisor/supervisord.conf && \
    echo "" >> /etc/supervisor/supervisord.conf && \
    echo "[program:mysql]" >> /etc/supervisor/supervisord.conf && \
    echo "command=/etc/init.d/mysql start -D" >> /etc/supervisor/supervisord.conf && \
    echo "" >> /etc/supervisor/supervisord.conf


# RUN git clone https://git.coding.net/harrifeng/emacs.d.git /home/hfeng/.emacs.d
# RUN chown -hR hfeng /home/hfeng/.emacs.d
# RUN chgrp -hR hfeng /home/hfeng/.emacs.d

EXPOSE 22
EXPOSE 3000
CMD ["/usr/bin/supervisord"]
