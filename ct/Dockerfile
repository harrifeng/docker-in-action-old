FROM ruby:2.1

MAINTAINER Haoran Feng

RUN curl -O http://www.javascriptlint.com/download/jsl-0.3.0-src.tar.gz && \
  tar -zxvf jsl-0.3.0-src.tar.gz && \
  cd jsl-0.3.0/src && \
  make -f Makefile.ref BUILD_OPT=1 && \
  cp Linux_All_OPT.OBJ/jsl /usr/local/bin && \
  cd - && \
  rm -r jsl-0.3.0 jsl-0.3.0-src.tar.gz

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV TZ US/Pacific

ENV http_proxy http://proxy.wdf.sap.corp:8080
ENV https_proxy http://proxy.wdf.sap.corp:8080
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
       software-properties-common python-software-properties
RUN add-apt-repository ppa:jon-severinsson/ffmpeg
RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive apt-get -y install \
      ffmpeg \
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
      imagemagick \
      libmagick++-dev \
      openjdk-7-jre-headless \
      poppler-utils \
      phantomjs \
      opensaml2-tools \
      libicu-dev \
      unixodbc-dev \
      libffi-dev

ENV APP_HOME /myapp
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD Gemfile* $APP_HOME/
RUN bundle install

ADD . $APP_HOME
