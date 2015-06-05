FROM ubuntu:14.04
MAINTAINER Haoran Feng

RUN sed -i 's/archive.ubuntu/mirrors.163/g'  /etc/apt/sources.list

# company  firewall
# ENV http_proxy http://proxy.wdf.sap.corp:8080
# ENV https_proxy http://proxy.wdf.sap.corp:8080
# For testcase
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV TZ US/Pacific

# In order to connect mysql container
RUN echo 'export DB_PWD=$MYSQL_ENV_MYSQL_ROOT_PASSWORD' >> /root/.bashrc
RUN echo 'export DB_HOST=$MYSQL_PORT_3306_TCP_ADDR' >> /root/.bashrc

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
      imagemagick \
      libmagick++-dev \
      openjdk-7-jre-headless \
      poppler-utils \
      phantomjs \
      opensaml2-tools \
      libicu-dev \
      unixodbc-dev \
      libffi-dev
RUN curl -O http://192.168.59.3:8000/ruby-2.1.5.tar.gz && \
  tar -zxvf ruby-2.1.5.tar.gz && \
  cd ruby-2.1.5 && \
  CFLAGS="-march=native -O3" ./configure --disable-install-doc && \
  CFLAGS="-march=native -O3" make -j 9 && \
  make install && \
  cd .. && \
  rm -r ruby-2.1.5 ruby-2.1.5.tar.gz && \
  echo 'install: --no-rdoc --no-ri' > /.gemrc && \
  echo 'update: --no-rdoc --no-ri' >> /.gemrc
RUN curl -O http://192.168.59.3:8000/jsl-0.3.0-src.tar.gz && \
  tar -zxvf jsl-0.3.0-src.tar.gz && \
  cd jsl-0.3.0/src && \
  make -f Makefile.ref BUILD_OPT=1 && \
  cp Linux_All_OPT.OBJ/jsl /usr/local/bin && \
  cd - && \
  rm -r jsl-0.3.0 jsl-0.3.0-src.tar.gz
# RUN gem install bundler -v '1.6.0'

EXPOSE 3000
