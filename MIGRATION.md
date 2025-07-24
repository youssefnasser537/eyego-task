# Migration Guide: AWS TO GCP (GKE)

## 🔁 Common Preparation Steps

1. Clone this GitHub repository.
2. Ensure `kubectl`, `docker`, and the appropriate CLI tools are installed:
   - For GCP: `gcloud`
3. Authenticate to the new cloud provider using their CLI.

### 1. Create a GKE Cluster

```bash
gcloud container clusters create eyego-gke-cluster \
  --num-nodes=2 \
  --zone=europe-north1-a \
  --enable-ip-alias

### 2. Authenticate kubectl

gcloud container clusters get-credentials eyego-gke-cluster \
  --zone=europe-north1-a


### 3. Push Docker Image to Google Container Registry (GCR)

# Tag the image for GCR
docker tag eyego-image gcr.io/<your-gcp-project-id>/eyego-image

# Push the image
docker push gcr.io/<your-gcp-project-id>/eyego-image

### 4. Update k8s YAMLs

# Edit k8s/deployment.yaml and replace:
 
image: 911167899001.dkr.ecr.eu-north-1.amazonaws.com/eyego-repo
# with:
image: gcr.io/<your-gcp-project-id>/eyego-image

### 5. Apply K8s Configs

kubectl apply -f k8s/


