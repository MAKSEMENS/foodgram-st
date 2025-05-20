# Foodgram
**Разработчик:** Зиновьев Максим

## О проекте
**Foodgram** — это платформа, где пользователи могут делиться своими рецептами, сохранять понравившиеся блюда в «Избранное» и подписываться на авторов. Авторизованные участники получают доступ к функции «Список покупок»: удобному инструменту для формирования списка продуктов, необходимых для реализации выбранных рецептов.

## Используемые технологии

<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=ffffff"/>
<img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=React&logoColor=000000"/>
<img src="https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=Django&logoColor=ffffff"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=PostgreSQL&logoColor=ffffff"/>
<img src="https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=Nginx&logoColor=ffffff"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=ffffff"/>
<img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=ffffff"/>

## Локальный запуск (только бэкенд)
1. **Клонировать репозиторий и перейти в директорию**
    ```bash
    git clone https://github.com/dableshevich/foodgram-st.git
    cd foodgram-st/backend/
    ```
2. **Применить миграции**
    ```bash
    python manage.py migrate
    ```
3. **Создать суперпользователя**
    ```bash
    python manage.py createsuperuser
    ```
4. **Загрузить тестовые данные или только ингредиенты**
    - **Полный набор (пользователи, рецепты, ингредиенты):**
      ```bash
      python manage.py loaddata collected_data.json
      ```
    - **Только ингредиенты:**
      ```bash
      python manage.py load_ingredients
      ```
5. **Запустить сервер**
    ```bash
    python manage.py runserver
    ```

## Деплой с Docker (полная сборка)
Для развёртывания всей системы понадобится Docker и Docker Compose. Инструкции по установке:
- [Docker Desktop для Windows/MacOS](https://www.docker.com/products/docker-desktop/)
- [Docker Engine для Linux](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

1. **Клонирование и переход в корень проекта**
    ```bash
    git clone https://github.com/dableshevich/foodgram-st.git
    cd foodgram-st/
    ```
2. **Создание файла переменных окружения**
    - Скопировать `.env.example` в `.env` и заполнить:
      ```dotenv
      DB_ENGINE=django.db.backends.postgres
      POSTGRES_USER=postgres
      POSTGRES_PASSWORD=postgres
      POSTGRES_DB=postgres
      DB_HOST=postgres
      DB_PORT=5432
      DJANGO_SECRET_KEY="<ваш_секретный_ключ>"
      ```
3. **Сборка и запуск контейнеров**
    ```bash
    cd infra/
    sudo docker compose up --build
    ```
4. **В другом терминале выполнить миграции и загрузку данных**
    ```bash
    sudo docker compose exec backend python3 manage.py migrate
    ```
    - **Полный набор тестовых данных:**
      ```bash
      sudo docker compose exec backend python3 manage.py loaddata collected_data.json
      ```
    - **Только ингредиенты:**
      ```bash
      sudo docker compose exec backend python3 manage.py load_ingredients
      ```
5. **Сбор статических файлов и копирование**
    ```bash
    sudo docker compose exec backend python3 manage.py collectstatic --noinput
    sudo docker compose exec backend cp -r static/. /collected_static/static/
    ```

**Готово!** Откройте в браузере [http://localhost/](http://localhost/) и наслаждайтесь работой сайта.
