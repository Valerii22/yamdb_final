![yamdb_final status](https://github.com/Valerii22/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master&event=push)
<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
    </li>
    <li>
        <a href="#usage">Usage</a>
        <ul>
            <li><a href="registration-and-authorization">Registration and authorization</a></li>
            <li><a href="#available-urls">Available urls</a></li>
            <li><a href="#documentation">Documentation</a></li>
        </ul>
    </li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
    <li><a href="#developed-by">Developed by</a></li>
  </ol>
</details>

## About The Project
This is api service, where you can get or create reviews, ratings, comments on the different content.

### Built With
* Python
* SQLite
* Django

## Getting Started
1. Clone the repo
  ```sh
  git clone ...
  ```

2. Make and activate virtual environment
  ```sh
  python -m venv venv
  ```
  ```sh
  source venv/Scripts/activate
  ```

2. Create and open ```.env``` file:
```sh
cd infra
touch .env
```
3. Fill ```.env``` file, for exdample:
```sh
DB_ENGINE=django.db.backends.postgresql

DB_NAME=postgres

POSTGRES_USER=postgres

POSTGRES_PASSWORD=postgres

DB_HOST=db

DB_PORT=5432

```
4. Building container:
```sh
docker-compose up -d --build
```
5. Migrations, create superuser, collect static and dump db:
```sh
docker-compose exec web python manage.py migrate

docker-compose exec web python manage.py createsuperuser

docker-compose exec web python manage.py collectstatic --no-input 

docker-compose exec web python manage.py loaddata fixtures.json
```

## Usage

You may use Postman to create api requests.<br>
Only auth users can make reviews and leave comments.<br>
So your first goal is to **Sign Up** and then **Get Token**.

### Registration and authorization

Send POST to register new user with parameters:<br>
**email** and **username** to endpoint `/api/v1/auth/signup/`.

YaMBD will send you a **confirmation code** on your email.

Send POST to get a **bearer token** with parameters:<br>
**username** and **confirmation code** to endpoint `/api/v1/auth/token/`.

If you wish, you may send PATCH to endpoint `/api/v1/users/me/`<br>
and update your profile(check parameters in docs).

### Available urls

<details>
  <summary>Titles</summary><br>

  `/api/v1/titles/`

  **POST** to make new Title (ADMIN):

  ```sh
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
</details>
<details>
  <summary>Genres</summary><br>

  `/api/v1/genres/`

  **POST** to make new Genre (ADMIN):

  ```sh
  {
    "name": "string",
    "slug": "string"
  }
  ```
</details>
<details>
  <summary>Categories</summary><br>

  `/api/v1/categories/`

  **POST** to make new Category (ADMIN):

  ```sh
  {
    "name": "string",
    "slug": "string"
  }
  ```
</details>
<details>
  <summary>Reviews</summary><br>

  `/api/v1/titles/<title_id>/reviews/`

  **POST** to make new Review (AUTHORIZED):

  ```sh
  {
    "text": "string",
    "score": 1
  }
  ```
</details>
<details>
  <summary>Comments</summary><br>

  `/api/v1/titles/<title_id>/reviews/<review_id>comments/`

  **POST** to leave Comment (AUTHORIZED):
  
  ```sh
  {
    "text": "string"
  }
  ```

</details>

### Documentation
  
More data and examples available on ```127.0.0.1:8000/redoc/```

<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [SQLite](https://www.sqlite.org/docs.html)
* [Django](https://django.fun/ru/docs/django/3.2/)
* [Rest-framework](https://www.django-rest-framework.org/)
* [SimpleJWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/index.html)
* [Pytest](https://docs.pytest.org/en/7.2.x/)


<!-- DEVELOPED BY -->
## Developed by
> Kautarov Maksim - [https://github.com/psevdocoder](https://github.com/psevdocoder)<br>
> Sukonkin Valerii - [https://github.com/Valerii22](https://github.com/Valerii22)<br>
> Tsipichev Sergey - [https://github.com/n1chego](https://github.com/n1chego)<br>
