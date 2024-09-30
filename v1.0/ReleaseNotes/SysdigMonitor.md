---
title: "SaaS: Sysdig Monitor Release Notes"
linkTitle: "Monitor SaaS"
weight: "12"
category: "66ea35e1abfea54708f4ee84" 
description: Welcome to the release notes for the SaaS version of Sysdig Monitor. Here, you can review the latest features and enhancements. Please note that the dates listed indicate the initial release of each feature. Features may not be rolled out to all regions simultaneously, as regional availability depends on scheduling.
enable_rss: true
---

## August 8, 2024

### Alert Terminology

* **Metric Alerts** are now called **Threshold Alerts**.
* **Threshold Alerts** now include a **Duration** setting, specifying how long an alert condition must be continuously satisfied before triggering the alert rule.
* **PromQL Alerts** are now called **Prometheus Alerts**.
* Standarized terminology:
  * **Range** refers to the time period over which a metric is aggregated. The Alert Editor still refers to this field with "over the last".
  * **Duration** refers to how long an alert condition must be continuously met to trigger an alert rule.
* Standarized API fields to `duration_seconds` and `range_seconds` for consistency.

## August 2, 2024

### Microsoft Deprecates Office 365 Connectors

Microsoft is deprecating Office 365 Connectors for Microsoft Teams notifications. According to the [official deprecation notice](https://devblogs.microsoft.com/microsoft365dev/retirement-of-office-365-connectors-within-microsoft-teams/), new connectors cannot be created after August 15, 2024, and existing ones will require a URL update to function after December 31, 2024. To avoid any interruption in notifications, see [migrate from Office 365 Connects to Power Automate](/en/office-365-migrate/).

## July 30, 2024

### Alert Inhibition

You can now set up Alert Inhibition rules for Prometheus alerts. This feature stops secondary alert notifications from being forwarded if an upstream alert occurrence is already active. This helps reduce alert noise by preventing notifications from known downstream effects. To learn more, see [Alert inhibition](/en/docs/sysdig-monitor/alerts/alert-inhibition/).

{{% infobox type="note" %}}
Alert Inhibition can only be configured via the API and is only available for Prometheus Alert Rules.
{{% /infobox %}}

### Improved Alert Preview Accuracy

The Alert preview for Metric Alerts and PromQL Alerts now more accurately reflects alert rule checks. The data points in the alert preview aligns with the actual alert evaluation intervals, ensuring a realistic representation of alert behavior, since each point in the alert preview corresponds to an actual alert rule check.

### Unified Search

The Event feed now integrates scope-based search and free-text search in the same search bar, allowing you to filter events by both criteria from one convenient location.

### Disable Metric Collection for a Prometheus Job

You can now exclude metrics from being collected by the Sysdig Agent via Metrics Usage or the Metrics Collection API. This feature is useful for managing integrations or Prometheus jobs that collect a large number of metrics, helping to reduce time series consumption.See [Disable Collection of a Single Metric for a specific Prometheus job](/en/reduce-metrics/).

{{% infobox type="note" %}}
Metrics consumed with Prometheus Remote Write and Sysdig Agent metrics such as `sysdig_container_cpu_used_percent` are not eligible for filtering.
{{% /infobox %}}

## July 26, 2024

### Metric And Events Retention Increase

Sysdig has increased the data retention default for Monitor Metrics and Events.

#### Metrics Retention Increases Details

{{% infobox type="note" %}}
Metric Retention changes currently only applies to AWS regions: US East (Virginia), US West AWS (Oregon), AP Australia (Sydney), European Union (Frankfurt).
{{% /infobox %}}

* `10s samples` from **4 hours** to **7 days**.
* `1m samples` from **2 days** to **14 days**.
* `10m samples` from **14 days** to **30 days**.

#### Events Retention Increases Details

* `Total Limit` from **1 Million** to **2 Million events**.
* `Custom Events Retention` from **14 days** to **30 days**.

For more details, see [Data Retention Limits]({{< ref "Data Retention#sysdig-monitor-metric-retention-limits" >}}).

## June 20, 2024

### New Costs Metrics with Custom Labels Support

[Cost Explorer](/en/cost-explorer), part of the Costs module has been upgraded with new cost metrics, bringing support for Custom Kubernetes Labels from workloads and namespaces. For teams tagging their workloads, this enables more detailed cost breakdown.

Additionally, you can easily query cost metrics, thanks to the new [simplified metrics](/en/cost.html). Dashboards and Alerts (**Sysdig Cost Advisor** section) have been added to the Library to showcase these new capabilities.

## June 10, 2024

### New UI Themes

Sysdig introduces new themes for the Sysdig Monitor UI, featuring new colors, shapes, typefaces, and artwork in both Light and Dark modes.

With the introduction of the new themes, you can experience a cleaner and more contemporary user interface, enhancing the data narrative. The refined lines of the new font and the minimalist color palette aim to provide additional space for the story Sysdig wants to convey with your data.

The older Light and Dark themes are automatically updated to the new ones, so no action is required on your part. The previous themes will remain accessible as Light - Legacy and Dark - Legacy for the next few months.