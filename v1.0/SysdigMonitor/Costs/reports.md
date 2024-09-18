---
linkTitle: "Reports"
title: "Reports"
weight: "15"
aliases:
  - /en/cost-reports # main alias
description: "Cost Reports help you automate reporting of costs with Slack and email integrations, and generate periodic JSON/CSV exports for integration with 3rd party tooling."
category: 66eb3c72e9d67c0059a1cdeb
---

You can also use [Cost Explorer](/en/cost-explorer) to create cost reports.

## Key Features

### Create a Report

To create a cost report:

1. Log in to Sysdig Monitor, and select **Costs** > **Reports**.

2. Select **Create New Report** in the top right corner.

   The **New Report** page opens.

3. Specify a unique **Name** and **Description**.

4. Choose an **Export Format** of CSV of JSON. You might export reports for offline processing or integration with third-party tools.

5. Define the **Scope** of the report.

   Scope controls which portions of your infrastructure cost data will be included for.

6. Select appropriate grouping.

   You can **Group By** cluster, namespace, or workload.

7. Configure the **Frequency**.

   The frequency of the report will determine the timeframe of cost data included in the final report.

8. Configure **Notifications**.

   Currently, Slack and email are supported. Both the options will present friendly reports for your team.

You can generate a **Preview** of the data to export. You can also retrieve the latest report through our API and connect with your preferred tools.

### Download Reports

To download a report:

1. Log in to Sysdig Monitor and select **Costs** > **Reports**.

2. From the main **Reports** page, select a report from the list.

   The detail panel will open.

3. Select a generated report to **Download**.

   It will be formatted as CSV or JSON, depending on the Report's configuration.
