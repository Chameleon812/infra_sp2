# Group project of Yandex.Practicum students on the course "API: program interaction interface"

The YaMDb project collects user feedback on works. Works are not stored in YaMDb, you can not watch a movie or listen to music here.

## Functionality

- JWT tokens are used for authentication.
- Unauthenticated users have read-only access to the API.
- Creation of objects is allowed only for authenticated users.
- Getting a list of all categories and genres, adding and deleting.
- Getting a list of all works, adding them. Obtaining, updating and deleting a specific work.
- Getting a list of all reviews, adding them. Get, update, and delete specific feedback.
- Getting a list of all comments, adding them. Getting, updating and deleting a specific comment.
- Ability to get detailed information about yourself and delete your account.
- Filtering by fields.

### The API documentation is available at [http://127.0.0.1:8000/redoc/](http://127.0.0.1:8000/redoc/) after the server has started

### Technologies
- Python 3.7
- Django 3.2
- Nginx
- Docker-compose

### Env-file filling template:
1. Specify the secret key for settings.py:
```
    SECRET_KEY=default-key
```
2. Specify that we are working with postgresql:
```
    DB_ENGINE=django.db.backends.postgresql
```
3. Specify the database name:
```
    DB_NAME=postgres
```
4. Specify the login to connect to the database:
```
    POSTGRES_USER=login
```
5. Specify the password for connecting to the database:
```
    POSTGRES_PASSWORD=password
```
6. Specify the name of the service (container):
```
    DB_HOST=db
```
7. Specify the port for connecting to the database:
```
    DB_PORT=5432
```
### Instructions
 
1. Clone the repository:
```
    git clone git@github.com:Chameleon812/infra_sp2.git
```
2. Go to the infra folder and run docker-compose.yaml (with Docker installed and running):
```
    docker-compose up -d
```
3. To rebuild containers, run the command:
```
    docker-compose up -d --build
```
4. In the web container, run the migrations:
```
    docker-compose exec web python manage.py migrate
```
5. Create superuser:
```
    docker-compose exec web python manage.py createsuperuser
```
6. Collect static:
```
    docker-compose exec web python manage.py collectstatic --no-input
```
The project is up and running at: localhost

### Loading test values into the database
To load test values into the database, navigate to the project directory and copy the database file to the application container:
```
    docker cp <DATA BASE> <CONTAINER ID>:/app/<DATA BASE>
```
Go to the application container and load the data into the database:
```
    docker container exec -it <CONTAINER ID> bash
    python manage.py appdata <DATA BASE>
```

### Examples of some API requests

User registration:
```
    POST /api/v1/auth/signup/ 
```
Getting your account information:
```
    GET /api/v1/users/me/
```
Adding a new category:
```
    POST /api/v1/categories/
```
Removing a genre:
```
    DELETE /api/v1/genres/{slug}
```
Partial update of information about the work:
```
    PATCH /api/v1/titles/{titles_id}
```
Getting a list of all reviews:
```
    GET /api/v1/titles/{title_id}/reviews/
```
Adding a comment to a review:
```
    POST /api/v1/titles/{title_id}/reviews/{review_id}/comments/
```    

The full list of API requests are in the documentation
