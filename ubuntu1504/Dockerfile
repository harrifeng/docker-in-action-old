FROM ubuntu:15.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN rm /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list

RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive apt-get -y install \
      emacs24 \
      supervisor \
      openssh-server \
      mysql-server \
      default-jdk \
      sudo \
      net-tools \
      golang \
      git-core \
      g++
      # maven  \
      # iputils-ping \
      # curl \
      # vim \
      # dos2unix \
      # software-properties-common python-software-properties \
      # build-essential \
      # libcurl4-openssl-dev \
      # libreadline-dev \
      # libssl-dev \
      # libxml2-dev \
      # libxslt1-dev \
      # libyaml-dev \
      # p7zip-full \
      # zlib1g-dev \
      # libmysqlclient-dev \
      # mysql-client \
      # imagemagick \
      # libmagick++-dev \
      # poppler-utils \
      # opensaml2-tools \
      # libicu-dev \
      # unixodbc-dev \
      # libffi-dev \
      # ffmpeg  \
      # openjdk-7-jre-headless
      # phantomjs

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
