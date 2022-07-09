---
layout: default
title: Deploy PaaS SQL Database Solution
parent: SQL Deployment Solutions on Azure - Deep Dive
grand_parent: Plan and Implement Data Platform Resources
nav_order: 3
---

# PaaS Offerings

  There are two primary Platform as a Service (PaaS) offerings in Azure -

  * Azure SQL Database 
  * Azure SQL Managed Instance

    ![img](https://docs.microsoft.com/en-us/learn/wwl-data-ai/deploy-paas-solutions-with-azure-sql/media/module-22-plan-implement-final-25.png)

    Image Reference: https://docs.microsoft.com/en-us/learn/wwl-data-ai/deploy-paas-solutions-with-azure-sql/media/module-22-plan-implement-final-25.png

# Azure SQL Database (Deep-Dive)

  ## Deployment Models

   * Single Database - Dedicated resources even if deployed to the same logical server.
   * Elastic Pools - Shared resources for a group of databases. v-Core and DTU purchasing models are both supported.

  ## Purchasing Models

   * DTU - Bundle combining storage, memory, compute, and I/O resources. Basic, Standard, and Premium Service Tiers are available. 
   * vCore - Purchase of vCores. General Purpose, Business Critical, and Hyperscale service tiers are available. General Purpose Service Tier provides two compute tiers - Provisioned and Serverless. In Provisioned Compute Tier, compute resources are pre-allocated (Billed per hour based on vCores configured). In Serverless Compute Tier, compute resources are auto-scaled (Billed per second based on vCores used). When database no longer requires compute resources, it enters a paused state amd only storage is billed during this time. The database resumes again when a connection attempt is made. The setting to control pausing is called as the "autopause delay". It has a minimum of 60 minutes and a maximum of 7 days. With serverless, you can specify a minimum and maximum number of vCores. Also, applications should be configured to include a retry logic. Serverless is not compatbile with Azure features that require background processes to run all the time. 
     * Hyperscale - Allows for databases to be 100TB or more. Compute nodes are added as data sizes grow. Once Azure SQL Database is converted to Hyperscale , it cannot be converted back to "regular" Azure SQL Database. 

  ## Backups

  * Availability of Automatic Backups. Manual backups are not supported. 
  * Stored in Azure blob geo-redundant storage. This storage would replicate backups to a secondary region of your preference.
  * Retained between 7 and 35 days based on the service tier of the database. (Basic and vCore databases default to 7 days of retention. On vCore databases, this value can be adjusted by the administrator.)
  * Long Term Retention (LTR) allows the backups to be retained for up to 10 years.
  * Database backup schedule:
    * Full - Once a week
    * Differential - Every 12 hours
    * Log - Every 5-10 minutes depending on transaction log activity  
  * Restore database T-SQL command is not supported. Available options are: Resotre using Azure Portal, or  Restore using scripting (Powershell and Azure CLI)
  * It is not possible to restore over an existing database.
  * __Copy-only backup to Azure blob storage is available for SQL Managed Instance. SQL Database does not support this feature__

  ## Business Continuity

  * Active geo-replication

    Geo replication is a business continuity featyre that asynchronously replicates a database up to four secondary replicas. The secondary databases can be used to offload read only workloads. A failover can be initiated manually by the user or by the application. Connection string needs to be updates to reflect the new endpoint.

  * Failover groups
   
    Failover groups provide a single endpoint for connection for geo-replicated databases. With this feature, applications do not need to update the connection strings on failover. 




