---

copyright:
  years: 2024
lastupdated: "2024-02-07"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for service management
{: #service-management}

The following tables summarize the service management architecture decisions for SAP on {{site.data.keyword.Bluemix_notm}} VMware Cloud Foundation (VCF) for Classic.

## Architecture decisions for monitoring
{: #monitoring}

Typically, service management tools are integrated with a centralized service management SOC and ticketing system to provide a single pane of glass for all operations activities.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Monitoring for Application    | Provide Integration, Exception, and Health and System Monitoring | SAP FRUN (part of SAP Digital Ops Suite) \n HANA Cockpit SAP Solution Manager SAP NetWeaver exporter (sap_host_exporter) \n SAP HANA exporter (hanadb_exporter) {{site.data.keyword.Bluemix_notm}} Monitoring Prometheus Server  | Provides templates for the monitoring of technical systems that include their instances, databases, and hosts. Displays the status of managed objects and a detailed drill down to each single metric or event. Shows the history of each metric in the metric monitor. Automatic alert generation when thresholds are violated. |
| Monitoring Cloud for Platform | Monitor and correlate performance metrics and events         | Instana (Bring Your Own Monitoring)                                                                                                                                                               | Instana provides extra application performance metrics and automates Application Performance Management for the web, App, and Database tiers. Instana provides data and actionable insights to monitor the applications and automate root-cause analysis.                                                           |
{: caption="Architecture decisions for monitoring" caption-side="bottom"}

## Architecture decisions for logging
{: #logging}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Logging                   | Diagnose issues, analyze stack traces and exceptions, identify the source of errors, and monitor different log sources through a single view | [{{site.data.keyword.loganalysislong_notm}}](/docs/log-analysis?topic=log-analysis-getting-started) \n [VMware tools](/docs/log-analysis?topic=log-analysis-vmware-vcenter) \n [VMware Aria Operations](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-operations#vrw-operations-management-vrops) \n [VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-operations#vrw-operations-management-vrli) \n [VMware Aria Operations for Networks](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-operations#vrw-operations-management-vrni) | Aria operations tools are deployed in the VCS cluster to monitor the VCS environment, collect, and analyze data and generate health, risk, and efficiency alerts as an issue occurs with one of the monitored components. \n VMware Aria Operations for Logs provides centralized log collection and management, event correlation, and auditability. \n  VMware Aria Operations can collect, manage, and analyze logs across VCS \n Log Analysis is the {{site.data.keyword.IBM}} recommended tool for infrastructure logging for any non-VMware workloads. It offers ingestion and integration with other tools for diagnosis and alerts. |
{: caption="Architecture decisions for logging" caption-side="bottom"}

## Architecture decisions for alerting
{: #service-management-alerting}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Alerting                  | Provide tracking and alerting functions across application and infrastructure. | [{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.at_full_notm}} with LogDNA](/docs/power-iaas?topic=power-iaas-at-events) \n Alerting and Tracking: Pager Duty, ServiceNow (SNOW), and Customer Security Information and Event Mangement(SIEM) \n Instana is the full stack observability for application and infrastructure  | {{site.data.keyword.Bluemix_notm}} Activity Tracker provides interfaces to capture, store, view, search, and monitor API activity and supports the configuration of alerts to send notifications on one or more target channels.  |
{: caption="Architecture decisions for alerting" caption-side="bottom"}

## Architecture decisions for management and orchestration
{: #service-management-orchestration}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Management and orchestration | Automate management processes to keep applications and infrastructure secure, up to date, and available | Ansible and Terraform |               |
{: caption="Architecture decisions for management and orchestration" caption-side="bottom"}
