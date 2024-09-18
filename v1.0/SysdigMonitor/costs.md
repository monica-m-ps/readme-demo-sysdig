---
linkTitle: "Costs"
title: "Costs"
weight: "11"
aliases:
  - /en/costs
description: "Costs provide predictable cost analysis and savings estimates for Kubernetes environments."
category: 66eb3c2b0654ba00132aeac8
---

![](/image/cost_advisor_architecture.gif)

Costs help you get insights into the following use cases:

* Determining the cost of running compute, such as EC2 instances, within a Kubernetes cluster.
* Determining the cost of running Compute required for an application, workload, and namespace.
* Reducing the cost of running workloads by rightsizing.

## Key Features

Costs have multiple features to help you monitor and manage Kubernetes costs:

* **[Cost Advisor](/en/cost-advisor)**: Provides an overview of your costs, drill into clusters, namespaces, and workloads; presents insights and recommendations into where you can optimize and reduce your costs.
* **[Cost Explorer](/en/cost-explorer)**:  Presents a powerful exploration tool for costs; give you the ability to slice and dice by Kubernetes labels, browse historical costs, and spot anomalies. 
* **[Reports](/en/cost-reports)**:  Automate reporting of costs with Slack and email integrations, and generate periodic JSON/CSV exports for integration with thirdparty tooling.

## Supported Environments

* The [Sysdig Agent](/en/install-agent-monitor) is required for Costs. 
  
  The agent collects resource usage information that is augmented with billing data. There is no explicit configuration required for Costs if you are only interested in seeing costs based on public, on-demand pricing.
  
* (Optional) [Integrate with your cloud provider](/en/cost-integrations) to reconcile cost data with your specific costs, factoring in saving plans, reserved instances, and other discounts.
  
* Kubernetes clusters must be running in <strong>AWS</strong>, <strong>GCP</strong>, or <strong>Azure</strong>. Both managed clusters, such as EKS, and vanilla Kubernetes such as KOPS, are supported.



## Learn More

* [Costs](https://www.youtube.com/watch?v=ZD0jSUKEONk&t=11s)
* [Kubernetes Cost Optimization](https://sysdig.com/blog/kubernetes-cost-optimization/)
