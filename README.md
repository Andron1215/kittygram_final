# Kittygram

Kittygram — сайт для любителей котиков.

## Технологии

- Python 3.9
- Django 3.2.3
- Node.js 6.9.0
- React 17.0.2
- PostgreSQL 13
- Gunicorn 20.1.0
- Nginx 1.22.1
- Docker

## Установка и запуск для удалённого сервера на Linux

### Установка Docker на Linux

Cамый простой способ установить Docker на Linux — скачать и выполнить официальный скрипт. Для этого поочерёдно выполните в терминале следующие команды:
1) Скачайте и установите curl — консольную утилиту, которая умеет скачивать файлы по команде пользователя:
```
sudo apt update
sudo apt install curl
```
2) С помощью утилиты curl скачайте скрипт для установки докера с официального сайта:
```
curl -fSL https://get.docker.com -o get-docker.sh 
```
3) Запустите сохранённый скрипт с правами суперпользователя:
```
sudo sh ./get-docker.sh
```

### Запуск проекта

*Для запуска необходим установленный Docker*
1) Создайте каталок для проекта и войдите в него:
```
mkdir kittygram
cd kittygram
```
2) Скачайте файл docker-compose.production.yml
```
curl -o docker-compose.production.yml https://raw.githubusercontent.com/Andron1215/kittygram_final/main/docker-compose.production.yml
```
3) Скачайте файл .env и отредактируйте его:
```
curl -o .env https://raw.githubusercontent.com/Andron1215/kittygram_final/main/.env.example
nano .env
```
4) Скачайте и запустите проект:
```
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
```
5) Сделайте миграцию для базы данных:
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
```
6) Соберите статику и копируйте в каталог со статикой:
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/static/
```

## Авторы

- Backend: Yandex Praktikum Team
- Frontend: Yandex Praktikum Team
- DevOps: Богидаев Андрей
