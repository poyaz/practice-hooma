Introduction
========

This project is a practice for the "Hooma" company interview. This sample project have one gateway and two microservice and communicate with each other on GRPC protocol.

Projects
========

* [Api Gateway](https://github.com/poyaz/practice-hooma-api-gateway)
* [Authenticate Microservice](https://github.com/poyaz/practice-hooma-ms-auth)
* [Authenticate Proto](https://github.com/poyaz/practice-hooma-proto-auth)
* [Users Microservice](https://github.com/poyaz/practice-hooma-ms-users)
* [Users Proto](https://github.com/poyaz/practice-hooma-proto-users)

How to run
==========

## You need to run blow command for create secret

```bash
echo '<your-db-password>' > ./secrets/db_password.txt

ssh-keygen -t rsa -b 4096 -m PEM -f ./secrets/jwtRS256.key
openssl rsa -in ./secrets/jwtRS256.key -pubout -outform PEM -out ./secrets/jwtRS256.key.pub
```

## Clone all project

* https://github.com/poyaz/practice-hooma-api-gateway
* https://github.com/poyaz/practice-hooma-ms-auth
* https://github.com/poyaz/practice-hooma-ms-users

## Deploy

### Run with docker in demo mode for the Hooma company

```bash
docker-compose \
      -f docker-compose.yml \
      -f docker/docker-compose.env-secret.yml \
      \
      -f practice-hooma-api-gateway/docker-compose.yml \
      -f practice-hooma-api-gateway/docker/docker-compose.network.yml \
      -f practice-hooma-api-gateway/docker/docker-compose.env-secret.yml \
      \
      -f practice-hooma-ms-auth/docker-compose.yml \
      -f practice-hooma-ms-auth/docker/docker-compose.network.yml \
      -f practice-hooma-ms-auth/docker/docker-compose.env-secret.yml \
      \
      -f practice-hooma-ms-users/docker-compose.yml \
      -f practice-hooma-ms-users/docker/docker-compose.network.yml \
      -f practice-hooma-ms-users/docker/docker-compose.env-secret.yml \
  \
  up -d
```

### Run with docker in demo mode for the Hooma company (with different directory structure)

**If your directory structure is not like below** you should run docker with more environment:

```
/practice-hooma
├── practice-hooma-api-gateway
├── practice-hooma-ms-auth
├── practice-hooma-ms-users
├── docker
├── secrets
├── docker-compose.yml
└── README.md
```

| Name                        | Default                      | Description                            |
|-----------------------------|------------------------------|----------------------------------------|
| HOOMA_API_GATEWAY_BASE_PATH | ./practice-hooma-api-gateway | نام کاربری برای اتصال به سرور ssh      |
| HOOMA_MS_AUTH_BASE_PATH     | ./practice-hooma-ms-auth     | کلمه‌عبور کنونی برای اتصال به سرور ssh |
| HOOMA_MS_USERS_BASE_PATH    | ./practice-hooma-ms-users    | کلمه‌عبور جدید برای قرار گرفتن در سرور |

For example if your folder strutter like below:

```
<path-of-projects>/
├── practice-hooma
├── practice-hooma-api-gateway
├── practice-hooma-ms-auth
├── practice-hooma-ms-users
```

You should use environment to run docker:

```bash
### First go to practice-hooma folder
cd <path-of-projects>/practice-hooma

HOOMA_API_GATEWAY_BASE_PATH=<path-of-projects>/practice-hooma-api-gateway \
HOOMA_MS_AUTH_BASE_PATH=<path-of-projects>/practice-hooma-ms-auth \
HOOMA_MS_USERS_BASE_PATH=<path-of-projects>/practice-hooma-ms-users \
docker-compose \
  -f docker-compose.yml \
  -f docker/docker-compose.env-secret.yml \
  \
  -f <path-of-projects>/practice-hooma-api-gateway/docker-compose.yml \
  -f <path-of-projects>/practice-hooma-api-gateway/docker/docker-compose.network.yml \
  -f <path-of-projects>/practice-hooma-api-gateway/docker/docker-compose.env-secret.yml \
  \
  -f <path-of-projects>/practice-hooma-ms-auth/docker-compose.yml \
  -f <path-of-projects>/practice-hooma-ms-auth/docker/docker-compose.network.yml \
  -f <path-of-projects>/practice-hooma-ms-auth/docker/docker-compose.env-secret.yml \
  \
  -f <path-of-projects>/practice-hooma-ms-users/docker-compose.yml \
  -f <path-of-projects>/practice-hooma-ms-users/docker/docker-compose.network.yml \
  -f <path-of-projects>/practice-hooma-ms-users/docker/docker-compose.env-secret.yml \
  \
  up -d --build

```

### Run with docker own env compose file

If you want custom this composes file for you own demo and using your own environment, You can do it like below:

1. If you want to create custom compose file, You can use folder `docker/custom` for each project
2. If you want to use own environment, You can use folder `env` for each project

If you want to use your own env

```bash
# practice-hooma-api-gateway project
cd practice-hooma-api-gateway
cp env/gateway/.env.example env/gateway/.env

### Change api-gateway env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

###############################################

# practice-hooma-ms-auth project
cd practice-hooma-ms-auth
cp env/gateway/.env.example env/gateway/.env

### Change auth microservice env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

###############################################

# practice-hooma-ms-users project
cd practice-hooma-ms-users
cp env/gateway/.env.example env/gateway/.env

### Change users microservice env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

######################################################################
######################################################################
######################################################################

### If you use your own env
docker-compose \
  -f docker-compose.yml \
  -f docker/docker-compose.env-secret.yml \
  \
  -f practice-hooma-api-gateway/docker-compose.yml \
  -f practice-hooma-api-gateway/docker/docker-compose.network.yml \
  -f practice-hooma-api-gateway/docker/docker-compose.env-secret.yml \
  -f practice-hooma-api-gateway/docker/docker-compose.env.yml \
  \
  -f practice-hooma-ms-auth/docker-compose.yml \
  -f practice-hooma-ms-auth/docker/docker-compose.network.yml \
  -f practice-hooma-ms-auth/docker/docker-compose.env-secret.yml \
  -f practice-hooma-ms-auth/docker/docker-compose.env.yml \
  \
  -f practice-hooma-ms-users/docker-compose.yml \
  -f practice-hooma-ms-users/docker/docker-compose.network.yml \
  -f practice-hooma-ms-users/docker/docker-compose.env-secret.yml \
  -f practice-hooma-ms-users/docker/docker-compose.env.yml \
  \
  up -d

```
