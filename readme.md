# (For renaming Docker Images)
docker tag registry.fxxd.com/serverless/sample-python-helloworld us-central1-docker.pkg.dev/prj-xxxxxxxxx/fxxd-container-images/sample-py-helloworld

# (Alternatively For renaming Docker Images with new tag)
docker tag registry.fxxd.com/serverless/sample-python-helloworld us-central1-docker.pkg.dev/prj-xxxxxxxxx/fxxd-container-images/sample-py-helloworld:1.0.0

# Pushing Image to Google Artifactory
gcloud auth login

# change GCP project
gcloud config set project

# IMPORTANT STEP (change location to your registry region here US_CENTRAL1)
gcloud auth configure-docker us-central1-docker.pkg.dev

# (optional Build Docker Image )
docker build -t cloudrun-pubsub-bigquery:latest .

gcloud auth print-access-token | docker login -u oauth2accesstoken -password-stdin us-central1-docker.pkg.dev 
# Docker Push to Google Artifact Registry
docker push us-central1-docker.pkg.dev/prj-xxxxxxxxxxx/fxxd-container-images/sample-py-helloworld 

# Alternative
(

 docker login -u oauth2accesstoken -p "$(gcloud auth print-access-token)" https://gcr.io
 docker tag cloudrun-pubsub-bigquery gcr.io/prj-dxxxxxxxxx/cloudrun-pubsub-bigquery
 docker push gcr.io/prj-xxxxxxxx/cloudrun-pubsub-bigquery
)
