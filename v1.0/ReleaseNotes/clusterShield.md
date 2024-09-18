---
linkTitle: "Cluster Shield"
title: "Cluster Shield Release Notes"
weight: "10"
aliases:
  - /en/sysdig-cluster-shield-release-notes
enable_rss: true
Description: "Here are the most recent release notes for Cluster Shield. Review the entries to learn about the latest features, defect fixes, and known issues."
category: "66ea27461b649100103615cc"
---

## 1.3.1 Sep 10, 2024

### Defect Fixes
 * Fixed a defect where  the `container_vulnerability_management` parameter used incorrect credentials to pull an image from a registry. This occurred when the image pull string resolved by the container runtime differed from the one set in the Kubernetes workload manifest.

## 1.3.0 Sep 03, 2024

### Breaking Changes
 * Renamed internal component names to complete the transition to features. Now log groups and metric contain the feature names instead.

### Feature Enhancements
 * The helm chart now supports to set an existing secret for TLS Certificates used by the application.
 * Added a new prometheus metric that expose the enablement status of each feature.
 * The `container_vulnerability_management` parameter now detects GO runtime vulnerabilities.
 * The `kubernetes_metadata` parameter now allows to set `annotations_allowlist`.

   The `annotations_allowlist` parameter lets you specify a list of annotations to be included for each resource. This configuration is particularly useful for generating KSM annotation metrics.

### Defect Fixes
 * Fixed a defect that causes existing secret credentials to be injected as environment variables
 * Fixed a defect that caused the `admission_control` parameter to use IPs instead of FQDN when a proxy is configured

## 1.2.0 Aug 05, 2024

### Breaking Changes
 * The helm chart value `image.repository` has been split into two different values: `image.registry` and `image.repository`. These two values are then concatenated to create the image pull string. If `global.imageRegistry` is provided, it will override `image.registry`. If you currently have the setting `image.repository` should update your values to this new structure.

### Feature Enhancements
 * Added support for `in1` SaaS region.
 * Added support for `pods` events in `admission_control` parameter.
 * Allow to tune up the configuration for `container_vulnerability_management` parameter to properly manage the file size for processed files.
 * Improve manifests parsing on Java packages detection.

### Fixed Vulnerabilities
 * [CVE-2024-41110](https://nvd.nist.gov/vuln/detail/CVE-2024-41110)

### Defect Fixes
 * Fixed a defect that could cause truncated log lines.
 * Fixed a defect that could cause the helm chart generated Configmap to not be properly formatted.
 * Fixed a defect that could cause the helm chart to generate an uneeded empty `ValidatingWebhookConfiguration`.
 * Fixed a defect that could cause the `admission_control` and the `posture` parameter to ignore the `ssl.verify` configuration.
 * Fixed a defect that could cause the `admission_control` and the `posture` parameter to not properly use a proxy connection.
 * Fixed a defect that could cause the `container_vulnerability_management` parameter to incorrectly handle responses from older versions of Sysdig On-premises Backend.
 * Fixed a defect that could cause the helm chart to not use CA Certificates when defined in the `global` section.
 * Fixed a defect that could cause the helm chart installation to fail if the `kubernetes_metadata` parameter is enabled and the `global.sysdig.region` is defined.
 * Fixed a defect that could cause communication issues with the `audit` and the `admission_control` parameter on clusters using custom CNI.
 * Fixed a defect that define namespace in `ValidatingWebhookConfiguration` resource created by the helm chart

## 1.1.2 Jul 18, 2024

### Defect Fixes
 * Fixed a defect that could cause the `container_vulnerability_management` parameter to scan images using the x86_64 architecture in arm64 clusters.

## 1.1.1 July 09, 2024

### Defect Fixes
 * Fixed a defect that prevented the `container_vulnerability_management` parameter to properly manage the file size for processed files.

## 1.1.0 July 03, 2024

### Feature Enhancements

 * Ability to run on GKE when the cluster is configured to run with the Autopilot functionality. To enable this feature, add the flag `--set global.gke.autopilot=true` to the configuration while installation.

 * Added support for Windows worker nodes. Once installed with the kubernetes Metadata feature enabled, it pair with the Windows Agent to include kubernetes information in the events reported by the Sysdig backend.

## 1.0.1 June 17, 2024

### Feature Enhancements
 Added the ability to configure ports used by Admission Control and Audit

## 1.0.0 June 12, 2024

### Fixed Vulnerabilities
 * [CVE-2024-24789](https://nvd.nist.gov/vuln/detail/CVE-2024-24789)
 * [CVE-2024-24790](https://nvd.nist.gov/vuln/detail/CVE-2024-24790)

## 0.11.0 June 5, 2024

### Feature Enhancements
 * Ability to configure external distributed cache
 * Introduced Container Vulnerability Management feature through Admission Control
 * Secure API token is no longer required to configure Cluster Shield for Sysdig SaaS
 * Posture feature now collects information about secrets for Inventory

### Fixed Vulnerabilities
 * [CVE-2024-2961](https://nvd.nist.gov/vuln/detail/CVE-2024-2961)
 * [CVE-2024-33599](https://nvd.nist.gov/vuln/detail/CVE-2024-33599)
 * [CVE-2024-32473](https://nvd.nist.gov/vuln/detail/CVE-2024-32473)
 * [CVE-2024-33600](https://nvd.nist.gov/vuln/detail/CVE-2024-33600)
 * [CVE-2024-33601](https://nvd.nist.gov/vuln/detail/CVE-2024-33601)
 * [CVE-2024-33602](https://nvd.nist.gov/vuln/detail/CVE-2024-33602)

### Defect Fixes
 * Fixed a defect that was preventing already existing credential secrets to be correctly loaded
 * Fixed a defect causing some components to panics due to a missing message keys in their logs
 * Set exit code correctly when the application ends with an error
 * Fixed a memory leak when the Kubernetes Metadata feature was enabled
 * Fixed a memory leak issue when the Container Vulnerability Management feature was enabled
 * Fixed a defect that was blocking the application while starting Admission Control
 * Fixed a defect preventing to display DEBUG-level logs
 * Fixed a defect which could cause long-running workloads to disappear from the UI for Container Vulnerability Management

## 0.10.1 May 3, 2024

Fixed an issue preventing Cluster Shield to read `access_key` and `secure_api_token` from already existing secrets.

## 0.10.0 May 2, 2024

### Feature Enhancements

 * Improved communication with the Sysdig backend by reducing the network footprint for Container Vulnerability Management feature
 * Improved pull secrets retrieval, reducing the memory footprint by filtering supported secret types and adding support for pagination for Container Vulnerability Management feature
 * Decreased the time required to see preliminary container vulnerability results in the UI
 * Ability to configure `sysdig_endpoint` using region
 * Introduced liveness and readiness probes in the helm chart

### Fixed Vulnerabilities
 * [CVE-2023-45288](https://nvd.nist.gov/vuln/detail/CVE-2023-45288)
 * [CVE-2024-29018](https://nvd.nist.gov/vuln/detail/CVE-2024-29019)

### Defect Fixes
 * Fixed a defect that could cause Container Vulnerability Management feature to ignore the image digest, running the risk of analyzing an incorrrect image
 * Set correct exit code for sub-processes when running in multi-process mode
 * Fixed TLS certificate generation that was causing issues on AKS clusters

## 0.9.0 April 15, 2024

### Enhancements

- Supports sending the `k8s_metadata` message. The agent retrieves the tags used for the Cost Advisor feature from `k8s_metadata`.

## 0.8.0 April 4, 2024

### Enhancements

 * You can now use an already existing secret (managed from outside the cluster-shield helm chart) to deploy informations like **Secure API Token** and **Access Key**.
 * Internal comunication use TLS by default.
 * The `kubernetes_metadata` parameter now support monitor events
 * The `kubernetes_metadata` parameter now support short lived resources

## 0.7.0 March 19, 2024

### Enhancements

 * Added the Kubernetes Metadata feature lets you collect cluster metadata replacing the Delegated Agent functionality.
 * The Cluster Shield can now be executed as single process.
 * Added `onPremCompatibilityVersion` in the helm chart that can be used to specify the on-prem version used.

### Breaking changes

 * Configuration for the `container_vulnerability_management` parameter:
   * `offline_analyzer` is not longer avilable, if you set it please remove it from the configuration.
   * `platform_services_enabled` is now enabled by default
   * `registry_verify_certificate` is now replaced by `registry_ssl`

## March 07, 2024

### Sysdig Cluster Shield Released as Controlled Availability

Sysdig is delighted to announce the controlled availability of Sysdig Cluster Shield. This solution consolidates multiple agent deployments into a single containerized component, marking a significant advancement in simplifying the deployment, management, and configuration of the Sysdig suite of security and compliance tools at the cluster level. By streamlining operations for Kubernetes environments, Cluster Shield makes it easier than ever to maintain your security and compliance posture.

For more information, see [Sysdig Cluster Shield](/en/cluster-shield).
