# kubernetes_formation
https://github.com/dockersamples/example-voting-app
 ####key#####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
################### Installation Docker ############################""
#sudo apt install ca-certificates curl gnupg
 #sudo install -m 0755 -d /etc/apt/keyrings
 #curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
 #sudo chmod a+r /etc/apt/keyrings/docker.gpg
 #echo "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
 #sudo apt update 
#apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
#sudo docker run hello-world
#sudo docker pull debian
#sudo docker images
#sudo docker run debian
#sudo docker ps
#sudo docker ps 
#sudo docker run -it debian /bin/bash
#sudo docker exec -it debian /bin/bash
#sudo docker ps
#sudo docker images
#sudo docker restart ca1a8403096e 
#sudo docker inspect ca1a8403096e

############### installation binaire kubectl kubernetes ###########################
#curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

#curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

#echo "$(cat kubectl.sha256) kubectl" | sha256sum --check

#sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
#kubectl version --client
#kubectl version --short

################# minicube ########################
#curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
#sudo apt-get install virtualbox
#sudo install minikube-linux-amd64 /usr/local/bin/minikube
#minikube start
#kubectl cluster-info
#minikube status
#minikube ip
#minikube dashboard
#kubectl config get-contexts
################################### pod ##############################
# kubectl create -f nginx-pod.yaml 
# kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          2m6s
#kubectl exec nginx -- nginx -v ### pour executer le pod/conteneur la version
nginx version: nginx/1.12.2
#kubectl exec -it nginx -- /bin/bash ### pour lancer le pod/conteneur en bash
#kubectl exec -it debug -- /bin/sh  ### pour lancer le pod/conteneur en sh
root@nginx:/# ls
#kubectl delete pod nginx ## pour supprimer un pod 
#kubectl describe pod nginx
#kubectl port-forward nginx 8080:80 #lancer nginx avec la commande forward

#kubectl exec -it debug -- /bin/sh ### pinguer le pod nginx
/ # ping 10.244.0.5
PING 10.244.0.5 (10.244.0.5): 56 data bytes
64 bytes from 10.244.0.5: seq=0 ttl=64 time=1.167 ms
64 bytes from 10.244.0.5: seq=1 ttl=64 time=0.111 ms
64 bytes from 10.244.0.5: seq=2 ttl=64 time=0.095 ms
64 bytes from 10.244.0.5: seq=3 ttl=64 time=0.103 ms

#kubectl port-forward nginx 8080:80 #lancer nginx avec la commande forward

#kubectl get pod
NAME    READY   STATUS    RESTARTS      AGE
wp      2/2     Running   1 (10s ago)   73s
#kubectl port-forward wp 8080:80 #lancer wordpress avec la commande forward

################### wordpress ##################"
#kubectl get pod
NAME    READY   STATUS    RESTARTS      AGE
wp      2/2     Running   1 (10s ago)   73s
#kubectl port-forward wp 8080:80 #lancer wordpress avec la commande forward

######################## clusterIP ##################################
#kubectl get svc
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes              ClusterIP   10.96.0.1        <none>        443/TCP        6h23m
vote-service            ClusterIP   10.110.197.135   <none>        80/TCP         35m

#kubectl exec -it debug sh
#curl http://vote-service
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Cats vs Dogs!</ti
     
 ######################### Nodeport #########################
 kubectl get svc
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
vote-service-nodeport   NodePort    10.100.14.29     <none>        80:31000/TCP   15m

pour accerder à l'application 
http://192.168.59.100:31000/
######################## deployment ########################
#kubectl get deployments
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
vote-deploy   3/3     3            3           3m4s
#kubectl get pod
NAME                           READY   STATUS    RESTARTS       AGE
vote-deploy-68bcfcf748-2vc26   1/1     Running   0              5m1s
vote-deploy-68bcfcf748-pwkc2   1/1     Running   0              5m1s
vote-deploy-68bcfcf748-xdbsn   1/1     Running   0              5m1s

#kubectl get rs
NAME                     DESIRED   CURRENT   READY   AGE
vote-deploy-68bcfcf748   3  
# kubectl delete pod vote-deploy-68bcfcf748-2vc26
pod "vote-deploy-68bcfcf748-2vc26" deleted

#kubectl get pod
NAME                           READY   STATUS    RESTARTS       AGE
vote-deploy-68bcfcf748-fgpjc   1/1     Running   0              11s
vote-deploy-68bcfcf748-pwkc2   1/1     Running   0              12m
vote-deploy-68bcfcf748-xdbsn   1/1     Running   0              12m

#kubectl delete rs vote-deploy-68bcfcf748
replicaset.apps "vote-deploy-68bcfcf748" deleted
#kubectl get rs
NAME                     DESIRED   CURRENT   READY   AGE
vote-deploy-68bcfcf748   3         3         2       6s
# kubectl get pod
NAME                           READY   STATUS    RESTARTS         AGE
vote-deploy-68bcfcf748-8swd7   1/1     Running   0                17s
vote-deploy-68bcfcf748-htwg7   1/1     Running   0                17s
vote-deploy-68bcfcf748-p6w6v   1/1     Running   0                17s

#kubectl set image deployment/vote-deploy  vote=instavote/vote:indent # ajout une version
deployment.apps/vote-deploy image updated
#kubectl get deploy vote-deploy
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
vote-deploy   3/3     3            3           24m

#kubectl get rs
NAME                     DESIRED   CURRENT   READY   AGE
vote-deploy-68bcfcf748   0         0         0       13m
vote-deploy-6cd67469dd   3         3         3       2m27s

#kubectl get pod
NAME                           READY   STATUS    RESTARTS       AGE
vote-deploy-6cd67469dd-2mk58   1/1     Running   0              3m44s
vote-deploy-6cd67469dd-k8lrj   1/1     Running   0              4m
vote-deploy-6cd67469dd-lmpp9   1/1     Running   0              4m21s

#kubectl rollout undo deployment/vote-deploy # faire un roolback
deployment.apps/vote-deploy rolled back
#kubectl get rs
NAME                     DESIRED   CURRENT   READY   AGE
vote-deploy-68bcfcf748   3         3         3       18m
vote-deploy-6cd67469dd   0         0         0       7m20s


 #kubectl get pod
NAME                           READY   STATUS              RESTARTS         AGE
vote-deploy-68bcfcf748-5k9tc   1/1     Running   0              8m52s
vote-deploy-68bcfcf748-xlsfn   1/1     Running   0              9m10s
vote-deploy-68bcfcf748-zrv8l   1/1     Running   0              8m59s


########################## secret #######################""
 #openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out cert.pem
#kubectl create secret tls domain-pki --cert cert.pem --key key.pem
secret/domain-pki created
#kubectl get secret domain-pki -o yaml
apiVersion: v1
data:
  tls.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FUR
kind: Secret
metadata:
  creationTimestamp: "2023-04-20T10:13:24Z"
  name: domain-pki
  namespace: default
  resourceVersion: "74329"
  uid: 0e41a2fa-c797-40f2-b66b-66e17cd09d4e
type: kubernetes.io/tls
# kubectl get pod
NAME                           READY   STATUS      RESTARTS         AGE
proxy                          1/1     Running     0                104m
 
#kubectl get secret
NAME                                     TYPE                 DATA   AGE
domain-pki                               kubernetes.io/tls    2      24h

################### configmap #############################"
#kubectl create configmap nginx-config --from-file=./nginx.conf
configmap/nginx-config created
#kubectl create -f pod-config-volume.yaml 
pod/www created

# kubectl exec -ti www --container proxy -- bash
root@www:/# cat /etc/nginx/nginx.conf 
user www-data;
worker_processes 4;
pid /run/nginx.pid;
events {
 worker_connections 768;
}
http {
 server {
   listen *:8000;
   location / {
     proxy_pass http://localhost;
   }
 }
}
#kubectl exec -ti www --container proxy -- bash
root@www:/#curl localhost:8000
{"message":"www suggests to visit Hadvuhoga"}

############configmap avec variable d'environnement ######################
#kubectl create configmap app-config-env --from-file=./app.env
configmap/app-config-env created
#kubectl get cm app-config-env -o yaml
apiVersion: v1
data:
  app.env: |
    log_level= WARN
    env= production
    cache=redis
kind: ConfigMap
metadata:
  creationTimestamp: "2023-04-20T13:20:34Z"
  name: app-config-env
  namespace: default
  resourceVersion: "83412"
  uid: 8cc62ed2-f2e7-483a-b4f0-13fbb6ee23e4
#kubectl get cm
NAME                                         DATA   AGE
app-config-env                               1      19h
nginx-config                                 1      21h


##################namespace ###############
#kubectl get pod -n kubernetes-dashboard
NAME                                        READY   STATUS    RESTARTS      AGE
dashboard-metrics-scraper-5c6664855-6hc9b   1/1     Running   1 (22h ago)   46h
kubernetes-dashboard-55c4cbbc7c-jmlrt       1/1     Running   1 (22h ago)   46h

# kubectl create namespace development 
namespace/development created

pod/nginx created
stagiaire@form128:~/.kube$ kubectl get pod -n development
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          2m20s
kubectl get pod --all-namespaces
NAMESPACE              NAME                                        READY   STATUS                       RESTARTS        AGE
default                db-989b6b476-j54zw                          1/1     Running                      1 (22h ago)     22h
default                debug                                       1/1     Running                      153 (15m ago)   42h
default                nginx                                       1/1     Running                      1 (22h ago)     45h
default                pi-dd45n                                    0/1     Completed                    0               22h
default                proxy                                       1/1     Running                      0               21h
default                redis-7fdbb9576f-fppvb                      1/1     Running                      1 (22h ago)     22h
default                result-f9f4fbbc7-9b9f4                      1/1     Running                      0               22h
default                vote                                        1/1     Running                      1 (22h ago)     40h
default                vote-5f865477fc-jfbfx                       1/1     Running                      0               22h
default                vote-deploy-68bcfcf748-5k9tc                1/1     Running                      1 (22h ago)     23h
default                vote-deploy-68bcfcf748-xlsfn                1/1     Running                      1 (22h ago)     23h
default                vote-deploy-68bcfcf748-zrv8l                1/1     Running                      1 (22h ago)     23h
default                w3                                          0/1     CreateContainerConfigError   0               16h
default                worker-667975666-6crvw                      1/1     Running                      0               22h
default                wp                                          2/2     Running                      4 (22h ago)     42h
default                www                                         2/2     Running                      0               18h
development            nginx                                       1/1     Running 


########## Application stateful volume : EmptyDir ############


#kubectl create -f mongo-emptydir.yaml 
pod/mongo created
#kubectl exec -ti mongo -- bash
root@mongo:/# mongo
MongoDB shell version v3.6.23
connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("d81fe9cc-8284-49ed-a3b6-32f3ed376448") }
MongoDB server version: 3.6.23
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	http://docs.mongodb.org/
Questions? Try the support group
	http://groups.google.com/group/mongodb-user
Server has startup warnings: 
2023-04-21T07:48:18.929+0000 I STORAGE  [initandlisten] 
2023-04-21T07:48:18.929+0000 I STORAGE  [initandlisten] ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
2023-04-21T07:48:18.929+0000 I STORAGE  [initandlisten] **          See http://dochub.mongodb.org/core/prodnotes-filesystem
2023-04-21T07:48:19.966+0000 I CONTROL  [initandlisten] 
2023-04-21T07:48:19.966+0000 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2023-04-21T07:48:19.966+0000 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2023-04-21T07:48:19.966+0000 I CONTROL  [initandlisten] 
> use test
switched to db test
> db.k8.insert({ok:1})
WriteResult({ "nInserted" : 1 })
> db.k8s.insert({ok:1})
WriteResult({ "nInserted" : 1 })
> db.k8s.insert({ok: 1})
WriteResult({ "nInserted" : 1 })
> exit
bye
root@mongo:/# kill 1
root@mongo:/# command terminated with exit code 137
root@mongo:/mongo# command terminated with exit code 137
stagiaire@form128:~/.kube$ kubectl exec -ti mongo -- bash


########## Application stateful volume : HOSPATH ############

kubectl create -f mongo-hostpath.yaml 
pod/mongohostpath created
# minikube ssh #connexion au vm
                         _             _            
            _         _ ( )           ( )           
  ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __  
/' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
| ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
(_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

$ cd /data-db/
$ ls
WiredTiger	   WiredTiger.wt     collection-0-3878545255871246073.wt  diagnostic.data		  index-5-3878545255871246073.wt  mongod.lock
WiredTiger.lock    WiredTigerLAS.wt  collection-2-3878545255871246073.wt  index-1-3878545255871246073.wt  index-6-3878545255871246073.wt  sizeStorer.wt
WiredTiger.turtle  _mdb_catalog.wt   collection-4-3878545255871246073.wt  index-3-3878545255871246073.wt  journal			  s
#kubectl delete po mongohostpath # on va supprimer le pod
pod "mongohostpath" deleted
## apres la suppression du pod les données sont toujours dans le vms
$ ls
WiredTiger	   WiredTiger.wt     collection-0-3878545255871246073.wt  diagnostic.data		  index-5-3878545255871246073.wt  mongod.lock
WiredTiger.lock    WiredTigerLAS.wt  collection-2-3878545255871246073.wt  index-1-3878545255871246073.wt  index-6-3878545255871246073.wt  sizeStorer.wt
WiredTiger.turtle  _mdb_catalog.wt   collection-4-3878545255871246073.wt  index-3-3878545255871246073.wt  journal			  storage.bson
$ 
############################ Horizontal pod autoscaler ###############"
# minikube addons enable metrics-server 
💡  metrics-server est un addon maintenu par Kubernetes. Pour toute question, contactez minikube sur GitHub.
Vous pouvez consulter la liste des mainteneurs de minikube sur : https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Utilisation de l'image registry.k8s.io/metrics-server/metrics-server:v0.6.3
🌟  Le module 'metrics-server' est activé
# activation addons et stop minikube et redemarrer minikube
#kubectl apply -f https://k8s.io/examples/application/php-apache.yaml
deployment.apps/php-apache created
service/php-apache created

#kubectl get pod,rs,deploy,svc
NAME                               READY   STATUS                       RESTARTS       AGE
pod/php-apache-7495ff8f5b-l5dbt    1/1     Running                      0              75s


NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/db-989b6b476             1         1         1       23h
replicaset.apps/php-apache-7495ff8f5b    1         1         1       76s
replicaset.apps/redis-7fdbb9576f         1         1         1       23h
replicaset.apps/result-f9f4fbbc7         1         1         1       23h
replicaset.apps/vote-5f865477fc          1         1         1       23h
replicaset.apps/vote-deploy-68bcfcf748   3         3         3       25h
replicaset.apps/vote-deploy-6cd67469dd   0         0         0       24h
replicaset.apps/worker-667975666         1         1         1       23h

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/db            1/1     1            1           23h
deployment.apps/php-apache    1/1     1            1           76s
deployment.apps/redis         1/1     1            1           23h
deployment.apps/result        1/1     1            1           23h
deployment.apps/vote          1/1     1            1           23h
deployment.apps/vote-deploy   3/3     3            3           25h
deployment.apps/worker        1/1     1            1           23h

NAME                   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/db             ClusterIP   10.110.158.212   <none>        5432/TCP         23h
service/kubernetes     ClusterIP   10.96.0.1        <none>        443/TCP          2d
service/php-apache     ClusterIP   10.104.62.45     <none>        80/TCP           76s
service/redis          ClusterIP   10.98.173.4      <none>        6379/TCP         23h
service/result         NodePort    10.99.28.12      <none>        5001:31001/TCP   23h
service/vote           NodePort    10.104.19.109    <none>        5000:31000/TCP   23h
service/vote-service   ClusterIP   10.110.197.135   <none>        80/TCP           42h

#kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
horizontalpodautoscaler.autoscaling/php-apache autoscaled
#kubectl get hpa
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   1%/50%    1         10        1          15s
#kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache;done" ### la commande pour tester autoscaling 
If you don't see a command prompt, try pressing enter.
OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK!OK

#kubectl get hpa --watch # nous pouvons voir la montée en charge
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   0%/50%    1         10        1          71s
php-apache   Deployment/php-apache   238%/50%   1         10        1          2m
php-apache   Deployment/php-apache   238%/50%   1         10        4          2m15s
php-apache   Deployment/php-apache   238%/50%   1         10        5          2m30s
php-apache   Deployment/php-apache   86%/50%    1         10        5          3m
php-apache   Deployment/php-apache   57%/50%    1         10        5          4m

#kubectl get pod #  5 pods en cours d'execution
NAME                           READY   STATUS                       RESTARTS          AGE
php-apache-7495ff8f5b-4w9mx    1/1     Running                      0                 101s
php-apache-7495ff8f5b-j67k7    1/1     Running                      0                 3m41s
php-apache-7495ff8f5b-jxsdr    1/1     Running                      0                 3m41s
php-apache-7495ff8f5b-k27dl    1/1     Running                      0                 3m41s
php-apache-7495ff8f5b-l5dbt    1/1     Running                      1 (9m48s ago)     43m

#kubectl get pod # apres avoir arreter la commande nous avons pu avoir que maintenan qu'on un seul pod en cours d'execution 
NAME                           READY   STATUS                       RESTARTS          AGE
php-apache   Deployment/php-apache   0%/50%     1         10        1          13m


################ installation helm et gitlab##########################
#curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

#chmod 700 get_helm.sh
# ./get_helm.sh 
Downloading https://get.helm.sh/helm-v3.11.3-linux-amd64.tar.gz
Verifying checksum... Done.
Preparing to install helm into /usr/local/bin
[sudo] Mot de passe de stagiaire : 
helm installed into /usr/local/bin/helm
#helm repo add gitlab http://charts.gitlab.io
"gitlab" has been added to your repositories
#helm install my-gitlab gitlab/gitlab --set certmanager-issuer.email=you@toto.com


kubectl get deploy
NAME                                 READY   UP-TO-DATE   AVAILABLE   AGE
db                                   1/1     1            1           25h
my-gitlab-certmanager                1/1     1            1           4m37s
my-gitlab-certmanager-cainjector     1/1     1            1           4m37s
my-gitlab-certmanager-webhook        1/1     1            1           4m37s
my-gitlab-gitlab-exporter            0/1     1            0           4m37s
my-gitlab-gitlab-runner              0/1     1            0           4m37s
my-gitlab-gitlab-shell               1/2     2            1           4m37s
my-gitlab-kas                        2/2     2            2           4m37s
my-gitlab-minio                      1/1     1            1           4m37s
my-gitlab-nginx-ingress-controller   2/2     2            2           4m37s
my-gitlab-prometheus-server          1/1     1            1           4m37s
my-gitlab-registry                   2/2     2            2           4m37s
my-gitlab-sidekiq-all-in-1-v2        0/1     1            0           4m37s
my-gitlab-toolbox                    0/1     1            0           4m37s
my-gitlab-webservice-default         0/2     2            0           4m37s

#kubectl get svc
NAME                                         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)                                   AGE
db                                           ClusterIP      10.110.158.212   <none>        5432/TCP                                  25h
kubernetes                                   ClusterIP      10.96.0.1        <none>        443/TCP                                   2d1h
my-gitlab-certmanager                        ClusterIP      10.107.140.30    <none>        9402/TCP                                  5m34s
my-gitlab-certmanager-webhook                ClusterIP      10.100.43.99     <none>        443/TCP                                   5m34s
my-gitlab-gitaly                             ClusterIP      None             <none>        8075/TCP,9236/TCP                         5m34s
my-gitlab-gitlab-exporter                    ClusterIP      10.96.78.140     <none>        9168/TCP                                  5m34s
my-gitlab-gitlab-shell                       ClusterIP      10.101.112.10    <none>        22/TCP                                    5m34s
my-gitlab-kas                                ClusterIP      10.110.138.43    <none>        8150/TCP,8153/TCP,8154/TCP,8151/TCP       5m34s
my-gitlab-minio-svc                          ClusterIP      10.96.8.173      <none>        9000/TCP                                  5m34s
my-gitlab-nginx-ingress-controller           LoadBalancer   10.106.52.236    <pending>     80:30410/TCP,443:30916/TCP,22:30397/TCP   5m34s
my-gitlab-nginx-ingress-controller-metrics   ClusterIP      10.100.248.103   <none>        10254/TCP                                 5m34s
my-gitlab-postgresql                         ClusterIP      10.105.157.69    <none>        5432/TCP                                  5m34s
my-gitlab-postgresql-headless                ClusterIP      None             <none>        5432/TCP                                  5m34s
my-gitlab-postgresql-metrics                 ClusterIP      10.104.132.32    <none>        9187/TCP                                  5m34s
my-gitlab-prometheus-server                  ClusterIP      10.97.19.76      <none>        80/TCP                                    5m34s
my-gitlab-redis-headless                     ClusterIP      None             <none>        6379/TCP                                  5m34s
my-gitlab-redis-master                       ClusterIP      10.102.61.189    <none>        6379/TCP                                  5m34s
my-gitlab-redis-metrics                      ClusterIP      10.100.121.44    <none>        9121/TCP                                  5m34s
my-gitlab-registry                           ClusterIP      10.97.180.143    <none>        5000/TCP                                  5m34s
my-gitlab-webservice-default                 ClusterIP      10.102.1.130     <none>  

#kubectl get po
NAME                                                  READY   STATUS                       RESTARTS        AGE
db-989b6b476-j54zw                                    1/1     Running                      2 (46m ago)     25h
debug                                                 1/1     Running                      164 (10m ago)   45h
load-generator                                        0/1     Error                        0               41m
mongo                                                 1/1     Running                      3 (46m ago)     154m
my-gitlab-certmanager-596bc45d5c-pdkg8                1/1     Running                      0               6m43s
my-gitlab-certmanager-cainjector-7b6bd9b5cd-qtmml     1/1     Running                      0               6m43s
my-gitlab-certmanager-webhook-77c4844677-6652n        1/1     Running                      0               6m43s
my-gitlab-gitaly-0                                    0/1     PodInitializing              0               6m43s
my-gitlab-gitlab-exporter-6df776d8fb-45c99            0/1     PodInitializing              0               6m42s
my-gitlab-gitlab-runner-58cc7cd54f-664kn              0/1     Running                      1 (101s ago)    6m43s
my-gitlab-gitlab-shell-6b86b74bd7-kzj9c               1/1     Running                      0               6m28s
my-gitlab-gitlab-shell-6b86b74bd7-zpt4p               0/1     PodInitializing              0               6m43s
my-gitlab-issuer-1-rptzr                              0/1     Completed                    0               6m43s
my-gitlab-kas-86457f8666-n4w26                        1/1     Running                      0               6m28s
my-gitlab-kas-86457f8666-rwpfs                        1/1     Running                      0               6m42s
my-gitlab-migrations-1-5j4z9                          0/1     PodInitializing              0               6m43s
my-gitlab-minio-67ddc9cf87-lckln                      1/1     Running                      0               6m43s
my-gitlab-minio-create-buckets-1-njvxp                0/1     Completed                    0               6m43s
my-gitlab-nginx-ingress-controller-7bc4697598-2dbqn   1/1     Running                      0               6m43s
my-gitlab-nginx-ingress-controller-7bc4697598-x6fp7   1/1     Running                      0               6m43s
my-gitlab-postgresql-0                                2/2     Running                      0               6m43s
my-gitlab-prometheus-server-697d499f77-6xzsh          2/2     Running                      0               6m43s
my-gitlab-redis-master-0                              2/2     Running                      0               6m43s
my-gitlab-registry-7d85f6f7ff-4wvgs                   1/1     Running                      0               6m43s
my-gitlab-registry-7d85f6f7ff-xdpgq                   1/1     Running                      0               6m28s
my-gitlab-sidekiq-all-in-1-v2-5bc549bf5d-z7skl        0/1     Pending                      0               6m42s
my-gitlab-toolbox-77f5f87bf7-w4vxr                    0/1     PodInitializing              0               6m42s
my-gitlab-webservice-default-7df675fc8-ll6qc          0/2     Pending                      0               6m28s
my-gitlab-webservice-default-7df675fc8-nrmq8          0/2     Init:2/3

#kubectl get secret
NAME                                     TYPE                 DATA   AGE
domain-pki                               kubernetes.io/tls    2      24h
my-gitlab-acme-key                       Opaque               1      6m28s
my-gitlab-certmanager-webhook-ca         Opaque               3      7m22s
my-gitlab-gitaly-secret                  Opaque               1      7m58s
my-gitlab-gitlab-initial-root-password   Opaque               1      8m
my-gitlab-gitlab-kas-secret              Opaque               1      7m57s
my-gitlab-gitlab-runner-secret           Opaque               2      7m58s
my-gitlab-gitlab-shell-host-keys         Opaque               8      7m54s
my-gitlab-gitlab-shell-secret            Opaque               1      7m59s
my-gitlab-gitlab-suggested-reviewers     Opaque               1      7m57s
my-gitlab-gitlab-workhorse-secret        Opaque               1      7m54s
my-gitlab-kas-private-api                Opaque               1      7m57s
my-gitlab-minio-secret                   Opaque               2      7m58s
my-gitlab-postgresql-password            Opaque               2      7m59s
my-gitlab-rails-secret                   Opaque               1      7m55s
my-gitlab-redis-secret                   Opaque               1      7m59s
my-gitlab-registry-httpsecret            Opaque               1      7m53s
my-gitlab-registry-notification          Opaque               1      7m53s
my-gitlab-registry-secret                Opaque               2      7m55s
sh.helm.release.v1.my-gitlab.v1          helm.sh/release.v1   1      8m19s

#kubectl get cm
NAME                                         DATA   AGE
my-gitlab-certmanager-issuer-certmanager     2      9m12s
my-gitlab-gitaly                             2      9m12s
my-gitlab-gitlab-chart-info                  2      9m12s
my-gitlab-gitlab-exporter                    2      9m12s
my-gitlab-gitlab-runner                      6      9m12s
my-gitlab-gitlab-shell                       3      9m12s
my-gitlab-gitlab-shell-sshd                  1      9m12s
my-gitlab-kas                                1      9m12s
my-gitlab-migrations                         7      9m12s
my-gitlab-minio-config-cm                    3      9m12s
my-gitlab-nginx-ingress-controller           11     9m12s
my-gitlab-nginx-ingress-custom-add-headers   1      9m12s
my-gitlab-nginx-ingress-tcp                  1      9m12s
my-gitlab-postgresql-init-db                 2      9m12s
my-gitlab-prometheus-server                  6      9m12s
my-gitlab-redis                              3      9m12s
my-gitlab-redis-health                       6      9m12s
my-gitlab-redis-scripts                      1      9m12s
my-gitlab-registry                           3      9m12s
my-gitlab-sidekiq                            8      9m12s
my-gitlab-toolbox                            8      9m12s
my-gitlab-webservice                         8      9m12s
my-gitlab-webservice-tests                   1      9m12s
my-gitlab-workhorse-default                  3      9m12s

### installation gitlab avec helm #####################"
#helm install my-gitlab gitlab/gitlab --version 6.10.3 --set certmanager-issuer.email=you@toto.com
#helm install -n development my-gitlab2 gitlab/gitlab --version 6.10.3 --set certmanager-issuer.email=akhibou1sokhona@gmail.com avec namespaces development

lien helm et gitlab
https://artifacthub.io/packages/helm/gitlab/gitlab

openshift okd 
https://mirror.openshift.com/pub/openshift-v4/clients/oc/latest/linux/
https://www.okd.io/

