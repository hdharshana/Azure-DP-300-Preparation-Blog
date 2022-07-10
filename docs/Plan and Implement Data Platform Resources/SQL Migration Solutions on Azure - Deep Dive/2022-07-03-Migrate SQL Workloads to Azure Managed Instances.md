---
layout: default
title: Migrate SQL Workloads to Azure Managed Instances
parent: SQL Migration Solutions on Azure - Deep Dive
nav_order: 3
---

Azure SQL Database managed instance provides almost 100 percent compatibility with on-prem versions of SQL Server. It is designed to enable a "lift and shift" solution for customers. 

# Key features

  * Backward Compatibility support up to SQL 2008 databases
  * Easy lift and shift
    
    ![img](https://docs.microsoft.com/en-us/learn/wwl-data-ai/migrate-sql-workloads-azure-managed-instances/media/2-easy-migration.png)
    
    Image Reference: https://docs.microsoft.com/en-us/learn/wwl-data-ai/migrate-sql-workloads-azure-managed-instances/media/2-easy-migration.png
    
   * Fully managed PaaS
   * Security Features (TDE, Bring your own Encryption Key, Vulnerability assessment and Advance Threat Protection settings)
   * Secure network isolation - Managed instance has complete security isolation from any other tenant in the Azure cloud. It is solely exposed through a private IP address that only allows connectivity from privta Azure networks or hybrid networks. On-prem applications can connect to managed instance through Azure ExpressRoute configuration or VPN gateway. 
   * Instance failover groups - Set of databases managed within a single managed instance that can failover as a unit to another region.
 
 # Migration Tools
 
   * MAP
   * Azure Database Migrate Service
     - Database Migration Assistant
     - SQL Server Migration Assistant
     - Data Experimentation Assistant
   * Data Migration Assistant
   * Database Experimentation Assistant

# Migration Planning

  * Six types of subscription models
  
    - Enterprise Agreement
    - Pas-as-you-go
    - Cloud service Provider
    - Enterprise Dev/Test
    - Pas-as-you-go Dev/Test
    - Subscriptions with monthly Azure credit for Visual Studio subscribers
 
 # Networking
 
   Azure SQL Database managed instance must be deployed within an Azure virtual network, with the subnet dedicated to managed instances only. SQL Database managed instance is fully isolated. The compute and storage are placed in a virtual cluster that's fully isolated from all other tenants in Azure.

# Connectivity Options with on-prem servers

  * Point-to-Site (End user device to Azure virtual network)
  * Site-to-Site - On-prem site to Azure network
  * ExpressRoute- Private connection  between Azure DC and On-Prem DC

Azure SQL Database managed instance supports the following replication types:

- Transactional
- Snapshot
- One-way
- Bidirectional
