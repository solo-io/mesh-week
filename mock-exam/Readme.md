# Mock exam


## IstioOperator

```bash
kubectl create ns egress
kubectl create ns frontend
kubectl create ns payments
istioctl install -f mock-exam/installation/istio-operator.yaml -y
```

## Traffic management

```bash
export NAME=payments; export VERSION=v1; envsubst < traffic-management/httpbin.yaml | kubectl apply -n ${NAME} -f -

export NAME=frontend; export VERSION=v1; envsubst < traffic-management/httpbin.yaml | kubectl apply -n ${NAME} -f -
```
