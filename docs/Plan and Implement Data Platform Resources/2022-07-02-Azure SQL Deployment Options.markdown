---
layout: default
title:  Azure SQL  Deployment Options
parent: Plan and Implement Data Platform Resources
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



