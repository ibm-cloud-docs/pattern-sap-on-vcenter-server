---

copyright:
  years: 2024
lastupdated: "2024-01-30"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Service management design
{: #service-management-design}

Typically, service management tools are integrated with a centralized service management or ticketing system to provide a single pane of glass for all operations activities.

VMware Aria® Operations™, formerly known as VMware vRealize® Operations™, and VMware Aria Operations™ for Logs, formerly known as VMware vRealize® Log Insight™, on {{site.data.keyword.Bluemix_notm}}® deploys the VMware Aria Operations and VMware Aria Operations for Logs Enterprise Edition tools. These tools operate and monitor the performance, health, and capacity of the {{site.data.keyword.IBM}}hosted, dedicated VMware® vCenter Server® environment. VMware Aria Operations for logs helps troubleshoot issues by using log files more quickly.

These tools are deployed by using the {{site.data.keyword.IBM}} advanced automation, from the {{site.data.keyword.Bluemix_notm}} catalog. The following VMware Aria components are ordered and included in the service:

* VMware Aria Operations Enterprise Edition

* VMware Aria Operations for Logs Enterprise Edition

VMware Aria Operations includes preinstalled and configured management packs to provide deeper visibility into the core VMware Software Defined Data Center (SDDC) components like VMware NSX®, vSAN™, and HCX™. The automation provides optimized dashboards out of the box so the full VMware stack can be monitored.
