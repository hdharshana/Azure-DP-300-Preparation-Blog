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
