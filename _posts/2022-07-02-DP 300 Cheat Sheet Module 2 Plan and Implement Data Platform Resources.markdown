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

  - For Managed Instance, Server name is the same as in SQL Server
  - For Azure SQL Database, Server nae is a logical server that acts as a central administrative point. The server name must be unique across all of Azure.

* Compute and Storage

  - Selection of the desired configuration based on purchasing model (DTU vs vCore), Service Tier (General Purpose, Business Critical, or Hyperscale), and estimate of     vCores and Data max size (A tool like Data Migration Assistant SKU recommender can be used for this estimation)
   
* Networking Configuration

  - For SQL Database

    - Currently the default network configuration for SQL Database  is No Access
    - You can choose a private endpoint of a public endpoint.
    - Allow Azure services and resources option - When set to yes, the other Azure services (for example: Azure Data Factory) can access the database if you configure       it.
    - Add Clurrent Client IP Address : When added you can connect from the IP address of the client computer that was used to deploy the Azure SQL database.

  - With Azure SQL Managed Instance

    - You deploy inside an Azure virtual network and a subnet that is dedicated to managed instances, which lets you have a secure private IP address.
    - Connections to on-prem network and resources are possible.
    - You can also enable a public endpoint so you can connect to a managed instance from the internet without a virtual private network (VPN). This access is disabled 
      by default.

* Data Source

  - In Azure SQL database, you can select the AdventureWorksLT database as the sample upon deployment in the Azure portal.
  - In Azure SQL Managed Instance, the instance is deployed first so there is no option to have the sample databsae upon deployment. 
  - A blank DB or imported DB can also be specified during deployment. 

* Database Collatioms
  
  - In SQL Server boc product, the default collation is typically determined by OS locale. 
  - In Azure SQL Managed Instance, you can set the server collation on creation of the instance and this cannot be changed later.  Databae and column collations can be 
    modified though.
  - In Azure SQL Database, you cannot set the server collation. Default collation is set to SQL_Latin1_General_CPI1_CI_AS

* Opt-In for Microsoft Defender for Cloud

  - This gives functionality related to identifying/mitigating potential database vulnerabilities and thread detection.
  - Starts as a free trial and charged after the trial period ends.

### Key Deployment Implementation Details

* Azure SQL Managed Instance - Deploys a dediicated ring (sometimes called a virtual cluster) for your service. With this deployment, scaling up or down deploys a new 
  virtual cluster and seeds data from the current deployment. To optimize the long deployment time, you can pre-deploy a pool of dedicated resources. This offers 
  faster deployment speeds and higher packing density.

* Azure SQL Database - This is contained by a logical database server. In most cases, a SQL database is hosted by a dedicated SQL Server instance. Within each logical   database server is a logical master database, which can provide instance level diagnostics. 

* Azure SQL Database (Hyperscale) - Includes a multilayer caching system for spped and scale. Once you move a database to the Hyperscal tier, you cannot go back to the 
  General Purpose or Business Critical tier. 

* Resource Governance 

  - Windows job objects allows a grouo of processes to be managed and governed as a unit. Files' virtual memory commit, working ste camps, CPU affinity, and rate caps 
    can be governed. DMV: sys.dm_os_job_object to see the limits in place.

  - Resource Governor 

  - File Server Resource Manager - used to govern file directory quotas, which are used to manage Data maz size

  - Transaction log rate governance is laso available to limit high ingestion rates for workload such as bulk insert, index builds etc.

* Deplyment Verification

  - You can run the following queries to better understand what you've deployed and to verify that it was deployed correctly:

    ```sql
    SELECT @@VERSION
    SELECT * FROM sys.databases
    SELECT * FROM sys.objects
    SELECT * FROM sys.dm_os_schedulers
    SELECT * FROM sys.dm_os_sys_info
    SELECT * FROM sys.dm_os_process_memory --Not supported in Azure SQL Database
    SELECT * FROM sys.dm_exec_requests
    SELECT SERVERPROPERTY('EngineEdition')
    SELECT * FROM sys.dm_user_db_resource_governance -- Available only in Azure SQL Database and SQL Managed Instance
    SELECT * FROM sys.dm_instance_resource_governance -- Available only in Azure SQL Managed Instance
    SELECT * FROM sys.dm_os_job_object -- Available only in Azure SQL Database and SQL Managed Instance
    ```
   Source: https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/2-plan-deploy-verify

## 3. Configure Azure SQL Database and Azure SQL Managed Instance

## 4. Load Data into Azure SQL



