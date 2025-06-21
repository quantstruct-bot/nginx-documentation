---
title: NGINX App Protect WAF Administration Guide
# Changelog (2024-06):
- Readability improved: Shorter sentences, clearer structure, more lists, and plain language.
- Screenshot audit: No screenshots present; no PII or outdated UI issues.

weight: 100
toc: true
type: how-to
product: NAP-WAF
docs: DOCS-1362
---

## Introduction

F5 NGINX App Protect WAF v5 is a Web Application Firewall (WAF) for NGINX Open Source and NGINX Plus. It offers advanced security features and supports everything available in [NGINX App Protect WAF v4]({{< ref "/nap-waf/v4/admin-guide/install.md" >}}).

This solution is available for an additional cost. It includes a dynamic NGINX module and containerized WAF services, making it secure and scalable.

### Key Advantages

- Works with both NGINX Open Source and NGINX Plus.
- Scalable for small and large deployments.
- Integrates easily with DevOps and SecOps workflows.

### Use Case Scenarios

- **E-Commerce Platforms:** Protects user data and transactions in busy online stores.
- **API Protection:** Secures API gateways from common threats.
- **DevOps Environments:** Adds security to continuous integration and delivery pipelines.

### Before You Begin

Make sure you have:
- A basic understanding of NGINX and containers.
- Docker or Kubernetes installed, depending on how you want to deploy.

## Supported Operating Systems

NGINX App Protect WAF v5 works on these operating systems:

| Distribution | Version             |
| ------------ | ------------------- |
| Alpine       | 3.19                |
| Debian       | 11, 12              |
| Ubuntu       | 20.04, 22.04, 24.04 |
| Amazon Linux | 2023                |
| RHEL         | 8, 9                |
| Rocky Linux  | 8                   |
| Oracle Linux | 8.1                 |

## Deployment Options

You can deploy NGINX App Protect WAF v5 in several ways:

1. **[Docker Compose Deployment]({{< ref "/nap-waf/v5/admin-guide/deploy-on-docker.md" >}}):**
   - Runs NGINX and WAF in containers.
   - Good for development, testing, and production.

2. **[Kubernetes Deployment]({{< ref "/nap-waf/v5/admin-guide/deploy-with-helm.md" >}}):**
   - Runs NGINX and WAF together in a Kubernetes pod.
   - Best for cloud-native, scalable setups.

3. **[NGINX on Host/VM with Containerized WAF]({{< ref "/nap-waf/v5/admin-guide/install.md" >}}):**
   - NGINX runs on your host or VM; WAF runs in containers.
   - Use this if you already have NGINX on your system. Adding WAF will not disrupt your current setup.

## NGINX App Protect WAF Compiler

NGINX App Protect WAF v5 uses a compiler to speed up deployments. It turns your security policies and logging profiles (in JSON format) into bundle files.

- Use the [NGINX App Protect WAF Compiler]({{< ref "/nap-waf/v5/admin-guide/compiler.md" >}}) to create these bundles.
- For signature updates, see the [Update App Protect Signatures]({{< ref "/nap-waf/v5/admin-guide/compiler.md#update-app-protect-signatures" >}}) section.

---

## Transitioning from NGINX App Protect WAF v4 to v5

> **Important:** You cannot upgrade directly from v4 to v5. The architecture has changed, so you must deploy v5 as a new installation.

### Migration Steps

1. **Back up your configuration files.**
   - Save your NGINX configs, JSON policies, logging profiles, user-defined signatures, and global settings.

2. **Install NGINX App Protect WAF v5.**
   - Choose either NGINX Open Source or NGINX Plus, depending on your needs.
   - See:
     - [Installing NGINX App Protect WAF]({{<ref "/nap-waf/v5/admin-guide/install.md">}})
     - [Deploying on Docker]({{<ref "/nap-waf/v5/admin-guide/deploy-on-docker.md">}})
     - [Deploying on Kubernetes]({{<ref "/nap-waf/v5/admin-guide/deploy-with-helm.md">}})

3. **Compile your policies and logging profiles.**
   - Use the [compiler image]({{<ref "/nap-waf/v5/admin-guide/compiler.md">}}) to convert `.json` files to `.tgz` bundles. v5 only supports the compiled bundle format.

   > **Note:**
   > If you used the default [logging profile]({{<ref "/nap-waf/v5/admin-guide/deploy-on-docker.md#using-policy-and-logging-profile-bundles">}}) JSON (like `/opt/app_protect/share/defaults/log_all.json`), you can now use the constant `log_all` instead. You do not need to compile this profile.
   >
   > ```nginx
   > app_protect_security_log log_all /log_volume/security.log;
   > ```

4. **Update your nginx.conf.**
   - Replace `.json` references with the new `.tgz` [bundles]({{<ref "/nap-waf/v5/admin-guide/install.md#using-policy-and-logging-profile-bundles">}}).

5. **Check bundle accessibility.**
   - Make sure the `.tgz` bundles are accessible to the `waf-config-mgr` container.

6. **Restart your deployment.**
   - If you already started the deployment, restart it now. If you use the VM + containers setup, also restart NGINX.
   - After migration, check the NGINX error log to confirm the process is running and there are no issues.

> **Tip:**
> Deploy v5 in a staging environment first. Compile and test your policies before moving traffic from v4 to v5. Keep your v4 deployment as a backup until you confirm everything works.


---

## Troubleshooting and FAQs

If you run into problems, check the [Troubleshooting Guide]({{< ref "/nap-waf/v5/troubleshooting-guide/troubleshooting.md#nginx-app-protect-5" >}}) for solutions to common issues.

> **Note:**
> The Docker images for NGINX App Protect WAF v5 are built using Ubuntu 22.04 (Jammy) binaries.
