FROM ubuntu:15.04

MAINTAINER harrifeng "harrifeng@gmail.com"

RUN apt-get install -y openssh-server sudo
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config


RUN useradd admin
RUN echo "admin:admin" | chpasswd
RUN echo "admin   ALL=(ALL)       ALL" >> /etc/sudoers

RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

RUN mkdir /var/run/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
