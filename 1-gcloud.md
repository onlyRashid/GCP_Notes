# Google Cloud Notes

## IaaS vs PaaS

    IaaS 
        * includes VMs, Compute resources
        * IaaS Model pay for resources ahead of time 
    PaaS 
        * includes App Engine 
        * Serverless technologies offered by Google include Cloud Run, which allows customers to deploy their containerized microservices based application in a fully-managed environment
        * Cloud Run functions, which manages event-driven code as a pay-as-you-go service.
    SaaS
        * SaaS applicationss run in the cloud as a service and are consumed directly over the internet by end users.
        * Popular Google applications such as Gmail, Docs, and Drive, that are a part of Google Workspace, are all examples of SaaS.

## Resource Hierarchy

    Resources (Level 01)
        * These represent virtual machines, Cloud Storage buckets, tables in BigQuery, or anything else in Google Cloud.

![Resource Hierarchy](Resource-hierarchy.png)
![Resource Hierarcy Diagram](cloud-hierarchy.svg)

## gcloud

    gcloud init 
    gcloud auth login 
    gcloud auth application-default login 
    gcloud auth list 
    gcloud config set project [PROJECT_ID] 
    gcloud config list 
    gloud projects list 
    gcloud config list
    gcloud projects create my_new_project 
    gcloud projects list 
    gcloud project delete my_new_project 
    gcloud billing accounts list

## gsutil

    clear the shell prompt 
    export PS1 ='$' 

## Some cloud shell bash commands

    pwd 
    clear 
    ls 
    free --giga
    lscpu 
    htop 

## gsutil  --> means google storage utility

### gsutil mb gs://rashid_storage

    This created storage space called rashid_storage 
