
# CentOS7������
FROM centos:7

# �^�C���]�[����JST�ɂ���B
RUN \cp -f /usr/share/zoneinfo/Japan /etc/localtime && echo -e 'ZONE="Asia/Tokyo"\nUTC=false' > /etc/sysconfig/clock

# PHP7.0�����邽�߂Ƀ��|�W�g�����C���X�g�[��
RUN rpm -ivh http://ftp-srv2.kddilabs.jp/Linux/distributions/fedora/epel/7/x86_64/e/epel-release-7-9.noarch.rpm
RUN rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

# PHP7.0�AApache�������C���X�g�[��
RUN yum clean all && yum -y update && yum -y install httpd php libmcrypt --enablerepo=remi-php70

# PHP7.0�̊g���C���X�g�[��
RUN yum -y install php-gd php-mysqlnd php-pgsql php-mbstring php-xml php-mcrypt php-zip php-opcache --enablerepo=remi-php70

# Composer�C���X�g�[��
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer 

# Apache�̕s�v�t�@�C������
RUN \rm -f /etc/httpd/conf.d/README && \rm -f /etc/httpd/conf/d/welcome.conf

# PHP.INI�̐ݒ���R�s�[
COPY ./php/php.ini /etc/php.ini
# opcache�̐ݒ���R�s�[
COPY ./php/10-opcache.ini /etc/php.d/10-opcache.ini

# Apache�̃o�[�`�����z�X�g�ݒ���R�s�[
COPY ./apahce/virtual.conf /etc/httpd/conf.d/virtual.conf

# Apache���O�o�͐�쐬
RUN mkdir /var/log/httpd/php


# �|�[�g80���O�����J
EXPOSE 80
# Apache���t�H�A�O���E���h�Ŏ��s
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]