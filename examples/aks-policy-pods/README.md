
# Demo Azure AKS Policy

## Deploy AKS cluster

```bash
# Login into Azure Cloud
az login
# Check if correct subscription is set
az account show
# Create a resource group for AKS cluster
az group create -g aks03-rg -l westeurope
# Createa an AKS cluster
az aks create -g aks03-rg -n aks03 --node-count 1 --no-ssh
```

## Connect to the cluster

```bash
# Get kubernetes credentials (login into kubernetes cluster)
az aks get-credentials --overwrite-existing --resource-group aks03-rg  --name aks03 --admin
# Check if we are connected
kubectl get ns
kubectl get nodes
```

## Demo preparation

```bash
# Deploy endless running container with busybox without labels
kubectl apply -f initial-pods.yaml -n default

# Deploy nginx (image will be restricted)
kubectl run my-nginx --image=nginx --replicas=2 --port=80
```

## Go and enable AKS policy plugin and deploy them

### Ensure only allowed container images in AKS

Parameters: `^busybox$`

### Enforce labels on pods in AKS

Parameters: `env`

## Testing policy: Ensure only allowed container images in AKS

```bash
kubectl apply -f hello-kubernetes.yaml -n default
```

## Testing policy: Enforce labels on pods in AKS

```bash
kubectl apply -f pod-without-label.yaml -n default
```

```bash
kubectl apply -f pod-with-label.yaml -n default
```

## Check existing policies

Check which exactly policies were applied

```bash
kubectl -n azure-policy get cm -o yaml
```

Check management container and logs

```bash
kubectl -n kube-system get pods -l app=azure-policy
```
