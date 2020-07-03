# Istio Architecture

## High level view
An Istio service mesh is logically split into a data plane and a control plane.
* **Data Plane** is composed of a set of intelligent proxies (Envoy) deployed as sidecars. These proxies mediate and control all network communication between microservices. They also collect and report telemetry on all mesh traffic.
* **Control Plane** manages and configures the proxies to route traffic. Istio 1.6 reorganizes the control plane into one service 'istiod'.

> The data plane (the Envoy proxy) is written in C++, however, all of the Istio control plane components are written in Go.

![Alt text](/images/istio15.jpg)

## Getting closer to the Data Plane
Istio uses an extended version of the [Envoy (L7) proxy.](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy) Envoy proxies are the only Istio components that interact with data plane traffic. Envoy proxies are deployed as sidecars to services. It is important to understand that the sidecar injection into the application pods happens automatically, though manual injection is also possible. Traffic is directed from the application services to and from these sidecars without developers needing to worry about it.

### How sidecar injection works?
In simple terms, sidecar injection is adding the configuration of additional containers to the pod template. The added containers needed for the Istio service mesh are:

* istio-init - This init container is used to setup the iptables rules so that inbound/outbound traffic will go through the sidecar proxy. An init container is different than an app container in following ways:
    * It runs before an app container is started and it always runs to completion.
    * If there are many init containers, each should complete with success before the next container is started.  
So, you can see how this type of container is perfect for a set-up or initialization job which does not need to be a part of the actual application container. In this case, istio-init does just that and sets up the iptables rules.

* istio-proxy This is the actual sidecar proxy (based on Envoy).

> This is explained in detail [here](https://istio.io/blog/2019/data-plane-setup/)

## Getting closer to the Control Plane
From Istio v1.5, the control plane has been reorganized into one service i.e. *istiod* which provides proxy sidecar loading, mesh calculation, security and validation. The different components of the istiod service are mentioned below:
* Pilot - Provides service discovery and traffic management policy/configuration for the proxies.
* Galley - Abstracts and provides configuration to components. It also does validation for Istio.
* Citadel - It provides security features by providing TLS encryption to every Envoy proxy. It also provides authentication, authorization and audit (AAA) tools to protect services and data.

> Mixer Adapater plugins are reimplemented within the mesh as Envoy plugins. Mixer enforces access control and usage policies. Collects telemetry from the proxies that is pushed into Prometheus.
