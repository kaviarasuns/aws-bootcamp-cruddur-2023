# Week 1 — App Containerization

https://code.visualstudio.com/docs/containers/overview

> Gitpod is preinstalled with theis extension

** Containerize Backend

*** Run Python

---sh
cd backend-flask
export FRONTEND_URL="**
export BACKEND_URL="*"
python3 -m flask run--host-0.0.0.0 --port-4567
cd . .
---

- make sure to unlock the port on the port tab
- open the link for 4567 in your browser
- change the url to '/api/activities/home'
- you should get back json



### Build Container

```
docker build -t backend-flask ./backend-flask


docker build -t frontend-react-js ./frontend-react-js
```

### Run Container

# Run 

```
docker run --rm -p 4567:4567 -it backend-flask

docker run --rm -p 3000:3000 -it frontend-react-js
```


// below command is working
```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
```

docker run --rm -p 4567:4567 -it backend-flask -e FRONTEND_URL -e BACKEND_URL

Run in background

docker container run --rm -p 4567:4567 -d backend-flaskl


### Docker Compose


### Adding DynamoDB Local and Postgres

We are going to use Postgres and DynamoDB local in future labs. We can bring them in as container and reference them externally

Lets integrate the following into our existing docker compose file:

## Postgres

```
services:
    db:
        image: postgres:13-alpine
        restart: always
        environment:
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=password
        ports:
            - '5432-5432'
        volumes:
            - db:/var/lib/postgres/data
    volumes:
        db:
            driver: local
```

DynamoDB Local

```
services:
    dynamodb-local:
    # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
    # We need to add user::root to get this working
    user: root
    command: "-jar DynamoDBLocal.jar -shareDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
        - "8000:8000"
    volumes:
        - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
```

### Volumes

directory volume mapping

```
- "./docker/dynamodb:/home/dynamodblocal/data"
