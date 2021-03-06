How to contribute.

1. Add a new directory for each new terraform module in order to increase extensibility

### Pre-requiste

In order to avoid explicitly using the GCP service key, we are going to use GOOGLE_APPLICATION_CREDENTIAL environment variable that points to our GCP service key.

1. Install Terraform ~> 0.12.26

2. If you have a service key at your disposal <br/>

   > export GOOGLE_APPLICATION_CREDENTIAL = {path to your service key file}

3. If you have not created a service account and a service key then follow below steps

   - Install gcloud cli
   - Run the following scripts

   ````bash
   export PROJECT_ID={Name of your GCP Project}

   export GOOGLE_APPLICATION_CREDENTIALS=~/.config/gcloud/${PROJECT_ID}-terraform-admin.json

   gcloud iam service-accounts create terraform --display-name "Terraform admin account"

   gcloud projects add-iam-policy-binding ${PROJECT_ID} --member serviceAccount:terraform@${PROJECT_ID}.iam.gserviceaccount.com   --role roles/owner

   gcloud services enable compute.googleapis.com

   gcloud services enable iam.googleapis.com

   gcloud iam service-accounts keys create ${GOOGLE_APPLICATION_CREDENTIALS} --iam-account terraform@${PROJECT_ID}.iam.gserviceaccount.com```
   ````

**Note** - you would need to export the GOOGLE_APPLICATION_CREDENTIALS every time you work with terraform when interacting with your configurations.