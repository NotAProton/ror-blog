# RORBlog

Because the world needed another blogging app written in RoR but deployed on k8s for handling the large traffic of two visitors with user agents being google-bot and bing-bot twice a day...

## Features
- **Ruby on Rails**: A modern web framework for building scalable applications.
- **PostgreSQL**: A powerful, open-source relational database.
- **Kubernetes (K8s)**: Container orchestration for managing deployments.
- **Ingress with Nginx**: Handles routing of incoming requests.

## Deployment
Follow these steps to deploy the application.

### 1. Apply the YAML files
```sh
kubectl apply -f postgres.yml
kubectl apply -f rorblog.yml
kubectl apply -f ingress.yml
```

### 2. Verify Deployment
```sh
kubectl get pods
kubectl get services
kubectl get ingress
```

### 3. Access the Application
If your cluster is local, add the following entry to your `/etc/hosts` file:
```
127.0.0.1  rorblog.example
```
Then, open [http://rorblog.example](http://rorblog.example) in your browser.

## Kubernetes Configuration
### **1. Ingress (ingress.yml)**
Defines routing rules and directs traffic to the application service.

### **2. PostgreSQL (postgres.yml)**
Manages database deployment, persistent storage, and environment configuration.

### **3. RORBlog Deployment (rorblog.yml)**
Deploys the Rails application and connects it to the PostgreSQL database.

## Notes
- Ensure that the PostgreSQL password is securely managed in production.
- The container image for RORBlog (`rorblog:0.0.3`) must be built locally before deployment:
  ```sh
  docker build -t rorblog:0.0.3 .
  ```
- The `ingress.yml` configuration requires an ingress controller. Install it if necessary:
  ```sh
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
  ```

## License
Do whatever you want, just don't blame me when your cluster catches fire.
