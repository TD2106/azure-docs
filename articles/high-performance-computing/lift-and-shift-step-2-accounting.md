---
title: "Accounting configuration"
description: Learn how to configure accounting during a migration of high performance computing architecture.
author: tomvcassidy
ms.author: tomcassidy
ms.date: 04/10/2025
ms.topic: how-to
ms.service: azure-virtual-machines
ms.subservice: hpc
# Customer intent: "As an HPC administrator, I want to configure accounting systems during migration, so that I can ensure efficient resource utilization, optimize costs, and maintain compliance with organizational policies."
---

# Accounting configuration

A key aspect of your high performance computing migration is the configuration of accounting systems. Your accounting components ensure efficient resource utilization, cost management, and compliance. This part of the guide covers the needs, tools, services, and best practices associated with your accounting systems.

Slurm Accounting is a powerful tool that helps administrators monitor and report on job and resource usage, providing insights into workload performance and user activity.

## Define accounting needs

* **Resource usage tracking:**
   - To ensure efficient utilization, monitor compute node usage, job execution times, and resource allocation.
   - Track user and group activities to understand workload patterns and resource demands.

* **Cost management:**
   - Implement policies to manage and optimize costs by tracking resource consumption.
   - Use accounting data to allocate costs to different departments, projects, or users based on resource usage.

* **Compliance and reporting:**
   - Generate detailed reports on resource usage for compliance with organizational policies and external regulations.
   - Maintain historical records of job execution and resource consumption for auditing and analysis.

## Tools and services

**Slurm Accounting:**
  - Use Slurm Accounting to track and manage job and resource usage in HPC environments.
  - To collect and store accounting data, configure Slurm Accounting with the necessary settings.
  - Generate reports and analyze accounting data to optimize resource utilization and cost management.

## Best practices

* **Accurate data collection:**
   - Ensure that Slurm Accounting is properly configured to collect comprehensive data on job and resource usage.
   - To maintain reliable records, regularly verify the accuracy and completeness of the accounting data.

* **Effective cost management:**
   - Use accounting data to identify cost-saving opportunities, such as optimizing job scheduling and resource allocation.
   - Implement chargeback policies to allocate costs to departments or projects based on actual resource usage.

* **Compliance and auditing:**
   - Generate regular reports to comply with organizational policies and external regulations.
   - To ensure accountability and transparency, maintain historical records and perform periodic audits.

* **Data analysis and reporting:**
   - Use accounting data to analyze workload performance and identify trends in resource usage.
   - Generate custom reports to provide insights to stakeholders and support decision-making.

## Example Slurm accounting commands

**Query job accounting data:**

```bash
#!/bin/bash

# Query job accounting data for a specific user and time period
sacct -S 2023-01-01 -E 2023-01-31 -u john_doe -o JobID,JobName,Account,User,State,Elapsed,TotalCPU
```

## Resources

- Setting up Slurm Job Accounting with Azure CycleCloud and Azure Database for MySQL Flexible Server: [blog post](https://techcommunity.microsoft.com/t5/azure-high-performance-computing/setting-up-slurm-job-accounting-with-azure-cyclecloud-and-azure/ba-p/4083685)
- Slurm accounting: [external](https://slurm.schedmd.com/accounting.html)
