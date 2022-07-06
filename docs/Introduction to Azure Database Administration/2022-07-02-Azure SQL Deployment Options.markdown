---
layout: default
title:  Azure SQL  Deployment Options
parent: Introduction to Azure Database Administration
nav_order: 1
#date: 2020-07-01 21:00:00 -0300
#categories: DP-300
---

# __Azure SQL Deployment Options__

## __Purpose__

   This document gives an overview of the different Azure SQL Server deployment options. Azure offers two main offerings for SQL Server - Infrastructure as a Service 
   (IaaS) and Platform as a Service (PaaS).

## __Azure Offerings__

   SQL Server can be installed on any of the Azure offerings below depending on business needs and existing database workload characteristics.

   * Infrastructure as a Service (IaaS)
  
     SQL Server Azure VM allows installation of SQL Server in an Azure VM hosted on the cloud. It is very similar to installing and maintaining SQL on an on-prem VM with the added benefits of cloud resiliency, availability of Azure extensions, and underlying infrastructure management by Microsoft. Applications get more granular control on the underlying VM, OS, and SQL  Server instance when hosted on IaaS. It is an easier migration path for applications with features incompatible with the PaaS model. However, this requires ongoing maintenance to keep the infrastructure up to date.

  * Platform as a Service (PaaS)

    - Azure SQL Managed Instance
  
      Managed Instance offers a pre-installed SQL Server instance installation on the cloud. Azure manages the SQL instance with this option, including patching and backups. VM or OS access is not available. This migration path allows applications to utilize most of the SQL native features while offloading underlying OS and VM-related maintenance. 

    - Azure SQL Database

      Azure SQL Database offers a SQL Server database hosted on the cloud. With this option, applications do not need to maintain an instance or VM. With a simple    connection string, applications can connect to the SQL database to execute any SQL workloads and get results. The Azure infrastructure performs all the underlying maintenance, such as ongoing updates to SQL Server, OS, and VM components. Azure SQL Database, by default, has a public internet endpoint. Access to this endpoint can be controlled via firewall rules or limited to specific Azure VNets, or private links. Azure SQL database offers two primary deployment models 
      
    - Single Database (Individual database with resources allocated to the single database)
    
    - Elastic Pool (Pool of databases that share storage and compute resources allocated to the pool)

## __Azure SQL Server Deployment Options__

   | Deployment | Use Case | Offering | 
   | ---------- | -------- | -------- |
   | SQL Virtual Machines | For applications that need access to OS components | IaaS (Tenants to manage updates, patching, and backups)|
   | Managed Instances | For applications that have instance-level dependency such as CLR, Service Broker, linked server,  etc. | PaaS (Managed patching, updates, and 
   backups)|
   | Azure SQL Database | For applications that need a connection string to connect to a SQL database | PaaS (Managed patching, updates, and backups)|

## __Feature comparison between different Azure deployment options__

   | Feature | Offering  | What is available?  |
   | ------- | ------------------ | ---------------------- |
   | Backup | Azure VM | Backup to URL (and) Azure Backup |
   | Deployment | Azure VM | ARM Templates |
   | Storage | Azure VM | Standard, Standard SSD, Premium SSD (5-10 ms delay), Ultra DIsk (Sub-second latency) |
   | High Availability | Azure VM |Availability Sets, Availability Zones, and load-balancing techniques |
   | Backup and Restore | Azure SQL DB | Continuous Backup, Geo-Restore, Point-in-time restore Long-term retention |
   | Automatic Tuning | Azure SQL DB | Identify Expensive Queries, Force Good Plan, Add, and Remove Indexes |
   | Elastic Query (preview) | Azure SQL DB | Vertical and horizontal partitioning (Not supported in Azure SQL Managed Instance) |
   | Elastic Job (preview) | Azure SQL DB | T-SQL commands in target deployments like SQL DB, SQL elastic pool, and SQL database in shard map can run in parallel |
   | SQL Data Sync | Azure SQL DB | Incremental synchronization of data using the hub and spoke approach (Not supported with SQL Server Managed Instance offering) |
   | Hybrid Licensing Options | Azure SQL DB and Azure SQL Managed Instance | On-prem license offers 40% savings in Azure |
   | Backup and Restore | Azure SQL Managed Instance  | Automated backups, geo-redundant, and point-in-time-restore to the same instance are not available. Backup 
    restore support to another Managed Instance is available. Restoring to SQL Azure VM or SQL Database is not available. Copy only Backup to BLOB is available (SQL database does not support this |
   | High Availability | Azure SQL Database and Azure SQL Managed Instance | failover groups |
   | Migration Options | Azure SQL Managed Instance | Backup restore or Database Migration Service (DMS) |
   | ML Services, CLR, Linked Server, and SQL Agent | Azure SQL Managed Instance | Supported (not supported in SQL Database) |






