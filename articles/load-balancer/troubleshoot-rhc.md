---
title: Troubleshoot Azure Load Balancer resource health, frontend, and backend availability issues 
description: Use the available metrics to diagnose your degraded or unavailable Azure Standard Load Balancer.
services: load-balancer
author: mbender-ms
ms.service: load-balancer
ms.topic: article
ms.workload: infrastructure-services
ms.date: 08/14/2020
ms.author: mbender
---

# Troubleshoot resource health, and inbound availability issues 

This article is a guide to investigate issues impacting the availability of your load balancer frontend IP and backend resources. 

The Resource Health Check (RHC) for the Load Balancer is used to determine the health of your load balancer. It analyzes the Data Path Availability metric over a **2-minute** interval to determine whether the load balancing endpoints, the frontend IP and frontend ports combinations with load balancing rules, are available.

The below table describes the RHC logic used to determine the health state of your load balancer.

| Resource health status | Description |
| --- | --- |
| Available | Your standard load balancer resource is healthy and available. |
| Degraded | Your standard load balancer has platform or user initiated events impacting performance. The Datapath Availability metric has reported less than 90% but greater than 25% health for at least two minutes. You'll experience moderate to severe performance impact. 
| Unavailable | Your standard load balancer resource isn't healthy. The Datapath Availability metric has reported less the 25% health for at least two minutes. You'll experience significant performance impact or lack of availability for inbound connectivity. There may be user or platform events causing unavailability. |
| Unknown | Resource health status for your standard load balancer resource hasn't been updated yet or hasn't received Data Path availability information for the last 10 minutes. This state should be transient and will reflect correct status as soon as data is received. |


## About the metrics we'll use
The two metrics to be used are *Data path availability* and *Health probe status* and it's important to understand their meaning to derive correct insights. 

## Data path availability
The data path availability metric is generated by a TCP ping every 25 seconds on all frontend ports that have load-balancing and inbound NAT rules configured. This TCP ping will then be routed to any of the healthy (probed up) backend instances. If the service receives a response to the ping, it's considered a success and the sum of the metric will be iterated once, if it fails it won't. The count of this metric is 1/100 of the total TCP pings per sample period. Thus, we want to consider the average, which will show the average of sum/count for the time period. The data path availability metric aggregated by average thus gives us a percentage success rate for TCP pings on your frontend IP:port for each of your load-balancing and inbound NAT rules.

## Health probe status
The health probe status metric is generated by a ping of the protocol defined in the health probe. This ping is sent to each instance in the backend pool and on the port defined in the health probe. For HTTP and HTTPS probes, a successful ping requires an HTTP 200 OK response whereas with TCP probes any response is considered successful. The consecutive successes or failures of each probe determine the health of the backend instance and whether the assigned backend pool is able to receive traffic. Similar to data path availability we use the average aggregation, which tells us the average successful/total pings during the sampling interval. This health probe status value indicates the backend health in isolation from your load balancer by probing your backend instances without sending traffic through the frontend.

>[!IMPORTANT]
>Health probe status is sampled on a one minute basis. This can lead to minor fluctuations in an otherwise steady value. For example, if there are two backend instances, one probed up and one probed down, the health probe service may capture 7 samples for the healthy instance and 6 for the unhealthy instance. This will lead to a previously steady value of 50 showing as 46.15 for a one minute interval. 

## Diagnose degraded and unavailable load balancers
As outlined in the [resource health article](load-balancer-standard-diagnostics.md#resource-health-status), a degraded load balancer is one that shows between 25% and 90% data path availability, and an unavailable load balancer is one with less than 25% data path availability, over a two-minute period. These same steps can be taken to investigate the failure you see in any health probe status or data path availability alerts you've configured. We'll explore the case where we've checked our resource health and found our load balancer to be unavailable with a data path availability of 0% - our service is down.

First, we go to the detailed metrics view of our load balancer insights page in the Azure portal. You can do this via your load balancer resource page or the link in your resource health message.  Next we navigate to the Frontend and Backend availability tab and review a thirty-minute window of the time period when the degraded or unavailable state occurred. If we see our data path availability has been 0%, we know there's an issue preventing traffic for all of our load-balancing and inbound NAT rules and can see how long this impact has lasted. 

The next place we need to look is our health probe status metric to determine whether our data path is unavailable is because we have no healthy backend instances to serve traffic. If we have at least one healthy backend instance for all of our load-balancing and inbound rules, we know it isn't our configuration causing our data paths to be unavailable. This scenario indicates an Azure platform issue.  While platform issues are rare, an automated alert is sent to our team to rapidly resolve all platform issues.

## Diagnose health probe failures
Let's say we check our health probe status and find out that all instances are showing as unhealthy. This finding explains why our data path is unavailable as traffic has nowhere to go. We should then go through the following checklist to rule out common configuration errors:
* Check the CPU utilization for your resources to determine if they are under high load.
  * You can check this by viewing the resource's Percentage CPU metric via the Metrics page. Learn how to [Troubleshoot high-CPU issues for Azure virtual machines](/troubleshoot/azure/virtual-machines/troubleshoot-high-cpu-issues-azure-windows-vm).
* If using an HTTP or HTTPS probe check if the application is healthy and responsive.
  * Validate application is functional by directly accessing the applications through the private IP address or instance-level public IP address associated with your backend instance.
* Review the Network Security Groups applied to our backend resources. Ensure that there are no rules of a higher priority than AllowAzureLoadBalancerInBound that will block the health probe.
  * You can do this by visiting the Networking blade of your backend VMs or Virtual Machine Scale Sets.
  * If you find this NSG issue is the case, move the existing Allow rule or create a new high priority rule to allow AzureLoadBalancer traffic.
* Check your OS. Ensure your VMs are listening on the probe port and review their OS firewall rules to ensure they aren't blocking the probe traffic originating from IP address `168.63.129.16`.
  * You can check listening ports by running `netstat -a` from a Windows command prompt or `netstat -l` from a Linux terminal.
* Don't place a firewall NVA VM in the backend pool of the load balancer, use [user-defined routes](../virtual-network/virtual-networks-udr-overview.md#user-defined) to route traffic to backend instances through the firewall,
* Ensure you're using the right protocol. For example, a probe using HTTP to probe a port listening for a non-HTTP application fails.

If you've gone through this checklist and are still finding health probe failures, there may be rare platform issues impacting the probe service for your instances. In this case, Azure has your back and an automated alert is sent to our team to rapidly resolve all platform issues.

## Next steps

* [Learn more about the Azure Load Balancer health probe](load-balancer-custom-probe-overview.md)
* [Learn more about Azure Load Balancer metrics](load-balancer-standard-diagnostics.md)
