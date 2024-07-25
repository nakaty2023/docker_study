FROM debian:latest

#　環境変数の設定
ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=database
ENV MYSQL_USER=user
ENV MYSQL_PASSWORD=password

# 必要パッケージとmysqlのインストール
RUN apt-get update && apt-get install -y \
    gnupg \
    lsb-release \
    wget && \
    apt-get install -y mysql-server

# mysqlの設定ファイルをコピー
COPY my.cnf /etc/mysql/my.cnf

# 初期化スクリプトをコピー
COPY init.sql /docker-entrypoint-initdb.d/

# mysqlのポートを開放
EXPOSE 3306

# mysqlの起動
CMD ["mysqld"]