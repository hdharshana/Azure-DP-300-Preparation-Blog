---
layout: default
title:  Cheat Sheet for Azure DP-300 Exam Prep  (Module 1 - Introduction to Azure SQL)
parent: Module 1
nav_order: 2
#date: 2020-07-01 21:00:00 -0300
#categories: DP-300
---

# Cheat Sheet for Azure DP-300 Exam Prep (Module 1: Introduction to Azure SQL)

# __Purpose__

This document gives an overview of the different Azure SQL Server deployment options, purhasing options, and management interfaces for the three different Azure SQL offerings.

# [Azure SQL Server Deployment Options](#tab/azure-sql-deployment-options) 

| Deployment | Use Case | Offering | 
| ---------- | -------- | -------- |
| SQL Virtual Machines | For applications that need access to OS components | IaaS (Tenants to maange updates, patching, and backups)|
| Managed Instances | For applications that have instance level dependency such as CLR, Service broker, linked server,  etc. | PaaS (Managed patching, updates and backups)|
| Azure SQL Database | For applications that just need a connection string to connect to a SQL database | PaaS (Managed patching, updates and backups)|

# [Azure Purchasing Models and Service Tiers](#tab/azure-sql-purchasing-options) 

### Purchasing Models : 

* vCore based or DTU based
* vCore allows independent selection of compute and storage resources. It aalso allws Azure Hybrid benefot for SQL Server and/or reserved capacity which is not available in DTU model.
* DTU is a bundled measure of compute, storage, and I/O resources.

### Service Tiers

* General Purpose - Budget oriented scalable compute and storage options
* Hyperscale - Suitable for applications that need 100TB+ stoarage and have read scale requirements. Only available in single database with Azure SQL
* Business Critical - Suitable for applications that need low latency response. This is the only tier that offers In-Memory OLTP.

### Compute Tier

* Provisioned Compute - Regular usage patterns with higher average compute utilization over time. Provides a fixed amout of resources over time to ensure optimal performance.
* Serverless Copute - Intermittent unpredictable usage patterns. Provides automatic compute scaling and is billed only for the amount of compute used.

### Hardware

* Default is Gen5 Hardware

# [Azure SQL Management Interfaces](#tab/azure-sql-management-interface-options)  

* Azure Portal
* SSMS
* Azure Data Studio
* Languages and APIs (Azure SQL supports REST APIs for management of SQL managed isntances and SQL databases; All drivers that work with SQL Server also work with Azure SQL)
* CLI (sqlcmd and bcp support; Azure CLI and PS cmdlet support; tools like sqlcmd and az are pre-installed in Azure Cloud Shell)

