Deployments
 
frontend , backend pods( stateless pods)  we will deploy using k8s deployemnts
Depoyments are used to create and manage stateless pods
Deployents will make sure that our pods are running everytime
If any pod is crashed then deployemt will replace that pod with new pod automaticallty
Using deploymentys we can scale up and sacle down our pods
Deploymets will support rollout and rollback
Deployments will support startigies like rollingupdate and replace
deployment will create a pods with random names

rollingupdate
=============
Pods will recreate one by one ( no down time)

Replace
===========
it will delete old pods and it will create new pods (down time)



     Statefulsets
========================

we will deploy stateful applicatuion using k8s statefulsets
statefulset will create pods with name sticky identity
sts1-0 (master)
sts1-1  (secondary)
sts1-2    """

if we delete any pod using sts, it will remove in revrese order
in sts pods will create with the same names
in sts, pods will create one by one ( 2nd pod will create using 1st pod data, 3rd pod will creare using 2nd pod data)
in sts we have primary and secondary pods 
primary pod is called master pod (read and write access)
secondary pods are called reader pod (only read access)
we will expose statefulset pods using headless service( head less means we are going to use the pod ip directly)
in sts, each pod will have its own pv and pvc
in sts, if we delete sts also pv and pvc will not delete
and if we create new sts then it will attach to existing pv and pvc

pvc (persistent volume calim) it will request the volume 
=============================

It will request for volume


pv(persistent volume) main volume
======================

is nothing but volume

sc( hostpath, ebs, efs)
===
storage class will create pv (volume)  dynamically







service in k8s
===============
by default pods are not accessable outside the cluster
to expose or access the pods outside the cluster then we need to use k8s service

There are below type of service
==================================

services will identify the pods based on labels

1 ClusterIP (it is used to access the pods within the cluster)
2 NodePort  (we can access the pod outside the cluster using nodeip:port) in nodeport ports are from 30,000 - 32,767
3 Load Balancer ( we can access using lb endpoint url)


user -> service -> pod
user -> LoadBalancer -> NodePort -> ClusterIP -> pod
user -> Nodeport -> Clusterip -> pod


pod -> backend service -> backend pod
pod  -> Cluserip -> pod



user - service - pod
               - pod
               - pod

servces will route the trafiic to pods in round robbin method

 

frontend  - Nodeport


backend    - Cluserip,  

database    - Headless