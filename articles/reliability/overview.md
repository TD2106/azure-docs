---
title: Azure reliability documentation
description: Overview of Azure reliability documentation, including platform capabilities, guides for how each Azure service supports reliability, and reliability concepts.
author: anaharris-ms
ms.topic: conceptual
ms.date: 06/23/2025
ms.author: anaharris
ms.service: azure
ms.subservice: azure-reliability
ms.custom: subject-reliability
CustomerIntent: As a cloud architect/engineer, I want to learn about Azure Reliability.
---

# What is Azure reliability documentation?

Azure provides a comprehensive set of reliability capabilities to help you meet your workload requirements.  The Azure reliability documentation provides service-specific guides on how each Azure service supports those platform reliability capabilities, such as transient fault handling, availability zones, multi-region support, and backup support. To see the current list of reliability service guides, see [Reliability guides by service](./reliability-guidance-overview.md).

In addition to the reliability service guides, Azure reliability documentation also includes general information, such as:

- **Azure regions**: Information on Azure regions, paired and nonpaired regions, and different region configurations.
- **Azure availability zones**: Information on availability zones, including how they support high availability and disaster recovery. This section also includes lists of Azure services and regions that support availability zones.
- **Reliability concepts**: Fundamental reliability concepts, such as:
    - Business continuity, high availability, and disaster recovery.
    - Redundancy, replication (Data redundancy), and backup
    - Failover and failback.
    - Shared responsibility between Microsoft and you.

## What is reliability?

Reliability refers to the ability of a workload to perform consistently at the expected level, and in accordance with business continuity requirements. Reliability is a key concept in cloud computing. In Azure, reliability is achieved through a combination of factors, including the design of the platform itself, its services, the architecture of your applications, and the implementation of best practices.

A key approach to achieve reliability in a workload is *resiliency*, which is a workload's ability to withstand and recover from faults and outages. Azure offers a number of resiliency features such as availability zones, multi-region support, data replication, and backup and restore capabilities. These features must be considered when designing a workload to meet its business continuity requirements. 

> [!TIP]
> Reliability also incorporates other elements of your solution design too, including how you deploy changes safely, how you manage your performance to avoid downtime due to high load, and how you test and validate each part of your solution. To learn more, see the [Azure Well-Architected Framework](/azure/well-architected).


## Azure regions

Azure provides over 60 regions globally, that are located across many different geographies. Each region is a set of physical facilities that include datacenters and networking infrastructure. All regions may be divided into geographical areas called geographies. Each geography is a data residency boundary, and may contain one or more regions.

[Azure regions](./regions-overview.md) provide certain types of resiliency options. Many regions provide [availability zones](./availability-zones-overview.md), and some have a [paired region while other regions are nonpaired](./regions-overview.md). When you choose a region for your services, it's important to pay attention to the resiliency options that are available in that region. 

- To view the list of Azure regions, see [List of Azure regions](./regions-list.md).
- To see the list of services that are deployed to Azure regions, see [Product Availability by Region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/table) 

## Azure availability zones

Many Azure regions provide availability zones, which are separated groups of datacenters within a region. Availability zones are an important way to achieve reliability on the Azure platform because they provide some level of physical isolation within a region.

Availability zones are close enough to have low-latency connections to other availability zones, but are far enough apart to reduce the likelihood that more than one will be affected by local outages or weather. Availability zones have independent power, cooling, and networking infrastructure. They're designed so that if one zone experiences an outage, then regional services, capacity, and high availability are supported by the remaining zones. 

- For more information on availability zones, see [What are availability zones?](./availability-zones-overview.md).
- To view which regions support availability zones, see [List of Azure regions](./regions-list.md).


## Reliability concepts

The reliability concepts section provides an overview of some of the key concepts and principles that underpin reliability in Azure. 

### Business continuity, high availability, and disaster recovery

Business continuity planning can be understood as the ongoing process of risk management through high availability and disaster recovery design. 

When considering business continuity, it's important to understand the following terms:

- *Business continuity* is the state in which a business can continue operations during failures, outages, or disasters. Business continuity requires proactive planning, preparation, and the implementation of resilient systems and processes.

- *High availability* is about designing a solution to meet the business needs for availability, and being resilient to day-to-day issues that might affect the uptime requirements.

- *Disaster recovery* is about planning how to deal with uncommon risks and the catastrophic outages that can result.

For information on business continuity and business continuity planning through high availability and disaster recovery design, see [What are business continuity, high availability, and disaster recovery?](./concept-business-continuity-high-availability-disaster-recovery.md).
### Redundancy, replication, and backup

We often think about the cloud as a globally distributed, ubiquitous system. However, in reality the cloud is made up of hardware running in datacenters. Resiliency requires that you account for some of the risks associated with the physical locations in which your cloud-hosted components run.

*Redundancy* is the ability to maintain multiple identical copies of a service component, and to use those copies in a way that prevents any one component from becoming a single point of failure.

*Replication* or data redundancy is the ability to maintain multiple copies of data, called replicas.

*Backup* is the ability to maintain a timestamped copy of data that can be used to restore data that has been lost.

For an introduction to redundancy, replication, and backup, see [What is redundancy, replication, and backup?](./concept-redundancy-replication-backup.md).

### Failover and failback

A common reason for maintaining redundant copies of both applications and data replicas is to be able to perform a failover. With failover, you can redirect traffic and requests from unhealthy instances to healthy ones. Then, once the original instances become healthy again, you can perform a failback to return to the original configuration.

For more information on failover and failback, see [What is failover and failback?](./concept-failover-failback.md).

### Shared responsibility

Resiliency defines a workload's ability to automatically self-correct and recover from various forms of failures or outages. Azure services are built to be resilient to many common failures, and each product provides a service level agreement (SLA) that describes the uptime you can expect. However, the overall resiliency of your workload depends on how you have designed your solution to meet your business needs. Some business continuity plans may consider certain failure risks to be unimportant, while others may consider them critical.

In the Azure public cloud platform, resiliency is a shared responsibility between Microsoft and you. Because there are different levels of resiliency in each workload that you design and deploy, it's important that you understand who has primary responsibility for each one of those levels from a resiliency perspective. To better understand how shared responsibility works, especially when confronting an outage or disaster, see [Shared responsibility for resiliency](concept-shared-responsibility.md).


## Related content


- [Availability of service by category](availability-service-by-category.md)
- [Build solutions for high availability using availability zones](/azure/architecture/high-availability/building-solutions-for-high-availability)
- [Training: Describe high availability and disaster recovery strategies](/training/modules/describe-high-availability-disaster-recovery-strategies/) 
