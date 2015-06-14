FROM debian:6.0.10

MAINTAINER harrifeng "harrifeng@gmail.com"

# company  firewall
##################################################
# ENV http_proxy http://proxy.sha.sap.corp:8080  #
# ENV https_proxy http://proxy.sha.sap.corp:8080 #
##################################################
# For testcase
# ENV TZ US/Pacific

RUN rm /etc/apt/sources.list
COPY sources.list /etc/apt/sources.list

RUN apt-get update && \
      DEBIAN_FRONTEND=noninteractive apt-get -y install \
      libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev build-essential \
      unixodbc-dev libxslt1-dev libmysqlclient-dev imagemagick libmagickwand-dev libicu44 libicu-dev \
      supervisor \
      openssh-server \
      mysql-server \
      sudo
      # default-jdk \
      # maven  \
      # golang \
      # net-tools \
      # iputils-ping \
      # curl \
      # vim \
      # dos2unix \
      # software-properties-common python-software-properties \
      # build-essential \
      # git-core \
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
# RUN mkdir -p /var/run/mysqld
RUN mkdir -p /var/log/supervisor

VOLUME ["/var/lib/mysql"]

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN curl -O http://localhost:8000/ruby-2.1.5.tar.gz && \
  tar -zxvf ruby-2.1.5.tar.gz && \
  cd ruby-2.1.5 && \
  CFLAGS="-march=native -O3" ./configure --disable-install-doc && \
  CFLAGS="-march=native -O3" make -j 9 && \
  make install && \
  cd .. && \
  rm -r ruby-2.1.5 ruby-2.1.5.tar.gz && \
  echo 'install: --no-rdoc --no-ri' > /.gemrc && \
  echo 'update: --no-rdoc --no-ri' >> /.gemrc
RUN curl -O http://localhost:8000/jsl-0.3.0-src.tar.gz && \
  tar -zxvf jsl-0.3.0-src.tar.gz && \
  cd jsl-0.3.0/src && \
  make -f Makefile.ref BUILD_OPT=1 && \
  cp Linux_All_OPT.OBJ/jsl /usr/local/bin && \
  cd - && \
  rm -r jsl-0.3.0 jsl-0.3.0-src.tar.gz


RUN echo "export http_proxy='http://proxy.sin.sap.corp:8080'" >> /home/hfeng/.bashrc
RUN echo "export https_proxy='http://proxy.sin.sap.corp:8080'" >> /home/hfeng/.bashrc
RUN gem source -r https://rubygems.org/
RUN gem source -a http://ruby.taobao.org/
RUN gem install bundler -v '1.6.0'
#
# RUN apt-get install -y ffmpeg

EXPOSE 22 3000
CMD ["/usr/bin/supervisord"]
