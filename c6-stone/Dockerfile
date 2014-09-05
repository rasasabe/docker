FROM centos:centos6

MAINTAINER rasasabe@users.noreply.github.com <http://dba-ha.blogspot.jp/2014/08/stone-rpm.html>

ENV http_proxy http://proxyuser:proxypasswd@proxyserver:port

# perl -MMIME::Base64 -e "print encode_base64('proxyuser:proxypasswd');"
ENV CREDENTIAL_MIME_BASE64 cHJveHl1c2VyOnByb3h5cGFzc3dk
ENV PROXY_SERVER proxyuser:proxypasswd@proxyserver:port

RUN yum update -y
RUN yum install -y cpp

ADD stone-2.3e-2.3.3.17.el6.x86_64.rpm /tmp/stone-2.3e-2.3.3.17.el6.x86_64.rpm
RUN rpm -ihv /tmp/stone-2.3e-2.3.3.17.el6.x86_64.rpm

RUN openssl req -new -outform pem -out /tmp/stone.cert -newkey rsa:1024 -keyout /tmp/stone.key -nodes -rand ./rand.pat -x509 -batch -days 36500
RUN touch /etc/pki/tls/certs/stone.pem
RUN chmod 400 /etc/pki/tls/certs/stone.pem
RUN cat /tmp/stone.cert /tmp/stone.key | tee /etc/pki/tls/certs/stone.pem > /dev/null
RUN rm -f stone.cert stone.key

#RUN echo "localhost:22 443/ssl" | tee /etc/stone.conf
RUN  echo "${PROXY_SERVER}/proxy 8080 'Proxy-Authorization: Basic ${CREDENTIAL_MIME_BASE64}'" | tee /etc/stone.conf

# execute
#EXPOSE 443
EXPOSE  8080
CMD /usr/bin/stone -ddd -C /etc/stone.conf
