
# RecruterService - Вдохновляйтесь и создавайте свою вакансию, находите своего идеального кандидата, делясь возможностями с миром трудоустройства!

***

#### Ссылка на проект: [tracker-hiring.ddns.net](https://tracker-hiring.ddns.net)

***

## Технологии:

[![Python](https://img.shields.io/badge/Python-%203.10-blue?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-%203.2.18-blue?style=flat-square&logo=django)](https://www.djangoproject.com/)
[![DRF](https://img.shields.io/badge/DjangoRESTFramework-%203.14.0-blue?style=flat-square&logo=django)](https://www.django-rest-framework.org/)
[![Celery](https://img.shields.io/badge/Celery-%205.2.7-blue?style=flat-square&logo=celery)](https://docs.celeryq.dev/en/stable/)
[![Redis](https://img.shields.io/badge/Redis-%205.0.0-blue?style=flat-square&logo=redis)](https://redis.io/)
[![Swagger](https://img.shields.io/badge/Swagger-%201.21.7-blue?style=flat-square&logo=swagger)](https://swagger.io/)
[![Docker](https://img.shields.io/badge/Docker-%2024.0.5-blue?style=flat-square&logo=docker)](https://www.docker.com/)
[![DockerCompose](https://img.shields.io/badge/Docker_Compose-%202.21.0-blue?style=flat-square&logo=docsdotrs)](https://docs.docker.com/compose/)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-%20-blue?style=flat-square&logo=githubactions)](https://github.com/features/actions)
[![Gunicorn](https://img.shields.io/badge/Gunicorn-%2020.0.4-blue?style=flat-square&logo=gunicorn)](https://gunicorn.org/)
[![Nginx](https://img.shields.io/badge/Nginx-%201.22.1-blue?style=flat-square&logo=nginx)](https://www.nginx.com/)
[![Certbot](https://img.shields.io/badge/certbot-%202.7.3-blue?style=flat-square&logo=letsencrypt)](https://certbot.eff.org/)
[![Vite](https://img.shields.io/badge/Vite-%20-blue?style=flat-square&logo=vite)](https://vitejs.dev/)
[![React](https://img.shields.io/badge/React-%20-blue?style=flat-square&logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-%20-blue?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)

***

## Функционал:

CareerHub предоставляет следующие возможности:

- Регистрация: HR-специалисты могут создать учётную запись на платформе, 
предоставив необходимую информацию и учётные данные.

- Создание Вакансий: Зарегистрированные HR-специалисты могут создавать 
вакансии, предоставляя детальное описание требований, необходимых навыков 
и других параметров.

- Поиск Студентов: HR-специалисты имеют доступ к базе данных студентов, 
отфильтрованной строго по данным из созданной вакансии. Они могут 
просматривать профили студентов, фильтровать учитывая их навыки, опыт, 
грейд и специализацию.

- Избранное и сравнение: HR-специалисты могут добавлять студентов в избранные, 
чтобы позже к ним вернуться, или добавлять в список сравнения, чтобы 
индивидуально сравнить кандидатов по всем полям одновременно.

- Фильтрация и Сортировка: Чтобы найти наилучших кандидатов, платформа 
предоставляет инструменты для фильтрации студентов по различным 
дополнительным полям, таким как грейд, навыки, специализация и многим другим.

***

## Технические особенности:

Репозиторий включает в себя два файла **docker-compose.yml** и 
**docker-compose.production.yml**, что позволяет развернуть проект на
локальном или удалённом серверах.

Данная инструкция подразумевает, что на вашем локальном/удалённом сервере 
уже установлен Git, Python 3.10, пакетный менеджер pip, Docker, 
Docker Compose, утилита виртуального окружения python3-venv.

В проекте предусмотрена возможность запуска БД SQLite3 и PostgreSQL. Выбор 
БД осуществляется сменой значения DB_ENGINE на sqlite3 или postgresql. 
sqlite3 = SQLite3, postgresql = PostgreSQL.

В проекте настроена автодокументация с помощью **Swagger**. Для ознакомления 
перейдите по [ссылке](https://tracker-hiring.ddns.net/swagger/)

С подробными инструкциями запуска вы можете ознакомиться ниже.

***

## Запуск проекта локально в Docker-контейнерах с помощью Docker Compose

Склонируйте проект из репозитория:

```shell
git clone https://github.com/D-Nevskiy/CareerHub.git
```


Перейдите в директорию проекта:

```shell
cd CareerHub/
```

Перейдите в директорию **infra** и создайте файл **.env**:

```shell
cd infra/
```

```shell
nano .env
```

Добавьте строки, содержащиеся в файле **.env.example** и подставьте 
свои значения.

Пример из .env файла:

```dotenv
SECRET_KEY=DJANGO_SECRET_KEY               # Ваш секретный ключ Django
DEBUG=False                                # True - включить Дебаг. Или оставьте пустым для False
IS_LOGGING=False                           # True - включить Логирование. Или оставьте пустым для False
ALLOWED_HOSTS=127.0.0.1 backend            # Список адресов, разделенных пробелами

# Помните, если вы выставляете DEBUG=False, то необходимо будет настроить список ALLOWED_HOSTS.
# 127.0.0.1 и backend является стандартным значением. Через пробел.

# Присутствие backend в ALLOWED_HOSTS обязательно. Через название сервиса :
# docker-compose осуществляется отправка и подтверджение письма для активации аккаунта :
# с помощью celery и redis.

# БД выбирается автоматически на основе константы DB_ENGINE. Если DB_ENGINE = sqlite , используется SQLite3.
# Если DB_ENGINE = postgresql , используется PostgreSQL.

DB_ENGINE=postgresql

POSTGRES_USER=django_user                  # Ваше имя пользователя для бд
POSTGRES_PASSWORD=django                   # Ваш пароль для бд
POSTGRES_DB=django                         # Название вашей бд
DB_HOST=db                                 # Стандартное значение - db
DB_PORT=5432                               # Стандартное значение - 5432

EMAIL_HOST=smtp.yandex.ru                  # Адрес хоста эл. почты
EMAIL_PORT=465                             # Порт эл. почты
EMAIL_USE_TLS=False                        # Использование TLS
EMAIL_USE_SSL=True                         # Использование SSL
EMAIL_HOST_USER=careerhub@yandex.ru        # Адрес почты, с которой будут отправляться письма
EMAIL_HOST_PASSWORD=SecretPassword         # Пароль почты, с которой будут отправляться письма
DEFAULT_FROM_EMAIL=careerhub@yandex.ru     # Адрес почты, с которой будут отправляться письма
```

В директории **infra** проекта находится файл **docker-compose.yml**, с 
помощью которого вы можете запустить проект локально в Docker контейнерах.

Находясь в директории **infra** выполните следующую команду:
> **Примечание.** Если нужно - добавьте в конец команды флаг **-d** для запуска
> в фоновом режиме.
```shell
sudo docker compose -f docker-compose.yml up
```

Она сбилдит Docker образы и запустит backend, frontend, СУБД, Celery, Redis 
и Nginx в отдельных Docker контейнерах.

Выполните миграции в контейнере с backend:

```shell
sudo docker compose -f docker-compose.yml exec careerhub-backend python manage.py makemigrations
```

```shell
sudo docker compose -f docker-compose.yml exec careerhub-backend python manage.py migrate
```

Соберите статику backend'a:

```shell
sudo docker compose -f docker-compose.yml exec careerhub-backend python manage.py collectstatic
```

По завершении всех операции проект будет запущен и доступен по адресу
http://127.0.0.1/

Для остановки Docker контейнеров, находясь в директории **infra** выполните 
следующую команду:

```shell
sudo docker compose -f docker-compose.yml down
```

Либо просто завершите работу Docker Compose в терминале, в котором вы его
запускали, сочетанием клавиш **CTRL+C**.

***

# CI/CD - Развёртка проекта на удаленном сервере

В проекте уже настроен Workflow для GitHub Actions.

Ваш GitHub Actions самостоятельно запустит:

- 🧪 Тесты: Запускаются тесты для проекта.
- 🏗️ Сборку образов: Git Action создает Docker-образы приложения.
- 🚀 Деплой: Образы отправляются на ваш репозиторий DockerHub, проект
деплоится на сервер.
- ✉️ Уведомление: В случае успеха вы получите уведомление в Telegram.

Форкните репозиторий, перейдите в GitHub в настройки репозитория — 
**Settings**, найдите на панели слева пункт
**Secrets and Variables**, перейдите в **Actions**, нажмите
**New repository secret**.

Создайте следующие ключи:

> **Примечание.** При подключении к вашему удалённому серверу воркер GitHub 
> Actions создаст .env файл, создаст БД и запустит контейнер с backend'ом, 
> используя эти константы.

```
# Общие секреты
DOCKER_USERNAME (Ваш логин в DockerHub)
DOCKER_PASSWORD (Ваш пароль в DockerHub)
HOST (IP адрес вашего удалённого сервера)
USER (Логин вашего удалённого сервера)
SSH_KEY (SSH ключ вашего удалённого сервера)
SSH_PASSPHRASE (Пароль вашего удалённого сервера)
TELEGRAM_TO (Ваш ID пользователя в Telegram)
TELEGRAM_TOKEN (Токен вашего бота в Telegram)

# PostgreSQL
POSTGRES_USER(Ваше имя пользователя для бд)
POSTGRES_PASSWORD(Ваш пароль для бд)
POSTGRES_DB(Название вашей бд)
DB_HOST(Адрес бд. Стандартное значение - db)
DB_PORT(Порт бд. Стандартное значение - 5432)

# Django
SECRET_KEY(Ваш секретный ключ Django)
DEBUG(Вкл/выкл DEBUG)
IS_LOGGING(Вкл/выкл Логирование)
ALLOWED_HOSTS(Список адресов, разделенных пробелами)
DB_ENGINE(sqlite или postgresql)
EMAIL_HOST=(Адрес хоста эл. почты)
EMAIL_PORT=(Порт эл. почты)
EMAIL_USE_TLS=(Использование TLS)
EMAIL_USE_SSL=(Использование SSL)
EMAIL_HOST_USER=(Адрес почты, с которой будут отправляться письма)
EMAIL_HOST_PASSWORD=(Пароль почты, с которой будут отправляться письма)
DEFAULT_FROM_EMAIL=(Адрес почты, с которой будут отправляться письма)
```

> **Внимание!** Для корректного отображения изображений не забудьте помимо 
localhost, 127.0.0.1 и backend добавить в ALLOWED_HOSTS доменное 
имя вашего сайта.


### **Теперь можно приступать к деплою**

> **Внимание!** Дальнейшие действия подразумевают что на вашем удалённом 
> сервере Nginx установлен и настроен как прокси-сервер. Изначально Nginx в 
> Docker-контейнере слушает порт 8500.

В локальном проекте замените в файле **docker-compose.production.yml** названия
образов в соответствии с вашим логином на DockerHub в нижнем регистре
(Например **your_username/careerhub_backend**)

Аналогично измените названия образов и в файле **main.yml**, который находится
в директории **/.github/workflows/**.

Подключитесь к вашему удалённому серверу любым удобным способом. Создайте в
домашней директории директорию с названием **careerhub** и перейдите в неё.

```shell
mkdir careerhub
```

Готово.

Весь процесс автоматизирован! Как только вы инициируете коммит на локальной 
машине и отправите изменения на GitHub, GitHub Actions 
возьмёт дело в свои руки:

```shell
git add .
```

```shell
git commit -m "Ваше сообщение для коммита."
```

```shell
git push
```

После успешной отправки изменений перейдите в своём репозитории на GitHub во
вкладку **Actions**. Вы увидите процесс работы Actions. После успешного 
окончания работы воркера в ваш Telegram придёт сообщение от бота:

> Деплой проекта CareerHub успешно выполнен!

**Данное сообщение означает что проект успешно запущен на сервере, проведены 
миграции и собрана статика backend'а.**

После этого можно вернуться на удалённый сервер, в директорию **careerhub** и
создать суперпользователя: 

```shell
sudo docker compose -f docker-compose.production.yml exec -it careerhub-backend python manage.py createsuperuser
```

>**Внимание! :** Для полноценной работы проекта на вашем удалённом сервере 
должен быть установлен, настроен и запущен **Nginx**. Удостоверьтесь что 
в конфиге по вашему доменному имени настроена переадресация всех запросов на
**127.0.0.1:8500** и добавлена переадресация заголовков.

### Настройка SSL шифрования через Let's Encrypt

Чтобы проект отвечал базовым стандартам безопасности необходимо настроить
SSL сертификат.

Установите **certbot**:

```shell
sudo apt install snapd
```

```shell
sudo snap install core; sudo snap refresh core
```

```shell
sudo snap install --classic certbot
```

```shell
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

Запустите sertbot и получите свой SSL сертификат:

```shell
sudo certbot --nginx
```

После перезапустите Nginx:

```shell
sudo systemctl reload nginx
```  

```shell
sudo certbot certificates
```  

> **Примечание.** SSL-сертификаты от Let's Encrypt действительны в течение 
90 дней. Их нужно постоянно обновлять. Если вы не хотите делать это 
самостоятельно, вы можете настроить автоматическое обновление сертификата 
с помощью команды ниже.

```shell
sudo certbot renew --dry-run
```  

**Теперь вы можете получить доступ к сайту по его доменному имени.**

**Как только убедитесь, что все страницы отображаются корректно - можете 
начать приглашать пользователей для создания вакансий и подбора кандидатов.**

***

## Автор

**Кирилл Смирнов**




