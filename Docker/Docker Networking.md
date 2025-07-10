# 

For success attitude is equally important as ability.

– Harry F.Bank

## 1 / 9
Explore the current setup and identify the number of networks that exist on this system.

```
~ ➜  docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
861de7a6727a   bridge    bridge    local
a9ddd20e58a2   host      host      local
38672f05baf9   none      null      local
```

right answer - "3"

## 2 / 9
What is the ID associated with the bridge network?

```
~ ➜  docker network inspect 861de7a6727a 
[
    {
        "Name": "bridge",
        "Id": "861de7a6727a007fbb01d67ddde9f3ad9a0381b6509c19484432b4a2ccf03913",
        "Created": "2025-07-10T09:59:44.696007948Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.12.0.0/24",
                    "Gateway": "172.12.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```

right answer - "861de7a6727a007fbb01d67ddde9f3ad9a0381b6509c19484432b4a2ccf03913"

## 3 / 9
We just ran a container named alpine-1. Identify the network it is attached to.

```
~ ➜  docker ps -a                       
CONTAINER ID   IMAGE     COMMAND        CREATED          STATUS          PORTS     NAMES
1170d99092b6   alpine    "sleep 1000"   45 seconds ago   Up 44 seconds             alpine-1

~ ➜ docker container inspect 1170d99092b6 | grep Network
            "NetworkMode": "host",
        "NetworkSettings": {
            "Networks": {
                    "NetworkID": "a9ddd20e58a296eb7739da0c571e8bf1ed78beb32306f2230c9eaf16e90077f5",
```					

right answer - "host"

## 4 / 9
What is the subnet configured on bridge network?

```
~ ➜ docker network ls                                   
NETWORK ID     NAME      DRIVER    SCOPE
861de7a6727a   bridge    bridge    local
a9ddd20e58a2   host      host      local
38672f05baf9   none      null      local

~ ➜  docker network inspect 861de7a6727a | grep Subnet
                    "Subnet": "172.12.0.0/24",
```

right answer - "172.12.0.0/24"

## 5 / 9
Run a container named alpine-2 using the alpine image and attach it to the none network.

Name: alpine-2 attached to none network

```
~ ➜ docker run -d --name=alpine-2 --network=none alpine 
2dd1078e825769313869c646b4d36ab30aa683ce810fff69a1226e76a2b7ea9a

~ ➜  docker ps -a                                       
CONTAINER ID   IMAGE     COMMAND        CREATED         STATUS                     PORTS     NAMES
2dd1078e8257   alpine    "/bin/sh"      7 seconds ago   Exited (0) 6 seconds ago             alpine-2
1170d99092b6   alpine    "sleep 1000"   8 minutes ago   Up 8 minutes                         alpine-1

~ ➜  docker container inspect 2dd1078e8257 | grep Network
            "NetworkMode": "none",
        "NetworkSettings": {
            "Networks": {
                    "NetworkID": "38672f05baf980d5744c3e05791f960d9f7f51ff9c75046dd4da0a714741b583",
```

## 6 / 9
Create a new network named wp-mysql-network using the bridge driver. Allocate subnet 182.18.0.0/24. Configure Gateway 182.18.0.1

Name: wp-mysql-network
Driver: bridge
subnet: 182.18.0.0/24
Gateway: 182.18.0.1

```
~ ➜ docker network create --driver=bridge --subnet=182.18.0.0/24 --gateway=182.18.0.1 wp-mysql-network
ee2d27e1ad5fcd4d09910a79006cc1e3f2720a3c232ac3e69aa0a24db5f39f88
```

## 7 / 9
Deploy a mysql database using the mysql:5.7 image and name it mysql-db. Attach it to the newly created network wp-mysql-network
Set the database password to use db_pass123. The environment variable to set is MYSQL_ROOT_PASSWORD.

Name: mysql-db
Image: mysql:5.7
Env: MYSQL_ROOT_PASSWORD=db_pass123
Network: wp-mysql-network

```
~ ➜  docker run -d --name=mysql-db --env MYSQL_ROOT_PASSWORD=db_pass123 --network=wp-mysql-network mysql:5.7
Unable to find image 'mysql:5.7' locally
5.7: Pulling from library/mysql
20e4dcae4c69: Pull complete 
1c56c3d4ce74: Pull complete 
e9f03a1c24ce: Pull complete 
68c3898c2015: Pull complete 
6b95a940e7b6: Pull complete 
90986bb8de6e: Pull complete 
ae71319cb779: Pull complete 
ffc89e9dfd88: Pull complete 
43d05e938198: Pull complete 
064b2d298fba: Pull complete 
df9a4d85569b: Pull complete 
Digest: sha256:4bc6bc963e6d8443453676cae56536f4b8156d78bae03c0145cbe47c2aad73bb
Status: Downloaded newer image for mysql:5.7
aaac60ecaed274773fbb0124ad4cf76ceff2ed8a6cd2f4d9e57dd4a3405658f3

~ ➜  docker ps                                                                                              
CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS          PORTS                 NAMES
aaac60ecaed2   mysql:5.7   "docker-entrypoint.s…"   18 seconds ago   Up 16 seconds   3306/tcp, 33060/tcp   mysql-db

~ ➜  docker container inspect aaac60ecaed2| grep Network 
            "NetworkMode": "wp-mysql-network",
        "NetworkSettings": {
            "Networks": {
                    "NetworkID": "ee2d27e1ad5fcd4d09910a79006cc1e3f2720a3c232ac3e69aa0a24db5f39f88",
```

автокомплаит на zsh говно - у них на тачках тормозит глючит не дописывает созданные мной сетки из докера. наверное избыточен 

## 8 / 9

Deploy a web application named webapp using the kodekloud/simple-webapp-mysql image.
Expose the container’s port 8080 to port 38080 on the host.

The application makes use of two environment variable:
1: DB_Host with the value mysql-db.
2: DB_Password with the value db_pass123.
Make sure to attach it to the newly created network called wp-mysql-network.


Also make sure to link the MySQL and the webapp container.

Name: webapp
Image: kodekloud/simple-webapp-mysql
Env: DB_Host=mysql-db
Env: DB_Password=db_pass123
Network: wp-mysql-network
Is the container's port 8080 exposed?
Is the container using port 38080 on the host?

```
~ ➜  docker run -d --name=webapp --env DB_Host=mysql-db --env DB_Password=db_pass123 -p 38080:8080 --network=wp-mysql-network kodekloud/simple-webapp-mysql
e89babe06e0c94e46ef75efb45284ea83cdceb11dd604931b51a617040c333ad

~ ➜  docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                                         NAMES
e89babe06e0c   kodekloud/simple-webapp-mysql   "/bin/sh -c 'python …"   5 seconds ago   Up 4 seconds   0.0.0.0:38080->8080/tcp, :::38080->8080/tcp   webapp
aaac60ecaed2   mysql:5.7                       "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes   3306/tcp, 33060/tcp                           mysql-db
```

## 9 / 9
If you are successfull, you should be able to view the application by clicking on the HOST:38080 at the top of your terminal. You should see a green success message.

меня родили в лифте без кнопок:

```
~ ➜  curl 127.0.0.1:38080
<!doctype html>
<title>Hello from Flask</title>
<body style="background: #39b54b;"></body>
<div style="color: #e4e4e4;
    text-align:  center;
    height: 90px;
    vertical-align:  middle;">

  
    <img src="/static/img/success.jpg">
    <h3> Successfully connected to the MySQL database.</h3>
  

  
    <h2> Environment Variables: DB_Host=mysql-db; DB_Database=Not Set; DB_User=Not Set; DB_Password=db_pass123;  </h2>
  

  
    <p> From e89babe06e0c!</p>
  

  

</div>#
```

чет есть

CONGRATULATIONS!!!!
You have successfully completed the challenge.