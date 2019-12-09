# api-chamados-kubernetes
This repo was created to learn how to deploy an application with k8s. I'm using minikube to do this so you need to create a minikube before run this commands.

First we need create config map and secret that will be used from database and application:
``` sh
$ kubectl create -f secret.yml
$ kubectl create -f config-map.yml
```

After we will create a database that needs a volume, deploy and service:
``` sh
$ kubectl create -f postgres/persisten-volume.yml
$ kubectl create -f postgres/deployment.yml
$ kubectl create -f postgres/service.yml
```

Now we have a database to run ower application so let's do this, we will create application deploy and than a service that allow us to have access of application:
``` sh
$ kubectl create -f api-chamados/deployment.yml
$ kubectl create -f api-chamados/service.yml
```

To see ower application we need to discovery wich ip addres it's runing from minikube:
``` sh
$ minikube service api-chamados --url
```

Also if you want access database:
``` sh
$ minikube service postgres --url
```

To end let's enable auto-scaling
``` sh
$ minikube api-chamados/hpa.yml
```
