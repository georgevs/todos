# Backend

### Manage secrets
Fetch secrets:
```bash
openssl enc -aes-128-cbc -pbkdf2 -salt -d -in ~/ws-archive/todos.secrets.tar.gz.enc | tar xzv
```
Update secrets:
```bash
tar czv secrets | openssl enc -aes-128-cbc -pbkdf2 -salt -out ~/ws-archive/todos.secrets.tar.gz.enc
```

### Run backend in Docker
```bash
docker container run --rm \
  --name node-backend \
  --network bridge-dev \
  --ip 172.20.0.102 \
  --user node \
  --workdir /home/node/backend \
  --volume "$PWD:/home/node/backend" \
  -it node bash

npm install
node app/main
```
Test with curl:
```bash
curl http://172.20.0.102:8080/api/v1/todos
```
