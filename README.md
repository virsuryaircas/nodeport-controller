# # k get np - K8s CRD NodePort Controller

Tired of manually checking machine IPs and NodePort numbers to access your services? This **NodePort Controller** is a lightweight Kubernetes controller that automatically watches for `NodePort` services across your cluster and maintains a custom resource for each, summarizing key details like ports, node IPs, and age.

## 🌍 Use Case

- **Testing & Development**: Ideal for these environments where most services are of type `NodePort`.


## 🚀 Features

- **Clickable Links**: Automatically generates clickable URLs combining node IP and NodePort number for easy access to your services.

## 🏗️ How It Works

The NP controller:

1. Watches `Service` objects with type `NodePort`.
2. Populates it with details:
   - NAME
   - NODE-IP:PORT
   - ClusterIP
   - PORT(s)
   - AGE
3. Updats the np if the nodeport number updated.
4. Deletes the np if the service is deleted.
5. Performs initial sync and orphaned CR cleanup on startup.

## ⚙️ Setup Instructions

```bash
# Clone the repository
git clone https://github.com/virsuryaircas/nodeport-controller.git

# Navigate to the project directory
cd nodeport-controller

# Apply the two manifests
kubectl apply -k .

# Verify the pod is in running state
kubectl get po -n kube-system

#Simply get the clickable URL
kubectl get np

#Output
NAME         NODE-IP:PORT                CLUSTER-IP      PORT(S)   AGE
helloworld   http://192.168.0.18:31770   10.43.120.122   80/TCP    1m
```
> **NOTE:** Ensure the `CRD` is installed before running the controller.

## 📝 Docker Image Changelog

**Docker Image**: [virsuryaircas/nodeport-controller](https://hub.docker.com/r/virsuryaircas/nodeport-controller)

### Version 1
- Initial release (inception)
