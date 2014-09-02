FROM kitamura/c6-spv-ssh

MAINTAINER rasasabe@users.noreply.github.com

<<<<<<< Updated upstream
# EPEL
RUN yum install -y --nogpgcheck http://dl.iuscommunity.org/pub/ius/stable/Redhat/6/x86_64/epel-release-6-5.noarch.rpm
RUN yum update -y
RUN yum install -y --nogpgcheck wget

# SSH
RUN yum install -y --nogpgcheck openssh-server sudo
RUN ssh-keygen -t rsa -f -N '' /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f -N '' /etc/ssh/ssh_host_dsa_key
RUN sed -i 's/UsePAM.*/UsePAM no/g' /etc/ssh/sshd_config
RUN useradd ssh-user && echo 'ssh-user:ssh-user' | chpasswd
RUN echo 'ssh-user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
=======
ENV http_proxy http://z1000008:teletran1@proxy.senri.ogis-ri.co.jp:8080
ENV https_proxy http://z1000008:teletran1@proxy.senri.ogis-ri.co.jp:8080
>>>>>>> Stashed changes

# Subversion
RUN wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.i686.rpm
RUN rpm -ivh rpmforge-release-0.5.3-1.el6.rf.i686.rpm
RUN yum install -y --enablerepo=rpmforge-extras subversion
RUN useradd svn && echo 'svn:svn' | chpasswd

# setting Subversion
USER svn
RUN mkdir -p /home/svn/repos
RUN svnadmin create /home/svn/repos
RUN echo -ne '[general]\nanon-access=none\nauth-access=write\npassword-db=passwd\n' >> /home/svn/repos/conf/svnserve.conf
RUN echo -ne '[users]\nkitamura=kitamura\n' >> /home/svn/repos/conf/passwd

# execute
USER root
EXPOSE 22 3690
CMD ["/usr/bin/supervisord"]
