# Istio Service Mesh (v1.6)
[Istio](https://istio.io/docs/concepts/what-is-istio/) is an open source independent [service mesh](https://istio.io/docs/concepts/what-is-istio/#what-is-a-service-mesh) that provides the fundamentals to run a distributed microservice architecture. Istio makes it easy to create a network of deployed services with load balancing, service-to-service authentication, monitoring, and more, with [few](https://istio.io/docs/tasks/observability/distributed-tracing/overview/#trace-context-propagation) or no code changes in service code. 

This is done by adding Istio support to services by deploying a special sidecar proxy throughout the environment that intercepts all network communication between microservices, then configure and manage Istio using its control plane functionality, which provides:
* **Intelligent Load balancing** - Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
* **Intelligent Routing** - Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
* **API Management** - A pluggable policy layer and configuration API supporting access controls, rate limits and quotas.
* **Visibility** - Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.
* **Security** - Secure service-to-service communication in a cluster with strong identity-based authentication and authorization.

> Istio service mesh explained [here](https://www.youtube.com/watch?v=VzQetbvXCAw)

## Explore Istio
* [Architecture](/architecture/readme.md)
* [Istio install on Docker Desktop](/implementation/istio-install-local-readme.md)
* [Hello Istio](/implementation/hello-istio-readme.md)
* [Service Mesh features](/concepts/features-readme.md)
* [Istio deployment models](https://istio.io/docs/ops/deployment/deployment-models/)
* [Istio in AKS](https://docs.microsoft.com/en-us/azure/aks/servicemesh-istio-install?pivots=client-operating-system-linux)