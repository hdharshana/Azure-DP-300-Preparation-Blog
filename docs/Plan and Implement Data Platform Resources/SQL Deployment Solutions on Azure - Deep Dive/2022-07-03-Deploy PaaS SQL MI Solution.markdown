---
layout: default
title: Deploy PaaS SQL MI Solution
parent: SQL Deployment Solutions on Azure - Deep Dive
grand_parent: Plan and Implement Data Platform Resources
nav_order: 4
---

Azure Manage Instance is a fully functional SQL Server isnatnce. It allows access to instance level features such as SQL Server Agent, TempDV, cross-database query, and CLR. In addition, PaaS offering benefits such as automated backups, automated patching, and built-in HA are also available.

# Link feature (preview)

  With link, your on-prem SQL Server databases can be replicated to Azure SQL Managed Instance using distributed availability groups. 

# Instance pool (preview)

  Instance pool is groupiing of SQL Server instnaces running within the same virtual cluster. Isolation between instances within the same pool is implemented by using Windows Job objects. All instances in the instance pol reside in te same virtual machine. This offering offers benefits in the area of faster provisioning (additional instances can be easily added in minutes) , and more efficiency with instance stacking. 
  
# Backups

Backup feature is same as in Azure SQL Database offering. Some key differences are -

* Copy only backups are supported in Azure SQL Database.
* You can issue a RESTORE command ; in Azure SQL DB , restore command is not supported.
* You must restore from URL (Local drive access is not available)
* Backup files containing multiple log files cannot be restored.
* Backup files containing multiple backup sets cannot be restored.
* Backups containing In-Memory/Filestream cannot be restored.
* By default , managed instances databases are encrypted with TDE. Any copy_only backup can occur only after TDE is turned off.

# Disaster Recovery

* Auto-failover groups (Limited to only one replica on a paired region with the primary)
* Each managed instance, primary and secondary, must be within the same DNS zone.

# Azure SQL Edge

Optimized relational database engine designed for IoT workloads. It is a containerized version of the SQL Server database engine optimized for IoT. 
  
