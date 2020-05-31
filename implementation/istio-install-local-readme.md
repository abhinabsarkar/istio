# Istio installation on Docker Desktop
 To install Istio v1.6 locally on windows 10, follow the below steps:
 * [Install Docker Desktop](https://docs.docker.com/docker-for-windows/install/) with supported Kubernetes version (> 1.15)
 * [Configure Docker Desktop](https://istio.io/docs/setup/platform-setup/docker/)
 * [Download Istio](https://istio.io/docs/setup/getting-started/#download)
 > I prefer WSL & hence using the Linux flavour. But Istio is also available for Windows. Go to the [Istio release page](https://github.com/istio/istio/releases) to download the installation file for your OS.

 ### Install Istio
 At this point, assumption is previous steps have already been completed & kubectl is already installed on wsl.
 ```bash
# If wsl kubeconfig is not configured to point to the docker desktop, configure the same
# Create the .kube folder under $HOME, if the .kube folder is not present
mkdir ~/.kube
# Copy the kubeconfig from Windows to WSL Ubuntu folder
cp /mnt/c/Users/abhinab/.kube/config ~/.kube/config
# Check the kubectl configuration
kubectl get nodes
NAME             STATUS   ROLES    AGE   VERSION
docker-desktop   Ready    master   91m   v1.16.6-beta.0
```
For exploring the various features of Istio, install the `demo` configuration profile. This will install all the core components & complete set of addons. 
> The list of configuration profiles can be found [here](https://istio.io/docs/setup/additional-setup/config-profiles/)
```bash
# Install Istio with the 'demo' profile 
istioctl manifest apply --set profile=demo
Detected that your cluster does not support third party JWT authentication. Falling back to less secure first party JWT. See "https://istio.io/docs/ops/best-practices/security/#configure-third-party-service-account-tokens for details."
✔ Istio core installed
✔ Istiod installed
✔ Ingress gateways installed
✔ Egress gateways installed
✔ Addons installed
✔ Installation complete
 ```

 