OK, mình sẽ tổng hợp **các lệnh Kubernetes (kubectl)** theo kiểu **cheat sheet + thực chiến**, đủ để bạn dùng hằng ngày (Dev + DevOps).

---

# 🧠 1. Nhóm lệnh cơ bản

### 📌 Kiểm tra cluster

```bash
kubectl cluster-info
kubectl version
kubectl config view
kubectl config current-context
kubectl config use-context <context>
```

---

# 📦 2. Làm việc với resource (CRUD)

## 🔹 Get (xem resource)

```bash
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get all
```

Thêm options:

```bash
kubectl get pods -o wide
kubectl get pods -A              # all namespace
kubectl get pods -n <namespace>
```

---

## 🔹 Describe (xem chi tiết)

```bash
kubectl describe pod <pod-name>
kubectl describe deployment <name>
```

👉 dùng khi debug

---

## 🔹 Create / Apply

```bash
kubectl apply -f file.yaml
kubectl create -f file.yaml
```

👉 Best practice: dùng `apply`

---

## 🔹 Delete

```bash
kubectl delete pod <pod>
kubectl delete -f file.yaml
```

---

# 🚀 3. Deployment (quan trọng nhất)

## 🔹 Tạo deployment

```bash
kubectl create deployment my-app --image=nginx
```

---

## 🔹 Scale

```bash
kubectl scale deployment my-app --replicas=5
```

---

## 🔹 Update image (trigger rollout)

```bash
kubectl set image deployment/my-app app=nginx:1.26
```

---

## 🔹 Rollout

```bash
kubectl rollout status deployment my-app
kubectl rollout history deployment my-app
kubectl rollout undo deployment my-app
kubectl rollout restart deployment my-app
```

---

# 🧩 4. Pod (debug nhiều)

## 🔹 Xem pod

```bash
kubectl get pods
```

---

## 🔹 Logs

```bash
kubectl logs <pod>
kubectl logs -f <pod>
kubectl logs <pod> -c <container>
```

---

## 🔹 Exec vào container

```bash
kubectl exec -it <pod> -- /bin/sh
kubectl exec -it <pod> -- /bin/bash
```

---

## 🔹 Port-forward

```bash
kubectl port-forward pod/<pod> 8080:80
```

---

# 🌐 5. Service

```bash
kubectl get svc
kubectl expose deployment my-app --type=NodePort --port=80
```

---

# 📁 6. Namespace

```bash
kubectl get ns
kubectl create ns dev
kubectl config set-context --current --namespace=dev
```

---

# ⚙️ 7. ConfigMap & Secret

## 🔹 ConfigMap

```bash
kubectl create configmap my-config --from-literal=key=value
kubectl get configmap
```

---

## 🔹 Secret

```bash
kubectl create secret generic my-secret \
  --from-literal=password=123456
```

---

# 📊 8. Monitoring / Debug

```bash
kubectl top pods
kubectl top nodes
kubectl get events
```

---

# 📤 9. Export YAML

```bash
kubectl get deployment my-app -o yaml > deploy.yaml
```

---

# ✏️ 10. Edit trực tiếp (như bạn đang dùng)

```bash
kubectl edit deployment my-app
```

---

# 🔄 11. Autoscaling (HPA)

```bash
kubectl autoscale deployment my-app \
  --cpu-percent=70 --min=2 --max=10
```

---

# 🔍 12. Lọc bằng label

```bash
kubectl get pods -l app=my-app
```

---

# ⚡ 13. Một số lệnh nâng cao (rất hữu ích)

## 🔹 Dry run (test trước)

```bash
kubectl apply -f file.yaml --dry-run=client
```

---

## 🔹 Explain (xem schema YAML)

```bash
kubectl explain deployment
kubectl explain deployment.spec.template
```

---

## 🔹 Diff (so sánh config)

```bash
kubectl diff -f file.yaml
```

---

# 🧠 14. Workflow chuẩn Dev

Thực tế bạn sẽ dùng combo:

```bash
# 1. Export
kubectl get deploy my-app -o yaml > deploy.yaml

# 2. Sửa file

# 3. Apply
kubectl apply -f deploy.yaml

# 4. Check rollout
kubectl rollout status deployment my-app
```

---

# 🎯 Tóm tắt

## Nhóm quan trọng nhất:

- `get` → xem
- `describe` → debug
- `apply` → deploy
- `logs` → debug app
- `exec` → vào container
- `scale` → tăng pod
- `rollout` → deploy process

---

# 🚀 Nếu bạn muốn level up

Mình có thể làm tiếp cho bạn:

- Cheat sheet 1 trang PDF (in ra dùng)
- Giải thích từng resource: Pod → Deployment → Service → Ingress
- Hoặc **real project flow (CI/CD + K8s)** theo stack bạn đang dùng (NextJS + Golang)

Bạn muốn đi theo hướng nào?
