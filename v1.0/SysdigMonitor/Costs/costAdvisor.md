---
linkTitle: "Cost Advisor"
title: "Cost Advisor"
weight: "13"
aliases:
  - /en/cost-advisor
description: "Cost Advisor enables teams to get an overview of costs, drill into clusters, namespaces, workloads, and obtain insights and recommendations into where you can optimize and reduce your costs."
---

![](/image/cost_advisor_architecture.gif)

## Concepts

When using Cost Advisor, you can see a breakdown of multiple sources of cost. 

![](/image/cost_advisor_breakdown.png)

### CPU & Memory Cost Allocation

Cost Allocation is applicable to workloads and their associated namespaces, and displays the current allocated costs depending on resource requirements. Note that it is different from infrastructure costs, as workload cost allocation is calculated independently and can be considered a “logical cost”.

As workloads can exceed their configured requests (ie. it’s overcommitted using more than the number of requests, but less than resource limits) cost allocation is currently calculated daily by evaluating requests and usage, and taking whichever is greater for the given time period.

Given below is an example of cost allocation for a workload. It has requests set to 5 CPU cores and 16GB memory running on an t3.medium with a CPU cost of $0.02/hour and memory cost of $0.003/hour (on-demand pricing).

| Day&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |Calculation | Cost&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
| --| ------| ---|
| Day 1 | <strong>Requested CPU: 5 CPUs ($0.10/hr)</strong> <br />Actual CPU Usage: 2 CPUs ($0.04/hr) <br /><strong>Requested Memory: 16GB ($0.048/hr)</strong><br />Actual Memory Usage: 6GB ($0.018/hr)<br /><br />Requests are greater than the usage; therefore, actual usage is ignored. Sysdig considers requests for calculating the cost.<br /> | CPU cost: $2.40 <br />Memory cost: $1.15<br /><strong>Daily Cost: $3.55</strong>|
| Day 2 | Requested CPU: 5 CPUs ($0.10/hr) <br /><strong>Actual CPU Usage: 12 CPUs ($0.24/hr)</strong> <br /><strong>Requested Memory: 16GB ($0.048/hr)</strong><br />Actual Memory Usage: 6GB ($0.018/hr)<br /><br />Memory requests are greater than the usage; however the actual CPU usage is higher than the requests. <br />In this case, Sysdig considers actual CPU usage and memory requests.<br /> | CPU cost: $5.76 <br />Memory cost: $1.15<br /><strong>Daily Cost: $6.91</strong>|
| Day 3 | Requested CPU: 5 CPUs ($0.10/hr) <br /> <strong>Actual CPU Usage: 12 CPUs ($0.024/hr)</strong> <br />Requested Memory: 16GB ($0.048/hr)<br /><strong>Actual Memory Usage: 25GB ($0.075/hr)</strong><br /><br />Both the actual memory and CPU usage are higher than the requests (overcommitted). <br />Here, Sysdig considers the actual CPU and memory usage.  <br /> | CPU cost: $5.76 <br />Memory cost: $1.80<br /><strong>Daily Cost: $7.56</strong>|

### Storage Costs

Storage costs consider the cost of persistent volumes (PV) and associated claims in use by workloads. Within the <strong>Storage</strong> tab you will find all PVs for a given cluster and see which workload is claiming it, as well as the capacity, usage, cost per GB, and total monthly cost. Storage cost data is fed by integrations with cloud providers, for example when using EBS volumes in AWS, Sysdig will refer to EBS pricing.

{{% infobox type="tip" %}}
Storage costs consider persistent volumes; Sysdig Monitor does not currently display costs of host disks not associated with a PV.
{{% /infobox %}}

Practical tips for optimizing storage costs:

* The <strong>Storage</strong> tab will display actual usage against a claim. This helps you understand if a volume can be resized.
* Unused volumes will be listed in the <strong>Storage</strong> tab.  Sysdig reviews your storage infrastructure to identify any PVs that remain unattached or unmounted to pods. Consider repurposing any unused volumes for new or existing applications if suitable. Before proceeding with volume deletion, it is crucial to back up any data stored on these volumes, ensuring it is no longer required for ongoing operations.

### Network Costs

Network costs display the associated costs by Kubernetes services configured to use a load balancer. Integration with cloud providers will feed the cost data of load balancers in use.

{{% infobox type="tip" %}}
Network costs display cost of load balancers. Sysdig Monitor does not currently display costs associated with network throughput/traffic.
{{% /infobox %}}

### Idle Costs

Idle costs are applicable when viewing a cluster and quantify how much compute capacity (CPU and memory) is not being used/requested by workloads. This allows platform teams to gauge whether a cluster is a candidate for rightsizing, for example removing excess compute capacity or reshaping the instance types used.

### Cluster Management Costs

If you are running a managed Kubernetes service, such as EKS, GKE, AKS, Sysdig Monitor will display the associated management costs that cloud providers charge. 

### Efficiency Metrics

##### CPU Allocation

The average usage of CPU against requests over the last 10 minutes. No requests configured will show zero. For example:

`CPU Requests = sum workload CPU usage over the last 10 minutes/sum workload CPU requests`

##### Memory Allocation

The average usage of memory against requests over the last 10 minutes. No requests configured will show zero. For example:

`Memory Requests = sum workload memory usage over the last 10 minutes/sum workload memory requests`

Note that for CPU requests, memory requests, and resource efficiency, the calculation is made the individual workload level. This means when looking at a namespace, these values are an aggregate of all workloads within the same space.

## Cost Savings

Costs help teams optimize costs by recommending changes to their infrastructure.

![](/image/cost_recommend.png)

### Workload Rightsizing

For workloads running on your clusters, Cost Advisor evaluates the usage against requests. For oversized workloads (usage is less than requests) you can use Cost Advisor to:

- Quantify cost savings if you were to rightsize requests.
- View a recommendation on what values to rightsize workloads to.

#### Container rightsizing methodology

{{% infobox type="tip" %}}
Note that rightsizing recommendations in the Overview tab are always based on default usage (P95 over 1 Day), which provides a standard baseline for evaluation.
{{% /infobox %}}

Cost Advisor helps to baseline workload costs by recommending CPU and memory requests. By default, the recommendation is calculated by looking at the P95 usage of all unique containers running within a workload over the past 1 day. The recommendation is provided per container (in the case of pods running multiple containers). 

![](/image/cost_rightsize.png)

The **Improve Efficiency** drawer will present options to customize the algorithm and time window for generating the rightsizing recommendations:

* **Avg**: Refers to the average value of CPU or memory usage over a given time period.
* **P95**:  Refers to the 95th percentile of CPU or memory usage over a given time period. It will recommend a value that ignores the highest 5% of usage, excluding peaks and spikes.
* **Max**: Represents the highest level of usage that the CPU or memory reached during that period.

Consider a conservative approach (**Max** / **P95**) for the production of HA environments, and a more aggressive approach (**Avg**) for staging or test environments. The conservative approach may result in higher expenses compared to the aggressive approach. Prioritizing stability and risk mitigation, the conservative approach ensures reliable performance but may incur increased costs. 



