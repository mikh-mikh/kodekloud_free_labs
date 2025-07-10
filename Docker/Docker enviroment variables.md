# kodekloud free labs Docker - Docker enviroment variables

You can’t go back and change the beginning, but you can start where you are and change the ending.

– C.S. Lewis

## 1 / 4
Inspect the environment variables set on the running container and identify the value set to the APP_COLOR variable.

```
~ ➜  docker ps                            
CONTAINER ID   IMAGE                     COMMAND           CREATED         STATUS         PORTS      NAMES
e3dc827c4035   kodekloud/simple-webapp   "python app.py"   3 minutes ago   Up 3 minutes   8080/tcp   festive_wiles

~ ➜  docker exec e3dc827c4035 env | grep APP_COLOR
APP_COLOR=pink
```

right answer - "pink"

## 2 / 4
Run a container named blue-app using image kodekloud/simple-webapp and set the environment variable APP_COLOR to blue. Make the application available on port 38282 on the host. The application listens on port 8080.

Name: blue-app
Image: kodekloud/simple-webapp
ENV Variable: APP_COLOR=blue

```
~ ➜  docker run -d --name=blue-app --env APP_COLOR=blue -p 38282:8080  kodekloud/simple-webapp
a9760b598bd658401c7ed1a578d308f562ffb67d522b9b859af02553457d8b9c

~ ➜  docker ps                                                                                
CONTAINER ID   IMAGE                     COMMAND           CREATED          STATUS          PORTS                                         NAMES
a9760b598bd6   kodekloud/simple-webapp   "python app.py"   4 seconds ago    Up 3 seconds    0.0.0.0:38282->8080/tcp, :::38282->8080/tcp   blue-app
e3dc827c4035   kodekloud/simple-webapp   "python app.py"   23 minutes ago   Up 22 minutes   8080/tcp                                      festive_wiles

~ ➜  docker exec a9760b598bd6 env | grep APP_COLOR                               
APP_COLOR=blue
```

## 3 / 4
View the application by clicking the link HOST:38282 on the right side of your terminal bar and ensure it has the right colour.

```
~ ➜  curl 127.0.0.1:38282
<!doctype html>
<title>Hello from Flask</title>
<body style="background: #2980b9;"></body>
<div style="color: #e4e4e4;
    text-align:  center;
    height: 90px;
    vertical-align:  middle;">

  <h1>Hello from a9760b598bd6!</h1>


  

</div>
```
#2980b9 Color Hex - it is blue color

## 4 / 4
Deploy a mysql database using the mysql image and name it mysql-db.
Set the database password to use db_pass123. Lookup the mysql image 
on Docker Hub and identify the correct environment variable to use for setting the root password.

```
~ ➜  docker run -d --name=mysql-db --env MYSQL_ROOT_PASSWORD=db_pass123 -p 3306:3306 mysql       
fbc3aff6ead1eef8f1e9afb96d66c2781ce1529c9a1df5b8cad69aff945a7162

~ ➜  docker exec fbc3aff6ead1 env | grep MYSQL_ROOT_PASSWORD 
MYSQL_ROOT_PASSWORD=db_pass123
```

