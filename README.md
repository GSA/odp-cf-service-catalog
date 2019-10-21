# ODP Cloud Formations - AWS Service Catalog

## Overview <a name="s1"></a>

This project's purpose is to provide Cloud Formations templates and  CI Pipeline required configure the ODP team AWS Service Catalog and Products.

The general workflow is described below:

* 

## Table of Contents <a name="s2"></a>

* [Overview](#s1)
* [Table of Contents](#s2)
* [Project Contents](#s3)
* [Project Setup](#s4)
* [Developing This Project](#s5)

## Project Contents <a name="s3"></a>

| Folder / File      |  Description  |
|---          |---    |
| .circleci/config   |     |
| products/product_example_1.yml | Example product for the Service Catalog  |
| service_catalog/service_catalog.yml  | Configuration used to setup the initial Service Catalog |

## Project Setup <a name="s4"></a>

### Authenication and privileges

### Parameters

The following describes the parameters used to configure the resources.

| Variable      |  Type  |  Description  |
|---          |---        |---  | 
| variable  |  string |   description |



#### Setting environment variables

???


### Deploying Infrastructure


## Develop this project <a name="s5"></a>
  

### Docker 
It is not required to develop from a Docker container, but for the sake of setup speed we will use a Docker.

### Manual tests

To test you Cloud Formations code run these commands:

```
aws cloudformation validate-template --template-url https://s3.amazonaws.com/cloudformation-templates-us-east-1/S3_Bucket.template


```