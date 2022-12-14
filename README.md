# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Zabbix установлен с WEB-сервером NGINX и БД PostgreSQL. Соответственно, чать инструкций по установке взята из лекции, а другая часть с официального сайта Zabbix.`

1. `Установка репозитория Zabbix:`
   `# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bdebian11_all.deb`
   `# dpkg -i zabbix-release_6.0-4+debian11_all.deb`
   `# apt update`
2. `Установка Zabbix сервера, веб-интерфейса и агента:`
   `# apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-agent`
3. `Создание пользователя с помощью psql из под root:`
   `su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'`
   `su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'`
4. `На хосте Zabbix сервера импортируем начальную схему и данные:`
   `zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`
5. `Задаём пароль в DBPassword:`
   `sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf`
6. `Редактируем файл /etc/zabbix/nginx.conf раскомментируем и настроим директивы 'listen' и 'server_name':`
   `# listen 8080;`
   `# server_name example.com;`
7. `Запустим процессы Zabbix сервера и агента и настроим их запуск при загрузке ОС:`
   `# systemctl restart zabbix-server zabbix-agent nginx php7.4-fpm`
   `# systemctl enable zabbix-server zabbix-agent nginx php7.4-fpm`



![Установленный Zabbix](img/9.2-01.png)


---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Установка репозитория Zabbix:`
   `# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bdebian11_all.deb`
   `# dpkg -i zabbix-release_6.0-4+debian11_all.deb`
   `# apt update`
2. `Установка Zabbix агента`
   `# apt install zabbix-agent`
3. `Запустим процессы Zabbix сервера и агента и настроим их запуск при загрузке ОС:`
   `# systemctl restart zabbix-agent`
   `# systemctl enable zabbix-agent`



![Агенты подключены к серверу](img/9.2-02.png)
![Zabbix agent работает с сервером](img/9.2-04.png)
![Monitoring > Latest data для обоих хостов](img/9.2-05.png)


