FROM centos:centos7
MAINTAINER demiglacesource <demiglacesource@gmail.com>

ADD ./MariaDB.repo /etc/yum.repos.d/

RUN yum update -y
RUN yum install -y \
  tar \
  openssh-server \
  git \
  vim \
  wget \
  telnet \
  tcpdump \
  MariaDB-server-10.0.16-1.el7.centos \
  MariaDB-client-10.0.16-1.el7.centos

RUN mkdir /var/run/sshd
ENTRYPOINT /usr/sbin/sshd -D

RUN echo 'root:p@ssw0rd' | chpasswd
RUN sed -ri 's/^#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key

ADD https://raw.githubusercontent.com/creationix/nvm/v0.23.3/install.sh .
RUN bash install.sh
RUN source /root/.bashrc && nvm install v0.12.0
ENV PATH /root/.nvm/versions/node/v0.12.0/bin:$PATH

EXPOSE 22
EXPOSE 3000
EXPOSE 3306

