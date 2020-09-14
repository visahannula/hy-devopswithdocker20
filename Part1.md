# DevOpswithDocker, Part 1
https://devopswithdocker.com/part1/

## Part 1.1 Getting started

- Run containers
```console
$ sudo docker run --name nginx1 -d nginx
521f1bc14c579352c384a87b4fa6fef5f5e10cb2621dabd722d387951d7d4424
$ sudo docker run --name nginx2 -d nginx
de55876601e95595658df862125fac3ddfaddc0a429e75c02e8fc2233b22fe62
$ sudo docker run --name nginx3 -d nginx
7c7c8103764bd8b48a29fdd95afe065a371bc1ae62b84fe0ac40f69453c4331b
```

- Check running containers
```console
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
7c7c8103764b        nginx               "/docker-entrypoint.…"   10 seconds ago      Up 9 seconds        80/tcp              nginx3
de55876601e9        nginx               "/docker-entrypoint.…"   14 seconds ago      Up 12 seconds       80/tcp              nginx2
521f1bc14c57        nginx               "/docker-entrypoint.…"   17 seconds ago      Up 16 seconds       80/tcp              nginx1
```

- Stop containers
```console
$ sudo docker container stop nginx2 nginx3
nginx2
nginx3
```

- **Check final result**
```console
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
7c7c8103764b        nginx               "/docker-entrypoint.…"   34 seconds ago      Exited (0) 3 seconds ago                       nginx3
de55876601e9        nginx               "/docker-entrypoint.…"   38 seconds ago      Exited (0) 3 seconds ago                       nginx2
521f1bc14c57        nginx               "/docker-entrypoint.…"   41 seconds ago      Up 40 seconds              80/tcp              nginx1
```

## Part 1.2 Cleanup

- Remove containers (forcefully)
```console
$ sudo docker rm -f nginx1 nginx2 nginx3
nginx1
nginx2
nginx3
```

- Check running containers
```console
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

- Check images
```console
$ sudo docker images
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
nginx                 latest              4bb46517cac3        10 days ago         133MB
```

- Remove images
```console
$ sudo docker rmi nginx
Untagged: nginx:latest
Untagged: nginx@sha256:b0ad43f7ee5edbc0effbc14645ae7055e21bc1973aee5150745632a24a752661
Deleted: sha256:4bb46517cac397bdb0bab6eba09b0e1f8e90ddd17cf99662997c3253531136f8
Deleted: sha256:80b21afd8140706d5fe3b7106ae6147e192e6490b402bf2dd2df5df6dac13db8
Deleted: sha256:0f04ae71e99f5ef9021b92f76bac3979e25c98d73a51d33ce76a78da6afa9f27
Deleted: sha256:9a14852344d88a1fdf8297914729834521ec1c77a27e7e7e394f9c1ef9b87f9d
Deleted: sha256:74299126f8099031c5bbd4774147f4ab6b0d0c3afcec774be65d4d07b956752e
Deleted: sha256:d0f104dc0a1f9c744b65b23b3fd4d4d3236b4656e67f776fe13f8ad8423b955c
```

- Check images
```console
$ sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

## 1.3 Hello Docker Hub

The secret password is **"basics"** and the message is **"This is the secret message"**. Password can be found from "index.js" line 35.

```console
$ sudo docker run -it devopsdockeruh/pull_exercise
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete
5e2195587d10: Pull complete
6f595b2fc66d: Pull complete
165f32bf4e94: Pull complete
67c4f504c224: Pull complete
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## 1.4

The secred message is **"Docker is easy"**. Message can be found in ways below:

```console
root@23a7a6512d10:/usr/app# cat Dockerfile
FROM node:14.4

ARG SECRET_MESSAGE
ENV SECRET_MESSAGE=$SECRET_MESSAGE

WORKDIR /usr/app
COPY . .

CMD ["node", "index"]
root@23a7a6512d10:/usr/app# echo $SECRET_MESSAGE
Docker is easy
```

```console
root@23a7a6512d10:/usr/app# tail -f logs.txt
Thu, 27 Aug 2020 20:14:00 GMT
Secret message is:
"Docker is easy"
Thu, 27 Aug 2020 20:14:06 GMT
Thu, 27 Aug 2020 20:14:09 GMT
Thu, 27 Aug 2020 20:14:12 GMT
Thu, 27 Aug 2020 20:14:15 GMT
Secret message is:
"Docker is easy"
Thu, 27 Aug 2020 20:14:21 GMT
Thu, 27 Aug 2020 20:14:24 GMT
Thu, 27 Aug 2020 20:14:27 GMT
^C
```

## 1.5

Example command to achieve results of the assignment:
```console
$ docker run -it ubuntu sh -c 'apt update && apt install curl; echo "Input website:"; read we
bsite; echo "Searching.."; sleep 1; curl http://$website;'
```

## 1.6

Create [Dockerfile](exercise_1.6/Dockerfile):
```Dockerfile
FROM devopsdockeruh/overwrite_cmd_exercise
CMD ["-c 0"]
```

Build image:
```console
$ sudo docker build -t docker-clock .
```

Run container:
```console
$ sudo docker run --rm docker-clock
1
2
3
4
5
6
7
```

## 1.7

* Create [script.sh](exercise_1.7/script.sh) file.
```sh
echo "Input website:";
read website;
echo "Searching..";
sleep 1;
curl http://$website;
```

* Create [Dockerfile](exercise_1.7/Dockerfile)
```Dockerfile
FROM ubuntu:16.04
COPY ./script.sh /
RUN apt-get update && apt-get install -y curl
CMD ["sh", "/script.sh"]
```


**Build image**

Build image and set name as "curler".
```console
$ sudo docker build --tag curler .
```
Output not shown since it gets and installs many packages.

* Check images
```console
$ sudo docker images
REPOSITORY                          TAG                 IMAGE ID            CREATED             SIZE
curler                              latest              9fd4b31df5d5        11 seconds ago      169MB
ubuntu                              16.04               4b22027ede29        12 days ago         127MB
ubuntu                              xenial              4b22027ede29        12 days ago         127MB
ubuntu                              latest              4e2eef94cd6b        12 days ago         73.9MB
```

* Run container
```console
$ docker run -it --rm curler
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>

--SNIP--
```

# 1.8

**Run**
```console
$ touch logs.txt
$ sudo docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise
```

**Check logfile**
```console
$ head -n 6 logs.txt
Thu, 03 Sep 2020 19:46:52 GMT
Thu, 03 Sep 2020 19:46:55 GMT
Thu, 03 Sep 2020 19:46:58 GMT
Thu, 03 Sep 2020 19:47:01 GMT
Secret message is:
"Volume bind mount is easy"
```

# 1.9

* Run

```console
$ sudo docker run -p 8088:80/tcp devopsdockeruh/ports_exercise

> ports_exercise@1.0.0 start /usr/app
> node index.js

Listening on port 80, this means inside of the container. Use -p to map the port to a port of your local machine.
```

* Check response from another terminal

```console
$ curl -i localhost:8088
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/html; charset=utf-8
Content-Length: 28
ETag: W/"1c-FlnMl0kiaW1T7+FukN6N5hGQtKM"
Date: Mon, 14 Sep 2020 20:55:15 GMT
Connection: keep-alive

Ports configured correctly!!
```

