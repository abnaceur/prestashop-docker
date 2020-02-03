PRESTASHOP + DOCKER PROJECT
=========================

## Description of the project :

Use docker for better implementation of a prestashop 
e-commerce solution.

## Technologies :
 - Prestashop
 - Docker 
 - Docker-compose

## Install the development environment

Get the source:

```bash
git clone https://github.com/abnaceur/prestashop-docker.git
```

#### Prerequisite :
 - Docker 17.12.1-ce
 - Docker compose
 - Port 80 and 8080 available

## Build the project in dev

Create the environment variables
```bash
cp .env-template .env
```

Build the project
```bash
docker-compose -f docker-compose-template.yml up --build
```


## Setup thte database

Create a prestashop user

Connect to your mysql container
```bash
docker exec -ti prest_mysql bash
```

Once within the container connect to mysql

```bash
# Username : root
# Password root
mysql -u root -p
```
Creat a new user
```bash
CREATE USER 'ps_user'@'%' IDENTIFIED BY 'PASSWORD';
GRANT ALL ON *.* TO 'ps_user'@'%';
FLUSH PRIVILEGES;
EXIT;
```

Now you can navigate to you localhost and setup your e-shop


### Help

If you face this error message 

```bash
 File './mysql/user.MYD' not found (Errcode: 13 - Permission denied
```

Solution

```bash
chown -R mysql:mysql /var/lib/mysql 
```
If you face a permission denided on PHP while setting up the e-shop
then  


```bash
docker stop $(docker ps -a -q)
```

Connect to a container via bash (get the container name you want to connect to via command `docker ps`)
```bash
docker exec -ti containername bash
```

Execute a command directly in a container without connecting in bash (get the container name you want to connect to via command `docker ps`)

```bash
docker exec -i containername yourcommand
```

Delete all images 

```bash
docker rmi -f $(docker images -q)
```

Show images 

```bash
docker images
```