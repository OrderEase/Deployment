# Deployment

## Usage

```bash
$ git clone https://github.com/OrderEase/Deployment.git
$ cd Deployment
$ git submodule init && git submodule update
```

### Configuration

*docker-compose.yml*

```yml
services:
  nginx:
    ...

    ports:
      - '8888:8888'  # Business Port
      - '8000:8000'  # Customer Port

    ...
```

You can modify the ports and the following configuration must correspond to the modification here.

#### OrderEase-2C

Build

```bash
$ cd OrderEase-2C
$ npm install
$ npm run build
```

#### OrderEase-2B

*OrderEase-2B/config/prod.dev.js*

```js
module.exports = {
    ...

    CUSTOMER_BASE_URL: '"http://{YOUR_HOST_NAME}:{CUSTOMER_PORT}/#/login"'
}
```

Build

```bash
$ cd OrderEase-2B
$ npm install
$ npm run build
```

#### Server

```bash
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