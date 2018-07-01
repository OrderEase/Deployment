# Deployment

## How to run

```bash
$ git clone https://github.com/OrderEase/Deployment.git
$ git submodule init && git submodule update
$ rm Deployment/mysql/data/.gitignore

$ export MYSQL_ROOT_PASSWORD=${YOUR_ROOT_PASSWORD}
$ export MYSQL_USER=${YOUR_USERNAME}
$ export MYSQL_PASSWORD=${YOUR_PASSWORD}
$ export MYSQL_DATABASE=${DATABASE_NAME}

$ export MODE=PRODUCTION
$ export SECRET_KEY=${YOUR_SECRET_KEY}
$ export PRODUCTION_DATABASE_URI=mysql://${MYSQL_USER}:${MYSQL_PASSWORD}@database:3306/${MYSQL_DATABASE}?charset=utf8

$ docker-compose up -d
```

After mysql is ready, you should init the database

```bash
$ docker exec -it ${SERVER_CONTAINER_ID} bash
$ python manage.py gen_basic_data
```

If no exception is reported, the database now has a basic restaurant and two users, with which you can login the admin system. 

| username | password | authority |
| -------- | -------- | --------- |
| manager  | 123      | manager   |
| cook     | 123      | cook      |

## License

[MIT](http://opensource.org/licenses/MIT)