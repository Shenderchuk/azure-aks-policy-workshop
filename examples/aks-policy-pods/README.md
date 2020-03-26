
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
# Deploy endless running container with busybox without labels
kubectl apply -f initial-pods.yaml -n default

# Deploy nginx (image will be restricted)
kubectl run my-nginx --image=nginx --replicas=2 --port=80
```

## Go and enable AKS policy plugin and deploy them

## Testing policy: Ensure only allowed container images in AKS

```bash
service/hello-kubernetes   LoadBalancer   10.0.201.153   <pending>     80:31892/TCP   15s
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
