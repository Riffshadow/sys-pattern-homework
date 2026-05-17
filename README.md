# Домашнее задание к занятию "Система мониторинга Zabbix"

## Выполнил
Чернобровкин Иван

---

# Задание 1

## Установка Zabbix Server с PostgreSQL

Был установлен и настроен Zabbix Server с PostgreSQL и веб-интерфейсом.

---

## Установка необходимых пакетов

```bash
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent php-pgsql
```

---

## Запуск PostgreSQL

```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

---

## Создание базы данных

```bash
sudo -u postgres createdb zabbix -O zabbix
```

---

## Импорт схемы базы данных

```bash
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | psql -U zabbix -d zabbix
```

---

## Перезапуск сервисов

```bash
sudo systemctl restart zabbix-server apache2
```

---

## Проверка статуса

```bash
systemctl status zabbix-server
systemctl status apache2
systemctl status postgresql
```

---

## Подключение к базе

```bash
psql -h localhost -U zabbix -d zabbix
```

---

# Задание 2

## Установка и настройка Zabbix Agent

На хосте Practica установлен Zabbix Agent и настроено подключение к серверу Zabbix.

---

## Установка агента

```bash
sudo apt install zabbix-agent -y
```

---

## Настройка конфигурации

Отредактирован файл:

```bash
sudo nano /etc/zabbix/zabbix_agentd.conf
```

Указаны параметры:
- Server = IP Zabbix Server
- ServerActive = IP Zabbix Server

---

## Перезапуск агента

```bash
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
```

---

## Проверка статуса

```bash
sudo systemctl status zabbix-agent
```

---

## Проверка порта

```bash
sudo ss -tlnp | grep 10050
```

---

# Скриншоты

## Задание 1

### Установка Zabbix Server
![Install](https://github.com/Riffshadow/sys-pattern-homework/blob/main/1.1.png)

### База данных
![DB](https://github.com/Riffshadow/sys-pattern-homework/blob/main/1.2.png)

---

## Задание 2

### Agent status
![Agent](https://github.com/Riffshadow/sys-pattern-homework/blob/main/2.1.png)

### Latest data
![Data](https://github.com/Riffshadow/sys-pattern-homework/blob/main/2.2.png)

### Hosts
![Hosts](https://github.com/Riffshadow/sys-pattern-homework/blob/main/2.3.png)
