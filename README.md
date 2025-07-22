
# 🔄 Update Deployment Image from Nginx to httpd:2.4 on Minikube

This guide walks through updating the container image in a Kubernetes deployment from `nginx:latest` to `httpd:2.4` using `kubectl` in a **Minikube** cluster.

---

## 📁 Project Structure

```
nginx-deployment/
├── nginx-deployment.yaml   # Original deployment YAML
├── README-scale.md         # Scaling to 5 replicas
└── README-update.md        # Update image from nginx to httpd
```

---

## 🛠 Prerequisites

- ✅ Minikube installed and running
- ✅ `kubectl` configured to use Minikube
- ✅ An existing deployment named `nginx-deployment`

Start Minikube if needed:
```bash
minikube start
```

---

## 🔍 Step 1: Verify the Current Deployment

List deployments and check the image:
```bash
kubectl get deployments
kubectl describe deployment nginx-deployment
```

You should see it currently uses `nginx:latest`.

---

## 🔄 Step 2: Update the Deployment Image

Update the deployment image to `httpd:2.4`:
```bash
kubectl set image deployment/nginx-deployment nginx=httpd:2.4
```

- `deployment/nginx-deployment`: name of the deployment
- `nginx=httpd:2.4`: container name and new image

---

## ⏳ Step 3: Monitor Rollout

Check if the update was successful:
```bash
kubectl rollout status deployment/nginx-deployment
```

---

## ✅ Step 4: Verify the Updated Image

Confirm the new image is in use:
```bash
kubectl describe deployment nginx-deployment | grep Image
```

Expected output:
```
Image:  httpd:2.4
```

You can also check pods:
```bash
kubectl get pods -o wide
```

---

## 🔁 Optional: Roll Back the Change

Undo the update if needed:
```bash
kubectl rollout undo deployment nginx-deployment
```

---

## 🧹 Cleanup

To delete the deployment:
```bash
kubectl delete deployment nginx-deployment
```

---

## 🧑‍💻 Author

**Suraj Molke**  
[GitHub](https://github.com/smolke9)

---

## 🏷️ Tags

`#kubernetes` `#httpd` `#nginx` `#minikube` `#deployment` `#kubectl` `#devops`
