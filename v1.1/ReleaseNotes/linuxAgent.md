---
title: "Linux Agent Release Notes"
excerpt: "brief description of page contents that show up on previews"
category: "66ea35e1abfea54708f4ee84"
---

## 13.4.0 September 04, 2024

- Supported `sysdig-deploy` version: 1.64.0
- Supported Falco Engine version: 1000.29.0

### Feature Enhancements

#### Host Shield Technical Preview for Kubernetes

Introducing Host Shield Technical Preview for Kubernetes! Host Shield simplifies the deployment, management, and configuration of Sysdig security tools by consolidating components such as Host Scanner, KSPM Analyzer, and Rapid Response into Host Shield. For this preview, Sysdig uses the existing `sysdig-deploy` Helm chart, with plans to release a simplified chart in the coming months. 

See [Host Shield (Technical Preview)](https://docs.sysdig.com/en/docs/sysdig-secure/install-agent-components/install-agent-components/kubernetes/host-shield/) for more information.

### Vulnerability Fixes

- [CVE-2024-41110](https://scout.docker.com/vulnerabilities/id/CVE-2024-41110)
- [CVE-2024-6345](https://scout.docker.com/vulnerabilities/id/CVE-2024-6345)
- [CVE-2024-2398](https://scout.docker.com/vulnerabilities/id/CVE-2024-2398)

### Defect Fixes

#### Enable Operation in IPv6-Only Environments

An issue preventing DNS resolution from choosing the correct IPv6 address in IPv6-only environments has been fixed.
The agent is now capable of connecting as expected in environments with no IPv4 stack.

#### Display AWS EC2 Hosts in Risks

The agent can now successfully add cloud metadata to deployments in all the AWS regions, regardless of the HTTP version used in the IMDS server.

#### Ability to Report UDP Connections in Secure Light Mode

An agent running in Secure Light mode can now report UDP connections correctly when reporting networking activity under Audit Tap and Secure Audit features.

#### Fixed Container Metrics Calculation

Fixed the memory calculations for the containers with multiple cgroup controllers. This correction also resolved issues with the container metrics calculation for the `sysdig_container_memory_used_bytes` metric.

#### Fixed Workload Name and Type for Pods Created by CronJobs

Fixed a defect pertaining to `kube_pod_info metric` reporting incorrect workload for cronJobs.

#### Fixed a Defect in RHEL 9 Environments

RHEL 9.4 backported a [commit](https://github.com/torvalds/linux/commit/0af950f57fefabab628f1963af881e6b9bfe7f38), which might cause misbehaviours with the agent kernel module. Sysdig added a fix that provides an alternative method to extract the necessary information from the kernel module without relying on the affected commit.

#### Fixed Reporting False Spikes in Container CPU Usage

Resolved an issue where false CPU spikes were incorrectly reported.

## 13.3.3 August 07, 2024

- Supported `sysdig-deploy` version: 1.61.10
- Supported Falco Engine version: 1000.28.0
  
### Feature Enhancements

#### Added Reference Field for Correlating Policy and Audit Events with UUID

Added the `reference` field in Policy and Audit events containing a UUID for correlating the events exported by the Sysdig Agent with the ones exposed by the Sysdig backend.

#### Added Kubernetes Metadata to Audit Events

Agent now adds Kubernetes cluster and host name labels to Audit events, even if the events are not associated with Pods. Previously, the agent added these labels only to events generated from Pods. Now, the agent includes them in all events generated from a host that is also a Kubernetes node. With this automatic node-level event enrichment, you can quickly and easily ascertain where in the cluster a host-level event took place.


## 13.3.2 July 25, 2024

- Supported `sysdig-deploy` version: 1.61.1
- Supported Falco Engine version: 1000.28.0

### Feature Enhancements

- The kernel module has been updated to support Linux kernel version 6.10

### Defect Fixes

- Fixed a defect that prevented the agent service to automatically start after an upgrade
- Fixed overlayfs issues on latest Red Hat Enterprise Linux (RHEL) Linux kernel that includes a patch from the newest version of the kernel

## 13.3.1 July 11, 2024

- Supported `sysdig-deploy` version: 1.59.7
- Supported Falco Engine version: 1000.28.0

This hotfix aims to improve the Linux Agent stability in some specific scenarios.

## 13.3.0 July 03, 2024

{{% infobox type="note" %}}
If you are a Sysdig Secure user, skip v13.3.0 and upgrade to Sysdig Agent v13.3.1.

{{% /infobox %}}

- Supported `sysdig-deploy` version: 1.58.0
- Supported Falco Engine version: 1000.28.0

### Feature Enhancements

#### Universal eBPF Is Generally Available

[Universal eBPF](/en/understand-agent-drivers/#universal-ebpf) is now GA, offering improved agent portability and simplified installation. It provides with single probe for all Linux kernels v5.8 and above shipped with the agent.

#### Added EulerOS Support

You can now install the Sysdig Agent on EulerOS servers on Huawei Cloud. Currently, only docker installation is supported.

#### Improved Resource Consumption for Loaded Threat Detection Rules

This new version of the agent reduces run-time memory usage for the loaded Threat Detection rules.

#### Least Privileged Agent

Sysdig Agent can now run in Kubernetes with `securityContext.privileged` set to false.
This option is available through the sysdig-deploy Helm chart, specifying `agent.privileged=false`.

Known limitations:

- Works only with [eBPF drivers](/en/understand-agent-drivers)
- Doesn't work on ARM Bottlerocket

#### Support for Case-Insensitive Field Comparison

Support to case-insensitive field comparison in threat detection rules is available through the `tolower` and `toupper` field transformers. For example, `tolower(proc.name) = cat` and `toupper(proc.name) != toupper(proc.pname)`.

#### Use IMDSv2 the Default Option for AWS Metadata Retrieval

The agent will now default to using the more secure IMDSv2 API for retrieving AWS metadata. Set `imds_version: 1` in the agent configuration file to continue with the legacy behavior.

#### Correlate Dynamic Values in Threat Detection Rules

Agent now supports comparing two fields in a rule to correlate the field with a dynamic value. For example:

```
not evt.arg.name startswith val(proc.cwd)
```

This condition expect the value of `evt.arg.name` to not begin with the value output of proc.cwd, prior to this release, the comparison was a static value.

#### Ability to Filter Invalid UTF-8 Characters in the Audit Message

The agent will now filter out invalid UTF-8 characters from the "comm" and "cmdline" fields in the Audit message.

#### Support for base64-Decoding of Falco Fields

Added support for base64 decoding of Falco fields. For example, `b64(fd.name) contains cat`.

### Defect Fixes

### Vulnerability Fixes

- [CVE-2024-6104](https://scout.docker.com/v/CVE-2024-6104)
- [CVE-2023-40577](https://scout.docker.com/v/CVE-2023-40577)
- [CVE-2024-24790](https://scout.docker.com/v/CVE-2024-24790)
- [CVE-2024-24789](https://scout.docker.com/v/CVE-2024-24789)

#### Fixed Native Agent Installation Failure in Ubuntu 24.04 LTS

In the case of a native installation on Ubuntu 24.04 LTS using the legacy eBPF driver, the agent would not start. The issue has now been fixed.

#### Fixed Agent Installation Failure on Certain Hosts with No Boot Directory or with Kernel Configuration

In native install, building kernel module didn't fail if it already exists but kernel configuration isn't available. `sysdigcloud-probe-loader` script will now search for kernel configuration only when the kernel module has to be built or downloaded.

#### Added Fields Operators Check

The agent now performs static checks while loading Threat Detection rules to ascertain the compatibility of the fields and operators used in the checks.

#### Dropped Curl Requirement for Universal eBPF and Native Linux Installs

On a native installation using Universal eBPF, the agent would refuse to start unless curl is installed. This requirement has been dropped.

#### Display Kubernetes Network Policies Correctly

This version fixes the agent to correctly send the Kubernetes cluster network policies so they can be shown in the network security UI.

#### Container Drift Works as Expected after Container Restart

When cluster scoping predicate is used, Sysdig Agent might skip applying policies on container restarts. This fix closes that gap and ensures that the policies take effect upon changes in container state.

#### Display Secure Network Objects with Correct Namespace

This version attaches the correct Kubernetes namespace labels so UI can display network objects with the right namespaces.

#### Ability to Filter Invalid UTF-8 Characters

The agent will now filter out invalid UTF-8 characters from policy event messages.

#### Improved Time Resolution

The agent can now detect multiple changes to the configuration files in a second, down to the time resolution used by the filesystem.

## 13.2.1 June 11, 2024

- Supported `sysdig-deploy` version: 1.56.3
- Supported Falco Engine version: 1000.26.0

This hotfix addressed the following:

- Loading policies is now faster and uses less resources up to 10x speedup is expected, with reduced memory usage
- Fixed a defect that caused dns event to be raised even if there wasn't a rule to match that event
- Fixed a race conditon that could lead to closing short-lived file descriptors.
- Vulnerability fixes:
  - [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961)
  - [CVE-2024-32487](https://nvd.nist.gov/vuln/detail/CVE-2024-32487)
  - [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599)
  - [CVE-2024-28182](https://nvd.nist.gov/vuln/detail/CVE-2024-28182)
  - [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600)
  - [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601)
  - [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602)

## 13.2.0 May 21, 2024

- Supported `sysdig-deploy` version: 1.53.0
- Supported Falco Engine version: 1000.25.0

### Feature Enhancements

#### Suse Linux Enterprise Server Support

You can now install the Sysdig Agent on SLES 12 and SLES 15.

- SLES12 only supports the kernel module driver
- If you want to enable legacy eBPF on an x86_64-based SLES15 Server, install `clang`  manually using `SUSEConnect`:

    `SUSEConnect --product PackageHub/15.5/x86_64`

#### Support for Adding Labels to JMX Metrics

Added support for labels on JMX metrics collected by the agent. For more information, see [Collect JMX Labels](/en/docs/sysdig-monitor/integrations/monitoring-integrations/custom-integrations/integrate-jmx-metrics-from-java-virtual-machines/#collect-jmx-labels).

### Defect Fixes

#### Fixed a Race Condition in Universal eBPF

Due to a kernel defect on x86 machines prior to versions [6.8](https://git.kernel.org/pub/scm/linux/kernel/git/netdev/net.git/commit/?id=32019c659ec), a page fault occurred when the agent tried to access the `VSYSCALL` address range using the `bpf_probe_read_kernel` method. The issue occurred in universal eBPF due to a race condition in the `accept`/`accept4` syscalls. In eBPF, locks cannot be used, and therefore, under some circumstances, race conditions could happen.

This agent release provides a fix to avoid race conditions in these syscalls.

#### Fixed Debian Package Upgrade

On debian-based native installations, upgrading from an older version might result in the agent packages being accidentally marked as unneeded dependencies and subsequently uninstalled by autoremove. This issue has been fixed.

#### Fixed Metadata Requests in Proxy Environments

When the agent had the `http_proxy` environment, obtaining the instance information for machines running in AWS, Azure, or GCP did not work. This issue has been fixed.

#### RPM Install Honors CPU Quota

Fixed the issue where RPM installation was not honoring the CPU quota for `subprocess_resource_limits`.

#### Fixed Limit Settings for Subprocess Resources

Fixed the issue where the `subprocess_resource_limits` setting was not working for some distro with cgroup v2.

## 13.1.1 May 08, 2024

- Supported `sysdig-deploy` version: 1.52.4
- Supported Falco Engine version: 1000.24.0

This hotfix addresses the following:

- Vulnerability fixes:
  - [CVE-2023-45288](https://nvd.nist.gov/vuln/detail/CVE-2023-45288)
  - [CVE-2024-24557](https://nvd.nist.gov/vuln/detail/CVE-2024-24557)

### Feature Enhancements

#### Support for Malware Detection and Prevention

Malware Detection and Prevention is now available in Technical Preview for Hosts and Containers.

Detection and Prevention is enabled by default for Containers.

Detection is enabled by default for Hosts, but Prevention is disabled by default for Hosts. To enable Prevention for Hosts, use this configuration:

```yaml
protections:
  malware_control:
    enable_detection_on_host: true
    enable_prevention_on_host: true
```

For more information, see [Malware Detection](/en/configuration-library-secure).

#### On-Demand Security Policy Loading

The agent now requests security policies only on start, or if the security policies are modified on the Sysdig backend. This should result in a significant reduction in network bandwidth consumption, while also reducing the performance impact of periodically updating security policies.

### Defect Fixes

#### Added Flatcar Support in Legacy eBPF Mode

In earlier versions, the legacy eBPF driver failed to compile on recent 6.8 kernels for Flatcar Container Linux. This issue has now been fixed.

## 13.1.0 April 19, 2024

- Supported `sysdig-deploy` version: 1.51.0
- Supported Falco Engine version: 1000.24.0

### Feature Enhancements

#### Activity Audit Support for Network and File Activity in Secure Light Mode

Sysdig Agent configured in `secure_light` mode will now support tracking network and file activity as part of the Activity Audit feature, in addition to the existing monitoring of command line activity.

#### Native Package enhancements

Native package installation has undergone a major revamping resulting in the following changes.

##### Switched supervisor from SysV to systemd

The agent now runs through a systemd service unit as opposed to a SysV init script.

##### Fine-grained packages depending on the driver

Depending on the driver you intend to use (`kmod`, `legacy_ebpf` or `universal_ebpf`) you should now install a specific package with a smaller set of dependencies.  The install script and the ansible role have been adapted accordingly.  Please refer to [Package Reference](/en/install-hosts-secure/) for more details.

#### Uptime Metrics for Agent Sub-Processes

Added agent health metrics to the prometheus exporter showing the uptime of agent sub-processes.

#### Feature-Enabled Metrics

Sysdig agent can now collect feature-enabled metrics using prometheus exporter when health metrics are enabled. See [Agent Health Metrics](/en/view-agent-health/#agent-health-metrics) for more information.

#### `kube_configmap_info` Metric

Added `kube_configmap_info` metric to provide information on the agent configmap. For more information, see [ConfigMap Metrics](/en/enable-kube-state-metrics/#customize-ksm-collection).

#### Enriched sysdig_agent_info with Linux Information

The `sysdig_agent_info` metric now is enriched with Linux kernel and distribution information.

#### Ability to Configure `kube_node_annotations`

Added the ability to configure the `kube_node_annotations` metric. For more information, see [Enable Node Annotations](/en/enable-kube-state-metrics/#customize-ksm-collection).

### Defect Fixes

#### Fixed Repeated Warning Log

Fixed the issue where a warning log was being repeated frequently in both debug and warning modes.

#### Fixed Automatic Unloading of the Kernel Module

In the case of native installations on Debian-based systems, stopping the service or uninstalling the package might leave the kernel module loaded.  This has been fixed.

#### No longer inserting the Kernel Module when legacy_ebpf or universal_ebpf are selected

In the case of native installations, the kernel module would be built and loaded even when not strictly needed (i.e. when legacy_ebpf or universal_ebpf is selected).
Provided the appropriate package is selected, this is no longer the case.

## 13.0.4 April 12, 2024

- Supported`sysdig-deploy` helm chart version: 1.49.8
- Supported Falco Engine version: 1000.23.0

This hotfix addresses the following:

- Fixed a defect that prevented the agent upgrade from v12.20 to v13.0 on EKS Bottlerocket
- Delivered a preventative change that removes Sysdig Agent's impact on node stability due to [GKE PDCSI Driver Defect](https://github.com/kubernetes-sigs/gcp-compute-persistent-disk-csi-driver/issues/1657). All the code paths that can potentially surface the GKE issue have been replaced with alternate logic.

## 13.0.3 March 27, 2024

- Released in `sysdig-deploy` helm chart version: 1.46.2
- Supported Falco Engine version: 1000.23.0

This hotfix addresses the following:

- Fixed build failures of the legacy eBPF probe on the most recent 6.x kernels.
- Fixed an issue where the Runtime Policy pausing Container Action was not working on environments with cgroup v1.

## 13.0.2 March 21, 2024

- Released in `sysdig-deploy` helm chart version: 1.45.5
- Supported Falco Engine version: 1000.23.0

This hotfix addresses the following:

- Vulnerability fixes:
  - [CVE-2024-24786](https://nvd.nist.gov/vuln/detail/CVE-2024-24786)
  - [CVE-2024-27304](https://nvd.nist.gov/vuln/detail/CVE-2024-27304)

- Fixed a build issue of the `legacy_ebpf` driver that impacted RHEL v5.14 kernels with RHEL subversion 410 or higher.

- Fixed kernel module build for linux kernel 6.8.

## 13.0.1 March 11, 2024

- Released in `sysdig-deploy` helm chart version: 1.42.3
- Supported Falco Engine version: 1000.23.0

This hotfix fixed an issue where the Sysdig Agent could retain allocated UDP ports until reaching port saturation, occurring under specific combinations of the driver used and enabled features.

## 13.0.0 March 06, 2024

- Released in `sysdig-deploy` helm chart version: 1.41.0
- Supported Falco Engine version: 1000.23.0

{{% infobox type="note" %}}

We strongly recommend you to skip v13.0.0 and upgrade to Sysdig Agent v13.0.1. See [Breaking Changes](/en/docs/release-notes/sysdig-agent-release-notes#breaking-changes) for more information.

{{% /infobox %}}

### Feature Enhancements

#### Updated Docker Image to UBI9

Sysdig Agent's Universal Base Image has been upgraded from UBI8 to UBI9.

#### Added Agent Health Metrics in secure_light Mode

Added the following health metrics when the agent is running in `secure_light` mode:

- `sysdig_agent_analyzer_num_evts`
- `sysdig_agent_analyzer_dropped_evts`

#### Support for TLS and Basic Authentication in Agent Prometheus Exporter

Agent Prometheus Exporter now supports TLS and basic authentications.

#### Ability to Collect Subattributes from JMX metrics

Added ability to collect individual subattributes from CompositeData JMX metrics.

#### Availability of Promscrape in ARM64 in FIPS Mode

Sysdig Agent now includes FIPS-mode promscrape binary previously missing for ARM platforms.

### Kill Process in Workload

In **Threat Detection Policies**, **Workload** and **List Matching** policies can now be configured to kill the event-triggering process. For details, see [**Workload**](/en/workload-policy).

### Breaking Changes

As part of Sysdig Agent 13.0.0 release, and as anticipated in the release notes for the 12.20.0, Sysdig dropped the support for:

- logwatcher
- RHEL6 and CentOS6

All Sysdig users affected by these changes have been notified. If you haven't received any communication from Sysdig, it means there is no impact on your usage.

### Defect Fixes

#### Updated `ssl_shim` Configuration

The `ssl_shim` configuration has been changed to fix an issue where `openssl.cnf` bundled with the agent expected `ssl_shim` to select the FIPS or non-FIPS providers at startup time. This configuration broke other programs that are dynamically linked against OpenSSL v3.

Added a <code>openssl_conf</code> configuration flag to allow users to specify a custom <a href="https://www.openssl.org/docs/man3.2/man5/config.html"><code>openssl.cnf</code></a> file for use with the agent.  To include custom OpenSSL v3 library, you need to set the [custom](https://www.openssl.org/docs/man3.2/man5/config.html) `openssl_conf` and your library path. This configuration is required when `openssl_lib` points the agent to a custom OpenSSL v3.x library. See [openssl_lib](/en/configuration-library) for more information.

#### Support for Universal eBPF on 1-vcore Machines

Universal eBPF is now supported on 1-vcore machines.

#### Scoping Events to Containers on Specific Kubernetes Clusters

The host scope resolution now works correctly when additional scope predicates are specified along with the standard `contauner_id=""`. For example, `contauner_id=""` and `kubernetes.cluster.name=my_cluster`

#### Fixed Misleading Collector Reconnection Attempts Logs

Fixed an issue where agent report a large number of logs with "No further retries left for attach to container".

## 12.20.0 January 31, 2024

- Supported `sysdig-deploy` version: 1.37.11
- Supported Falco Engine version: 1000.22.0

### Feature Enhancements

#### Removed the `sysdig_secure.enabled` Tag

Removed the hardcoded `sysdig_secure.enabled` tag generated when runtime detection is enabled using the following configuration:

```
security:
   enabled: true
```

Use the `agent_secure_enabled` label in the `sysdig_agent_info` metric instead to check if runtime detection is enabled.

#### Enhanced Kernel Sampling Ratio to Handle High Event Loads

The activation logic of the kernel sampling ratio has been improved. You may notice a change in sampling ratio metrics behavior after upgrading to v12.20.0. This behavior is intentional and indicative of a healthy system response.

The sampling ratio is a key tool for the agent to regulate performance during high workloads. Monitoring these metrics gives valuable insights into the overall health of the agent. Version 12.20.0 brings the improvement to optimize the agent's adaptability to high event loads.

#### Support for Container Actions and Captures

Sysdig agent supports the following new actions in [Container Drift](/en/drift) policies and Malware policies:

- The ability to create capture files
- The ability to Kill/Pause/Stop a container

Malware policies are currently in Controlled Availability. Contact Sysdig Support for access to the Malware feature.

### Defect Fixes

#### Updating Kernel No Longer Results in DKMS Failure

Fixed an issue where updating the kernel resulted in Dynamic Kernel Module Support(DKMS) failure in host installations with [kmod](https://man7.org/linux/man-pages/man8/kmod.8.html).

#### Additional Log Lines No Longer Appear After Agent Update

Fixed an issue where policy events with associated actions could cause a significant increase in the number of lines logged.

### Deprecation Notice

In the upcoming agent release, Sysdig will deprecate the support for logwatcher, RHEL6, and CentOS6.
