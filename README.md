# Итоговый совместный проект по теме API.
# Проект YaMDb
Бэкенд для работы с произведениям, отзывами и комментариями. 
Реализовано согласно ТЗ в формате redoc. Доступно после запуска проекта:
http://localhost:8000/redoc/

## Технологии
* Python 3.7
* Django 2.2.19
* Nginx
* Docker-comprose
* DRF

## Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:Ramiras123/api_yamdb.git
```

```
cd api_yamdb/
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv env
```

```
source env/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```
Перейти в папку infra и выпролнить команду

```
docker-compose up
```

Выполнить миграции:

```
docker-compose exec web python manage.py migrate
```

Создать суперпользователя:

```
docker-compose exec web python manage.py createsuperuser
```

Сбор статических файлов:

```
docker-compose exec web python manage.py collectstatic --no-input
```

## Импорт данных 

Импорт данных из static/data:
```
docker-compose exec web python manage.py import_data
```

Внимание, если при импорте возникают конфликты с ранее загруженными данными, то можно запустить скрипт с аругментов для предварительной очистки всех моделей:
```
docker-compose exec web python manage.py import_data --clear
```

Правда, в этом случае и суперюзер будет удален, так что скорее всего придется сделать 
```
docker-compose exec web python manage.py createsuperuser
```
Суперюзером можно войти в админку и посмотреть заполненность данных.

Чтобы загрузить тестовые значения в базу данных перейдите в каталог проекта и скопируйте файл базы данных в контейнер приложения:
```
docker cp <DATA BASE> <CONTAINER ID>:/app/<DATA BASE>
```
Перейдите в контейнер приложения и загрузить данные в БД:
```
docker container exec -it <CONTAINER ID> bash
python manage.py loaddata <DATA BASE>
```
