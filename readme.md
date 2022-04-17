# Spin up docker containers steps

With docker-compose
`docker-compose up`

Withought docker-compose

## 1. Mongo db database

`docker run -d --rm --name mongodb --network goals-net -v data:/data/db -e MONGO_INITDB_ROOT_USERNAME=username -e MONGO_INITDB_ROOT_PASSWORD=pass mongo`

### Breakdown:

> docker run <br>
> -d detached mode <br>
> -rm remove container when stoped <br>
> --name mongodb <br>
> --network goals-net (to assign to a network) <br>
> -v data:/data/db (to persist data) <br>
> -e MONGO_INITDB_ROOT_USERNAME=username <br>
> -e MONGO_INITDB_ROOT_PASSWORD=pass <br>
> mongo (to call the mongo image)<br>

## 2. backend - Create image and run the container using the Dockerfile

### a. Build the image

`cd backend/`<br>
`docker build -t goals-node .`

#### Breakdown

> docker build<br>
> -t goals-node (assign a tag name)<br>
> . (current directory)

### b. Run the container

`docker run -p 80:80 --name goals-backend --network goals-net -d --rm -v /web/docker-practice/multi-01-starting-setup/backend:/app -v logs:/app/logs -v /app/node_modules -e MONGODB_USERNAME=username -e MONGODB_PASSWORD=pass goals-node`

#### Breakdown

> docker run <br>
> -p 80:80 (expose port outside of the container)<br>
> --name goals-backend<br>
> --network goals-net (to assign to a network) <br>
> -d detached mode <br>
> -rm remove container when stoped <br>
> -v /web/docker-practice/multi-01-starting-setup/backend:/app (write file changes to /app)<br>
> -v logs:/app/logs (persist logs)<br>
> -v /app/node_modules (do not ovewrite node_modules with host file empty node_modules folder)<br>
> -e MONGODB_USERNAME=username<br>
> -e MONGODB_PASSWORD=pass<br>
> goals-node (to call the node image)<br>

## 3. frontend - Create image and run the container using the Dockerfile

### a. Build the image

`cd frontend/`<br>
`docker build -t goals-react .`

#### Breakdown

> docker build<br>
> -t goals-react (assign a tag name)<br>
> . (current directory)

### b. Run the container

`docker run -p 3000:3000 --rm -it --name goals-frontend -v /web/docker-practice/multi-01-starting-setup/frontend/src:/app/src -v /app/node_modules goals-react`

#### Breakdown

> docker run<br>
> -p 3000:3000 (expose port outside of the container)<br>
> -rm remove container when stoped<br>
> -it interactive mode<br>
> --name goals-frontend<br>
> -v /web/docker-practice/multi-01-starting-setup/frontend/src:/app/src<br>
> -v /app/node_modules<br>
> goals-react (to call the node image)<br>
