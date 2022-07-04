---
layout: post
title:  Cheat Sheet for Azure DP-300 Exam Prep  (Module 2 - Deploy and configure servers, instances, and databases for Azure SQL)
date: 2020-07-01 21:00:00 -0300
categories: DP-300
---

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


### Exercises 

* Follow the steps on the labs/exercises included with MS Learn to create and verify an Azure SQL Database on Azure portal using MS Learn Concierge Subscription
* Use DatabaseName is not suppoted in Azure SQL (either conenct to the target DB during connection phase or use dropdown to select a database)
* Verify deployment using basic queries on SSMS as well as Azure Data Studio with the sample Jupyter notebook.

## 3. Configure Azure SQL Database and Azure SQL Managed Instance

### Configure SQL Managed Instance

* You can configure using sp_configure and certain global trace flags.
* TempDB , Model, and master have some options for configuration
* Network connectivity configuraiton options are also available.
* Alter database set options are available
* dbcompat value can be set for migration scenarios
* File maintenance options are available.
* SQL Server Agent is available for job management.

### Configure Azure SQL Database

* Alter database set options available (dbcompat can be set)
* No access to file configuration underneath
* No support for SQL Server Agent. Elastic jobs for SQL Database can be used. With this T-SQL scripts can be run agains many databases including parallel execution.
* Azure Automation Service can also be used to orchestrate processes through rubook. Runbook contains code like PowerShell or Python, and it can be directed at any 
  Azure resource.
* In Azure SQL Database specifically, "stale" page detection is enabled and the default server collation SQL_Latin1_General_CP1_CI_AS is always used. Additionally, the 
  following default options are set to ON:

  - SNAPSHOT_ISOLATION_STATE
  - READ_COMMITTED_SNAPSHOT
  - FULL RECOVERY
  - CHECKSUM
  - QUERY_STORE
  - TDE
  - ACCELERATED_DATABASE_RECOVERY

### Restrcited Configuration Choices in Azure SQL and SQL Managed Instance

- You can't stop or restart servers.
- You can't use:
  - Instant file initialization.
  - Locked pages in memory (we may configure Locked pages in some SLO deployments)
  - FILESTREAM and availability groups. (We use availability groups internally.)
  - Server collation. (In SQL Managed Instance, you can select this during deployment but not change it.)
  - Startup parameters.
  - Error reporting and customer feedback.
  - ALTER SERVER CONFIGURATION.
  - ERRORLOG configuration.
  - "Mixed Mode" security is forced, though Azure Active Directory only authentication is in preview
  - Logon audit is done through SQL audit.
  - Server proxy account is not applicable.

### Storage Management

* Possible maximum storage size is based on the chosen SLO. 1105 ad 1133 errors are observed once the max storage is reached.
* Size of new DBs is based on the size of the model database.  (For Azure SQL DB, it is based on the chosen SLO)
* The transaction log is in addition to the data size and is included with storage charges. It is truncated regulary due to automatic backups because Accerlarated 
  Database Recovery is enabled by default in Azure SQL Datavase. The max transaction log is always set at 30% of the Data max size.
* The Azure SQL database hyperscale itier is different from the other service tiers in that it creates a database that is initially 40 GB and grows automatically in size to the limit of 100 TB. The transaction log has a fixed size restriction of 1 TB. 

### Connectivity Architecture and Policy

* Default connection policy - Proxy for connections from outside and Redirect for connections within Azure
![ConnectionPolocy](https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/media/5-connectivity.png)
Reference: https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/5-configure-database

* Complete the lab for Configuration of SQL Azure Database here https://docs.microsoft.com/en-us/learn/modules/azure-sql-deploy-configure/6-exercise-configure-database 
  
  ** Client tools: Azure Data Studio, Azure Portal, SSMS, Azure CLI, PowerShell, Azure Cloud Shell through browser
  ** FOr this lab,  Azure CLI is used.
  ** az sql db holds commands related to the Azure SQL Database logical server. az sql mi and az sql midb are for managed instances. 
  

## 4. Load Data into Azure SQL

* Here are the data load options available for loading data into Azure SQL - 

  1. BCP
  2. Bulk Insert (Load data from Azure Data Storage in place of local machine due to inaccessbility to the local file system)
  3. SSIS Packages 
  4. Create a DB using an existing DB for a copy in Azure Data Factory
  5. Import of a BACPACK file
  6. In Azure SQL Managed Instance, T-SQL can be used to restore a database natively from a URL.

* Considerations for Data Load

  1. Data that needs to be loaded into Azure needs to be hosted in Azure.
  2. Minimal logging is not supported in Azure so DBs are always running in full recovery mode. So aproriate batching and sizing needs to be done during bulk load for 
     transaction log governance.
  3. Use Clustered columnnstore indexes for efficient data load into Azure SQL or Azure SQL Managed Instance.







