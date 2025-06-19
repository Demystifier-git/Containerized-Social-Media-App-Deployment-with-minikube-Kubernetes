# 📱 Containerized Social Media App Deployment with minikube Kubernetes

This project demonstrates deploying a **containerized PHP + MySQL social media app** using **Minikube (Kubernetes)**.

---

## 🚀 Features

- PHP backend (PHP-Apache)
- MySQL database with persistent storage
- Kubernetes deployment using `Deployment`, `Service`, `Secret`, `StatefulSet`, flyway-job, configmap


## 🛠️ Requirements

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Docker](https://www.docker.com/)
- Internet connection to pull container images

---

## 📂 Directory Structure

.
├── k8s/
│ ├── statefulset.yaml
│ ├── phpDeployment.yaml
│ ├── services.yaml
      mysql-access.yaml
│ ├── configmaps/
│ └── secrets/
├
├── 
│ └── db.sql
└── README.md


---

## 🐳 Step-by-Step Deployment

### 1. Start Minikube

```bash
minikube start --memory=4096 --cpus=2
2. Enable Ingress and Metrics Server (Optional)

minikube addons enable ingress
minikube addons enable metrics-server
3. Deploy MySQL Database

kubectl apply -f k8s/secrets/mysql-secret.yaml
kubectl apply -f k8s/mysql-statefulset.yaml
Verify:


kubectl get pods -l app=mysql
4. Deploy PHP Application

kubectl apply -f k8s/php-deployment.yaml
Verify:


kubectl get pods -l app=php-app
5. Expose Services

kubectl apply -f k8s/services.yaml
minikube service php-service --url
Use the URL shown to access the app.


User: admin

Password: admin (or from Secret)

🗃️ Database Initialization:
use flyway job to migrate the db script,

This RBAC configuration is granting permissions to the default service account so that a Kubernetes Job (like Flyway database migrations) can do the following operations on Pods in the default namespaces
verbs: ["get", "list", "watch", "create", "delete"]
resources: ["pods"]

volumeMounts:
  - name: init-sql
    mountPath: /docker-entrypoint-initdb.d
volumes:
  - name: 
    configMap:
      name: mysql-persistent-storage
🔍 Troubleshooting
Use kubectl logs <pod> to check logs.

Use minikube dashboard for a GUI overview.

Make sure all services are Running before accessing endpoints.


📌 Notes
This setup is designed for local development/testing. For production, use AWS EKS, RDS, Secrets Manager, and CloudWatch integration.

Ensure secrets (like DB password, Datadog API key) are managed securely.

📚 Resources

👨‍💻 Author
Chukwuagoziem Delight David
GitHub: Demystifier-git