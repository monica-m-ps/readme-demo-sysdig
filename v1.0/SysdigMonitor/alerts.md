---
linkTitle: "Events"
title: "Events"
weight: "16"
no_list: true
slug: alerts
parentDocSlug: sysdig-monitor-introduction
description: "The Sysdig Monitor Events module provides a comprehensive real-time overview of activity within your infrastructure, in the form of a live events feed. The most recent events are displayed at the top of the list. Scroll down or use the time bar at the bottom of the screen to examine events as old as thirty days."
---

## Overview

An event represents a change in the state of an object in a monitored environment. In Sysdig Monitor, an event is a record indicating a specific occurrence or change within the monitored environment, encompassing alerts, containers, Kubernetes, infrastructure, and custom events.

Click any event to open the event detail panel on the right:

<div style="max-width: 70%">
  <img src="/image/event_feed.png" />
</div>
<br>

*The Event Feed with the event detail panel open.*

On the panel, you will find detailed information on the event, such as precisely when and where it occurred. Perform additional actions, such as [Explore](/en/explore.html) to examine the event's origin in your infrastructure, or [Create an Alert](/en/configure-event-alerts.html) to be notified about future occurrences of this event.

Additionally, you can:

- Examine event details to gather knowledge towards remediation.

- Filter your feed by severity, to find the most urgent events.

- Review an event to identify the exact origin of an issue.

- Search an event, such as a container crashing, to count how many times it has occurred within a given period.

- Look back over past events to identify patterns.

- Create an alert so you will be instantly notified whenever a known issue arises.

## Prerequisites

If you do not have Sysdig Agent installed in your environment, or you are not logged in to an account with permission to access an environment, the Events module will appear empty to you.

To populate the Events feed, ensure that:

1. Install [Sysdig Agent](/en/install-agent-monitor).

2. Log in to Sysdig Monitor and ensure that your account has permission to access the environment.

Once installed, the Sysdig Agent will collect certain events by default. These include Sysdig-integrated services like Kubernetes, ContainerD, and Docker. To collect events from additional sources, such as LogDNA, see [Collect Event Data](/en/collect-event-data.html).

Administrators will be able to see events from the entire infrastructure, while members of a team will only see events from the part of infrastructure assigned to their team.

## Types of Events

Events are classified by type and by status. Types of Events include 
- Alert Events
- Sysdig Events
- Infrastructure Events
- Custome Events

See [Event Types](/en/event-types) for more details. 

Statuses only apply to Alert Events. Alerts have two states and the state is conveyed by an icon.

- Triggered
  <br> A ringing bell icon indicates a triggered alert.
- Resolved
  <br> A silent bell icon indicates that it is resolved.

## Understand Events Detail Panel

The Events module is primarily a means to visualize activity within your environment, but it also allows for direct engagement with events, through the Events detail panel.

The operations available vary according to the nature of the event. 

The operations available vary according to the type and status of an event. Here are the mappings to the various options:

- Triggering Alert Event

  - Acknowledge
  - Manually Resolve
  - Create Silence from an event
  - Explore (if Threshold Alert)
  - Open in PromQL Query (if Prometheus Alert)

- Resolved Alert Event

  - Create Silence from an Event
  - Explore

- Triggering Event Alert

  - Acknowledge
  - Manually Resolve
  - Create Silence from Event

- Resolved Event Alert
  - Create Silence from Event
