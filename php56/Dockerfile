
# CentOS6を入れる
FROM centos:6

# タイムゾーンをJSTにする。
RUN \cp -f /usr/share/zoneinfo/Japan /etc/localtime && echo -e 'ZONE="Asia/Tokyo"\nUTC=false' > /etc/sysconfig/clock

# PHP5.4を入れるためにリポジトリをインストール
RUN rpm -ivh http://ftp.iij.ad.jp/pub/linux/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

# PHP5.6、Apacheもろもろインストール
RUN yum clean all && yum -y update && yum -y install httpd php libmcrypt --enablerepo=remi-php56

# PHP5.6の拡張インストール
RUN yum -y install php-gd php-mysqlnd php-pgsql php-mbstring php-xml php-mcrypt php-zip --enablerepo=remi-php56

# Composerインストール
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer 

# Apacheの不要ファイル除去
RUN \rm -f /etc/httpd/conf.d/README && \rm -f /etc/httpd/conf/d/welcome.conf

# PHP.INIの設定をコピー
COPY ./php/php.ini /etc/php.ini

# Apacheのバーチャルホスト設定をコピー
COPY ./apahce/virtual.conf /etc/httpd/conf.d/virtual.conf

# Apacheログ出力先作成
RUN mkdir /var/log/httpd/php


# ポート80を外部公開
EXPOSE 80
# Apacheをフォアグラウンドで実行
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
