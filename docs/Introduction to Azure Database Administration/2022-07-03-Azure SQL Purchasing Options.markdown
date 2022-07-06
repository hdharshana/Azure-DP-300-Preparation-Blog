---
layout: default
title: Azure SQL Purchasing Options
parent: Introduction to Azure Database Administration
nav_order: 3
#date: 2020-07-01 21:00:00 -0300
#categories: DP-300
---

# Azure Purchasing Models and Service Tiers

## Purchasing Models : 

   * vCore-based or DTU based
   * vCore allows independent selection of compute and storage resources. It also allows Azure Hybrid benefit for SQL Server and reserved capacity, which is not 
     available in the DTU model.
   * DTU is a bundled measure of compute, storage, and I/O resources.

## vCore-based Service Tiers

   | Service Tier | Capability |
   | ------------ | ---------- |
   | General Purpose | Budget-oriented scalable compute and storage options. It provides both provisioned compute tier, and serverless compute tier.|
   | Hyperscale | Suitable for applications that need 100TB+ storage and have dynamic compute and storage scale requirements. Only available in single database offering with Azure SQL. |
   | Business Critical | Suitable for applications that need low latency response. It is the only tier that offers In-Memory OLTP. |

## DTU-based Service Tiers

  * DTU offers three service tiers: Basic, Standard, and Premium. Compute, and Storage resources depend on the DTU level. Therefore, scaling can occur at the 
    granularity of DTU levels. 

  * Applications may experience a brief connection interruption during the scaling operation. As a best practice, applications should use retry logic to plan for any 
    scaling-related interruptions. 

  * Azure SQL Managed Instance does not support the DTU-based purchasing model. 

## Compute Tiers

   * Provisioned Compute - Suitable for regular usage patterns with predictable compute utilization over time. Provides a fixed amount of resources over time to ensure optimal 
     performance.

   * Serverless Compute - Suitable for intermittent, unpredictable usage patterns. Provides automatic compute scaling and is billed only for the amount of compute 
     used. It also has auto-pause to pause the database during periods of inactivity for compute cost savings. 

## Hardware

   * Default is Gen5 Hardware
