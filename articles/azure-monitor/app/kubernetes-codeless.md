---
title: Monitor applications on Azure Kubernetes Service (AKS) with Application Insights - Azure Monitor | Microsoft Docs
description: Azure Monitor seamlessly integrates with your application running on Kubernetes, and allows you to spot the problems with your apps in no time.
ms.topic: conceptual
ms.date: 11/15/2022
ms.reviewer: abinetabate
---

# Zero instrumentation application monitoring for Kubernetes - Azure Monitor Application Insights

> [!IMPORTANT]
>  Currently you can enable monitoring for your Java apps running on Kubernetes without instrumenting your code - use the [Java standalone agent](./opentelemetry-enable.md?tabs=java). 
> While the solution to seamlessly enabling application monitoring is in the works for other languages, use the SDKs to monitor your apps running on AKS: [ASP.NET Core](./asp-net-core.md), [ASP.NET](./asp-net.md), [Node.js](./nodejs.md), [JavaScript](./javascript.md), and [Python](./opencensus-python.md).

## Application monitoring without instrumenting the code
Currently, only Java lets you enable application monitoring without instrumenting the code. To monitor applications in other languages use the SDKs. 

For a complete list of supported auto-instrumentation scenarios, see [Supported environments, languages, and resource providers](codeless-overview.md#supported-environments-languages-and-resource-providers).

## Java
Once enabled, the Java agent will automatically collect a multitude of requests, dependencies, logs, and metrics from the most widely used libraries and frameworks.

Follow [the detailed instructions](./opentelemetry-enable.md?tabs=java) to monitor your Java apps running in Kubernetes apps, as well as other environments. 

## Other languages

For the applications in other languages we currently recommend using the SDKs:
* [ASP.NET Core](./asp-net-core.md)
* [ASP.NET](./asp-net.md)
* [Node.js](./nodejs.md) 
* [JavaScript](./javascript.md)
* [Python](./opencensus-python.md)

## Troubleshooting

[!INCLUDE [azure-monitor-app-insights-test-connectivity](../../../includes/azure-monitor-app-insights-test-connectivity.md)]

## Next steps

* Learn more about [Azure Monitor](../overview.md) and [Application Insights](./app-insights-overview.md)
* Get an overview of [Distributed Tracing](./distributed-tracing.md) and see what [Application Map](./app-map.md?tabs=net) can do for your business
