---
linkTitle: "Serverless Agent"
title: "Serverless Agent Release Notes"
weight: "11"
aliases:
  - /en/serverless-agent-release-notes.html
enable_rss: true
---

{{% infobox type="tip" %}}

For installation and upgrade steps, see [Serverless Agents](/en/install-serverless-secure).

{{% /infobox %}}

## Serverless Patcher 5.1.0 August 19, 2024

This release updates only the [Serverless Patcher](/en/install-ecs-serverless-patcher) to address the vulnerabilities.

### Defect Fixes

#### Vulnerability Fixes

Addressed the following vulnerability:

- [CVE-2024-41110](https://nvd.nist.gov/vuln/detail/CVE-2024-41110)

## Serverless Agent 5.0.2 June 25, 2024

### Feature Enhancements

#### Enhanced Process Logging

Process logging has been improved to reduce the memory usage. The agent now retains only the latest fatal log while discarding the previous ones. This bounds the potential memory used for crash logs and expresses the intent better, since if multiple fatal signals were received, the earlier ones weren't actually fatal but handled by the process.

Previously, all fatal signals for a process generated detailed reports with stack trace and memory map when the process was terminated because of the signal. This caused potentially unbounded memory growth because all the logs in memory were stored to log them when the process exited.

#### Improved Memory Usage

Reduced memory usage in the binpatch performance library.

### Defect Fixes

- Fixed missing process information for processes where the clone or fork event was missing. The max_n_proc_lookups parameter controls the maximum number of proc filesystem lookups performed. This change sets it to -1, meaning that no limit is applied to the number of proc scans. Previously, it was set to 1, meaning that only a single scan was allowed.
- The `memdump.size` setting was ignored in previous versions, leading to potentially excessive memory consumption up to 300 MB. The setting works as expected now, and the default is changed to 32 MB.
- Addressed a defect in which the event Process Tree fields were missing data.

#### Vulnerability Fixes

Addressed the following vulnerabilities:

- [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961)
- [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599)
- [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600)
- [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601)
- [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602)

## Serverless Agent 5.0.1 June 07, 2024

### Defect Fixes

- Improved performance in terms of CPU and memory usage for processing policy updates
- Fixed excessive memory usage with workloads starting many child processes on musl-based images, such as Alpine Linux, and with Go applications
- Reduced memory usage in the binpatch performance library

## Serverless Agent 5.0.0 April 08, 2024

### Feature Enhancements

#### Changes to Deploying the Serverless Agent

- To prioritize between `Security` and `Availability` in deployments, configurable Serverless Agent Priority Modes have been introduced. For more information, see [Configure Priority Modes](/en/configure-priority-modes).

- To reduce the load on the Orchestrator Agent, the following changes are introduced:
  
  - A single Workload Agent sidecar will now secure all containers within a task, whereas before each container would run its own Workload Agent.
  - The Workload Agent now runs within the sidecar container with only the `pdig` instrumentation stack remaining in the workload container.

For this enhancements to work, your system requires one of the following:

- serverless-patcher v5.0.0 or above for CloudFormation template
- Terraform provider v1.23.3 or above

#### Availability of `sysdig_serverless_agent_info`

Serverless Agent now exposes the Prometheus metric, `sysdig_serverless_agent_info`. This metric provides the following labels:

- `agent_type`
- `container_id`
- `serverless_account_id`
- `serverless_cloud_vendor`
- `serverless_cluster_id`
- `serverless_task_id`
- `serverless_version`

### Known Issues

The Workload Agent versions 4.2 and prior will not receive policies when connected to the Orchestrator v5.0.0.

For more information, see the [Compatibility Matrix](/en/install-ecs-fargate-secure/#compatibility-matrix).

### Defect Fixes

#### Vulnerability Fixes

Fixed the following vulnerabilities:

`serverless-patcher`

- [CVE-2024-24557](https://nvd.nist.gov/vuln/detail/CVE-2024-24557)

`orchestrator-agent`

- [CVE-2021-35937](https://nvd.nist.gov/vuln/detail/CVE-2021-35937)
- [CVE-2021-35938](https://nvd.nist.gov/vuln/detail/CVE-2021-35938)
- [CVE-2021-35939](https://nvd.nist.gov/vuln/detail/CVE-2021-35939)
- [CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218)
- [CVE-2023-5363](https://nvd.nist.gov/vuln/detail/CVE-2023-5363)
- [CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981)
- [CVE-2023-7104](https://nvd.nist.gov/vuln/detail/CVE-2023-7104)
- [CVE-2024-0553](https://nvd.nist.gov/vuln/detail/CVE-2024-0553)
- [CVE-2024-0567](https://nvd.nist.gov/vuln/detail/CVE-2024-0567)

## Serverless Agent 4.3.2 Hotfix Jan 12, 2024

This hotfix updated the CloudFormation template, `orchestrator-agent.yaml`, to include default values for autoscaling. When autoscaling is disabled, the autoscaling parameters now default to `0`.  

## Serverless Agent 4.3.2 Jan 11, 2024

### Defect Fixes

#### Improved Agent Error Logging

Enhanced error message clarity for cases where the Workload Agent fails to start the workload task.

#### Make signal handling more robust

Fixed an edge case in handling signals while running instrumentation code.

#### Improve ELF format compatibility

Fixed instrumentation crashes associated with specific workloads, such as Chromium webdriver, that occurred when loading ELF binaries with a particular structure.
