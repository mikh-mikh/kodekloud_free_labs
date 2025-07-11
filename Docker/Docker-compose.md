## 1 / 5

First create a redis database container called redis, image redis:alpine.
if you are unsure, check the hints section for the exact commands.

"redis" container running?

```
~ ➜  docker run -d --name=redis redis:alpine
Unable to find image 'redis:alpine' locally
alpine: Pulling from library/redis
f18232174bc9: Pull complete 
10753f8102ef: Pull complete 
a9c51c568321: Pull complete 
b96ac5b0d90b: Pull complete 
3b985785c0a3: Pull complete 
4f4fb700ef54: Pull complete 
6b9706545272: Pull complete 
Digest: sha256:73734b014e53b3067916918b70718ca188c16895511a272a020c9a71084eecda
Status: Downloaded newer image for redis:alpine
706edcb336f6432506fb03b044c82f95972d7f80db7db7997adad11f46d9c7f2

~ ➜  docker ps                              
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS      NAMES
706edcb336f6   redis:alpine   "docker-entrypoint.s…"   6 seconds ago   Up 4 seconds   6379/tcp   redis
```

## 2 / 5

Next, create a simple container called clickcounter with the image kodekloud/click-counter, link it to the redis container that we created in the previous task and then expose it on the host port 8085
The clickcounter app run on port 5000.
if you are unsure, check the hints section for the exact commands.

clickcounter exposed on the correct HostPort?
clickcounter linked to the redis container ?

```
~ ➜  docker run -d --name=clickcounter -p 8085:5000 --link redis kodekloud/click-counter
Unable to find image 'kodekloud/click-counter:latest' locally
latest: Pulling from kodekloud/click-counter
540db60ca938: Pull complete 
a7ad1a75a999: Pull complete 
37ce6546d5dd: Pull complete 
ec9e91bed5a2: Pull complete 
767433e10bb0: Pull complete 
156f0b0493cb: Pull complete 
3fe82d8a2401: Pull complete 
4a41f7c94204: Pull complete 
473063430a4f: Pull complete 
452c68a16ccd: Pull complete 
Digest: sha256:530e4532a718e8f5cbda05844a6c0638ebe8898fa4c4307ee6afbdd5d1f213db
Status: Downloaded newer image for kodekloud/click-counter:latest
14f8829224925ac8e1add686becef4b17e122c80a4afee7d00de6e0c1f1b0964

~ ➜  docker ps                                                                          
CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS          PORTS                                       NAMES
14f882922492   kodekloud/click-counter   "flask run"              18 seconds ago   Up 17 seconds   0.0.0.0:8085->5000/tcp, :::8085->5000/tcp   clickcounter
706edcb336f6   redis:alpine              "docker-entrypoint.s…"   2 minutes ago    Up 2 minutes    6379/tcp
```

## 3 / 5

You can now access this application using the Click-Counter tab above the terminal.
Refresh the page and see the count increase.

```
~ ➜  curl 127.0.0.1:8085
CLICK COUNTER! Refresh to see the count increase!

CLICK COUNT: 3

~ ➜  curl 127.0.0.1:8085
CLICK COUNTER! Refresh to see the count increase!

CLICK COUNT: 4
```

## 4 / 5

Let's clean up the actions carried out in previous steps. Delete the redis and the clickcounter containers.

clickcounter container deleted?
redis container deleted?

```
~ ➜  docker rm -f redis clickcounter                                                    
redis
clickcounter
```

## 5 / 5

Create a docker-compose.yml file under the directory /root/clickcounter. Once done, run docker-compose up.
The compose file should have the exact specification as follows -
redis service specification - Image name should be redis:alpine.
clickcounter service specification - Image name should be kodekloud/click-counter, app is run on port 5000 and expose it on the host port 8085 in the compose file.

syntax check for the docker-compose.yml
clickcounter running on the correct HostPort?
clickcounter webpage working correctly?

docker-compose.yml:
```
version: "3"
services:
  redis:
    image: "redis:alpine"
    container_name: redis
  clickcounter:
    image: "kodekloud/click-counter"
    container_name: clickcounter
    ports: 
      - 8085:5000
    links: 
      - redis
	  
```

```
~/clickcounter ✖ docker-compose up -d
[+] Running 2/2
 ✔ Container redis         Started                                                                         0.9s 
 ✔ Container clickcounter  Started                                                                         2.0s 

~/clickcounter ➜  cat docker-compose.yml 
version: "3"
services:
  redis:
    image: "redis:alpine"
    container_name: redis
  clickcounter:
    image: "kodekloud/click-counter"
    container_name: clickcounter
    ports: 
      - 8085:5000
    links: 
      - redis

~/clickcounter ➜  curl 127.0.0.1:8085
CLICK COUNTER! Refresh to see the count increase!

CLICK COUNT: 1

~/clickcounter ➜  curl 127.0.0.1:8085
CLICK COUNTER! Refresh to see the count increase!
 
CLICK COUNT: 2
```

