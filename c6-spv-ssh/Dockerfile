FROM centos:centos6

MAINTAINER rasasabe@users.noreply.github.com

# EPEL
RUN yum install -y --nogpgcheck http://dl.iuscommunity.org/pub/ius/stable/Redhat/6/x86_64/epel-release-6-5.noarch.rpm
RUN yum update -y

# ssh
RUN yum install -y --nogpgcheck openssh-server sudo
RUN ssh-keygen -t rsa -f -N /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f -N /etc/ssh/ssh_host_dsa_key
RUN sed -i 's/UsePAM.*/UsePAM no/g' /etc/ssh/sshd_config
RUN useradd ssh-user && echo 'ssh-user:ssh-user' | chpasswd
RUN echo 'ssh-user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Supervisor
RUN yum install -y --nogpgcheck supervisor
ADD supervisord.conf /etc/supervisord.conf
RUN mkdir -p /var/log/supervisor

# execute
EXPOSE 22

CMD ["/usr/bin/supervisord"]
