# kubernetes pods lab 

Tell me and I forget. Teach me and I remember. Involve me and I learn.

– Benjamin Franklin

## 1 / 13
How many pods exist on the system?
In the current(default) namespace.

```
controlplane ~ ✖ k -n default get pods
No resources found in default namespace.
```

## 2 / 13
Create a new pod with the nginx image.

i think k8s designed for declarative
google "nginx pod example"
nginx.yaml:
```
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
```	
```
controlplane ~ ➜  k create -n default -f nginx.yaml 
pod/nginx created

controlplane ~ ➜  k get pods -n default 
NAME            READY   STATUS    RESTARTS   AGE
newpods-bdgnc   1/1     Running   0          6m9s
newpods-jv5n4   1/1     Running   0          6m9s
newpods-8ksqp   1/1     Running   0          6m9s
nginx           1/1     Running   0          15s

controlplane ~ ➜  k describe pod nginx | grep IP
IP:               10.42.0.12
IPs:
  IP:  10.42.0.12
  
controlplane ~ ➜  curl 10.42.0.12
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

## 3 / 13
How many pods are created now?

Note: We have created a few more pods. So please check again in the current(default) namespace.

```
controlplane ~ ➜  k get pods -n default 
NAME            READY   STATUS    RESTARTS   AGE
newpods-bdgnc   1/1     Running   0          9m39s
newpods-jv5n4   1/1     Running   0          9m39s
newpods-8ksqp   1/1     Running   0          9m39s
nginx           1/1     Running   0          3m45s
```

right answer - 4 pods

## 4 / 13

What is the image used to create the new pods?
You must look at one of the new pods in detail to figure this out.

```
controlplane ~ ✖ k describe pods -n default newpods-8ksqp newpods-bdgnc newpods-jv5n4 | grep image
  Normal  Pulling    13m   kubelet            Pulling image "busybox"
  Normal  Pulled     13m   kubelet            Successfully pulled image "busybox" in 214ms (214ms including waiting)
  Normal  Pulling    13m   kubelet            Pulling image "busybox"
  Normal  Pulled     13m   kubelet            Successfully pulled image "busybox" in 362ms (362ms including waiting)
  Normal  Pulling    13m   kubelet            Pulling image "busybox"
  Normal  Pulled     13m   kubelet            Successfully pulled image "busybox" in 248ms (248ms including waiting)
 ```

i do not know how use wildcard (newpods-*) - only piping with awk - i think there is no woldcard support for kubectl because чтобы ебаные мартышки типа меня прод не захуярили
i will know later kubectl kung-fu practics i promise

right answer - busybox

## 5 / 13
Which nodes are these pods placed on?

You must look at all the pods in detail to figure this out.

```
controlplane ~ ➜  k get nodes
NAME           STATUS   ROLES                  AGE   VERSION
controlplane   Ready    control-plane,master   66m   v1.29.0+k3s1
```
right answer - controlplane (master)

## 6 / 13
How many containers are part of the pod webapp?

Note: We just created a new POD. Ignore the state of the POD for now.

```
controlplane ~ ➜  k describe -n default pod webapp | grep "Image:"
    Image:          nginx
    Image:          agentx
```

right answer - nginx & agentx

## 8 / 13
What is the state of the container agentx in the pod webapp?

Wait for it to finish the ContainerCreating state

DO NOT DO LIKE ME LIKE THIS:
```
 k describe -n default pod webapp | grep "State:"
    State:          Running
    State:          Waiting
```
second state -> second pod -> agentx - this is "waiting"
right answer - "error or waiting"

## 9 / 13
Why do you think the container agentx in pod webapp is in error?

Try to figure it out from the events section of the pod.

ой я низнаю я техподдержка я создам заявку спасибо досвиданья
индюк думал-думал да в суп попал - we need to check why agentx is not starting:

```
controlplane ~ ✖ k describe -n default pod webapp | grep "Failed"
  Warning  Failed     10m (x3 over 11m)    kubelet            Error: ErrImagePull
  Warning  Failed     9m52s (x5 over 11m)  kubelet            Error: ImagePullBackOff
  Warning  Failed     9m39s (x4 over 11m)  kubelet            Failed to pull image "agentx": failed to pull and unpack image "docker.io/library/agentx:latest": 
  failed to resolve reference "docker.io/library/agentx:latest": pull access denied, repository does not exist or may require authorization: server message: insufficient_scope: 
  authorization failed
```
"Всё ясно"
из вариантов ответов про репы ни слова - может оно так ругается в контексте авторизации если такого образа не существует?
right anwser - a docker image with this name is not exist in registry (?) (WTF) 

## 10 / 13
What does the READY column in the output of the kubectl get pods command indicate?

right anwser - "running / total containers (in pod)

## 11 / 13

Delete the webapp Pod.
Once deleted, wait for the pod to fully terminate.

```
controlplane ~ ✖ k delete pod webapp 
pod "webapp" deleted
controlplane ~ ➜  k get pods
NAME            READY   STATUS    RESTARTS      AGE
nginx           1/1     Running   0             44m
newpods-8ksqp   1/1     Running   3 (40s ago)   50m
newpods-bdgnc   1/1     Running   3 (40s ago)   50m
newpods-jv5n4   1/1     Running   3 (40s ago)   50m
```

## 12 / 13
Create a new pod with the name redis and the image redis123.
Use a pod-definition YAML file. And yes the image name is wrong!

redis.yaml:
```
---
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
    - name: redis
      image: redis123
```
```
controlplane ~ ➜  k create -f redis.yaml 
pod/redis created

k get pods
NAME            READY   STATUS         RESTARTS        AGE
nginx           1/1     Running        0               47m
newpods-8ksqp   1/1     Running        3 (3m16s ago)   53m
newpods-bdgnc   1/1     Running        3 (3m16s ago)   53m
newpods-jv5n4   1/1     Running        3 (3m16s ago)   53m
redis           0/1     ErrImagePull   0               5s
```

## 13 / 13
Now change the image on this pod to redis.
Once done, the pod should be in a running state.

```
controlplane ~ ➜  k delete pod redis 
pod "redis" deleted

controlplane ~ ➜  k apply -f redis.yaml 
pod/redis created

controlplane ~ ➜  k get pods
NAME            READY   STATUS    RESTARTS        AGE
nginx           1/1     Running   0               49m
newpods-8ksqp   1/1     Running   3 (5m11s ago)   55m
newpods-bdgnc   1/1     Running   3 (5m11s ago)   55m
newpods-jv5n4   1/1     Running   3 (5m11s ago)   55m
redis           1/1     Running   0               4s
```