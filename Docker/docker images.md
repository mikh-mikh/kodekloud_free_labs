# kodekloud free labs docker - docker images

Do the best you can. No one can do more than that.

– John Wooden

## 1 / 15
How many images are available on this host?

```
~ ➜  docker images | wc -l
10
```

right answer - "9"


## 2 / 15
What is the size of the ubuntu image?

```
~ ✖ docker images | grep ubuntu
ubuntu                          latest    edbfe74c41f8   11 months ago   78MB
```

right answer - "78MB"

## 3 / 15
We just pulled a new image. What is the tag on the newly pulled NGINX image?

```
~ ➜  docker images             
REPOSITORY                      TAG           IMAGE ID       CREATED         SIZE
alpine                          latest        91ef0af61f39   10 months ago   7.79MB
nginx                           alpine        c7b4f26a7d93   10 months ago   43.2MB
nginx                           latest        39286ab8a5e1   10 months ago   188MB
postgres                        latest        b781f3a53e61   11 months ago   432MB
ubuntu                          latest        edbfe74c41f8   11 months ago   78MB
redis                           latest        590b81f2fea1   11 months ago   117MB
mysql                           latest        a82a8f162e18   11 months ago   586MB
nginx                           1.14-alpine   8a2fb25a19f5   6 years ago     16MB
kodekloud/simple-webapp-mysql   latest        129dd9f67367   6 years ago     96.6MB
kodekloud/simple-webapp         latest        c6e3cd9aae36   6 years ago     84.8MB
```

right answer - "1.14-alpine" (there is not been presented on previous steps)

## 4 / 15
We just downloaded the code of an application. What is the base image used in the Dockerfile?

Inspect the Dockerfile in the webapp-color directory.

```
~ ➜  cat webapp-color/Dockerfile 
FROM python:3.6

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python", "app.py"]
```

right answer - "python:3.6"


## 5 / 15
To what location within the container is the application code copied to during a Docker build?

Inspect the Dockerfile in the webapp-color directory.

right answer - "/opt"

## 6 / 15
When a container is created using the image built with this Dockerfile, what is the command used to RUN the application inside it.

Inspect the Dockerfile in the webapp-color directory.

right answer - "python app.py"

## 7 / 15
What port is the web application run within the container?

Inspect the Dockerfile in the webapp-color directory.

right answer - "8080"

## 8 / 15
Build a docker image using the Dockerfile and name it webapp-color. No tag to be specified.

```
~/webapp-color via 🐍 ✖ docker build --tag=webapp-color .
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            BuildKit is currently disabled; enable it by removing the DOCKER_BUILDKIT=0
            environment-variable.

Sending build context to Docker daemon  8.704kB
Step 1/6 : FROM python:3.6
3.6: Pulling from library/python
0e29546d541c: Pull complete 
9b829c73b52b: Pull complete 
cb5b7ae36172: Pull complete 
- - - -
Step 6/6 : ENTRYPOINT ["python", "app.py"]
 ---> Running in 1a36d4362924
 ---> Removed intermediate container 1a36d4362924
 ---> 3c6a36fb564b
Successfully built 3c6a36fb564b
Successfully tagged webapp-color:latest

```
## 9 / 15
Run an instance of the image webapp-color and publish port 8080 on the container to 8282 on the host.

Container with image 'webapp-color'
Container Port: 8080
Host Port: 8282

```
~/webapp-color via 🐍 ➜  docker run -d -p 8282:8080 webapp-color
acd240bb006ae2c5a55ae159285ea3d0b728f347f1b2ce9af67d6dd9bb708586

~/webapp-color via 🐍 ➜  docker ps                              
CONTAINER ID   IMAGE          COMMAND           CREATED         STATUS         PORTS                                       NAMES
acd240bb006a   webapp-color   "python app.py"   5 seconds ago   Up 4 seconds   0.0.0.0:8282->8080/tcp, :::8282->8080/tcp   busy_sanderson
```
## 10 / 15
Access the application by clicking on the tab named HOST:8282 above your terminal.
After you are done, you may stop the running container by hitting CTRL + C if you wish to.
здрар я ваша тетя - а зачем же я контейнер с фоне запускал то чтоб его стопать ага

```
~/webapp-color via 🐍 ✖ curl 127.0.0.1:8282
<!doctype html>
<title>Hello from Flask</title>
<body style="background: #e74c3c;"></body>
<div style="color: #e4e4e4;
    text-align:  center;
    height: 90px;
    vertical-align:  middle;">

  <h1>Hello from acd240bb006a!</h1>


  

</div>#
```

чет есть

## 11 / 15
What is the base Operating System used by the python:3.6 image?

If required, run an instance of the image to figure it out.

```
~/webapp-color via 🐍 ➜  docker images | grep python
python
```
здоровый кабан
```
~ ➜  docker run -it python:3.6 bash
root@24147aaeb6be:/# cat /etc/os-release 
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
```

right answer - "debian"
эмоджи в виде среза имитации крабовой палочки из говяжьего дошика в коробочке

## 12 / 15
What is the approximate size of the webapp-color image?

```
~ ✖ docker images | grep webapp-color   
webapp-color                    latest        3c6a36fb564b   26 minutes ago   913MB
```

right answer - "920MB" (не спрашивайте)

## 13 / 15
That's really BIG for a Docker Image. Docker images are supposed to be small and light weight. Let us try to trim it down.

да да давайте сварим холодец из живого кабана

## 14 / 15
Build a new smaller docker image by modifying the same Dockerfile and name it webapp-color and tag it lite.
Hint: Find a smaller base image for python:3.6. Make sure the final image is less than 150MB.

Name: webapp-color:lite
Image size less than 150MB.

А мне мама говорила - что альпайн это сила!

```
cd webapp-color
sed 's/python:3.6/python:3.6-alpine/g' Dockerfile
~/webapp-color via 🐍 ✖ docker build --tag=webapp-color:lite .
```
```
~/webapp-color via 🐍 ➜  docker images | grep webapp
webapp-color                    lite          c9dccd5a01b5   2 minutes ago    51.9MB
webapp-color                    latest        3c6a36fb564b   38 minutes ago   913MB
```

кабан выжил


## 15 / 15
Run an instance of the new image webapp-color:lite and publish port 8080 on the container to 8383 on the host.

Container with image 'webapp-color:lite'
Container to publish port 8080 to 8383

```
~/webapp-color via 🐍 ➜  docker run -d -p 8383:8080 webapp-color:lite
17418cb99800a28d267e12df596c57ca3a10677520a4939ed6c8b80599cc056d

~/webapp-color ➜  curl 127.0.0.1:8382                         
<!doctype html>
<title>Hello from Flask</title>
<body style="background: #130f40;"></body>
<div style="color: #e4e4e4;
    text-align:  center;
    height: 90px;
    vertical-align:  middle;">

  <h1>Hello from 0b43460e7d33!</h1>


  

</div>
```

работает