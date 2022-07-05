---
layout: default
title: Azure SQL Purchasing Options
parent: Plan and Implement Data Platform Resources
nav_order: 2
#date: 2020-07-01 21:00:00 -0300
#categories: DP-300
---

# [Azure Purchasing Models and Service Tiers](#tab/azure-sql-purchasing-options) 

### Purchasing Models : 

* vCore based or DTU based
* vCore allows independent selection of compute and storage resources. It aalso allws Azure Hybrid benefit for SQL Server and/or reserved capacity which is not 
  available in DTU model.
* DTU is a bundled measure of compute, storage, and I/O resources.

### vCore-based Service Tiers

    | Service Tier | Capability |
    | ------------ | ---------- |
    | General Purpose | Budget oriented scalable compute and storage options. It provides both provisioned compute tier and serverless compute tier.|
    | Hyperscale | Suitable for applications that need 100TB+ stoarage and have dynamic compute and storage scale requirements. Only available in single database with Azure SQL. |
    | Business Critical | Suitable for applications that need low latency response. This is the only tier that offers In-Memory OLTP. |

### DTU-based Service Tiers

* DTU offers three service tiers: Basic, Standard, and Premium. Compute and Storage resources depend on the DTU level. Scaling can occur at the granularity of DTU 
  levels. Since DTU offers compute, storage, and IO as a bunvle, any scaling needs for one component will also cause scaling of the other components inherently due to 
  the nature of bundles. 

* Applications may experience a brief connection interruption during the scaling operation. As a best practice, applications should use retry logic to plan for any 
  scaling related interruptions. 

* Azure SQL Managed Instace does not support DTU-based purchasing model. 

### Compute Tiers

* Provisioned Compute - Regular usage patterns with higher average compute utilization over time. Provides a fixed amout of resources over time to ensure optimal performance.
* Serverless Compute - Suitable for intermittent unpredictable usage patterns. Provides automatic compute scaling and is billed only for the amount of compute used. Also has auto pause to pause the database during periods of inactivity for compute cost savings. 

### Hardware

* Default is Gen5 Hardware
