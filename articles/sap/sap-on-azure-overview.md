---
title: What SAP on Azure offerings are available?
description: Learn about the different offerings for running and managing your SAP systems on Azure. These include SAP virtual machine workloads, Azure Center for SAP solutions, the SAP on Azure deployment automation framework, and Azure Monitor for SAP solutions.
author: lauradolan
ms.author: ladolan
ms.service: sap-on-azure
ms.topic: overview 
ms.date: 01/27/2023
ms.custom: template-overview
---

# What SAP on Azure offerings are available?

There are multiple Microsoft Azure offerings for running and managing your SAP systems. These offerings range from traditional Azure virtual machine (VM) offerings, to top-level Azure services, to tools that integrate with other Azure services or external products.

## SAP on Azure VM workloads

You can run SAP workloads on the Azure platform using different Azure Virtual Machines (Azure VMs) offerings. Azure is [certified for multiple SAP products](workloads/certifications.md), including SAP HANA and SAP NetWeaver products. 

For more information, see the [SAP on Azure VM workloads](workloads/get-started.md) documentation.

### SAP HANA on Azure (Large Instances)

SAP HANA on Azure (Large Instances) is a solution that provides VMs for deploying and running SAP HANA. 

For more information, see the [SAP HANA on Azure (Large Instances)](large-instances/hana-overview-architecture.md) documentation.

> [!NOTE]
> This offering is no longer accepting new customers. For alternatives, please check the offers of HANA certified Azure VMs in the [HANA Hardware Directory](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/#/solutions?filters=iaas;ve:24).

## Azure Center for SAP solutions

Azure Center for SAP solutions is a service that makes SAP a top-level workload in Azure. This end-to-end solution allows you to create and run SAP systems as a unified workload on Azure. You can use this service through the Azure portal, a REST API, and the Azure CLI. 

For more information, see the [Azure Center for SAP solutions](center-sap-solutions/overview.md) documentation.

[!INCLUDE [Preview content notice](./center-sap-solutions/includes/preview.md)]

## SAP on Azure deployment automation framework

The SAP on Azure deployment automation framework is an open-source orchestration tool for deploying, installing and maintaining SAP environments.

For more information, see the [SAP on Azure deployment automation framework](automation/deployment-framework.md) documentation.

## Azure Monitor for SAP solutions

Azure Monitor for SAP solutions is an Azure-native monitoring product for SAP landscapes that run on Azure, which uses specific parts of the [Azure Monitor](../azure-monitor/overview.md) infrastructure.

For more information, see the [Azure Monitor for SAP solutions](monitor/about-azure-monitor-sap-solutions.md) documentation.

[!INCLUDE [Preview content notice](./monitor/includes/preview-azure-monitor.md)]

## Next steps

- [SAP solutions on Azure](https://azure.microsoft.com/solutions/sap/)
