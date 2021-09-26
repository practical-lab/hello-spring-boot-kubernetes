# Spring Boot Kubernetes

## kubectl

```sh
kubectl proxy
```

## Create Docker image

```sh
docker build -t localhost/spring-demo .
docker run -p 8080:8080 localhost/spring-demo
docker images
docker tag xxxxxxxxxxxx skunitomo/spring-demo
docker push skunitomo/spring-demo:latest
```

## Generate Kubernetes deployment.yaml

```sh
kubectl get all
kubectl create deployment demo --image=skunitomo/spring-demo --dry-run -o=yaml > deployment.yaml
echo --- >> deployment.yaml
kubectl create service clusterip demo --tcp=8080:8080 --dry-run -o=yaml >> deployment.yaml
```

## Create Kubernetes cluster

```sh
kubectl apply -f deployment.yaml
kubectl get all
kubectl port-forward svc/demo 8080:8080
kubectl delete -f deployment.yaml
kubectl get all
```

## Helm

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
helm search repo bitnami | grep wordpress
helm install bitnami/wordpress --generate-name
kubectl get all
eval (kubectl get secret --namespace default wordpress-1632659333 -o jsonpath="{.data.wordpress-password}" | base64 --decode)
minikube tunnel
helm list
helm uninstall wordpress-1632659333
```
