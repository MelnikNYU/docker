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
  wordpress:
    image: wordpress:latest
    ports:
      - 6080:8080
    volumes:
      - ./wordpress:/var/www/html
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: 1234
      WORDPRESS_DB_NAME: wordpress
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: 1234
      MYSQL_DATABASE: wordpress
    volumes:
      - ./db_data:/var/lib/mysql
root@hp-gb:/home/mn/simple_image3# docker-compose up -d
 


Задание 2*:
Установить 2 операционную систему в виртуальную машину(создать новый образ ОС). Создать кластер из двух машин(первой и второй), Сделать так, чтобы каждая нода могла управлять кластером (была лидером). Также необходимо добавить каждой ноде по метке: prod, stage или любые другие метки, но у каждой ноды должна быть своя отдельная метка. Проверить и убедиться, что метки действительно добавились. Раскатайте на 2 машины любое ваше приложение, проверьте, что контейнер с приложением создался. Использовать строго Swarm!
 


