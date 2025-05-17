# Voting App: A DevOps Learning Journey

This project is a fork of the Example Voting App that I used to learn and implement modern DevOps practices with Azure Kubernetes Service (AKS), ArgoCD, Azure DevOps, and Kubernetes.

## Original App Overview

A simple distributed application running across multiple containers with:

* A Python front-end web app for voting between two options
* Redis for collecting new votes
* A .NET worker consuming votes and storing them in...
* A Postgres database backed by a Docker volume
* A Node.js web app showing real-time voting results

## My DevOps Implementation

Through this project, I gained hands-on experience with:

### Azure Kubernetes Service (AKS)
- Set up and managed an AKS cluster in Azure
- Configured proper node pools and scaling settings
- Implemented Azure networking integration
- Applied resource quotas and limits for cost optimization

### GitOps with ArgoCD
- Implemented GitOps workflow for continuous deployment
- Configured ArgoCD for automated synchronization
- Set up application manifests and projects
- Managed rollouts and implemented health checks

### CI/CD with Azure DevOps
- Created build pipelines for containerizing applications
- Set up release pipelines for automated deployment
- Configured environment-specific variables
- Implemented automated testing within the pipeline

### Kubernetes Management
- Applied namespace organization for different environments
- Configured Kubernetes deployments, services, and ingress
- Implemented ConfigMaps and Secrets management
- Set up persistent storage for database components
- Configured horizontal pod autoscaling

### Monitoring and Observability
- Implemented logging with Azure Monitor
- Set up application metrics with Prometheus
- Created custom dashboards in Grafana
- Configured alerts for critical application states

## Getting Started

### Local Development

Download Docker Desktop for Mac or Windows. Docker Compose will be automatically installed. On Linux, make sure you have the latest version of Compose.

Run in this directory to build and run the app:

```
docker compose up
```

The `vote` app will be running at http://localhost:8080, and the `results` will be at http://localhost:8081.

### Docker Swarm Deployment

If you want to run it on a Docker Swarm, first make sure you have a swarm:

```
docker swarm init
```

Then deploy with:

```
docker stack deploy --compose-file docker-stack.yml vote
```

### Kubernetes Deployment

#### Standard Kubernetes (local or any K8s cluster)

```
kubectl create -f k8s-specifications/
```

The `vote` web app is available on port 31000, the `result` web app on port 31001.

To remove:

```
kubectl delete -f k8s-specifications/
```

#### Azure Kubernetes Service (AKS)

1. Set up your AKS cluster:
```
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys
```

2. Connect to your cluster:
```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

3. Deploy using either kubectl directly or through ArgoCD

#### ArgoCD Deployment

Once ArgoCD is installed on your cluster:

1. Apply the application manifest:
```
kubectl apply -f argo-app.yaml
```

2. Monitor the deployment through the ArgoCD UI

## Azure DevOps Pipeline

The repository includes Azure DevOps pipeline configurations in the `.azure-pipelines` directory that handle:

1. Building and testing application components
2. Publishing container images to Azure Container Registry
3. Deploying to AKS using Kubernetes manifests or ArgoCD


## Lessons Learned

This project has been invaluable for understanding:

- Container orchestration in production environments
- GitOps principles for infrastructure as code
- CI/CD best practices for microservices
- Cloud-native application design patterns
- Monitoring and observability in distributed systems

## Notes

- The voting application only accepts one vote per client browser
- This is a learning project, not a production-ready solution
- The original app was designed as a Docker demo, which I extended with modern DevOps practices
