
# Demo Azure AKS Policy

## Deploy AKS cluster

## Connect to the cluster

```bash
# Login into Azure Cloud
az login
# Check if correct subscription is set
az account show
# Get kubernetes credentials (login into kubernetes cluster)
az aks get-credentials --overwrite-existing --resource-group aks02-rg  --name aks02 --admin
# Check if we are connected
kubectl get ns
```

## Demo preparation

```bash
# Deploy endless running container with restricted image
kubectl apply -f initial-pods.yaml -n default
```

## Go and enable AKS policy plugin and deploy them

## Testing policy: Ensure only allowed container images in AKS

```bash
kubectl run my-nginx --image=nginx --replicas=2 --port=80
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
