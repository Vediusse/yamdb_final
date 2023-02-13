 
![yamdb](https://github.com/github/docs/actions/workflows/yamdb_workflow.yml/badge.svg)

**YaMDb** - Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»). 
Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число)
Пользователи могут оставлять комментарии к отзывам.
Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.
___
### **Что внутри**:
* Поддерживает все типовые операции CRUD
* Предоставляет данные в формате JSON
* Аутентификация по Jwt-токену
* Реализованы пермишены, фильтрации, пагинация ответов от API
___

### **Пользовательские роли**:
* **Аутентифицированный пользователь (user)** — может, как и Аноним, читать всё, дополнительно он может публиковать отзывы и ставить оценку произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать и удалять свои отзывы и комментарии. Роль присваивается по умолчанию каждому новому пользователю.
* **Модератор (moderator)** — облаадет правами аутентифицированного пользователя + право удалять любые отзывы и комментарии.
* **Администратор (admin)** — полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры, а так же назначать роли пользователям.

___
### **Как запустить проект**:

* Клонировать репозиторий и перейти в него в командной строке:
```
git@github.com:Vediusse/infra_sp2.git
cd infra_sp2
cd api_yamdb
```

### **Шаблон наполнения env-файла:**:
1) Шаблон наполнения .env должен быть расположен по пути infra/.env !
    ```
   DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
   DB_NAME=postgres # имя базы данных
   POSTGRES_USER=postgres # логин для подключения к базе данных
   POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
   DB_HOST=db # название сервиса (контейнера)
   DB_PORT=5432
   ```


### **Как запустит проект**:
1) Поднимаем контейнеры :
   ```
   docker-compose up -d --build
   ```
2) Выполняем миграции:
   ```
   docker-compose exec web python manage.py makemigrations
   docker-compose exec web python manage.py migrate
   ```
3) Подгружаем статику:
   ```
   docker-compose exec web python manage.py collectstatic --no-input
   ```
4) Создаем дамп базы данных:
   ```
   docker-compose exec web python manage.py dumpdata > dump.json
   ```
5) Останавливаем контейнеры: 
   ```
   docker-compose down -v
   ```
* Отправка email 
```
    1) Зайти в файл settings
    2) Исправить переменные
        EMAIL_HOST_USER = 'example@domen.ru'
        EMAIL_HOST_PASSWORD = 'Пароль приложения'
        EMAIL_HOST 
        EMAIL_PORT 
        EMAIL_USE_TLS = True/False
        EMAIL_USE_SSL = False/False
        (можно получить на сайте сервиса электронной почты )
ИЛИ
    Заменить 
        EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    На
        EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
```
* Для заполнения базы данных:
```
    python import_csv
```
* Запустить проект:
```
python manage.py runserver
```
___
### **Примеры запросов**:
* GET-запрос возвращает список всех произведений:
```
http://127.0.0.1:8000/api/v1/titles/
```
```
{
  "count": 0,
  "next": "string",
  "previous": "string",
  "results": [
    {
      "id": 0,
      "name": "string",
      "year": 0,
      "rating": 0,
      "description": "string",
      "genre": [
        {
          "name": "string",
          "slug": "string"
        }
      ],
      "category": {
        "name": "string",
        "slug": "string"
      }
    }
  ]
}
```
* GET-запрос возвращает отзыв по id для указанного произведен
```
http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/{review_id}/
```
```
{
  "id": 0,
  "text": "string",
  "author": "string",
  "score": 1,
  "pub_date": "2019-08-24T14:15:22Z"
}
```
* Остальные примеры запросов можно посмотреть по [ссылке](http://127.0.0.1:8000/redoc/) после запуска проект


