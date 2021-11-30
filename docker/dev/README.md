# dev_cakephp4

![スクリーンショット 2020-12-30 0 01 40](https://user-images.githubusercontent.com/5633085/103293010-5df3a180-4a32-11eb-9e75-3e0cd01a3042.jpg)


- docker images
  - cakephp-app
    - php:7.4-fpm-alpine (nginx,php-fpm,supervisor)
	- cakephp 4.2.1
  - cakephp-db
    - mysql:8.0.27
  - cakephp-redis


- git clone or fork

```
mkdir -p ~/git/github
cd ~/git/github
git clone git@github.com:RVIRUS0817/dev_cakephp4.git
```

- add localhost /etc/hosts

```
sudo vim /etc/hosts
127.0.0.1 dev.adachin.com
```

- docker run

```
cd dev_cakephp4
cp config/.env.example config/.env
cd docker/dev
docker-compose up -d
```

- app deploy

```
docker exec -it cakephp-app bash

composer install
bin/cake migrations migrate
supervisorctl restart app
``` 

- Access

http://dev.adachin.com/


![スクリーンショット 2020-12-29 23 59 18](https://user-images.githubusercontent.com/5633085/103292992-53390c80-4a32-11eb-9b12-63db925984e0.jpg)


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

## How to cakephp4 download

- https://book.cakephp.org/4/ja/installation.html
- https://getcomposer.org/download/

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

php composer-setup.php
php -r "unlink('composer-setup.php');"

php composer.phar create-project --prefer-dist cakephp/app:4.* my_app_name
```
