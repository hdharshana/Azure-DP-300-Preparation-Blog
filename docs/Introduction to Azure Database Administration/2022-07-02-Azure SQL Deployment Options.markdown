---
layout: default
title:  Azure SQL  Deployment Options
parent: Introduction to Azure Database Administration
nav_order: 1
#date: 2020-07-01 21:00:00 -0300
#categories: DP-300
---

# Azure SQL Deployment Options

# __Purpose__

This document gives an overview of the different Azure SQL Server deployment options. Azure offers two main offerings for SQL Server - Infrastructure as a Service (IaaS) and Platform as a Service (PaaS).

# __Azure Offerings__

SQL Server can be installed on any of the Azure offerings below depending on the business needs and existing database workload characteristics.

* Infrastructure as a Service (IaaS)
  
  SQL Server Azure VM allows installation of SQL Server in an Azure VM hosted on the cloud. This is very similar to installing and maintaining SQL on an on-prem VM     with the added benefits of cloud resiliency, extensions and infrastructure availability. Applications get more granular control on the underlying VM, OS, and SQL 
  Server instance when hosted on IaaS. This is a simpler migraton path if there are features that are incompatible with the PaaS model. However, this requires ongoing 
  maintenance to keep the infrastructure up to date.
  
* Platform as a Service (PaaS)

  - Azure Managed Instance
  
    Managed Instance offers a pre-installed SQL Server instance installation on the cloud. With this option, Azure manages the SQL instance including patching and 
    backups. VM or OS access is not available. This migration path allows applications to utilize most of the SQL native features while offloading underlying OS and VM 
    related maintenance. 
    
  - Azure SQL Database

    Azure SQL Database offers a SQL Server database hosted on the cloud. With this option, applications do not need to maintain an instance or VM. With a simple 
    connection string, applications can connect to the SQL database to execute any SQL workloads and get results. All the underlying maintenance is performed by the 
    Azure infrastructure. This includes ongoing updates to SQL Server, OS, and VM components.  Azure SQL Database by default has a public internet endpoint. Access to 
    this enpoint can be controlled via firewall rules, or limited to specific Azure VNets, or private links. Azure SQL database offers two main deployment models - 
    
    - Single Database (Individual database with resources allocated to the single database)
    - Elastic Pool (Pool of databases that share storage and compute resources allocated to the pool)

# [Azure SQL Server Deployment Options](#tab/azure-sql-deployment-options) 

| Deployment | Use Case | Offering | 
| ---------- | -------- | -------- |
| SQL Virtual Machines | For applications that need access to OS components | IaaS (Tenants to manage updates, patching, and backups)|
| Managed Instances | For applications that have instance level dependency such as CLR, Service broker, linked server,  etc. | PaaS (Managed patching, updates, and backups)|
| Azure SQL Database | For applications that just need a connection string to connect to a SQL database | PaaS (Managed patching, updates, and backups)|

# Feature comparison between different Azure deployment options

| Feature | Offering  | What is available?  |
| ------- | ------------------ | ---------------------- |
| Backup | Azure VM | Backup to URL (and) Azure Backup |
| Deployment | Azure VM | ARM Templates |
| Storage | Azure VM | Standard, Standard SSD, Premium SSD (5-10 ms delay), Ultra DIsk (Sub second latency) |
| High Availability | Azure VM |Availability Sets, Availability Zones, and load-banalcing techniques |
| Backup and Restore | Azure SQL DB | Continuous Backup, Geo-Restore, Point-in-time restore, Long-term retention |
| Automatic Tuning | Azure SQL DB | Identify Expensive Queries, Forcing Plan, Add and Remove Indexes |
| Elastic Query (preview) | Azure SQL Db | Vertical and horizontal partitioning (Not supported in MI) |
| Elastic Job (preview) | Azure SQL DB | T-SQL commnands in target deployments liek SQL DB, SQL elastic pool, and SQL database in shard map can be run in parallel |
| SQL Data Sync | Azure SQL DB | Incremental synchronization of data using hub and spoke approach (Not supported on MI) |
| Hybrid Licensing Options | Azure SQL DB and MI | On-prem license offers 40% savings in Azure |
| Backup and Restore | Azure SQL Managed Instance (MI) | Automated backups, geo-redundant, point-time-restore to same instance not possible, backups can be only restored to another MI; restore to SQL Azure VM or SQL Database not possible , copy only backup to BLOB possible (SQL database does not support this |
| High Availability | Azure SQL Database and MI | failover groups |
| Migration Options | MI | Backup restore or Dataabse Migration Service (DMS) |
| ML Services, CLR, Linked Server, and SQL Agent | MI | Supported (not supported in SQL Database) |







