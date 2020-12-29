# dev_cakephp4

![スクリーンショット 2020-12-30 0 01 40](https://user-images.githubusercontent.com/5633085/103293010-5df3a180-4a32-11eb-9e75-3e0cd01a3042.jpg)


- docker images
  - app-cakephp
    - php:7.4-fpm-alpine (nginx,php-fpm,supervisor)
	- cakephp 4.2.1
  - mysql-57
    - mysql:5.7


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
docker exec -it app-cakephp bash

composer install
bin/cake migrations migrate
upervisorctl restart app
``` 

- Access

http://dev.adachin.com/


![スクリーンショット 2020-12-29 23 59 18](https://user-images.githubusercontent.com/5633085/103292992-53390c80-4a32-11eb-9b12-63db925984e0.jpg)


- DB login

```
docker exec -it app-cakephp bash
mysql -u root -h db -p
```
