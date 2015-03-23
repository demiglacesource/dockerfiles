FROM centos:centos7
MAINTAINER demiglacesource <demiglacesource@gmail.com>

ENV NODE_VERSION 0.12.0
ENV SITE_NAME mysite

RUN yum update -y
RUN yum install -y \
  tar \
  openssh-server \
  git \
  vim \
  wget \
  telnet \
  tcpdump
RUN yum clean all

RUN mkdir /var/run/sshd
ENTRYPOINT /usr/sbin/sshd -D

RUN echo 'root:p@ssw0rd' | chpasswd
RUN sed -ri 's/^#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key

ADD https://raw.githubusercontent.com/creationix/nvm/v0.23.3/install.sh .
RUN bash install.sh
RUN source /root/.bashrc && nvm install v$NODE_VERSION
ENV PATH /root/.nvm/versions/node/v$NODE_VERSION/bin:$PATH

RUN npm install gulp -g
RUN npm install bower -g
RUN npm install express-generator@4.12.1 -g

RUN express /opt/$SITE_NAME -f --git -e
RUN cd /opt/$SITE_NAME && npm install

RUN touch /opt/$SITE_NAME/glupfile.js
RUN cd /opt/$SITE_NAME && npm install --save-dev gulp gulp-bower gulp-imagemin gulp-uglify

EXPOSE 22
EXPOSE 3000

