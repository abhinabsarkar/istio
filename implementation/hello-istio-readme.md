# Hello Istio

Ensure that Istioctl is configured permanently in the PATH.
```bash
# Set up the path permanently for istioctl
nano ~/.profile
export PATH="$PATH:/mnt/c/abhinab/istio/istio-1.6.0/bin"
# exit & login again
```
Install [bookinfo sample application](https://istio.io/docs/examples/bookinfo/)
```bash
# Enable automatic sidecar injection
kubectl label namespace abs istio-injection=enabled
# Install bookinfo application
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.6/samples/bookinfo/platform/kube/bookinfo.yaml -n abs
# Verify everything is working correctly up to this point
kubectl exec -it $(kubectl get pod -n abs -l app=ratings -o jsonpath='{.items[0].metadata.name}') -n abs -c ratings -- curl productpage:9080/productpage | grep -o "<title>.*</title>"
# Expose the application by creating an Istio Ingress Gateway
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.6/samples/bookinfo/networking/bookinfo-gateway.yaml -n abs
# Validate the istio app configuration
istioctl analyze -n abs
# Test the application by browsing the below url
http://localhost:80/productpage
```
Enable the Istio GUI dashboard
```bash
istioctl dashboard kiali
```

Traffic management via Request routing
```bash
# Apply default destination rules
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.6/samples/bookinfo/networking/destination-rule-all.yaml -n abs

# Apply virtual service. This will configure Istio to route to the v1 version of the Bookinfo microservices
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.6/samples/bookinfo/networking/virtual-service-all-v1.yaml -n abs

# Apply route based on user identity header
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.6/samples/bookinfo/networking/virtual-service-reviews-test-v2.yaml -n abs
```
All traffic from a specific user is routed to a specific service version. In this case, all traffic from a user named Jason will be routed to the service reviews:v2.