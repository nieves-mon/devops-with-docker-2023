# Part 2

## Exercise 2.1
### docker-compose.yml
```
version: '3.9'

services:
    simple-web-service:
        image: devopsdockeruh/simple-web-service
        volumes:
            - ./text.log:/usr/src/app/text.log
        container_name: simple-web-service
```
### text.log
```
2023-03-12 14:02:50 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
2023-03-12 14:02:52 +0000 UTC
```

## Exercise 2.2
### docker-compose.yml
```
version: '3.9'

services:
    simple-web-service:
        image: devopsdockeruh/simple-web-service
        build: .
        ports:
            - 8080:8080
        command: server
        container_name: simple-web-service
```
### Output
![exercise_2 2](https://user-images.githubusercontent.com/88223950/224550439-cd1fdea8-ae1c-48ac-9486-3912f9c86f82.png)

## Exercise 2.3
### docker-compose.yml
```
version: '3.9'

services:
    hello-frontend:
        build: ./example-frontend
        ports:
            - 5000:5000

    hello-backend:
        build: ./example-backend
        ports:
            - 8080:8080
```

## Exercise 2.4
### docker-compose.yml
```
version: '3.9'

services:
    hello-frontend:
        build: ./example-frontend
        ports:
            - 5000:5000

    hello-backend:
        build: ./example-backend
        ports:
            - 8080:8080
        environment:
            - REDIS_HOST=redis

    redis:
        image: redis:7.0.9-alpine
        restart: unless-stopped
        container_name: redis
```
### Output
![exercise_2 4](https://user-images.githubusercontent.com/88223950/224551738-7237528e-747b-4fa6-a09b-bd0e4b814d74.png)

## Exercise 2.5
### Commands
```
$ docker compose up --scale compute=2
```
### Output
![exercse_2 5](https://user-images.githubusercontent.com/88223950/224554388-b23d0b9f-4ed8-43e0-9219-7afe325e7b9d.png)

## Exercise 2.6
### docker-compose.yml
```
version: '3.9'

services:
    hello-frontend:
        build: ./example-frontend
        ports:
            - 5000:5000

    hello-backend:
        build: ./example-backend
        ports:
            - 8080:8080
        environment:
            - REDIS_HOST=redis
            - POSTGRES_HOST=db
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=postgres
            - POSTGRES_DATABASE=postgres
        depends_on:
            - db

    db:
        image: postgres:15.2-alpine
        environment:
            - POSTGRES_PASSWORD=postgres

    redis:
        image: redis:7.0.9-alpine
        restart: unless-stopped
        container_name: redis
```
### Output
![exercise_2 6](https://user-images.githubusercontent.com/88223950/224556609-7134df98-5e84-4c81-b8bd-21931539f347.png)

## Exercise 2.7
### docker-compose.yml
```
version: '3.9'

services:
    hello-frontend:
        build: ./example-frontend
        ports:
            - 5000:5000

    hello-backend:
        build: ./example-backend
        ports:
            - 8080:8080
        environment:
            - REDIS_HOST=redis
            - POSTGRES_HOST=db
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=postgres
            - POSTGRES_DATABASE=postgres
        depends_on:
            - db

    db:
        image: postgres:15.2-alpine
        environment:
            - POSTGRES_PASSWORD=postgres
        volumes:
            - ./database:/var/lib/postgresql/data

    redis:
        image: redis:7.0.9-alpine
        restart: unless-stopped
        container_name: redis

volumes:
    database:
```

## Exercise 2.8


## Exercise 2.9


## Exercise 2.10


## Exercise 2.11
