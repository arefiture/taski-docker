![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)

## Описание проекта

Taski - учебный проект от Яндекс.Практикум.

Цель этого сайта — отслеживать свои задачи. При старте задача является открытой (невыполненной), в процессе после выполнения задачу можно закрыть.

## Технологии

- Python 3.9
- Django 3.2.3
- Django REST framework 3.12.4
- JavaScript

## Запуск проекта из образов с Docker Hub

При первом запуске убедитесь, что Docker есть и работает:

```bash
sudo systemctl status docker
```
<details>
    <summary>Что делать, если Docker отсутствует</summary>
    
1. Скачиваем и устанавилваем curl:

    ```bash
    sudo apt update
    sudo apt install curl
    ```

2. С помощью утилиты скачиваем скрипт для установки докера с официального сайта:

    ```bash
    curl -fSL https://get.docker.com -o get-docker.sh 
    ```

3. Запускаем сохраненный скрипт:

    ```bash
    sudo sh ./get-docker.sh
    ```

4. Дополнительно скачиваем утилу Docker Compose:

    ```bash
    sudo apt install docker-compose-plugin 
    ```

5. Проверяем работоспособность Docker:

    ```bash
    sudo systemctl status docker
    ```

</details>

Для запуска необходимо создать папку проекта, например `foodgram` и перейти в нее:

```bash
mkdir foodgram
cd foodgram
```

В папку проекта скачиваем файл `docker-compose.production.yml` и запускаем его:

```bash
sudo docker compose -f docker-compose.production.yml up -d
```

Далее автоматически скачаются образы, произойдет создание и включение контейнеров и объедение их в одну сеть.

## Настройки переменных окружения (о том, как заполнить env)

В корне проекта следует создать файл .env и заполнить по образу из файла .env.example

## После запуска: Миграции, сбор статистики

После запуска необходимо выполнить сбор статистики и миграции бэкенда.
Статистика фронтенда собирается во время запуска контейнера, после чего он останавливается. 

```bash
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate

sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic

sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/
```

После этого проект будет доступен по адресам:
```
localhost:9000
127.0.0.1:9000
```

## Остановка проекта:

```bash
sudo docker compose -f docker-compose.production.yml down
```

## Автор

Раков Александр https://t.me/alexrinko
