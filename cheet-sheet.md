## Redis
### To Create Redis cluster:
`kubectl create -f ./redis.yaml`

### View pods: 
`kubectl get pods`
 
### View Service:
`kubectl get service`
### Frontend service 

## Create the service 
`kubectl creatd -f frontend-service.yaml`

## [Describe](https://kubernetes-v1-4.github.io/docs/user-guide/kubectl/kubectl_describe/) it
`kubectl descrive svc frontend`

## Frontend Deployment AutoDiscovered  
### Create Frontend (Redis ENV_VAR are auto-discovered using DNS)
`kubectl create -f frontend_env/frontend.yaml`

### View Pods
`kubectl get pods`

### View Service 
`kubectl get service`

### Access Service
`minikube service frontend`

### List of pods with ip address
`kubectl get pods -o wide`

### pod actions using labels 
`kubectl get pods -l tier=frontend`

### AutoScale pods
`kubectl scale --replica 4 deployment/frontend`

### View Deployment
`kubectl get deployment`

### View deployment details 
`kubectl get deployment fronted -o yaml` 

### Delete deployment
`kubectl delete -f frontend_env/frontend.yaml`
## Frontend ConfigMap

### Frontend Deployment (Redis ENV_VAR are set using Confimap)
`kubectl create -f frontend_configmap/frontend.yaml`

### [Describe](https://kubernetes-v1-4.github.io/docs/user-guide/kubectl/kubectl_describe/) Pod to debug the issue 
```
kubectl get pods 
kubectl describe pods <POD NAME>
```
### Update configmap
1. change ConfigMap values: `kubectl edit configmap frontend`
2. Save Configmap locally: `kubectl get configmap frontend  -o yaml > frontend_configmap/configmap.yaml`
3. Delete the Pods `kubectl delete pods -l tier=frontend`

### Update Deployment 
1. edit deployment `kubectl edit deployment frontend`

## Rolling Upgrade 
### Build new container 
```
cd php-redis/
make container
docker run ramakuka/gb-frontend-amd64:v5
```

## Edit deployment
`kubectl edit deployment frontend`