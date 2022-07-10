---
layout: default
title: Migrate SQL Workloads to Azure SQL Databases
parent: SQL Migration Solutions on Azure - Deep Dive
nav_order: 2
---

# Azure SQL Database Migration planning tools

  * MAP - Used during discovery stage to confirm the source enviromnent you are migration from.
  * Azure Database Migrate Service - Enables large-scale database migration from Azure portal.
  * Data Migration Assistant - Used during the planning and assessment stage to check for compatibility issues that impact database functionality in Azure database.
  * Database Experimentation Assistant - Use DEA to assess if target server can handle your  workloads.

# Migration planning for Azure SQL Database

  * SQL Server Agent in not supported in Azure SQL Database. Complementary technologies such as Azure Automation or Elastic Database jobs need to be evaluated.
  * SQL Server authentication and AAD authentication are supported.
  * Read scale-out allows for read-only workloads to be serviced by secondary replica.
  * Retry application connections - Retry logic needs to be built in so applications can recover from transient issues. 

# Offline Data Migration to SQL Azure Database

  * Best Practices for offline data migraiton

    1. Use DMA to assess the source DB for compatibility issues.
    2. Use the compatibility report to prepare fized in T-SQL code
    3. Deploy the T-SQL fixes on a copy of the source DB.
    4. Mifrate the database copy to the new Aure SQL Database by using the Data Migration Assistant. 
    5. Choose the highest resources during migration, it can be downsized once migration activity is complete. 
    6. Minimize the distance between BACPAC file location adn the target data center. 
    7. Disable autostats during migration.
    8. Partition tables and indexes. 
    9. Drop indexed views and recreate them after migration.
    10. Remove rarely used historical data to another database to be migrated into a separate Azure SQL Database.
    11. After migration, update all stats in the new database.

  * Using BACPAC for migration
  
    * Use BACPAC from Azure blob storage or on-prem location to import into Azure SQL DB. 
    * SQLPackage can also be used instead of using the Azure portal. SQLPackage method is more performant. 

  * Azure Database Migration Service

    Azure Database Migration Service offers a centralized migration service in the Azure portal to enable seamless migrations from multiple database sources to Azure Data platforms, with minimal downtime. DMA can migrate MySQL< PostegreSQL, MariaDB to the respective Azure OSS DBs.
   
# Online Migration to Azure SQL Database

  Transactional replication can be used to keep the Azure database in sync until the actual curover takes place. 
  
  The publisher and distributor must be at least the following version and update:

  - SQL Server 2017 (14.x)
  - SQL Server 2016 (13.x)
  - SQL Server 2014 (12.x) SP1 CU3
  - SQL Server 2014 (12.x) RTM CU10
  - SQL Server 2012 (11.x) CU8 or SP3

# DR options for Azure SQL Database

  - Active geo-replication
  - Auto failover groups
  - Geo-restore
  - Zone-redundant databases
 
 # Service scalability options for Azure SQL Database
 
   - Vertical scale-up/scale-down
   - Horizontal scale-up/scale-down (Sharding with a sharding key is available both on Single database and elastic pool)
   


