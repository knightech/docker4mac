### Docker for Mac exposes Kubernetes Services of type `LoadBalancer` to your Mac's network using `vpnkit` 

### Accessing HTTP(s) services with nginx-ingress and xip.io

* The [NGINX Ingress Controller](https://github.com/kubernetes/ingress-nginx) 
allows routing to services using hostnames mapped through an ingress 
[Ingress resources](https://kubernetes.io/docs/concepts/services-networking/ingress/)


* Combined with [xip.io](http://xip.io), you can configure access to HTTP services locally using 
addresses like `http://$service.127.0.0.1.xip.io/`

#### Setup nginx-ingress
* Install a recent version of Docker for Mac and [enable Kubernetes](https://docs.docker.com/docker-for-mac/#kubernetes)
* Deploy nginx-ingress from this repository's local implementation:

```
kubectl apply -f nginx-ingress/namespaces/nginx-ingress.yaml -Rf nginx-ingress
```

 or using helm
 
```
helm install --name nginx stable/nginx-ingress
```
and you can check progress using

```
kubectl --namespace default get services -o wide -w nginx-nginx-ingress-controller
```
* Visit http://127.0.0.1.xip.io/, which should show an unstyled 404.

#### Setup the example application

[`./helloworld/`](./helloworld/) is an example that maps ingress this way

* Visit hellish.127.0.0.1.xip.io/foo/bar, which should route to the helloworld app

#### In the testing directory there is a get.sh which will get all resources for all namespaces deployed to the cluster

```
sh get.sh
```

Running this command creates separate directories for each app