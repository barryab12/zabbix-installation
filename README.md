# zabbix-installation

## Install Zabbix 5.2 on ubuntu 18.04 using postgresql as DB and Nginx as webserver
- sudo apt update
- sudo apt upgrade -y
- wget https://repo.zabbix.com/zabbix/5.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.2-1+ubuntu18.04_all.deb
- dpkg -i zabbix-release_5.2-1+ubuntu18.04_all.deb
- apt update
- apt install zabbix-server-pgsql zabbix-frontend-php php7.2-pgsql zabbix-nginx-conf zabbix-agent postgresql
- sudo -u postgres createuser --pwprompt barry
- sudo -u postgres createdb -O zabbix zabbix
- zcat /usr/share/doc/zabbix-server-pgsql*/create.sql.gz | sudo -u zabbix psql zabbix
- nano /etc/zabbix/zabbix_server.conf
{
    DBPassword=password
    DBUser=zabbix
    DBHost=localhost
}
- nano /etc/zabbix/nginx.conf
{
    listen 8090;
    server_name 127.0.0.1;
}
- systemctl restart zabbix-server zabbix-agent nginx php7.2-fpm
- systemctl enable zabbix-server zabbix-agent nginx php7.2-fpm
