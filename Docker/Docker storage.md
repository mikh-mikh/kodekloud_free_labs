#

There is only one success - to be able to spend your life in your own way.

– Christopher Morley

## 1 / 10
What location are the files related to the docker containers and images stored?

```
~ ➜  ls /var/lib/docker 
buildkit    containers  image       overlay2    runtimes    tmp
containerd  engine-id   network     plugins     swarm       volumes
```

right answer - "/var/lib/docker"

## 2 / 10
What directory under /var/lib/docker are the files related to the container alpine-3 image stored?

```
~ ➜  docker ps -a | grep alpine-3
fb50cbd99dfa   alpine    "/bin/sh"   About a minute ago   Exited (0) About a minute ago             alpine-3

~ ➜  ls /var/lib/docker/containers | grep fb50cbd99dfa
fb50cbd99dfa0b2e07c589b9782fed77c683c985ba200338c55b3df0f68f7ff3
```

right answer - "fb50cbd99dfa0b2e07c589b9782fed77c683c985ba200338c55b3df0f68f7ff3"

## 3 / 10

Run a mysql container named mysql-db using the mysql image. Set database password to db_pass123
Note: Remember to run it in the detached mode.

Task completed
Correct Password set

```
~ ➜  docker run -d --name=mysql-db --env MYSQL_ROOT_PASSWORD=db_pass123 mysql
aa33557a2be25ccdb77b0110b0e53de92653c1d493f23230b06ca82e5860c4ff
```

## 4 / 10
We have just written some data into the database. To view the information we wrote, run the get-data.sh script available in the /root directory. How many customers data have been written to the database?

Command: sh get-data.sh

```
~ ➜  sh get-data.sh 
mysql: [Warning] Using a password on the command line interface can be insecure.
id      Name    Phone   Email
1       Kareem  130-5655        Duis.volutpat.nunc@quamCurabitur.org
2       Ruby    1-584-149-0770  Nulla.tempor@vitaeorciPhasellus.org
3       Rowan   199-8663        consectetuer.adipiscing.elit@Sedmalesuada.co.uk
4       Alisa   220-6017        elementum.sem.vitae@enimMauris.edu
5       Ella    731-0337        fermentum@nec.net
6       Tiger   658-4480        quis.diam@odiovelest.net
7       Felix   1-274-848-3378  Mauris.vel@arcu.com
8       Karina  1-390-796-3451  sagittis.semper@odioapurus.co.uk
9       Davis   605-8539        venenatis.vel@risusDonecnibh.com
10      Mohammad        1-590-174-1489  ornare.sagittis.felis@natoque.ca
11      Zane    362-1770        Aenean.euismod@condimentum.co.uk
12      Piper   1-231-386-6903  nunc.sed.pede@nascetur.ca
13      Marshall        1-383-729-4990  Cras.interdum.Nunc@neceuismod.ca
14      Zena    241-6641        Fusce.mollis.Duis@lobortis.org
15      Abdul   1-748-387-9935  eget.lacus.Mauris@Crasvehicula.com
16      Chase   1-401-241-9169  ante.dictum.mi@nascetur.org
17      Zahir   921-0663        non@nonummyutmolestie.edu
18      Brenda  1-691-909-5827  Quisque.ac@magnaCras.co.uk
19      Laura   1-562-983-9565  Quisque.ornare.tortor@sollicitudinadipiscing.ca
20      Madison 1-348-737-0587  Quisque.varius@Intinciduntcongue.org
21      Tanek   991-6278        dignissim.magna@Pellentesqueutipsum.net
22      Dakota  893-0792        Nullam.enim.Sed@nulla.net
23      Boris   1-297-302-5792  non.sollicitudin@eleifendegestasSed.co.uk
24      Celeste 723-6729        mauris.rhoncus@eunulla.edu
25      Connor  1-203-901-7531  et@loremipsumsodales.edu
26      Perry   1-756-607-9187  eros.turpis@tristiquepharetra.co.uk
27      Hayfa   1-609-407-3019  non.lobortis.quis@malesuadafringilla.net
28      Todd    343-0454        id.erat@arcu.org
29      Fuller  881-7273        non.feugiat.nec@adipiscingelit.net
30      Rama    1-927-605-0610  nonummy.ultricies.ornare@malesuada.co.uk
```

right answer - "30"

## 5 / 10
The database crashed. Are you able to view the data now?

Use the same command to try and view data. Try to find the container.

```
~ ➜  docker ps                    
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

ну вы че как же я увижу - сами же написали что база упала ёк макарек

right answer - "NO"

## 6 / 10
Damn! We didn't plan that well at all. Let's try again!!

ахахахахаха

## 7 / 10

Run a mysql container again, but this time map a volume to the container so that the data stored by the container is stored at /opt/data on the host.
Use the same name : mysql-db and same password: db_pass123 as before. Mysql stores data at /var/lib/mysql inside the container.

Task completed
Correct Password set
Host: /opt/data
Container: /var/lib/mysql

```
~ ➜ docker ps -a
CONTAINER ID   IMAGE     COMMAND     CREATED          STATUS                      PORTS     NAMES
fb50cbd99dfa   alpine    "/bin/sh"   18 minutes ago   Exited (0) 18 minutes ago             alpine-3
bb08df8df67e   alpine    "/bin/sh"   18 minutes ago   Exited (0) 18 minutes ago             alpine-2
1a94c7e730d2   alpine    "/bin/sh"   18 minutes ago   Exited (0) 18 minutes ago             alpine-1

~ ➜ ls /opt     
containerd

~ ➜  mkdir /opt/data

~ ➜  docker run -d --name=mysql-db --env MYSQL_ROOT_PASSWORD=db_pass123 --mount type=bind,src=/opt/data,dst=/var/lib/mysql  mysql
98e813f9e5ce0edcdca7fce2e50dd4fd92f10f9ba033fcc0c9fec8fbc5cae7af

~ ➜  docker ps   
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                 NAMES
98e813f9e5ce   mysql     "docker-entrypoint.s…"   5 seconds ago   Up 4 seconds   3306/tcp, 33060/tcp   mysql-db
```

## 8 / 10

We have now re-written data again. Run the get-data.sh script to ensure data is present.
Command: sh get-data.sh

```
~ ➜  sh get-data.sh 
mysql: [Warning] Using a password on the command line interface can be insecure.
id      Name    Phone   Email
1       Kareem  130-5655        Duis.volutpat.nunc@quamCurabitur.org
2       Ruby    1-584-149-0770  Nulla.tempor@vitaeorciPhasellus.org
3       Rowan   199-8663        consectetuer.adipiscing.elit@Sedmalesuada.co.uk
4       Alisa   220-6017        elementum.sem.vitae@enimMauris.edu
5       Ella    731-0337        fermentum@nec.net
6       Tiger   658-4480        quis.diam@odiovelest.net
7       Felix   1-274-848-3378  Mauris.vel@arcu.com
8       Karina  1-390-796-3451  sagittis.semper@odioapurus.co.uk
9       Davis   605-8539        venenatis.vel@risusDonecnibh.com
10      Mohammad        1-590-174-1489  ornare.sagittis.felis@natoque.ca
11      Zane    362-1770        Aenean.euismod@condimentum.co.uk
12      Piper   1-231-386-6903  nunc.sed.pede@nascetur.ca
13      Marshall        1-383-729-4990  Cras.interdum.Nunc@neceuismod.ca
14      Zena    241-6641        Fusce.mollis.Duis@lobortis.org
15      Abdul   1-748-387-9935  eget.lacus.Mauris@Crasvehicula.com
16      Chase   1-401-241-9169  ante.dictum.mi@nascetur.org
17      Zahir   921-0663        non@nonummyutmolestie.edu
18      Brenda  1-691-909-5827  Quisque.ac@magnaCras.co.uk
19      Laura   1-562-983-9565  Quisque.ornare.tortor@sollicitudinadipiscing.ca
20      Madison 1-348-737-0587  Quisque.varius@Intinciduntcongue.org
21      Tanek   991-6278        dignissim.magna@Pellentesqueutipsum.net
22      Dakota  893-0792        Nullam.enim.Sed@nulla.net
23      Boris   1-297-302-5792  non.sollicitudin@eleifendegestasSed.co.uk
24      Celeste 723-6729        mauris.rhoncus@eunulla.edu
25      Connor  1-203-901-7531  et@loremipsumsodales.edu
26      Perry   1-756-607-9187  eros.turpis@tristiquepharetra.co.uk
27      Hayfa   1-609-407-3019  non.lobortis.quis@malesuadafringilla.net
28      Todd    343-0454        id.erat@arcu.org
29      Fuller  881-7273        non.feugiat.nec@adipiscingelit.net
30      Rama    1-927-605-0610  nonummy.ultricies.ornare@malesuada.co.uk
```

## 9 / 10

Disaster strikes.. again! And the database crashed again. But this time we have the data stored at /opt/data directory. Re-deploy a new mysql instance using the same options as before.
Just run the same command as before. Here it is for your convenience: docker run -v /opt/data:/var/lib/mysql -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql

Task completed
Correct Password set
Host: /opt/data
Container: /var/lib/mysql

```
~ ➜  docker run -v /opt/data:/var/lib/mysql -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
ca92587d015baa28d34272d11bb0c8818d4da09747d491f4444e7a3a2cfeff82

~ ➜  docker ps                                                                                        
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                 NAMES
ca92587d015b   mysql     "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp, 33060/tcp   mysql-db
```

## 10 / 10

Fetch data and make sure it is present.
command: sh get-data.sh

вот маразм:

```
~ ➜ sh get-data.sh                                                                                   
mysql: [Warning] Using a password on the command line interface can be insecure.
id      Name    Phone   Email
1       Kareem  130-5655        Duis.volutpat.nunc@quamCurabitur.org
2       Ruby    1-584-149-0770  Nulla.tempor@vitaeorciPhasellus.org
3       Rowan   199-8663        consectetuer.adipiscing.elit@Sedmalesuada.co.uk
4       Alisa   220-6017        elementum.sem.vitae@enimMauris.edu
5       Ella    731-0337        fermentum@nec.net
6       Tiger   658-4480        quis.diam@odiovelest.net
7       Felix   1-274-848-3378  Mauris.vel@arcu.com
8       Karina  1-390-796-3451  sagittis.semper@odioapurus.co.uk
9       Davis   605-8539        venenatis.vel@risusDonecnibh.com
10      Mohammad        1-590-174-1489  ornare.sagittis.felis@natoque.ca
11      Zane    362-1770        Aenean.euismod@condimentum.co.uk
12      Piper   1-231-386-6903  nunc.sed.pede@nascetur.ca
13      Marshall        1-383-729-4990  Cras.interdum.Nunc@neceuismod.ca
14      Zena    241-6641        Fusce.mollis.Duis@lobortis.org
15      Abdul   1-748-387-9935  eget.lacus.Mauris@Crasvehicula.com
16      Chase   1-401-241-9169  ante.dictum.mi@nascetur.org
17      Zahir   921-0663        non@nonummyutmolestie.edu
18      Brenda  1-691-909-5827  Quisque.ac@magnaCras.co.uk
19      Laura   1-562-983-9565  Quisque.ornare.tortor@sollicitudinadipiscing.ca
20      Madison 1-348-737-0587  Quisque.varius@Intinciduntcongue.org
21      Tanek   991-6278        dignissim.magna@Pellentesqueutipsum.net
22      Dakota  893-0792        Nullam.enim.Sed@nulla.net
23      Boris   1-297-302-5792  non.sollicitudin@eleifendegestasSed.co.uk
24      Celeste 723-6729        mauris.rhoncus@eunulla.edu
25      Connor  1-203-901-7531  et@loremipsumsodales.edu
26      Perry   1-756-607-9187  eros.turpis@tristiquepharetra.co.uk
27      Hayfa   1-609-407-3019  non.lobortis.quis@malesuadafringilla.net
28      Todd    343-0454        id.erat@arcu.org
29      Fuller  881-7273        non.feugiat.nec@adipiscingelit.net
30      Rama    1-927-605-0610  nonummy.ultricies.ornare@malesuada.co.uk
```

