# kodekloud free labs Docker - Docker CMD & Entrypoint

In learning you will teach, and in teaching you will learn.

– Phil Collins


## 1 / 6

Dockerfiles for a few commonly used Docker Images are given in the /root (current) directory. 
Inspect them and try to answer the following questions.

```
~ ➜  ls
Dockerfile-mysql      Dockerfile-python     Dockerfile-ubuntu     Dockerfile-wordpress  app
```

## 2 / 6
What is the ENTRYPOINT configured on the mysql image?

```
~ ➜  cat Dockerfile-mysql | grep ENTRY
ENTRYPOINT ["docker-entrypoint.sh"]
```

right answer - "docker-entrypoint.sh"

## 3 / 6
What is the CMD configured on the wordpress image?

```
~ ➜  cat Dockerfile-wordpress | grep CMD
CMD ["apache2-foreground"]
```

right answer - "apache2-foreground"

## 4 / 6
What is the final command run at startup when the wordpress image is run. Consider both ENTRYPOINT and CMD instructions

```
~ ➜  cat Dockerfile-wordpress | grep ENTRY -A 5
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
```

right answer - "docker-entrypoint.sh apache2-foreground"

## 5 / 6
What is the command run at startup when the ubuntu image is run?

```
~ ➜  cat Dockerfile-ubuntu | grep CMD 
CMD ["bash"]
```

right answer - "bash"

## 6 / 6
Run an instance of the ubuntu image to run the sleep 1000 command at startup.
Run it in detached mode.

```
~ ✖ docker run -d edbfe74c41f8 sleep 1000  
6ecdfb3f08aac9c7e45008224ad1f2e6e252b392c4eba2dc7e6004021cd9e8f1

~ ➜  docker ps                            
CONTAINER ID   IMAGE          COMMAND        CREATED         STATUS         PORTS     NAMES
6ecdfb3f08aa   edbfe74c41f8   "sleep 1000"   5 seconds ago   Up 4 seconds             optimistic_tu
```

