# DeployPostgres-Adminer
Deployment of Postgres and Adminer on Kubernetes cluster (minikube)

Create a namespace: `kubectl create namespace postgres`

Run:
```
kubectl apply -f postgres-configmap.yaml -n postgres
kubectl apply -f postgres-volume.yaml -n postgres
kubectl apply -f postgres-pvc.yaml -n postgres
kubectl apply -f postgres-deployment.yaml -n postgres
kubectl apply -f postgres-service.yaml -n postgres
kubectl apply -f ingress-controller.yaml -n postgres
```
Test:

`kubectl exec -it -n postgres "PostgresPodName" -- psql -h localhost -U appuser --password -p 5432 appdb`

`psql -h IP -U appuser --password -p PORT appdb`

To Find "PostgresPodName": `kubectl get pods -n postgres`

To Find IP : `minikube ip`

To Find PORT : `kubectl get svc -n postgres | grep 5432 `

The Password on values.yaml file : `strongpasswordapp`

Run: `minikube addons enable ingress`
And: `minikube tunnel`

Add: `IP adminer.k8s.com` ==> /etc/hosts

Ex: 192.168.59.142 adminer.k8s.com

Then browse: http://adminer.k8s.com

How To Connect:

```
Systeme: PostgresSQL
Server: postgres
User: appuser
Password: strongpasswordapp
DB: appdb
```
