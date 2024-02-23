# IWNO3: Использование контейнеров как среды выполнения

- [IWNO3: Использование контейнеров как среды выполнения](#iwno3-использование-контейнеров-как-среды-выполнения)
  - [Цель работы](#цель-работы)
  - [Задание](#задание)
  - [Описание выполнения работы](#описание-выполнения-работы)
  - [Выводы](#выводы)

## Цель работы
Данная лабораторная работа призвана напомнить основные команды ОС Debian/Ubuntu. Также она позволит познакомиться с Docker и его основными командами.
## Задание
Запустить контейнер Ubuntu, установить Web-сервер Apache и вывести в браузере страницу с текстом "Hello, World!".
## Описание выполнения работы

Откройте терминал в папке containers03 и выполните команду:
```
docker run -ti -p 8000:80 --name containers03 ubuntu bash
```

В открывшемся окне выполните следующие команды и объясните их назначение:

```
apt update
apt install apache2 -y
service apache2 start
```

`apt update`: Эта команда используется для обновления списка доступных пакетов с удаленных репозиториев. 

`apt install apache2 -y`: Эта команда используется для установки пакета Apache HTTP Server с помощью менеджера пакетов APT. Флаг -y указывает, что ответ на все вопросы о подтверждении установки должен быть автоматически "да".

`service apache2 start`: После установки Apache необходимо запустить его службу, чтобы веб-сервер начал прослушивать запросы и обслуживать их. Эта команда запускает службу Apache.

Откройте браузер и введите в адресной строке http://localhost:8000. Что вы видите?

![image](https://github.com/S1ngle777/containers03/assets/128795707/6e03846b-acb7-45b1-82e1-e87bf7595db7)


Выполните следующие команды:
```
ls -l /var/www/html/
echo "<h1>Hello, World</h1>" > /var/www/html/index.html
```

![image](https://github.com/S1ngle777/containers03/assets/128795707/12a3058b-9877-4eeb-9f17-bfe09ba597f7)


Обновите страницу в браузере. Что вы видите?

![image](https://github.com/S1ngle777/containers03/assets/128795707/64440925-4314-4d59-87b0-71d323a206ed)


Выполните следующие команды:
```
cd /etc/apache2/sites-enabled/
cat 000-default.conf
```
Что вы видите на экране?

```
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

Закройте окно терминала командой exit.

Просмотрите список контейнеров:
```
docker ps -a
```
![image](https://github.com/S1ngle777/containers03/assets/128795707/e947c6a8-ab96-4475-8ee3-b3f905e44264)


Удалите контейнер:
```
docker rm containers03
```

![image](https://github.com/S1ngle777/containers03/assets/128795707/fcbf971c-34a9-41f7-84d7-15976c1d9dc9)

## Выводы

Из данной работы можно сделать следующие выводы:

1. Освоены основные команды ОС Debian/Ubuntu, такие как apt update для обновления списка доступных пакетов и apt install для установки пакетов.
2. Получен опыт работы с Docker и его основными командами. В частности, была выполнена команда docker run для запуска контейнера.
3. Установлен и настроен веб-сервер Apache внутри контейнера Ubuntu.
4. Была создана простая веб-страница с текстом "Hello, World!", которая была доступна через браузер.
5. Изучена структура файла конфигурации Apache 000-default.conf, который определяет настройки виртуального хоста по умолчанию.
6. Был выполнен вывод списка контейнеров и удаление созданного контейнера с помощью команды docker rm.
