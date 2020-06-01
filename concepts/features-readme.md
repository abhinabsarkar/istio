# Service Mesh Features
Each of the service meshes have a natural fit and focus on supporting specific scenarios, but you'll typically find that most will implement a number of, if not all, of the following capabilities.

### Traffic management
* Protocol – layer 7 (http, grpc)
* Dynamic Routing – conditional, weighting, mirroring
* Resiliency – timeouts, retries, circuit breakers
* Policy – access control, rate limits, quotas
* Testing - fault injection
### Security
* Encryption – mTLS, certificate management, external CA
* Strong Identity – SPIFFE or similar
* Auth – authentication, authorisation
### Observability
* Metrics – golden metrics, prometheus, grafana
* Tracing - traces across workloads
* Traffic – cluster, ingress/egress
### Mesh
* Supported Compute - Kubernetes, virtual machines
* Multi-cluster - gateways, federation