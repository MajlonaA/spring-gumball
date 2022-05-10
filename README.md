# Lab #10 - DevOps CI/CD

### CI Workflow (Part 1)
  ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/CI%20Workflow%20Part%201.png)
  
  
### CD Workflow (Part 2)

  - ###### GCP Service Account & JSON Service Account Key
  ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/GCP%20Service%20Account%201.png)
  
  ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/GCP%20Service%20Account%202.png)
  
  
  - ###### GitHub Action Secrets
    ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/GitHub%20Action%20Secrets.png)
    
   
  - ###### Trigger a CD Deployment by creating a new GitHub Release
    ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/Build%20Release.png)
    
    ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/build.png)
    
    ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/K8%20Cluster.png)
    
    ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/Service.png)
    
    ![](https://github.com/MajlonaA/spring-gumball/blob/main/images/Ingress.png)
    
    
    
 ### Notes
  - During this lab I ran into many issues with permission credentials. 
    First issue was incorrect setup for Google Cloud and that was due to the JSON file secret key.
    I tried recreating the Service Account in GCP and generated other keys.
    After reading the following: https://github.com/google-github-actions/get-gke-credentials#via-google-github-actionsauth
    I figured I had to use the name of the Service Account as the GKE_PROJECT and the entire JSON file for the GKE_SA_KEY.
    
    Second issue that I could not fix it after many many attempts was due to permissions.
    I kept getting the following error "Required 'container.clusters.get' permission (s) for 'projects/zones/us-central1-c/clusters/cmpe172' "
    This issue deals with permissions from GKE. To solve it I tried different things such as providing permissions when I created the Service
    which originally is set to optional. I also enabled APIs and authorized access from CLI since I read that could work. In addition, I tried changing
    the google.yml code to directly authorize using $gcloud container clusters get-credentials cmpe172 --zone us-central1-c --project cmpe172-349720.
    Other things I tried was redoing all the steps with default files only making changes to GKE_ZONE, GKE_CLUSTER, IMAGE, and DEPLOYMENT_NAME environment variables.
    Resources I used:
      - https://cloud.google.com/iam/docs/manage-access-service-accounts
      - https://stackoverflow.com/questions/53420870/keep-getting-permissions-error-gcloud-container-clusters-get-credentials
      - https://serverfault.com/questions/1044638/sudden-permissions-denied-for-service-account
      - https://discuss.circleci.com/t/gcloud-permissions-error/2631/16
      - https://cloud.google.com/kubernetes-engine/docs/reference/api-permissions etc.
    
