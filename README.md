# golang + cloudrun + cloudsql 
How to deploy a Golang app to GCP Cloud Run with postgresql running in cloudsql and basic CI via a basic Gitlab CI

- Still writing ver 0.02 - 27 Nov 2019
- Still writing Ver 0.01 - 28 Oct 2019

## Background
As part of learning, testing and using different cloud platforms and offerings, I have experimented with a few of Google Cloud and AWS offerings. I've started with GCP as I have found it a lot easier to find what I need product and documentation wise.

Cloud Run [launched](https://cloud.google.com/blog/products/serverless/announcing-cloud-run-the-newest-member-of-our-serverless-compute-stack) not too long ago and very recently became [GA](https://cloud.google.com/blog/products/serverless/knative-based-cloud-run-services-are-ga), and I already see its great potential. From my perspective, it sits somewhat between AppEngine flex and Kubernetes on the GC Compute paradigm - and can deploy to a Kubernetes cluster as it is knative based. For the bulk of the platforms we are building (at alba.one), we suspect we will use managed cloud run.

## General useful links:
- https://medium.com/google-cloud/cloud-run-cloud-sql-6c8879ef96da

## Basic Steps
1. Initial Configuration
2. Cloud SQL Setup
3. Sample Go App Setup
4. Cloud Run Local Deployment



## 1. Initial Configuration 

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
```
The first step automatically activates this configuration i.e. a1-lab-run. If you have more than one configuration you can list these by running:

```
gcloud config configurations list
```

and then activating the one you need by:

```
gcloud config configurations activate <configuration name>
```

I find this pretty useful - especially when you are managing multiple environments, projects, users as well as in scripts.

## 2. Cloud SQL Setup
Useful Resources:
- [Cloud SQL quick starts](https://cloud.google.com/sql/docs/postgres/quickstarts)
- [Cloud SQL Proxy for Local Testing](https://cloud.google.com/sql/docs/postgres/quickstart-proxy-test)

Navigate to your project and create a new Cloud Sql instance for postgresql. (This will also enable the Cloud SQL API if not already enabled). I'm using the following parameters but you can choose whatever you prefer. Look at the quickstart for the detailed process. 

  * instance id: runsql
  * database version: PostgreSQL 11
  * default (postgres) user password: p0stgres
  * Machine Type: f1 micro (under Configuration Options) - this is not recommended for production environments 
  * compute region/zone: us-central1/us-central1-a (as configured for default above)

Click create. It should take a few minutes to create the instance. While waiting, take note of the instance connection name from the instance list. In my case this is: `a1-lab-run:us-central1:runsql`. You can also get the instance connection name by clicking on the instance id. 

Click on the instance id and then the users tab to create the database user. You will be prompted to enter the database user/password. I'm using:

* user/password: runsql/p4ssword!

Create the database as the newly created user by navigating to databases and clicking create database: I used:

* database name: runsql-db

There are several ways to connect to your new database. One way is to use [use the cloudsql proxy locally for testing](https://cloud.google.com/sql/docs/postgres/quickstart-proxy-test). After downloading it to your local environment, invoke it by running the following from the install location (or add it to your $PATH and leave out the ./ )


```
./cloud_sql_proxy -instances=<INSTANCE CONNECTION NAME>=tcp:5432 
```

in my case, this is:

```
./cloud_sql_proxy -instances=a1-lab-run:us-central1:runsql=tcp:5432 
```

You should have output similar to this:

```
[josiah:~/scripts]$ cloud_sql_proxy -instances=a1-lab-run:us-central1:runsql=tcp:5432
2019/12/07 11:34:55 Rlimits for file descriptors set to {&{8500 9223372036854775807}}
2019/12/07 11:34:58 Listening on 127.0.0.1:5432 for a1-lab-run:us-central1:runsql
2019/12/07 11:34:58 Ready for new connections
```


## 3. Sample Go App Setup 
Useful Resources:
- [Using Cloud SQL with Go](https://cloud.google.com/go/getting-started/using-cloud-sql)


## 4. Cloud Run Deployment
Useful Resources:
- [Cloud Run quickstarts](https://cloud.google.com/run/docs/quickstarts?hl=en_GB&_ga=2.100862087.-704505203.1547643049)



