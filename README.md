Задание 1:
Развернуть и запустить контейнер с любым вашим образом(сайт на CMS, образ ОС, образ базы данных, что угодно). Использовать строго Compose!
Установка докеров
root@hp-gb:/home/mn# apt install docker-compose -y
root@hp-gb:/home/mn# apt install docker swarm -y
Создаем дир-ю и yml, заполняем данные
root@hp-gb:/home/mn# mkdir simple_image3
root@hp-gb:/home/mn# cd simple_image3/
root@hp-gb:/home/mn/simple_image3# nano docker-compose.yml
version: '3'
services:
  db:
    image: mysql:5.7
    restart: unless-stopped
    volumes:
      - dbdata:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: 1234
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: 1234
  wordpress:
    depend_on:
      - db
    image: wordpress:latest
    ports:
      - 6080:8080
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: 1234
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - ./wordpress:/var/www/html
root@hp-gb:/home/mn/simple_image3# docker-compose up -d

 


Задание 2*:
Установить 2 операционную систему в виртуальную машину(создать новый образ ОС). Создать кластер из двух машин(первой и второй), Сделать так, чтобы каждая нода могла управлять кластером (была лидером). Также необходимо добавить каждой ноде по метке: prod, stage или любые другие метки, но у каждой ноды должна быть своя отдельная метка. Проверить и убедиться, что метки действительно добавились. Раскатайте на 2 машины любое ваше приложение, проверьте, что контейнер с приложением создался. Использовать строго Swarm!

root@hp-gb:/home/mn#
root@hp-gb:/home/user2#
root@hp-gb:/home/mn# docker swarm init
root@hp-gb:/home/mn# docker node ls
root@hp-gb:/home/user2# docker swarm join –token
root@hp-gb:/home/mn# docker promote user2
root@hp-gb:/home/mn# docker node promote user2
root@hp-gb:/home/mn# docker node ls
![image](https://github.com/MelnikNYU/docker/assets/122616911/5d9c5f6e-b5ad-4c43-97e1-a819747773ab)



