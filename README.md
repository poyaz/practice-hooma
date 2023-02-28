How to run
==========

### You need to run blow command for create secret

```bash
echo '<your-db-password>' > ./secrets/db_password.txt

ssh-keygen -t rsa -b 4096 -m PEM -f ./secrets/jwtRS256.key
openssl rsa -in ./secrets/jwtRS256.key -pubout -outform PEM -out ./secrets/jwtRS256.key.pub
```

### Clone all project

* https://github.com/poyaz/practice-hooma-api-gateway
* https://github.com/poyaz/practice-hooma-ms-auth
* https://github.com/poyaz/practice-hooma-ms-users

### Change env if you want to use your own env

```bash
# practice-hooma-api-gateway project
cd practice-hooma-api-gateway
cp env/gateway/.env.example env/gateway/.env

### Change api-gateway env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

###############################################3

# practice-hooma-ms-auth project
cd practice-hooma-ms-auth
cp env/gateway/.env.example env/gateway/.env

### Change auth microservice env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

###############################################3

# practice-hooma-ms-users project
cd practice-hooma-ms-users
cp env/gateway/.env.example env/gateway/.env

### Change users microservice env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

```

### Run with docker

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
