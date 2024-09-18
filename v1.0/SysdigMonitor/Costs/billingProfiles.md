---
linkTitle: "Billing Profiles"
title: "Billing Profiles"
weight: "50"
aliases:
  - /en/billing-profiles # new alias added January 2024
  - /en/cost-integrations # legacy
description: "Integrate with your cloud provider to reconcile cost data with your specific costs, leverage Sysdig's Default Pricing, or define your own Pricing."
category: 66eb3c2b0654ba00132aeac8
parentDoc: 66eb3c72e9d67c0059a1cdeb
---

## Overview

No explicit configuration is required for Costs if you solely intend to view the expenses based on public, on-demand pricing, which is available for all major cloud providers.

### AWS

Configure the AWS integration to accurately reconcile costs in Sysdig with your AWS saving plans, reserved instances, spot usage, and enterprise discount programs. Without this configuration, cost data will default to publicly available on-demand pricing.

![](/image/cost_private_billing.png)

To setup the AWS cost integration, see [AWS Cost and Usage Reporting](/en/aws-cost-and-usage-reporting).

{{% infobox type="note" %}}
Cost reconciliation may take up to 24 hours the first time you configure your AWS account. Note that Sysdig does not currently reconcile historical cost data.
{{% /infobox %}}

### Default Pricing

Default Pricing is applied when Sysdig is unable to detect the cloud provider of a specific Kubernetes Cluster. This scenario commonly occurs with on-premises clusters, where the unit cost cannot be automatically determined.

Clusters with Sysdig Default Pricing use an indicative unit price that closely resembles the public on-demand prices of major cloud providers.

### Custom Pricing

Cost Advisor now supports Custom Pricing, enabling you to define custom cost configurations for your on-premises Kubernetes clusters. This feature enhances cost management accuracy, especially when the Default Pricing figures are not precise.

## Usage

### Viewing the Billing Profile of a Cluster

|  |  |
|--------|-----|
| In **Cost Advisor**, the **Details** tab displays information about the the Billing Profile currently in use by a cluster. | ![](/image/gke_billing_profile.png) |

### Leveraging Custom Pricing

|  |  |
|--------|-----|
| When **Default Pricing** is enabled, you can see the unit prices for costs in the **Details** tab and access guidance on overriding them through the API. See [API documentation](/en/docs/developer-tools/sysdig-api/#access-the-new-standardized-sysdig-api-documentation-using-the-regional-endpoints) for more information. | ![](/image/default-pricing.png) |

