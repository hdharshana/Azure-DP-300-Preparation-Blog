---
layout: default
title: Deploy IaaS Solution
parent: SQL Deployment Solutions on Azure - Deep Dive
grand_parent: Plan and Implement Data Platform Resources
nav_order: 2
---

# Overview

Azure VM for SQL Server offers the easiest migration path for on-prem SQL server installations into Azure. This allows for the maximum control over the underlying stack including networking layer, Guest OS, VM, Virtual network, Virtual storage, and any additional software you might need to install on the VM. In this deployment, Microsoft manages any underlying resources below the operating system layer. 

# SQL Server IaaS Agent Extension

  Extensions execute post deployment code such as anti-virus installations, or installing any Windows feature. The SQL Server IaaS Agent extension installs some 
  features that ease SQL Server adminstration overhead. Some featuures are - 

  - Automated backup
  - Automated Patching
  - Azure Key Vault Integration
  - Defender 
  - View Disk Utilization in the portal
  - Flexible Licensing
  - Flexible Version or Edition
  - SQL Best Practices Assessment
  - View information about your SQL Server configuration and storage utilization

# SQL Server Licensing Options

  1. If you are  not part of the Software Assurance (SA) program, you can create an Azure VM with a pre-configured SQL Server image and choose the pas-as-you-go 
     pricing model.

  2. If you are a part of the Software Assurance (SA) program, you can still use the pay-as-you-go model with the pre-configured SQL Server image, or you can choose to 
     port your existing on-prem license to Azure with the BYOL program. With BYOL, you can install using the VM image from your existing on-prem deployment. 

# Virtual Machine Families

  When deploying to Azure, there are several VM family options to choose from. The families are categorized by the CPU to memory balance ratio. Some are more CPU 
  bound, whereas others are more memory bound. You can choose the appropriate family based on your workload characteristics. The following six series/families are 
  available -

  | Family | CPU to Memory Ratio | Workload Characteristics |
  | ------ | ------------------- | ------------------------ |
  | General Purpose | Balanced CPU to memory ratio | Ideal for small workloads like test/dev, small web servers, small to med size databases |
  | Compute Optimized | High CPU to memory ratio | Web servers with medium traffic, network appliances, batch processes, application servers, and ML workloads that cannot use GPU |
  | Memory Optimized | High memory to CPU ratio | Well suited for most database workloads |
  | Storage Optimized | Fast local storage that is ephemeral | Useful for scale out data workloads such as Cassandra (Not useful with SQL Server unless disk redundancy is made available through AlwaysOn or Log Shipping) |
  | GPU | GPU | graphic processing operations and ML workloads etc. |
  | High Performance Compute | High Performance Compute | Applications that can scale horizontally to thousands of CPU cores. Remore DMA networking and high performance CPU provides low latency communications between VMs |

# Azure Marketplace

  Azure Marketplace is a centralized location that provides the ability to provision resources based on templates. Some basic parameters can be provided as inputs to 
  start a resource deployment. Azure Resource Manager initiates the deployment and makes it available within minutes. The deployment can be further automated for reuse 
  with ARM templates. 

  For a walkthrough of provisioning SQL Server Azure VM through Azure portal, please refer to this link https://docs.microsoft.com/en-us/azure/azure-sql/virtual-
  machines/windows/create-sql-vm-portal?view=azuresql

  For a walkthrough of provisioning SQL Server Azure VM through Powershell, please refer to this link https://docs.microsoft.com/en-us/azure/azure-sql/virtual-
  machines/windows/create-sql-vm-powershell?view=azuresql

# Security Considerations

  * Disk Encryption
  
    - Data at Rest offered with TDE
    - Azure Disk Encryption with Bitlocker

    Both the above integrate with Azure Key Vault and allow you to bring your own encryption key.

  * Microsoft Defender for SQL (Vulnerability Assessments and Security Alerts)

  * Azure Security Center

# Storage Considerations

  * Azure VM Disk Configuration

    - Four disk types - Standard HDD, Standard SSD, Premium SSD, and Ultra Disk SSD (Increasing levels of IoPS and performance from left to right)
    - Each VM comes with at least two disks - OS disk, and Temporary disk
    - Additionally you can add data disks. These disks can be pooled for higher IoPS and storage capacity using storage spaces. Best practice for data disks is to use 
      Premium disks in their own pool with read caching enabled.
    - Transaction log files should go into their own pool of premium disks without caching.
    - TempDB can go into its own pool or be hosted on the temporary drive attached to the VM.
    - Premium disks have a latncy in single digit milliseconds and Ultra disk SSD has a latency lower than that. 

# Performance Considerations

  - Table Partitioning

    The example below illustrates how to create a partition function for January 1, 2021 through December 1, 2021, and distribute the partitions across different 
    filegroups.

    ```sql
    -- Partition function
    CREATE PARTITION FUNCTION PartitionByMonth (datetime2)
        AS RANGE RIGHT
        -- The boundary values defined is the first day of each month, where the table will be partitioned into 13 partitions
        FOR VALUES ('20210101', '20210201', '20210301',
        '20210401', '20210501', '20210601', '20210701',
        '20210801', '20210901', '20211001', '20211101', 
        '20212101');

    -- The partition scheme below will use the partition function created above, and assign each partition to a specific filegroup.
    CREATE PARTITION SCHEME PartitionByMonthSch
        AS PARTITION PartitionByMonth
        TO (FILEGROUP1, FILEGROUP2, FILEGROUP3, FILEGROUP4,
            FILEGROUP5, FILEGROUP6, FILEGROUP7, FILEGROUP8,
            FILEGROUP9, FILEGROUP10, FILEGROUP11, FILEGROUP12);

    -- Creates a partitioned table called Order that applies PartitionByMonthSch partition scheme to partition the OrderDate column  
    CREATE TABLE Order ([Id] int PRIMARY KEY, OrderDate datetime2)  
        ON PartitionByMonthSch (OrderDate) ;  
    GO
    ```
    Above Code Source: https://docs.microsoft.com/en-us/learn/modules/deploy-iaas-solutions-with-azure-sql/4-explore-performance-and-security

   - Data Compression

     Allows data to be compressed into the 8 KB data pages. This results in fewer page fetches to read the same amount of data and also lesser buffer pool use.  It 
     needs a small amount of CPU cycles to perform compression. There are three types of compression available - 

     - Row Compression (Compression at the row level)
     
     - Page Compression (At the first level row compression is performed , then page compression is performed by replacing duplicate values with pointers to reduce 
       storage space)
       
     - Columnstore archical compression (Columnstore objects are always compressed but they can be further compressed with archival compression which uses the 
       Microsoft XPRESS compression algorithm on the data. Best suited for archival data that needs to be retained for regulatory reasons. )

  For performance best practices, refer to [Checklist: Best practices for SQL Server on Azure VMs
  (https://docs.microsoft.com/en-us/azure/azure-sql/virtual-machines/windows/performance-guidelines-best-practices-checklist?view=azuresql)

# High Availability  Options

 - Availability Zones (Independent units of power/cooling/networking within a region - Kind of like Data Centers in a region. Workload is spread across Data Centers in a region)
 - Availabiltiy Sets (Workload is spread across servers and racks in a data center. Guarantees that two VMs containing your AG members are not running on the same physical host)
 - AlwaysOn AG (upto 9 replicas - if some latency is acceptable , choose synchronous for HA replica; if latency is not acceptable , choose aasynchronous)
 - SQL Server Failover Cluster Instances - Shared storage HA solution (Not DR)

# Disaster Recover Options

  - Native SQL Server backups

    - Azure VMs offer a granular control of when backups occur and where they are stored. 
    - SQL Agent jobs can be used to backup directly to a URL linked to Azure blob storage. 
    - Azure provides the option to use GRS or RA-GRS to ensure your backups are stored across the geopgraphic landscape. 
    - You can also opt for auto managed backups by the paltform as part of Azure VM offering.

  - Azure Backup for SQL Server

    The Azure backup solution requires an agent to be isntalled on the Azure VM. THe agent then communicate with an Azure service that manages backups centrally. 

    ![image](https://docs.microsoft.com/en-us/learn/wwl-data-ai/deploy-iaas-solutions-with-azure-sql/media/module-22-plan-implement-final-04.png)
    
    Reference: https://docs.microsoft.com/en-us/learn/modules/deploy-iaas-solutions-with-azure-sql/5-explain-high-availability-and-disaster-recovery-options

  - Azure Site Recovery

    Low-cost solution that performs block level replication of the Azure VM. THis solution is best suited for stateless environments such as web servers and not ideal for transactional systems such as databases. 

    ![image](https://docs.microsoft.com/en-us/learn/wwl-data-ai/deploy-iaas-solutions-with-azure-sql/media/module-55-optimize-queries-final-17.png)











