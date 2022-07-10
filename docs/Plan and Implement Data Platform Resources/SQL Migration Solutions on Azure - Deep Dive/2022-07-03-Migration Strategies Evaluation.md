---
layout: default
title: Migration Strategies Evaluation
parent: SQL Migration Solutions on Azure - Deep Dive
nav_order: 1
---

# Compatibility Level

SQL Server database compatibility level is a setting that guarantees that the T-SQL keywords and exeuction plan stay intact with the older version as long  as that older version is a supported release. The database engine version for Azure SQL Database and Azure SQL Managed Instance are not comparable with SQL Server internal build numbers, but they do refer to the same compatibility level.

# Support policy for SQL Server

Releases are supported for five years in primary support, and then five additional years in extended support. During the primary support period, all features are enhanced and fully supported. During the extended support period, only security bugs are fixed. Microsoft recommends that software vendors should certify applications for a compatibility level rather than a specific version. 

# Azure preview features

* Private Preview (Subscription needs to be added into an allowlist for a given feature by Microsoft)
* Public Preview (Customers can opt in from portal)

# Azure Migration Options

* Azure Migrate Tool

  Centralized location on the portal to assess and migrate on-prem servers, infrastructure, applications, and data to Azure. Azure Migrate helps with selecting the right size of VM and provides cost estimation. An appliance is installed on the On-Prem network to relay metadata about each server along with performance metrics to Azure Migrate, which resides in the cloud.
  
* MAP Toolkit and DEA

  - The Microsoft Assessment and Planning Toolkit collects the inventory of all SQL Servers in a given network, along with version and server information.
  - Database Experimentation Assistant (DEA) can be used to evaluate version upgrades of SQL Server by checking syntax compaibility and also assists with providing query performance information on the target version.

* Data Migration Assistant

  MAP and DEA provide incompatibilities and potential performance issues in the database. DMA takes it a bit further and  assesses and identifies new features that can benefit the application and also assists with the actual migration. 
  
* Azure Database Migration Service

  Two types of migration - 
  
  * Online (continuous data sync) migration
  * Offline (one-time) migration

  The Data Migration Service needs a virtual network in Azure created. For migration of any on-prem resources, VPN or ExpressRoute connection is needed from on-prem to Azure.
  
  

  
  
