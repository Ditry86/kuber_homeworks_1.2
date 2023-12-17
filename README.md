# Домашнее задание к занятию «Базовые объекты K8S»

<br>

## Задание 1. Создать Pod с именем hello-world

<br>

1. Результат выполнения команды `kubectl get pods`

```
$ kubectl get nodes

NAME           READY   STATUS    RESTARTS   AGE
netology-web   1/1     Running   0          13m
```  

2. Ответ при подключении curl к поду netology-web (TCP-порт 8080 (nginx tcp listen для данного image пода)) с помощью `kubectl port-forward pod/netology-web 8008:8080`

```
$ curl localhost:8008


Hostname: netology-web

Pod Information:
        -no pod information available-

Server values:
        server_version=nginx: 1.12.2 - lua: 10010

Request Information:
        client_address=127.0.0.1
        method=GET
        real path=/
        query=
        request_version=1.1
        request_scheme=http
        request_uri=http://localhost:8080/

Request Headers:
        accept=*/*  
        host=localhost:8000  
        user-agent=curl/8.2.1  

Request Body:
        -no body in request-
```
<br>

## Задание 2. Создать Service и подключить его к Pod

<br>

1. Результат выполнения команды `kubectl get service`

```
$ kubectl get service
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.152.183.1     <none>        443/TCP   122m
netology     ClusterIP   10.152.183.247   <none>        80/TCP    18m
```

2. Ответ при подключении curl к сервису netology (TCP-порт 80) с помощью `kubectl port-forward service/netology 80:8000`

```
$ curl localhost:8000


Hostname: netology-web

Pod Information:
        -no pod information available-

Server values:
        server_version=nginx: 1.12.2 - lua: 10010

Request Information:
        client_address=127.0.0.1
        method=GET
        real path=/
        query=
        request_version=1.1
        request_scheme=http
        request_uri=http://localhost:8080/

Request Headers:
        accept=*/*  
        host=localhost:8000  
        user-agent=curl/8.2.1  

Request Body:
        -no body in request-
```

3. Вывод команды `kubectl describe service/netology`

```
$ kubectl describe service/netology
Name:              netology
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=netology-web
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.152.183.247
IPs:               10.152.183.247
Port:              web  80/TCP
TargetPort:        8080/TCP
Endpoints:         10.1.211.199:8080
Session Affinity:  None
Events:            <none>
```