# API_YAMDB

### REST API проект для сервиса YaMDb — сбор отзывов пользователей на произведения.

## Описание
Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку. Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Добавлять произведения, категории и жанры может только администратор. Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); Пользователи могут оставлять комментарии к отзывам. Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

### Как запустить проект:
Клонируем репозиторий и переходим в него:
~~~
cd infra_sp2

cd api_yamdb
~~~

Создаем и активируем виртуальное окружение:
~~~
python3 -m venv venv

source venv/bin/activate 

python -m pip install --upgrade pip
~~~

Ставим зависимости из requirements.txt:
~~~
pip install -r requirements.txt
~~~

Добавьте файл (.env) , расположенный по пути infra/.env
~~~
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
~~~

Переходим в папку с файлом docker-compose.yaml:
~~~
cd infra
~~~

Поднимаем контейнеры:
~~~
docker-compose up -d --build
~~~

Выполняем миграции:
~~~
docker-compose exec web python manage.py migrate
~~~

Создаем суперпользователя:
~~~
docker-compose exec web python manage.py createsuperuser
~~~

Србираем статику:
~~~
docker-compose exec web python manage.py collectstatic --no-input
~~~

Создаем дамп базы данных (резервную копию):
~~~
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
~~~

---
Документация API YaMDb доступна по эндпойнту: http://localhost/redoc/
