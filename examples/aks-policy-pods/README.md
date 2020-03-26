
# Demo Azure AKS Policy

Demo preparation:

```bash
kubectl apply -f initial-pods.yaml -n default
```

## Testing Enforce Labels on Pods AKS policy

```bash
kubectl apply -f pod-without-label.yaml -n default
```

```bash
kubectl apply -f pod-with-label.yaml -n default
```

## Testing Allowed only repositories

```bash
kubectl run my-nginx --image=nginx --replicas=2 --port=80
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
