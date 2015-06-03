FROM ubuntu:15.04
MAINTAINER Haoran Feng
# company  firewall
ENV http_proxy http://proxy.wdf.sap.corp:8080
ENV https_proxy http://proxy.wdf.sap.corp:8080
# For testcase
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV TZ US/Pacific

# In order to connect mysql container
echo 'export DB_PWD=$MYSQL_ENV_MYSQL_ROOT_PASSWORD' >> /root/.bashrc
echo 'export DB_HOST=$MYSQL_PORT_3306_TCP_ADDR' >> /root/.bashrc

RUN gem install bundler

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
       software-properties-common python-software-properties
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
RUN curl -O http://ftp.ruby-lang.org/pub/ruby/ruby-2.1.5.tar.gz && \
  tar -zxvf ruby-2.1.5.tar.gz && \
  cd ruby-2.1.5 && \
  CFLAGS="-march=native -O3" ./configure --disable-install-doc && \
  CFLAGS="-march=native -O3" make -j 9 && \
  make install && \
  cd .. && \
  rm -r ruby-2.1.5 ruby-2.1.5.tar.gz && \
  echo 'install: --no-rdoc --no-ri' > /.gemrc && \
  echo 'update: --no-rdoc --no-ri' >> /.gemrc
RUN curl -O http://www.javascriptlint.com/download/jsl-0.3.0-src.tar.gz && \
  tar -zxvf jsl-0.3.0-src.tar.gz && \
  cd jsl-0.3.0/src && \
  make -f Makefile.ref BUILD_OPT=1 && \
  cp Linux_All_OPT.OBJ/jsl /usr/local/bin && \
  cd - && \
  rm -r jsl-0.3.0 jsl-0.3.0-src.tar.gz
