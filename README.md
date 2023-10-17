# Connection of back,front,db in docker

### DB(Mongo)
docker run --name mongodb --rm -d 

### BACK-END(Node)
docker build -t goals-backend .<br />
docker run --name goals-backend --rm -d -p 80:80 goals-node

### FRONT-END(React)
docker build -t goals-react .<br />
docker run --name goals-frontend --rm -p 3000:3000 -it goals-react
