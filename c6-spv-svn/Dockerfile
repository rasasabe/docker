FROM kitamura/c6-spv-ssh

MAINTAINER rasasabe@users.noreply.github.com

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
