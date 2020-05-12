FROM centos
RUN yum install httpd -y
COPY weppage/  /var/www/html/
EXPOSE 80
CMD /usr/sbin/httpd -DEFORGROUND

