# Jenkins CI/CD Pipeline for Java Application Deployment

This guide describes how to set up a Jenkins pipeline for Continuous Integration and Continuous Deployment (CI/CD) of a Java application, with steps to integrate with Argo CD for deployment to a Kubernetes cluster.

## 1. Install Necessary Jenkins Plugins

Install the following Jenkins plugins:
- **Git Plugin**: For integrating with Git repositories.
- **Maven Integration Plugin**: For building the Java application using Maven.
- **Pipeline Plugin**: For defining Jenkins pipeline stages.
- **Kubernetes Continuous Deploy Plugin**: For deploying to Kubernetes environments.

## 2. Create a New Jenkins Pipeline

1. In Jenkins, create a new **Pipeline Job**.
2. Configure the job with the **Git repository URL** for your Java application.
3. Add a **Jenkinsfile** to the Git repository to define the pipeline stages.

## 3. Define the Pipeline Stages

The pipeline will consist of the following stages:

- **Stage 1**: Checkout the source code from Git.
- **Stage 2**: Build the Java application using Maven.
- **Stage 3**: Run SonarQube analysis to check the code quality.
- **Stage 4**: Package the application into a JAR file.
- **Stage 5**: Make docker image
- **Stage 6**: Scan docker image with trivy
- **Stage 7**: push to docker hub
- **Stage 8**: update deployment file in Github using shell script
- **Stage 9**: Deploy the application using Argo CD.

## 4. Configure Jenkins Pipeline Stages

- **Stage 1**: Use the **Git Plugin** to check out the source code from the Git repository.
- **Stage 2**: Use the **Maven Integration Plugin** to build the Java application.
- **Stage 3**: Use the **SonarQube Plugin** to analyze the code quality of the Java application.
- **Stage 4**: Use the **Maven Integration Plugin** to package the application into a JAR file.
- **Stage 6**: Use **Argo CD** to promote the application to a production environment.

## 5. Set Up Argo CD

1. Install **Argo CD** on the Kubernetes cluster.
2. Set up a Git repository for Argo CD to track changes in Helm charts and Kubernetes manifests.
3. Create a **Helm chart** for the Java application, including the necessary Kubernetes manifests and Helm values.
4. Add the Helm chart to the Git repository that Argo CD is tracking.

## 6. Configure Jenkins Pipeline to Integrate with Argo CD

Install Argo CD with:
``kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml``

Port-forward Argo CD API server:
``kubectl port-forward svc/argocd-server -n argocd 8080:443``

Retrieve the initial admin password:
``kubectl -n argocd admin initial-password -o jsonpath="{.status.message}"``

Access the Argo CD UI at ``https://localhost:8080`` using the admin credentials.

Add your Git repository in the UI under Settings > Repositories and create an app.

## 7. Run the Jenkins Pipeline

1. Trigger the Jenkins pipeline to start the CI/CD process for the Java application.
2. Monitor the pipeline stages and address any issues that arise during execution.

---

This pipeline setup will automate the process of building, testing, deploying, and promoting your Java application to production, ensuring efficient CI/CD practices with integration to Argo CD for Kubernetes deployments.
