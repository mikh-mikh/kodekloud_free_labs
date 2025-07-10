# kodekloud free labs Docker - Docker run

You don’t understand anything until you learn it more than one way.

– Marvin Minsky

## 1 / 6
Let us first inspect the environment. How many containers are running on this host?

```
~ ➜  docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                                                                NAMES
6d2890c4f634   nginx:alpine   "/docker-entrypoint.…"   19 seconds ago   Up 18 seconds   0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp   gracious_hamilton
```

right answer - "1"

## 2 / 6
What is the image used by the container?

right answer - "nginx:alpine"

## 3 / 6
How many unique ports are published on this container (count each port only once even if it appears for IPv4 and IPv6)?

right answer - "2"

## 4 / 6
Which of the following ports are mapped on the container side (i.e., exposed inside the container)?

right answer - "3456 & 80"

## 5 / 6
Which of the below ports are published on Host?

right answer - "3456 & 38080"

## 6 / 6
Run an instance of kodekloud/simple-webapp:blue and name the container blue-app, mapping port 8080 on the container to port 38282 on the host

Is the blue-app container running?
Is the blue-app utilizing the image: kodekloud/simple-webapp:blue?
Is the application exposed on Container Port 8080?
Is the application exposed on Host Port 38282?

```
~ ➜  docker run -d --name=blue-app -p 38282:8080 kodekloud/simple-webapp:blue
cd6440112ea7b4bc64d2d8b1b5639adac5f19061538ea0ea274c6d42b7d2fe45

~ ➜  docker ps                                                               
CONTAINER ID   IMAGE                          COMMAND                  CREATED          STATUS          PORTS                                                                                NAMES
cd6440112ea7   kodekloud/simple-webapp:blue   "python app.py"          6 seconds ago    Up 5 seconds    0.0.0.0:38282->8080/tcp, :::38282->8080/tcp                                          blue-app
6d2890c4f634   nginx:alpine                   "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes   0.0.0.0:3456->3456/tcp, :::3456->3456/tcp, 0.0.0.0:38080->80/tcp, :::38080->80/tcp   gracious_hamilton
~ ➜  curl 127.0.0.1:38282
<!doctype html>
<title>Hello from Flask</title>
<body style="background: #2980b9;"></body>
<div style="color: #e4e4e4;
    text-align:  center;
    height: 90px;
    vertical-align:  middle;">

  <h1>Hello from cd6440112ea7!</h1>


  

</div>
```

CONGRATULATIONS!!!!
You have successfully completed the challenge.


Мама меня похвалили - дай мне пирожок
