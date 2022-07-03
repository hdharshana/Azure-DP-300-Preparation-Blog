# Cheat Sheet for Azure DP-300 Exam Prep  (Module 2 - Deploy and configure servers, instances, and databases for Azure SQL)

__Resource__: https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/1-introduction

## 1. Introduction

* Make sure that the machine or virtual machine is running Windows. SSMS is available only on Windows.
* Download and install the latest version of SSMS.
* Download and install the latest version of Azure Data Studio.
* Download the zip file or clone the repository from GitHub to access lab files. Extract the contents of the zip file to something similar to C:\Users\[YourUsername]\ so you can access them easily in the exercises.

## 2. Plan, Deploy, and Verify Azure SQL

### Pre-Deployment Planning

Decisions to make prior to deployment - 

* Deployment method: Azure portal or command-line interface?
* Deployment option: virtual machine (VM), database, elastic pool, managed instance, or instance pool?
* Purchasing model (Azure SQL Database only): DTU or vCore?
* Service tier: General Purpose, Business Critical, or Hyperscale?
* Hardware: Gen5, or something new?
* Sizing: number of vCores and Data max size?

### Deployment

* __Reference__: https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/2-plan-deploy-verify

* For PaaS offerings, there are essentially 6 panes in the Azure portal to fill during deployment

  ![Deployment Panes](https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/media/2-deploy-panes.png)

* Server

** For Managed Instance, Server name is the same as in SQL Server
** For Azure SQL Database, Server nae is a logical server that acts as a central administrative point. The server name must be unique across all of Azure.

* Compute and Storage

** Selection of the desired configuration based on purchasing model (DTU vs vCore), Service Tier (General Purpose, Business Critical, or Hyperscale), and estimate of  
   vCores and Data max size (A tool like Data Migration Assistant SKU recommender can be used for this estimation)
   
* Networking Configuration

** For SQL Database

- Currently the default network configuration for SQL Database  is No Access
- You can choose a private endpoint of a public endpoint.
- Allow Azure services and resources option - When set to yes, the other Azure services (for example: Azure Data Factory) can access the database if you configure it.
- Add Clurrent Client IP Address : When added you can connect from the IP address of the client computer that was used to deploy the Azure SQL database.

** With Azure SQL Managed Instance

- You deploy inside an Azure virtual network and a subnet that is dedicated to managed instances, which lets you have a secure private IP address.
- Connections to on-prem network and resources are possible.
- You can also enable a public endpoint so you can connect to a managed instance from the internet without a virtual private network (VPN). This access is disabled by 
  default.

** Data Source

- In Azure SQL database, you can select the AdventureWorksLT database as the sample upon deployment in the Azure portal.
- In Azure SQL Managed Instance, the instance is deployed first so there is no option to have the sample databsae upon deployment. 
- A blank DB or imported DB can also be specified during deployment. 

** Database Collatioms
  
 - In SQL Server boc product, the default collation is typically determined by OS locale. 
 - In Azure SQL Managed Instance, you can set the server collation on creation of the instance and this cannot be changed later.  Databae and column collations can be 
   modified though.
 - In Azure SQL Database, you cannot set the server collation. Default collation is set to SQL_Latin1_General_CPI1_CI_AS

** Opt-In for Microsoft Defender for Cloud

- This gives functionality related to identifying/mitigating potential database vulnerabilities and thread detection.
- Starts as a free trial and charged after the trial period ends.

* Compute and Storage

## 3. Configure Azure SQL Database and Azure SQL Managed Instance

## 4. Load Data into Azure SQL



