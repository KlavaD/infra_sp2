# Проект API_YAMDB собирает отзывы пользователей на различные произведения.
Проект создавали:
* ### Андрей Мельников
  * система регистрации и аутентификации,
  * права доступа,
  * работа с токеном,
  * система подтверждения через e-mail.
* ### Клавдия Дунаева
  Пишет модели, view и эндпойнты для
  * произведений,
  * категорий,
  * жанров;
* ### Николай Артемьев
  Пишет модели, view и эндпойнты для
  * отзывов,
  * комментариев,
  * рейтинг произведений.
### Как запустить проект:

В данном проекте использованы технологии:
Python, Django, DRF, Api, Postman

**Описание команд для запуска приложения в контейнерах**

Создайте файл .env с переменными окружения для работы с базой данных:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=< имя базы данных>
POSTGRES_USER=<логин для подключения к базе данных>
POSTGRES_PASSWORD=<пароль для подключения к БД (установите свой)>
DB_HOST=< название сервиса (контейнера)>
DB_PORT=5432 # порт для подключения к БД 
```
Запустите контейнер из папки infra/
```
docker-compose up -d --build
```

Выполните следующие команды:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```

**Как запустить проект:**

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://git@github.com:KlavaD/api_yamdb.git
```

```
cd api_yamdb
```

Создать и активировать виртуальное окружение:

```
python3 -m venv env
```

* Если у вас Linux/macOS

    ```
    source env/bin/activate
    ```

* Если у вас windows

    ```
    source env/scripts/activate
    ```

Обновить pip:

```
python3 -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Сделать импорт из csv файлов:

```
python manage.py addcsv
```

Запустить проект:

```
python3 manage.py runserver
```
## Примеры запросов: ##
Регистрация нового пользователя:
>**POST** http://127.0.0.1:8000/api/v1/signup/

Для получения токена отправьте логин и код, который пришел вам на электронную почту:
>**POST** http://127.0.0.1:8000/api/v1/auth/token/

Получение списка произведений:
>**GET** http://127.0.0.1:8000/api/v1/titles/

Создание публикации (только администратор):
>**POST** http://127.0.0.1:8000/api/v1/titles/
> 
```
{
"name": "string",
"year": 0,
"description": "string",
"genre": [
"string"
],
"category": "string"
}
```

Получение списка категорий:
>**GET** http://127.0.0.1:8000/api/v1/categories/

Получение списка жанров:
>**GET** http://127.0.0.1:8000/api/v1/genre/

Просмотр отзывов на произведение:
>**GET** http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/

Создание отзывов на произведение:
>**POST** http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/
```
{
"text": "string",
"score": 1
}
```

Просмотр комментариев к отзыву:
>**GET** http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/commenta/

Создание комментария к отзыву:
>**Post** http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/commenta/
```
{
"text": "string"
}
```
Остальные запросы можно посмотреть в документации для API Yamdb:
> http://127.0.0.1:8000/redoc/
