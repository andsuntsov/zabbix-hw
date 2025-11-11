# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Сунцов Андрей`


### Задание 1

```

sudo apt -y install postgresql postgresql-contrib
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest+ubuntu24.04_all.deb
sudo dpkg -i zabbix-release_latest+ubuntu24.04_all.deb
sudo apt -y install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
sudo ufw allow 80/tcp
sudo ufw allow 10050/tcp
sudo ufw allow 10051/tcp

```

![скриншот авторизации в админке](https://github.com/andsuntsov/zabbix-hw/blob/main/img/auth-zabbix.png)

---

### Задание 2


```

sudo apt -y install zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
sudo ufw allow 10050/tcp

```

![скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу](https://github.com/andsuntsov/zabbix-hw/blob/main/img/hosts-status.png)

![скриншот лога zabbix agent, где видно, что он работает с сервером](https://github.com/andsuntsov/zabbix-hw/blob/main/img/agent-log.png)

![скриншот раздела Monitoring > Latest data для zbx-server](https://github.com/andsuntsov/zabbix-hw/blob/main/img/latest-data-zbx-server.png)

![скриншот раздела Monitoring > Latest data для zbx-agent-2](https://github.com/andsuntsov/zabbix-hw/blob/main/img/latest-data-zbx-agent-2.png)