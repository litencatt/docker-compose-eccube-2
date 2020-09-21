FROM centos:7

RUN yum update -y
RUN yum install -y sudo
RUN yum install -y epel-release
RUN yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
RUN yum clean all
RUN yum -y install wget
RUN yum -y install httpd
RUN yum -y install --enablerepo=remi,remi-php73 php php-devel php-mbstring php-pdo php-gd php-xml php-mcrypt php-mysqli

RUN wget https://github.com/EC-CUBE/ec-cube2/releases/download/eccube-2.17.1/eccube-2.17.1.tar.gz
RUN tar zxvf eccube-2.17.1.tar.gz

RUN mv /ec-cube2/ /var/www/html/ec-cube \
    && chown -R apache:apache /var/www/html/ec-cube

RUN sed -i \
    -e 's#DocumentRoot "/var/www/html"#DocumentRoot "/var/www/html/ec-cube/html"#g' \
    -e 's#<Directory "/var/www/html">#<Directory /var/www/html/ec-cube/html">#g' \
    -e 's#Options Indexes FollowSymLinks#Options -Indexes +FollowSymLinks#g' \
    -e 's#AllowOverride None#AllowOverride All#g' \
    /etc/httpd/conf/httpd.conf

#RUN rm -rf ec-cube2
#RUN rm -rf eccube-2.17.1.tar.gz

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
EXPOSE 80
