# KinD-Kubernetes

[KinD Install](https://kind.sigs.k8s.io/docs/user/quick-start/)

````
# Install Kind on mac
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.10.0/kind-darwin-amd64
chmod u+x kind
mv kind kind-0.10.0
mv kind-0.10.0 /usr/local/bin
ln -s /usr/local/bin/kind-0.10.0 /usr/local/bin/kind

# Creat DEV Cluster
kind create cluster --name dev --imge kindest/node:1.20.2 --config dev-cluster.yaml

#  Deploy NGinX Ingress 
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml
kubectl wait --namespace ingress-nginx --for=condition=ready pod --selector=app.kubernetes.io/component=controller --timeout=90s

# Test NGinX Ingress
kubectl apply -f ./NGinX/ingress-ngingx-example.yaml
curl localhost/foo
curl localhost/bar
```