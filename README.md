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

### Change env
### You can use of any of editor like: vim, nano, etc
vi env/gateway/.env

```

### Run with docker

```bash
docker-compose \
  -f docker-compose.yml \
  -f practice-hooma-api-gateway/docker-compose.yml \
  -f practice-hooma-api-gateway/docker/docker-compose.env-secret.yml \
  up -d

### If you use your own env
docker-compose \
  -f docker-compose.yml \
  -f practice-hooma-api-gateway/docker-compose.yml \
  -f practice-hooma-api-gateway/docker/docker-compose.env-secret.yml \
  -f practice-hooma-api-gateway/docker/docker-compose.env.yml \
  up -d

```
