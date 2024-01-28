# GCP-kubernetes
 ## Google Cloud compute options for Kubernetes -> Getting started with GKE

 ## Prerequisites: Ensure that the GKE and Cloud operations API are enabled in your GCP project.
   - Start by setting the project id
    ```
    PROJECT_ID=”<your-project-id>"
    ```

  - Enable the GKE API & Enable the Cloud operations API
    ```
     gcloud services enable apigateway.googleapis.com
     gcloud services enable servicemanagement.googleapis.com
     gcloud services enable servicecontrol.googleapis.com
    ```
  - Start by setting the project ID using the below command:
    ```
     gcloud config set project <<project id>
    ```
  - Set the compute zone for the cluster. For this demo, we will be using the zone us-central1-a
    ```
     gcloud config set compute/zone us-central1-a
    ```
  - Let’s now create a GKE standard cluster named ‘testcluster’, with default settings and single node in the node pool with auto scaling enabled
    ```
     gcloud container clusters create hello-cluster — enable-autoscaling — min-nodes=1 — max-nodes=3
    ```
  - Clone the Microservices demo application
    ```
     git clone https://github.com/574n13y/microservices-demo.git
     cd microservices-demo
    ```
  - Deploy the sample application to the GKE cluster
    ```
     kubectl apply -f ./release/kubernetes-manifests.yaml
    ```
  - Once the deployment is completed successfully, you should be able to see the namespace
    ```
     kubectl get ns
    ```
  - Once the deployment is completed successfully, you should be able to see the pods associated with the application using the following command
    ```
     kubectl get pods
    ```
  - Access the application using its external IP address at Port 80
    ```
     kubectl get service frontend-external | awk '{print $4}'
    ```
  - Alternatively, you can also browse to Kubernetes Engine service in GCP portal -> services and ingress and look for the endpoint of the service named “frontend-external”.
  - The application will open once you click on the link:
  - we deployed the cluster from cloud shell, however, the whole process, including the cluster creation and application deployment, can be automated using DevOps tools.