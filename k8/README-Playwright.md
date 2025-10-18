# Build and Deploy Playwright Tests to Kubernetes

## Prerequisites
- Docker installed
- Kubernetes cluster running (minikube, kind, or cloud provider)
- kubectl configured

## Steps

### 1. Build Docker Image
```bash
# Navigate to todomvc directory
cd capstone_nagashree_playwright/examples/todomvc

# Build the Docker image with your DockerHub tag
docker build -t nagashreeha/playwright-todomvc:latest .
```

### 2. Push to DockerHub
```bash
# Login to DockerHub
docker login

# Push the image to your DockerHub repository
docker push nagashreeha/playwright-todomvc:latest
```

### 3. Deploy to Kubernetes
```bash
# Deploy all components at once
kubectl apply -f k8/playwright-kube.yaml
```
```bash
# Deploy all components at once
kubectl apply -f k8/playwright-kube.yaml
```

### 4. Monitor Test Execution
```bash
# Check all resources in the namespace
kubectl get all -n playwright-tests

# View test logs
kubectl logs deployment/playwright-deployment -n playwright-tests

# Get detailed deployment info
kubectl describe deployment playwright-deployment -n playwright-tests
```

### 5. Clean up
```bash
# Delete everything
kubectl delete -f k8/playwright-kube.yaml
```

## Files Created
- `Dockerfile` - Containerizes Playwright tests
- `playwright-kube.yaml` - All Kubernetes manifests in one file (namespace, configmap, secret, service, deployment)

## What it does
1. Creates a dedicated namespace `playwright-tests`
2. Uses ConfigMap for test configuration
3. Uses Secret for test credentials
4. Creates a Service to expose the tests
5. Deploys Playwright tests using official Docker image
6. Provides test results and logs through kubectl