# TP7 - Orchestration avec Kubernetes

## Projet

Déploiment des deux microservices (service-user et service-order) sur Kubernetes avec Minikube. C'est les mêmes services que le TP6 mais orchestré par Kubernetes au lieu de Docker Compose.

## Architecture

deployment.yaml : définit les 2 pods (service-user + service-order)
service.yaml : expose service-order en LoadBalancer et service-user en ClusterIP

service-order communique avec service-user via le DNS interne de Kubernetes.

## Lancer le projet

minikube start
eval $(minikube docker-env)
docker build -t user-service:latest ../tp6-microservices/service-user/
docker build -t order-service:latest ../tp6-microservices/service-order/
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

Tester : curl http://$(minikube service service-order --url)/orders
