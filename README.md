Writing a Kubernetes Operator in Java
-------------------------------------

Source code of my Devoxx Belgium 2019 talk.

[![Youtube: Writing a Kubernetes Operator in Java](https://img.youtube.com/vi/Q9nuMJ6usFY/0.jpg)](https://www.youtube.com/watch?v=Q9nuMJ6usFY)

Build:

```
./mvnw package -Pnative -DskipTests -Dnative-image.docker-build=true
docker build -f src/main/docker/Dockerfile.native -t instana/operator-demo:2 .
```

Run:

Download the `kind` executable from [https://github.com/kubernetes-sigs/kind/releases](https://github.com/kubernetes-sigs/kind/releases) and put it in your path. Then run:

```
kind create cluster --config ./kind-config.yaml
export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"

kind load docker-image instana/operator-demo:2

kubectl apply -f customresourcedefinition.yaml
kubectl apply -f deploy.yaml

kubectl apply -f customresource.yaml
```
