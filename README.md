# kubernetes_formation
https://github.com/dockersamples/example-voting-app
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 ####key#####
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
#kubectl exec nginx -- nginx -v ### pour executer le pod/conteneur
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





