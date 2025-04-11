# Kubernetes Deployment for Tic Tac Toe

This directory contains Kubernetes manifests for deploying the Tic Tac Toe application.

## Components

1. **Deployment** - Manages the application pods with scaling and update strategies
2. **Service** - Exposes the application within the cluster
3. **Ingress** - Exposes the application to external traffic

## Prerequisites

- Kubernetes cluster (e.g., Minikube, EKS, GKE, AKS)
- kubectl configured to communicate with your cluster
- Container registry access (GitHub Container Registry in this case)

## Setup Container Registry Secret

Before deploying, you need to create a secret for pulling images from GitHub Container Registry:

```bash
kubectl create secret docker-registry github-container-registry \
  --docker-server=ghcr.io \
  --docker-username=YOUR_GITHUB_USERNAME \
  --docker-password=YOUR_GITHUB_TOKEN \
  --docker-email=YOUR_EMAIL
```

Replace the placeholders with your actual GitHub credentials.

## Deployment

To deploy the application:

```bash
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
kubectl apply -f kubernetes/ingress.yaml
```

## Accessing the Application

If you're using Minikube:

```bash
minikube service tic-tac-toe --url
```

If you've set up the Ingress with a domain, access it at the configured domain (e.g., tic-tac-toe.example.com).

## Scaling

To scale the application:

```bash
kubectl scale deployment tic-tac-toe --replicas=5
```

## Updating

When a new image is pushed to the registry, update the deployment:

```bash
kubectl rollout restart deployment tic-tac-toe
```

## Monitoring

Check deployment status:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
kubectl get ingress
```

View logs:

```bash
kubectl logs -l app=tic-tac-toe
```


## MY setup:
minikube start --profile=devsecops-demo
minikube profile list
minikube stop -p minikube
minikube profile devsecops-demo
minikube status

kubectl config current-context
kubectl get nodes

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl get pods -n argocd -w
kubectl get svc -n argocd

kubectl port-forward svc/argocd-server 9000:80 -n argocd
kubectl get secrets -n argocd
kubectl edit secret argocd-initial-admin-secret -n argocd
echo UklGLXVXRXEyT3BCOU04OQ== | base64 --decode
username: admin
Password: after decode

kubectl get pods --all-namespaces
kubectl exec -it tic-tac-toe-6c9fb64c9f-9vrhx -n <namespace> -- sh

 minikube service tic-tac-toe --url

 kubectl get ingress
 kubectl get pods -n ingress-nginx
 minikube addons enable ingress
 kubectl get pods -n ingress-nginx
 
 minikube ip
 sudo nano /etc/hosts
 kubectl describe ingress tic-tac-toe-ingress

kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
tic-tac-toe-6c9fb64c9f-2jb7d   1/1     Running   0          4m36s
tic-tac-toe-6c9fb64c9f-cq7xl   1/1     Running   0          4m26s
tic-tac-toe-6c9fb64c9f-htx2h   1/1     Running   0          4m47s

kubectl port-forward tic-tac-toe-6c9fb64c9f-2jb7d 3700:80
