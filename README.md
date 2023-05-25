# inplace-resize

killercoda:
```
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.27.1%2BK3s1 sh -s - --kube-apiserver-arg feature-gates=InPlacePodVerticalScaling=true
```
Minikube:
```
minikube start --kubernetes-version=v1.27.1 --feature-gates=InPlacePodVerticalScaling=true
```
Consider the manifest for a Pod that has one Container.
```
kubectl apply -f pod.yaml
```
Create the pod in the qos-example namespace:
```
kubectl create namespace qos-example
```
View detailed information about the pod:
```
kubectl get pod -n qos-example -oyaml
```
Patch the Pod's Container with CPU limits both set to 120m:
```
kubectl -n qos-example patch pod qos-demo-5 --patch '{"spec":{"containers":[{"name":"qos-demo-ctr-5", "resources":{"limits":{"cpu":"120m"}}}]}}'
```
Query the Pod's detailed information after the Pod has been patched.
kubectl get pod -n qos-example -oyaml

Resources:
</br>
https://kubernetes.io/blog/2023/05/12/in-place-pod-resize-alpha/#when-to-use-this-feature
https://kubernetes.io/docs/tasks/configure-pod-container/resize-container-resources/
https://wuestkamp.medium.com/k8s-1-27-update-pod-requests-limits-for-running-pods-baa28565960e
https://youtu.be/7LuzKvnMdpk
