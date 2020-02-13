# ODP CloudFormation - AWS Service Catalog

## Overview <a name="s1"></a>

This project's purpose is to provide the CloudFormations template and CI/CD Pipeline to setup the ODP team's AWS Service Catalog configuration.


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
| service_catalog/service_catalog.yml  | Configuration used to setup the initial Service Catalog |

## Project Setup <a name="s4"></a>

### Setting up new products

* Upload the CloudFormation template for your new product to <strong><S3_BUCKET_NEEDS_TO_BE_DEFINED></strong> s3 bucket.
* Copy these lines replacing the values within `<>` to the setting for your product, and append the entire section to the end of the `ODPServiceCatalog.yml` file.

```
#New product starts here      
  <PRODUCT_RESOURCE_NAME>:
    Type: AWS::ServiceCatalog::CloudFormationProduct
    Properties: 
      Description: <PRODUCT DESCRIPTION>
      Distributor: OCISO DevSecOps
      Name: <PRODUCT_NAME>
      Owner: OCISO DevSecOps
      ProvisioningArtifactParameters: 
       -
          Description: Default version.
          DisableTemplateValidation: false
          Info: 
            LoadTemplateFromURL : "https://s3.amazonaws.com/<S3_BUCKET_NEEDS_TO_BE_DEFINED>/<CLOUD_FORMATION_TEMPLATE>"
          Name: v1.0
      SupportDescription: <PRODUCT DESCRIPTION>
      SupportEmail: 
        Ref: SupportEmail
      SupportUrl: 
        Ref: SupportURL
    DependsOn:
      - ODPPortfolio
  ODPPortfolio<PRODUCT_RESOURCE_NAME>:
    Type: AWS::ServiceCatalog::PortfolioProductAssociation
    Properties: 
      PortfolioId: !Ref ODPPortfolio
      ProductId: !Ref <PRODUCT_RESOURCE_NAME>
    DependsOn:
      - <PRODUCT_RESOURCE_NAME>


```
* To create a new product CI/CD pipeline use the following repository as an example:

https://github.com/GSA/odp-cf-ise-cross-acount-roles

### Parameters

The following describes the parameters used to configure the resources.

| Variable      |  Type  |  Description  |
|---          |---        |---  | 
| SupportEmail  |  string |   Email address to contact for support questions. |
| SupportURL  |  string |   URL on where find support for the Service Catalog and Products under it. |
| ProfileName  |  string |   Name of the Service Catalog profile to deploy|


### Deploying Infrastructure

* A successful push to any branch will result in the CloudFormation a validation of the template `ODPServiceCatalog.yml`. 
* CloudFormation template `ODPServiceCatalog.yml` will be deployed on a successful push to the `master` branch.

## Develop this project <a name="s5"></a>  

### Manual tests

To test your CloudFormation code run these commands:

```
#Test template in bucket
aws cloudformation validate-template --template-url https://s3.amazonaws.com/cloudformation-templates-us-east-1/S3_Bucket.template
#Test template local
aws cloudformation validate-template --template-body file:///home/templates/template.yml

```
