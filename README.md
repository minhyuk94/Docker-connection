# Connection of back,front,db in docker

## 1. 도커 환경을 이용한 통신

### DB(Mongo)
docker run --name mongodb --rm -d -p 27017:27017 mongo

### BACK-END(Node)
docker build -t goals-backend .<br />
docker run --name goals-backend --rm -d -p 80:80 goals-node

### FRONT-END(React)
docker build -t goals-react .<br />
docker run --name goals-frontend --rm -p 3000:3000 -it goals-react


## 2. 도커 네트워크를 통한 통신(단, 컨테이너간의 통신 한정, 브라우저로의 통신은 localhost 혹은 공용 도메인주소로 가능)

### NETWORK 
docker network ls <br />
docker network create goals-net

### DB
docker run --name mongodb --rm -d --network goals-net -p 27017:27017 mongo

### BACK-END
docker run --name goals-backend --rm -d -p 80:80 --network goals-net goals-node

### FRONT-END
-- 항상 브라우저에서만 실행되므로 어차피 도커환경에서 실행되지않으므로 컨테이너간의 네트워크 핋요 x <br />
docker run --name goals-frontend --rm -p 3000:3000 -it goals-react

### NETWORK CHECK
docker container inspect [docker-name]

## 3. 볼륨에 데이터를 저장하여 도커 컨테이너가 삭제 되어도 데이터를 보존하기.
### DB(데이터 보존)
docker run --name mongodb -v data:/data/db --rm -d --network goals-net -p 27017:27017 mongo

### DB(데이터 보존 및 인증설정)
docker run --name mongodb -v data:/data/db --rm -d --network goals-net -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=yoo -e MONGO_INITDB_ROOT_PASSWORD=secret mongo

#### Docker All Stop
docker stop $(docker ps -a -q)


## Docker compose
https://docs.docker.com/compose/compose-file/

###