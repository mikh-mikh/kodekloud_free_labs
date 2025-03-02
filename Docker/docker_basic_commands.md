# kodekloud free labs docker - docker basic commands

Practice as if you are the worst, Perform as if you are the best.

-

## 1 / 17
What is the version of Docker Server Engine running on the Host?

```
~ ➜  docker -v
Docker version 25.0.5, build d260a54c81efcc3f00fe67dee78c94b16c2f8692
```

right answer - "25.0.5"

## 2 / 17
How many containers are running on this host?

```
~ ➜  docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

right answer - "0"

## 3 / 17
How many images are available on this host?

```
~ ➜  docker images
REPOSITORY                      TAG       IMAGE ID       CREATED        SIZE
alpine                          latest    91ef0af61f39   5 months ago   7.79MB
nginx                           alpine    c7b4f26a7d93   6 months ago   43.2MB
nginx                           latest    39286ab8a5e1   6 months ago   188MB
postgres                        latest    b781f3a53e61   6 months ago   432MB
ubuntu                          latest    edbfe74c41f8   7 months ago   78MB
redis                           latest    590b81f2fea1   7 months ago   117MB
mysql                           latest    a82a8f162e18   7 months ago   586MB
kodekloud/simple-webapp-mysql   latest    129dd9f67367   6 years ago    96.6MB
kodekloud/simple-webapp         latest    c6e3cd9aae36   6 years ago    84.8MB
~ ➜  docker images | wc -l
10
```

right answer - "9"

## 4 / 17
Run a container using the redis image

```
~ ➜  docker run redis 
1:C 01 Mar 2025 18:07:23.799 * oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1:C 01 Mar 2025 18:07:23.799 * Redis version=7.4.0, bits=64, commit=00000000, modified=0, pid=1, just started
1:C 01 Mar 2025 18:07:23.799 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
1:M 01 Mar 2025 18:07:23.800 * monotonic clock: POSIX clock_gettime
1:M 01 Mar 2025 18:07:23.801 * Running mode=standalone, port=6379.
1:M 01 Mar 2025 18:07:23.802 * Server initialized
1:M 01 Mar 2025 18:07:23.802 * Ready to accept connections tcp
```

## 5 / 17
Stop the container you just created

press ztrl+c :)

## 6 / 17
How many containers are RUNNING on this host now?

```
~ ➜  docker ps            
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

right answer - "0"

## 7 / 17

How many containers are RUNNING on this host now?
We just created a few.

```
~ ➜  docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
5905d20ac63d   alpine         "sleep 1000"             22 seconds ago   Up 20 seconds             ecstatic_shannon
5cd23f6e7c6d   nginx:alpine   "/docker-entrypoint.…"   23 seconds ago   Up 21 seconds   80/tcp    nginx-2
17bdc8431724   nginx:alpine   "/docker-entrypoint.…"   25 seconds ago   Up 23 seconds   80/tcp    nginx-1
93c2fd79fc92   ubuntu         "sleep 1000"             26 seconds ago   Up 24 seconds             awesome_northcut

~ ➜  docker ps | wc -l
5

right answer - "4"

## 8 / 17

How many containers are PRESENT on the host now?
Including both Running and Not Running ones

```
~ ➜  docker ps -a | wc -l
7
```

right answer - "6"

## 9 / 17

What is the image used to run the nginx-1 container?

```
~ ➜  docker ps -a | grep nginx-1
17bdc8431724   nginx:alpine   "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes               80/tcp    nginx-1
```
экономим текст чтобы выполнить KPI по сокращению расходов на вывод символов в терминал (не делайте так я прикалываюсь)
```
~ ➜  docker ps -a | grep nginx-1 | awk '{print $2}'
nginx:alpine
```

right answer - "nginx:alpine"

## 10 / 17
What is the name of the container created using the ubuntu image?

```
docker ps -a | grep ubuntu                    
93c2fd79fc92   ubuntu         "sleep 1000"             8 minutes ago    Up 8 minutes                         awesome_northcut
```

right answer - "awesome_northcut"

## 11 / 17
What is the ID of the container that uses the alpine image and is not running?

```
~ ➜  docker ps -a | grep alpine       
76ce303a3c70   alpine         "/bin/sh"                14 minutes ago   Exited (0) 14 minutes ago             upbeat_goodall
5905d20ac63d   alpine         "sleep 1000"             14 minutes ago   Up 14 minutes                         ecstatic_shannon
5cd23f6e7c6d   nginx:alpine   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               80/tcp    nginx-2
17bdc8431724   nginx:alpine   "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               80/tcp    nginx-1
```
```
~ ➜  docker ps -a --no-trunc | grep alpine
76ce303a3c707945747eda1cd80491c69ea01f757bf6cc4762528c432d25ae2a   alpine         "/bin/sh"                                        18 minutes ago   Exited (0) 18 minutes ago                 upbeat_goodall
5905d20ac63d9d358e42ce323010966179596fafd765ea73233300635893299c   alpine         "sleep 1000"                                     18 minutes ago   Exited (0) About a minute ago             ecstatic_shannon
5cd23f6e7c6df956a4e1ee36b145d8762cc463811a1daebfc95b9006ed30d4b3   nginx:alpine   "/docker-entrypoint.sh nginx -g 'daemon off;'"   18 minutes ago   Up 18 minutes                   80/tcp    nginx-2
17bdc843172459d7a59d3796c57070310fba47848cbb44110344f9aee403815b   nginx:alpine   "/docker-entrypoint.sh nginx -g 'daemon off;'"   18 minutes ago   Up 18 minutes                   80/tcp    nginx-1
```

right answer - "76ce303a3c707945747eda1cd80491c69ea01f757bf6cc4762528c432d25ae2a"

## 12 / 17
What is the state of the stopped alpine container?

right answer - "Exited"

## 13 / 17

Delete all containers from the Docker Host.
Both Running and Not Running ones. Remember you may have to stop containers before deleting them.

```
~ ✖ docker rm -v -f $(docker ps -qa)
76ce303a3c70
5905d20ac63d
5cd23f6e7c6d
17bdc8431724
93c2fd79fc92
38ea28f5c8a6
~ ✖ docker ps -a                         
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## 14 / 17
Delete the ubuntu Image.

```
~ ➜  docker image rm ubuntu 
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:8a37d68f4f73ebf3d4efafbcf66379bf3728902a8038616808f04e34a9ab63ee
Deleted: sha256:edbfe74c41f8a3501ce542e137cf28ea04dd03e6df8c9d66519b6ad761c2598a
Deleted: sha256:f36fd4bb7334b7ae3321e3229d103c4a3e7c10a263379cc6a058b977edfb46de
```

## 15 / 17

You are required to pull a docker image which will be used to run a container later. Pull the image nginx:1.14-alpine
Only pull the image, do not create a container.

```
~ ➜  docker pull nginx:1.14-alpine
1.14-alpine: Pulling from library/nginx
bdf0201b3a05: Pull complete 
3d0a573c81ed: Pull complete 
8129faeb2eb6: Pull complete 
3dc99f571daf: Pull complete 
Digest: sha256:485b610fefec7ff6c463ced9623314a04ed67e3945b9c08d7e53a47f6d108dc7
Status: Downloaded newer image for nginx:1.14-alpine
docker.io/library/nginx:1.14-alpine

~ ➜  docker images | grep nginx   
nginx                           alpine        c7b4f26a7d93   6 months ago   43.2MB
nginx                           latest        39286ab8a5e1   6 months ago   188MB
nginx                           1.14-alpine   8a2fb25a19f5   5 years ago    16MB
```

## 16 / 17
Run a container with the nginx:1.14-alpine image and name it webapp

```
~ ➜  docker run --name=webapp nginx:1.14-alpine

## 17 / 17

Cleanup: Delete all images on the host
Remove containers as necessary

```
~ ➜  docker rm -v -f $(docker ps -qa)      
e35a92e78c00
4f7cdc263853
68b1a70c2f25
c01801e8c5be

~ ➜  docker rm -v -f $(docker ps -qa)

~ ✖ docker rmi -f $(docker images -aq)
Untagged: alpine:latest
Untagged: alpine@sha256:beefdbd8a1da6d2915566fde36db9db0b524eb737fc57cd1367effd16dc0d06d
Deleted: sha256:91ef0af61f39ece4d6710e465df5ed6ca12112358344fd51ae6a3b886634148b
Untagged: nginx:alpine
Untagged: nginx@sha256:a5127daff3d6f4606be3100a252419bfa84fd6ee5cd74d0feaca1a5068f97dcf
Deleted: sha256:c7b4f26a7d93f4f1f276c51adb03ef0df54a82de89f254a9aec5c18bf0e45ee9
Deleted: sha256:df45629925efee5af98c24cd09fa6eb06f53bf8a31eb6255e25efd729c902e1e
Deleted: sha256:e9d09343f346fd7a1ae6dde03c9d2a948dba60c99be0083f703c10acb691a29b
Deleted: sha256:96e2f7e5b1089cb71e9d94d9674deaeeb39e6d1f7e988daf9c56eaff124ec56d
Deleted: sha256:2623c1762532f09221eb40e4ab51f7ead353946407f9c79ba2d95733438a2ae2
Deleted: sha256:171ed8c2c65615bfa0a7cc81c114daadd52280d027663767b20777dbfe3c39ef
Deleted: sha256:dce3a61c1de2c34ccdab8af349ba2cdc64bfb6c56591e672a04d9cdc52637e4e
Deleted: sha256:a5bb40ea103b2ce0b5593487f519ec2754b12b2437f4b1e28fc6727b141e7a46
Deleted: sha256:63ca1fbb43ae5034640e5e6cb3e083e05c290072c5366fcaa9d62435a4cced85
Untagged: nginx:latest
Untagged: nginx@sha256:04ba374043ccd2fc5c593885c0eacddebabd5ca375f9323666f28dfd5a9710e3
Deleted: sha256:39286ab8a5e14aeaf5fdd6e2fac76e0c8d31a0c07224f0ee5e6be502f12e93f3
Deleted: sha256:d71f9b66dd3f9ef3164d7023cc99ce344d209decd5d6cd56166c0f7a2f812c06
```