# go-cloudrun-sql-gitlabci
How to deploy a Golang app to GCP Cloud Run with postgresql running in cloudsql and basic CI via a basic Gitlab CI

- ver 0.02 - 27th Nov 2019
- Still writing Ver 0.01 - 28 Oct 2019

## Background
As part of learning, testing and using different cloud platforms and offerings, I have experimented with a few of Google Cloud and AWS offerings. I've started with GCP as I have found it a lot easier to find what I need product and documentation wise.

Cloud Run launched not too long ago and very recently became GA, but I already see its great potential. From my perspective, tt sits somewhat between AppEngine flex and Kubernetes on the GC Compute paradigm - and can deploy to a Kubernetes cluster. For the bulk of the platforms we are building (at alba.one), we will be using managed cloud run.

## General useful links:
- https://medium.com/google-cloud/cloud-run-cloud-sql-6c8879ef96da

## Basic Steps
1. Initial Configuration
2. Cloud SQL Setup
3. Sample Go App Setup
4. Cloud Run Local Deployment
5. Gitlab CI setup


## 1. Initial Configuration (assumes Linux or OS-X terminal unless otherwise indicated)

1) Create a new project via GCP Console

Simply head over to the [cloud console](https://console.cloud.google.com/) , login with your credentials if required, create a new project. (Take advantage of 300$ credit if you haven't and the always [free tier](https://cloud.google.com/free/) )

2) If you haven't, download and install the latest [Google Cloud SDK](https://cloud.google.com/sdk/docs/) on to your computer.

3) Create a custom configuration

I generally like to create a custom configuration for this project to take care of some defaults so as to be able to switch between different projects without much trouble.

For the purpose of this document, I'm using ``a1-lab-run`` as the name of both the configuration and project but you can use whatever suits you as long as it conforms to the project naming conventions. 

```
gcloud config configurations create a1-lab-run
gcloud auth login 
gcloud config set project a1-lab-run
gcloud config set compute/region us-central1
gcloud config set compute/zone us-central1-a
gcloud config configurations list
```

## 2. Cloud SQL Setup
Useful Resources:
- [Cloud SQL quick starts](https://cloud.google.com/sql/docs/postgres/quickstarts)

## 3. Sample Go App Setup 
Useful Resources:
- [Using Cloud SQL with Go](https://cloud.google.com/go/getting-started/using-cloud-sql)

## 4. Cloud Run Deployment
Useful Resources:
- [Cloud Run quickstarts](https://cloud.google.com/run/docs/quickstarts?hl=en_GB&_ga=2.100862087.-704505203.1547643049)

## 5. Basic Gitlab CI
