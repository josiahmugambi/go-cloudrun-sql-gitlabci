# go-cloudrun-sql-gitlabci
How to deploy a Golang app to GCP Cloud Run with postgresql running in cloudsql and basic CI via a basic Gitlab CI
Ver 0.01 - 28 Oct 2019

## Background
As part of learning, testing and using different cloud platforms and offerings, I have experimented with a few of Google's and AWS's offerings. (I sort of lean towards GCP as I find it alot easier to find what I need product and documentation wise). 

Cloud Run launched not too long ago and is still in beta, but I already see its great potential. It sits somewhat between app engine flex and Kubernetes on the compute paradigm - and can deploy to a Kubernetes cluster. For the bulk of the platforms we are building (at alba.one), we will be using managed cloud run.

## Basic Steps
1. Initial Configuration
2. Cloud SQL Setup
3. Cloud Run Local Deployment
4. Gitlab CI setup


## 1. Initial Configuration (assumes Linux or OS-X terminal)
1) Create a new project via GCP Console
2) If you haven't, download and install the latest [Google Cloud SDK](https://cloud.google.com/sdk/docs/).
3) Enable the beta components:
```
gcloud components install beta
```
4) Update the components:
```
gcloud components update
```
5) Via the Cloud SDK, create a custom configuration for this project to take care of some defaults:
For the purpose of this document, I'm using ``a1-lab-run`` as the name of both the configuration and project. 

```
gcloud config configurations create a1-lab-run
gcloud auth login 
gcloud config set project a1-lab-run
gcloud config set compute/region us-central
gcloud config set compute/zone us-central1-a
gcloud config configurations list
```

## 2. Cloud SQL Setup
Useful Resources:
- [Cloud SQL quick starts](https://cloud.google.com/sql/docs/postgres/quickstarts)

## Cloud Run Local Deployment:
Useful Resources:
- [Cloud Run quickstarts](https://cloud.google.com/run/docs/quickstarts?hl=en_GB&_ga=2.100862087.-704505203.1547643049)

