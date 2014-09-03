FROM kitamura/c6-spv-ssh

MAINTAINER rasasabe@users.noreply.github.com

# init
ENV http_proxy=http://z1000008:teletran1@proxy.senri.ogis-ri.co.jp:8080
RUN yum install -y --nogpgcheck wget

# Subversion
RUN wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.i686.rpm
RUN rpm -ivh rpmforge-release-0.5.3-1.el6.rf.i686.rpm
RUN yum install -y --nogpgcheck --enablerepo=rpmforge-extras subversion
RUN useradd svn && echo 'svn:svn' | chpasswd

# configuration
ADD supervisord.conf /etc/supervisord.conf

# execute
EXPOSE 22 3690
CMD ["/usr/bin/supervisord"]
