# K8s_example

0/ Création du namespace

kubectl create namespace eval 

1/ Création des secrets en déclaratifs (cf fichiers YAML)
kubectl create -f mysql-user-secet.yml -n eval
kubectl create -f mysql-user-secret.yml -n eval
kubectl describe secret mysql-user -n eval


### Création  du PV 




### CREATION D'UN STATEFULSET 
Création de statefulset.yml

### CREATION DE 2 SECRETS

kubectl create secret generic mysql-root-password --from-literal MYSQL_ROOT_PASSWORD=my-secret-pw -n eval
kubectl create secret generic mysql-user --from-literal=MYSQL_USER=vincent --from-literal=MYSQL_PASSWORD=vincent-pw@ --from-literal=MYSQL_DATABASE=eval-db -n eval

kubectl get secret -n eval
kubectl get secret mysql-root-password -o jsonpath='{.data.MYSQL_ROOT_PASSWORD}'| base64 --decode
kubectl get secret mysql-user -o jsonpath='{.data.MYSQL_PASSWORD}'| base64 --decode

### CREATION d'UN PV
Création de mysql-local-data-folder-pv.yml
Création de my-service.yml
Mise à jour de statefulset.yml avec le volumeClaimTemplate

kubectl apply -f mysql-local-data-folder-pv.yml #les pv ne sont pas associés à un namespace
kubectl create -f statefulset.yml -n eval 
kubectl get statefulset -n eval

docker login -u dock4vincent
token :  xxxxxx
 
docker image build . -t dock4vincent/k8s-dst-eval-fastapi:1.0.3
docker push dock4vincent/k8s-dst-eval-fastapi:1.0.3

 
Retagage si nécessaire 
docker tag eval-image:latest dock4vincent/k8s-dst-eval-fastapi:1.0.x


kubectl logs -f fastapi

kubectl run -it --rm --image=mysql --restart=Never mysql-client -- mysql --host mysql --password=<super-secret-password>

kubectl exec -it fastapi -- /bin/bash
