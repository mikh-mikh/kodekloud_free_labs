# kodekloud free labs docker - docker registry

I can and I will. Watch me.

– Carrie Green

## 1 / 10

In this lab we will explore some concepts related to Docker Registry and also practice setting up our own simple registry server.

## 2 / 10
What is a Docker Registry?

right answer - "it is a storage and distribution system for named Docker images"

## 3 / 10
By default, the Docker engine interacts with ?

right answer - "DockerHub"

## 4 / 10
DockerHub is a hosted registry solution by Docker Inc.

Besides public and private repositories, it also provides:
automated builds,
integration with source control solutions like Github and Bitbucket etc.

## 5 / 10
Which command is used for Login to a self-hosted registry?

right answer - "docker login [SERVER]"

## 6 / 10

Let practice deploying a registry server on our own.
Run a registry server with name equals to my-registry using registry:2 image with host port set to 5000, and restart policy set to always.

Note: Registry server is exposed on port 5000 in the image.

Here we are hosting our own registry using the open source Docker Registry.
NOTE: You do not need to run docker login for this local registry setup because authentication is not configured. This registry allows for anonymous access.

Container Name: my-registry
Host Port: 5000
Image: registry:2
Restart Policy: always

```
~ ➜  docker run -d --restart=always  -p 5000:5000 --name my-registry registry:2

~ ➜  docker ps                                                                
CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS         PORTS                                       NAMES
b897b22a2d64   registry:2   "/entrypoint.sh /etc…"   8 seconds ago   Up 7 seconds   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp   my-registry
```

## 7 / 10

Now its time to push some images to our registry server. Let's push two images for now .i.e. nginx:latest and httpd:latest.
Note: Don't forget to pull them first.
To check the list of images pushed , use curl -X GET localhost:5000/v2/_catalog

Image nginx:latest pushed?
Image httpd:latest pushed?

```
~ ➜  docker pull nginx:latest
latest: Pulling from library/nginx
3da95a905ed5: Pull complete 
6c8e51cf0087: Pull complete 
9bbbd7ee45b7: Pull complete 
48670a58a68f: Pull complete 
ce7132063a56: Pull complete 
23e05839d684: Pull complete 
ee95256df030: Pull complete 
Digest: sha256:93230cd54060f497430c7a120e2347894846a81b6a5dd2110f7362c5423b4abc
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

~ ➜  docker pull httpd:latest            
latest: Pulling from library/httpd
3da95a905ed5: Already exists 
1a50d37c990c: Pull complete 
4f4fb700ef54: Pull complete 
365277d54dac: Pull complete 
d812016dda12: Pull complete 
816d153af128: Pull complete 
Digest: sha256:1ae8051591a5ded56e4a3d7399c423e940e8475ad0e5adb82e6e10893fe9b365
Status: Downloaded newer image for httpd:latest
docker.io/library/httpd:latest

~ ➜  docker tag nginx:latest localhost:5000/nginx:latest

~ ➜  docker tag httpd:latest localhost:5000/httpd:latest

~ ➜  docker push localhost:5000/httpd:latest            
The push refers to repository [localhost:5000/httpd]
f40e449f3eed: Pushed 
878f1432290d: Pushed 
29cc24402c05: Pushed 
5f70bf18a086: Pushed 
585be1c33ee0: Pushed 
1bb35e8b4de1: Pushed 
latest: digest: sha256:3879aca820eca410c49067b9cec91daf9af15440b72a9021d25877d01b6a147d size: 1572

~ ➜  docker push localhost:5000/nginx:latest
The push refers to repository [localhost:5000/nginx]
07eaefc6ebf2: Pushed 
de2ef8ceb76a: Pushed 
e6c40b7bdc83: Pushed 
f941308035cf: Pushed 
81a9d30670ec: Pushed 
1bf33238ab09: Pushed 
1bb35e8b4de1: Mounted from httpd 
latest: digest: sha256:ccde53834eab53e85b35526a647cdb714ea4521b1ddf5a07b5c8787298d13087 size: 1778

~ ➜  curl -X GET localhost:5000/v2/_catalog
{"repositories":["httpd","nginx"]}
```

кабанчики в загончике

## 8 / 10
Let's remove all the dangling images we have locally. Use docker image prune -a to remove them. How many images do we have now?
Note: Make sure we don't have any running containers except our registry-sever.
To get list of images use: docker image ls

```
~ ➜  docker images | wc -l                  
13

~ ➜  docker image prune -a                  
WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
Deleted Images:
untagged: redis:latest
untagged: redis@sha256:eadf354977d428e347d93046bb1a5569d701e8deb68f090215534a99dbcb23b9
deleted: sha256:590b81f2fea1af9798db4580a6299dafba020c2f5dc7d8d734663e7fa5299ca0
deleted: sha256:34091e3dcc5223209fe41f1ac689e012032858d081488c15137b8555d63b9818
deleted: sha256:c4609e7a6099bef7542d93d7b72da926542a48e5a1334d8cbdd014e723d03093
deleted: sha256:60a5ffcecb4cf73a6ab04a27740bae0122da7771482b784b48656ec7ca58b762
deleted: sha256:9588e7fd68e322f74150da182b43a865cdcdb7a815e596da2ed5eb72a5b94f23
deleted: sha256:4ab98545f740fb1eb1395a180fcf2e74f36a39cffa27b83ac35bf4f3f9f1b24b
deleted: sha256:2df51a972858377a46db224abba6b0ba780a81f9be25b0a1e55ba72ec15f6365
deleted: sha256:6a37f9e6c319837a554a53039ae0ace140c034812df571d9ddf864f446427cab
untagged: postgres:latest
---
deleted: sha256:edbfe74c41f8a3501ce542e137cf28ea04dd03e6df8c9d66519b6ad761c2598a
deleted: sha256:f36fd4bb7334b7ae3321e3229d103c4a3e7c10a263379cc6a058b977edfb46de

Total reclaimed space: 1.593GB

~ ➜  docker images        
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
registry     2         26b2eb03618e   21 months ago   25.4MB
```

right answer - "1"

## 9 / 10

Now we can pull images from our registry-server as well. Use docker pull [server-addr/image-name] to pull the images that we pushed earlier.
In our case we can use: docker pull localhost:5000/nginx

```
~ ➜  docker pull localhost:5000/nginx            
Using default tag: latest
latest: Pulling from nginx
d0b609e4bacb: Pull complete 
6c8e51cf0087: Pull complete 
9bbbd7ee45b7: Pull complete 
48670a58a68f: Pull complete 
ce7132063a56: Pull complete 
23e05839d684: Pull complete 
ee95256df030: Pull complete 
Digest: sha256:ccde53834eab53e85b35526a647cdb714ea4521b1ddf5a07b5c8787298d13087
Status: Downloaded newer image for localhost:5000/nginx:latest
localhost:5000/nginx:latest

~ ➜  docker pull localhost:5000/httpd
Using default tag: latest
latest: Pulling from httpd
d0b609e4bacb: Already exists 
1a50d37c990c: Pull complete 
4f4fb700ef54: Pull complete 
365277d54dac: Pull complete 
d812016dda12: Pull complete 
816d153af128: Pull complete 
Digest: sha256:3879aca820eca410c49067b9cec91daf9af15440b72a9021d25877d01b6a147d
Status: Downloaded newer image for localhost:5000/httpd:latest
localhost:5000/httpd:latest
```

## 10 / 10
Let's clean up after ourselves.
Stop and remove the my-registry container.

```
~ ➜  docker rm -f my-registry                                                 
my-registry

~ ➜  docker ps                       
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES 
```