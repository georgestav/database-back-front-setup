# Spin up docker containers steps
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)

Includes a simple CRUD app to test everything out before moving on

With docker-compose: 
`docker-compose up`

Withought docker-compose:

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
