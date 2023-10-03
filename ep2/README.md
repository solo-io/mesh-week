# Mesh Week episode 2: Traffic Management

[Link to the slides](https://docs.google.com/presentation/d/1vodrDm50FaKoYIWtCAdtHFCuuyeAZ6zfWMqxQEBBa9w/edit?usp=sharing)


## Setup

Create the cluster:

```bash
kind create cluster --name istio --image kindest/node:v1.28.0
```

Install Istio:

```bash
istioctl install --set profile=demo -y
kubectl kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v0.8.0" | kubectl apply -f -;
```
