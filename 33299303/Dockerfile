FROM ubuntu:14.04

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
#RUN groupadd -r mysql && useradd -r -g mysql mysql

# FATAL ERROR: please install the following Perl modules before executing /usr/local/mysql/scripts/mysql_install_db:
# File::Basename
# File::Copy
# Sys::Hostname
# Data::Dumper
#RUN apt-get update && apt-get install -y perl --no-install-recommends && rm -rf /var/lib/apt/lists/*

#http://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/
RUN apt-get install -y mysql-server-5.5

# gpg: key 5072E1F5: public key "MySQL Release Engineering <mysql-build@oss.oracle.com>" imported
#RUN apt-key adv --keyserver pool.sks-keyservers.net --recv-keys A4A9406876FCBD3C456770C88C718D3B5072E1F5

#ENV MYSQL_MAJOR 5.6
#ENV MYSQL_VERSION 5.6.24

#RUN echo "deb http://repo.mysql.com/apt/debian/ wheezy mysql-${MYSQL_MAJOR}" > /etc/apt/sources.list.d/mysql.list

# the "/var/lib/mysql" stuff here is because the mysql-server postinst doesn't have an explicit way to disable the mysql_install_db codepath besides having a database already "configured" (ie, stuff in /var/lib/mysql/mysql)
# also, we set debconf keys to make APT a little quieter
#RUN { \
#        echo mysql-community-server mysql-community-server/data-dir select ''; \
#        echo mysql-community-server mysql-community-server/root-pass password ''; \
#        echo mysql-community-server mysql-community-server/re-root-pass password ''; \
#        echo mysql-community-server mysql-community-server/remove-test-db select false; \
#    } | debconf-set-selections \
#    && apt-get update && apt-get install -y mysql-server="${MYSQL_VERSION}"* && rm -rf /var/lib/apt/lists/* \
#    && rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql

#RUN apt-get update && apt-get install -y procps

# comment out a few problematic configuration values
#RUN sed -Ei 's/^(bind-address|log)/#&/' /etc/mysql/my.cnf

# VOLUME /var/lib/mysql
# Install database
#ADD ./database.sql /var/db/database.sql

# Set Standard settings
#ENV user student
#ENV password secret
#ENV url file:/var/db/database.sql
#ENV right READ

# Install starting script
#ADD ./start-database.sh /usr/local/bin/start-database.sh
#RUN chmod +x /usr/local/bin/start-database.sh

#EXPOSE 3306

#RUN mysql_install_db --user=mysql --basedir=/usr/ --ldata=/var/lib/mysql/

CMD service mysql start