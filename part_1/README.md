# Part 1

## Exercise 1.1: GETTING STARTED
```
$ docker ps -a
```
![exercise_1 1](https://user-images.githubusercontent.com/88223950/224532420-076f1063-4b72-4ce5-846f-4179c0a9998d.png)


## Exercises 1.2: CLEANUP
![exercises_1 2](https://user-images.githubusercontent.com/88223950/224532449-92db526f-78fc-468e-87de-23125f342753.png)


## Exercise 1.3: SECRET MESSAGE
```
$ docker run -d devopsdockeruh/simple-web-service:ubuntu
3d91577d1b5bfc82c191258ab3bacd311c7efc6fd7fad3595ffc458bda31a4bf

$ docker exec -it 3d /bin/bash
root@3d91577d1b5b:/usr/src/app# tail -f ./text.log
2023-03-12 08:13:43 +0000 UTC
2023-03-12 08:13:45 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
2023-03-12 08:13:47 +0000 UTC
```

## Exercise 1.4: MISSING DEPENDENCIES
```
$ docker run -it ubuntu sh -c 'while true; do echo; "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website; done'

Input website:
helsinki.fi
Searching..
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.20.1</center>
</body>
</html>
```
### Command in different terminal before inputting website
```
$ docker exec -it 18 /bin/bash

root@18c17e6a3011:/# apt-get update
Get:1 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
...
Reading package lists... Done

root@18c17e6a3011:/# apt-get install curl
Reading package lists... Done
...
done.
```

## Exercise 1.5: SIZES OF IMAGES
```
$ docker images
```
![exercise_1 5](https://user-images.githubusercontent.com/88223950/224533224-1919e685-9e0b-48a8-bf29-c1ff24c1ba65.png)
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

## Exercise 1.6: HELLO DOCKER HUB
```
$ docker run -it devopsdockeruh/pull_exercise

Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## Exercise 1.7: IMAGE FOR SCRIPT
### Dockerfile
```
FROM ubuntu:20.04

WORKDIR /usr/src/app

RUN apt-get -y update && apt-get -y install curl

COPY search_website.sh .

RUN chmod +x search_website.sh

CMD ./search_website.sh
```

## Exercise 1.8: TWO LINE DOCKERFILE
### Dockerfile
```
FROM devopsdockeruh/simple-web-service:alpine

CMD server
```
### Commands
```
$ docker build . -t web-server
$ docker run web-server
```

## Exercise 1.9: VOLUMES
### Commands
```
$ touch text.log
$ docker run -v "$(pwd)/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service
```
### Output
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

## Exercise 1.10: PORTS OPEN
```
docker run -p 8080:8080 devopsdockeruh/simple-web-service ser server
```
![exercise_1 10](https://user-images.githubusercontent.com/88223950/224533649-13bb4f9b-d77d-4c40-afa0-0848595b1e8a.png)

## Exercise 1.11: SPRING
### Dockerfile
```
FROM openjdk:8

WORKDIR /usr/src/app

COPY . .

RUN ./mvnw package

CMD ["java", "-jar", "./target/docker-example-1.1.3.jar"]

EXPOSE 8080
```
### Output
![exercise_1 11](https://user-images.githubusercontent.com/88223950/224543841-ffb867fd-8a5f-4b5b-8c52-f36d65fe7a24.png)

## Exercise 1.12: HELLO, FRONTEND!
### Dockerfile
```
FROM node:14-alpine

WORKDIR /usr/src/app

COPY . .

RUN npm install && npm run build && npm install -g serve

CMD ["serve", "-s", "-l", "5000", "build"]

EXPOSE 5000
```
### Commands
```
$ docker build . -t example-frontend
$ docker run -p 5000:5000 example-frontend
```

## Exercise 1.13: HELLO, BACKEND!
### Dockerfile
```
FROM golang:1.16

WORKDIR /usr/src/app

COPY . .

RUN go build

ENV PORT 8080
ENV REQUEST_ORIGIN https://example.com

CMD ["./server"]

EXPOSE 8080
```
### Commands
```
$ docker build . -t example-backend
$ docker run -p 8080:8080 example-backend
```
![exercise_1 13](https://user-images.githubusercontent.com/88223950/224546461-9fd36fa3-aeb2-45d9-8fac-cdb14db226f8.png)


## Exercise 1.14: ENVIRONMENT
### Dockerfile (example-frontend)
```
FROM node:14-alpine

WORKDIR /usr/src/app

COPY . .

ENV REACT_APP_BACKEND_URL http://localhost:8080/

RUN npm install && npm run build && npm install -g serve

CMD ["serve", "-s", "-l", "5000", "build"]

EXPOSE 5000
```
### Dockerfile (example-backend)
```
FROM golang:1.16

WORKDIR /usr/src/app

COPY . .

RUN go build

ENV PORT 8080
ENV REQUEST_ORIGIN http://localhost:5000

CMD ["./server"]

EXPOSE 8080
```
### Commands
```
$ docker build . -t example-frontend
$ docker build . -t example-backend
$ docker run -p 5000:5000 example-frontend
$ docker run -p 8080:8080 example-backend
```
![exercise_1 14](https://user-images.githubusercontent.com/88223950/224548209-29e6ede2-7490-4f9b-81a1-a77419b5abae.png)

## Exercise 1.15: HOMEWORK


## Exercise 1.16: CLOUD DEPLOYMENT
