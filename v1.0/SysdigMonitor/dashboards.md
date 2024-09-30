---
linkTitle: Dashboards
title: Dashboards
weight: "11"
aliases:
  - /en/costs
description: "Costs provide predictable cost analysis and savings estimates for Kubernetes environments."
category: 66eb3c2b0654ba00132aeac8
slug: dashboards-overview
parentDocSlug: sysdig-monitor-introduction
---
Try staging environment

Costs provide predictable cost analysis and savings estimates for Kubernetes environments.

![](https://docs.sysdig.com/image/cost_advisor_architecture.gif)

Costs help you get insights into the following use cases:

* Determining the cost of running compute, such as EC2 instances, within a Kubernetes cluster.
* Determining the cost of running Compute required for an application, workload, and namespace.
* Reducing the cost of running workloads by rightsizing.

{{% infobox type="note" %}}

Metric descriptor labels can only be used for segmenting, not grouping or scoping.

{{% /infobox %}}

[!NOTE]
Metric descriptor labels can only be used for segmenting, not grouping or scoping.

## Key Features

Costs have multiple features to help you monitor and manage Kubernetes costs:

* **[Cost Advisor](/en/cost-advisor)**: Provides an overview of your costs, drill into clusters, namespaces, and workloads; presents insights and recommendations into where you can optimize and reduce your costs.
* **[Cost Explorer](/en/cost-explorer)**:  Presents a powerful exploration tool for costs; give you the ability to slice and dice by Kubernetes labels, browse historical costs, and spot anomalies. 
* **[Reports](/en/cost-reports)**:  Automate reporting of costs with Slack and email integrations, and generate periodic JSON/CSV exports for integration with thirdparty tooling.

## Supported Environments

* The Sysdig Agent is required for Costs. 
  
  The agent collects resource usage information that is augmented with billing data. There is no explicit configuration required for Costs if you are only interested in seeing costs based on public, on-demand pricing.
  
* Kubernetes clusters must be running in <strong>AWS</strong>, <strong>GCP</strong>, or <strong>Azure</strong>. Both managed clusters, such as EKS, and vanilla Kubernetes such as KOPS, are supported.

## Test Table

The table below shows the current metrics and options for similar functionality.

| Current Metric                          | Alternative Starting August 1, 2018                                                                                                                                                                                                                                                                                                             |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| capacity.estimated.request.stolen.count | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| capacity.estimated.request.total.count  | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| capacity.stolen.percent                 | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| capacity.total.percent                  | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| capacity.used.percent                   | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| net.request.time.file                   | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| net.request.time.local                  | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| net.request.time.net                    | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| net.request.time.nextTiers              | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| net.request.time.processing             | Create your application metrics using [Prometheus](https://sysdig.atlassian.net/wiki/spaces/PD/pages/64946336/Prometheus+metrics), [StatsD](https://support.sysdig.com/hc/en-us/articles/204376099-Metrics-integrations-StatsD) or [JMX](https://support.sysdig.com/hc/en-us/articles/204178959-Metrics-integrations-JMX) for Java applications |
| net.sql.request.time.worst              | Max aggregation (net.sql.request.time)                                                                                                                                                                                                                                                                                                          |
| net.mongodb.request.time.worst          | Max aggregation (net.mongodb.request.time)                                                                                                                                                                                                                                                                                                      |
| net.http.request.time.worst             | Max aggregation (net.http.request.time)                                                                                                                                                                                                                                                                                                         |

## Learn More

* [Costs](https://www.youtube.com/watch?v=ZD0jSUKEONk&t=11s)
* [Kubernetes Cost Optimization](https://sysdig.com/blog/kubernetes-cost-optimization/)