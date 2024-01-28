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
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/cb8a9b98-4839-4bed-83f7-d22d95d8ffc0)

  - Start by setting the project ID using the below command:
    ```
     gcloud config set project <<project id>
    ```
  - Set the compute zone for the cluster. For this demo, we will be using the zone us-central1-a
    ```
     gcloud config set compute/zone us-central1-a
    ```
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/b1cccc10-5e27-4717-9c42-d76f47bbfa4b)

  - Let’s now create a GKE standard cluster named ‘testcluster’, with default settings and single node in the node pool with auto scaling enabled
    ```
     gcloud container clusters create hello-cluster — enable-autoscaling — min-nodes=1 — max-nodes=3
    ```
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/94042d4d-5e63-426d-b92a-42cb5597a102)

  - Clone the Microservices demo application
    ```
     git clone https://github.com/574n13y/microservices-demo.git
     cd microservices-demo
    ```
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/9f705a78-88a8-4bed-a1c1-7c24cdb127ca)

  - Deploy the sample application to the GKE cluster
    ```
     kubectl apply -f ./release/kubernetes-manifests.yaml
    ```
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/a333e148-ecca-432a-b645-80610a5e1e13)

  - Once the deployment is completed successfully, you should be able to see the namespace
    ```
     kubectl get ns
    ```
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/4cad0116-0214-4817-8a3c-36f832813ad9)

  - Once the deployment is completed successfully, you should be able to see the pods associated with the application using the following command
    ```
     kubectl get pods
    ```
    ![image](https://github.com/574n13y/GCP-kubernetes/assets/35293085/4f756966-f520-420a-86eb-554c4cc19256)

  - Access the application using its external IP address at Port 80
    ```
     kubectl get service frontend-external | awk '{print $4}'
    ```