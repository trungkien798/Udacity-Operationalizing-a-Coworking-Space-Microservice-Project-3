# Coworking Space Service Extension

### 1. Create EKS
Optional: Enabling IAM principal access to your cluster
https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html

### 2. Configure a Database
Set up a Postgres database using a Helm Chart. Using port forward to run SQL files to init dummy data

### 3. Create a new repository on ECR 
### 4. Create CodeBuild to build and push the image to ECR
Related to Dockerfile, buildspec.yml

For each build, the pipeline will push image with a tag by the hash of the commit and update the latest tag 

### 5. Create service and deployment
Related to:
- Deployment and services: `deployment\coworking-api.yaml`
- ConfigMap for un-security env: `deployment\db-configmapi.yaml`
- Secret for security env: `deployment\db-secret.yaml`

### 5. Configuring CloudWatch Insights

### 6. How to change deploy
- Commit and push code to the GitHub repository
- GitHub repository will process a webhook to CodeBuild
- CodeBuild will run a new pipeline to build a new image for ECR
- Based on this new image, you can update your resource through: 
    - The manifest file `deployment\coworking-api.yaml` 
    - Or delivery-specific tag by Performing a Rolling Update https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/
