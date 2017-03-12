
# CentOS6を入れる
FROM centos:6

# タイムゾーンをJSTにする。
RUN \cp -f /usr/share/zoneinfo/Japan /etc/localtime && echo -e 'ZONE="Asia/Tokyo"\nUTC=false' > /etc/sysconfig/clock

# PHP5.3、Apacheもろもろインストール
RUN yum clean all && yum -y update && yum -y install httpd php libmcrypt

# PHP5.3の拡張インストール
RUN yum -y install php-gd php-mysqlnd php-pgsql php-mbstring php-xml php-mcrypt php-zip

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
