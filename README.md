Setup
=====

Set up Istio on a Kubernetes cluster.
This was tested on Istio 14.1 using Minikube v1.26.0.

Deploy the `bookinfo` sample application:
```
 kubectl apply -f bookinfo.yaml
```

This is the Istio `bookinfo` sample app, with a slight change to turn up the logging level for the Istio proxy around the product page.

Then deploy the filter:
```
kubectl apply -f product-page-filter.yaml
```

And delete the product page pod (to restart it and pick up the new filter).

A request to the product page can be generated using the following command:
```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage
```

This will cause a HTTP request to be made against the product page, which will in turn result in request + response information being written to the Istio proxy logs.

