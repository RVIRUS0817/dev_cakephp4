# dev_cakephp

![スクリーンショット 2020-12-19 13 16 24](https://user-images.githubusercontent.com/5633085/102680644-77f4df00-41fd-11eb-9f15-fc1a36eb88cc.jpg)


- docker images
  - cakephp-nginx
    - nginx 1.25.2
  - cakephp-app
    - php:7.4-fpm-alpine (php-fpm)
    - cakephp 4.2.1
  - cakephp-db
    - mysql:8.0.27
  - cakephp-redis


- git clone or fork

```
mkdir -p ~/git/github
cd ~/git/github
git clone git@github.com:RVIRUS0817/dev_cakephp.git
```

- add localhost /etc/hosts

```
sudo vim /etc/hosts
127.0.0.1 dev.adachin.com
```

- docker run

```
cd dev_cakephp
cp .env.example .env
cd docker/dev-micro
docker-compose up -d
```

- app deploy

```
docker exec -it cakephp-app bash

composer install
bin/cake migrations migrate
``` 

- Access

http://dev.adachin.com/


![スクリーンショット 2020-12-19 13 41 49](https://user-images.githubusercontent.com/5633085/102680880-fe122500-41ff-11eb-9562-d284dd369142.jpg)


- DB login

```
docker exec -it cakephp-app bash
mysql -u root -h db -p
```

- redis login

```
docker exec -it cakephp-app bash
redis-cli -h redis
```

## How to download cakephp app

```
composer global require cakephp/installer

cakephp new app
or
composer create-project --prefer-dist cakephp/cakephp app
```
