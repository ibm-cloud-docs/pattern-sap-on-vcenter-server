---

copyright:
  years: 2024
lastupdated: "2024-01-30"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for compute
{: #compute-decisions}

The following table summarizes the compute architecture decisions for SAP on {{site.data.keyword.Bluemix_notm}} VMware® vCenter Server®.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Virtualization (NetWeaver) | Verify that the target environment and the workload requirements match and are SAP certified.                                    | {{site.data.keyword.Bluemix_notm}} vCenter Server (VCS) note: Overcommitment of CPU and memory is a standard VMware practice, especially for nonproduction and disaster recovery (DR) systems, and is allowed for Netweaver  | - {{site.data.keyword.IBM}} is the only SAP-certified provider that can run production VMware workloads on Cloud. \n - Minimize the business disruption from migrating on-premise VMware workloads, which requires the target environment to be on VMware  \n - Choose only SAP certified and SAP NetWeaver certified compute. For more information, see [VMware SDDC certified profiles for SAP NetWeaver](/docs/sap?topic=sap-nw-iaas-offerings-profiles-vmware)  |
| Virtualization (SAP HANA)   | Verify that the target environment and the workload requirements match and are SAP certified.                                   | {{site.data.keyword.Bluemix_notm}} vCenter Server (VCS) \n SAP recommends to not overcommit CPU or memory for SAP HANA                                                                  | - {{site.data.keyword.IBM}} is the only SAP-certified provider that can run production VMware workloads on Cloud  \n - Minimize business disruption migrating on-premise VMware workloads, which requires the target environment to be on VCS and VMware  \n - Choose only SAP certified and SAP HANA certified compute. For more information, see [VMware SDDC certified profiles for SAP HANA](/docs/sap?topic=sap-hana-iaas-offerings-profiles-vmware).    |
| Backup infrastructure       | Backup infrastructure for data retention                                                                  | {{site.data.keyword.baremetal_short}}(s)                                                                                                                                                       | Server to host backup services that are provided by Veeam \n Bare Metal can meet large backup requirements                                                                                                                                                                                                                                                                                 |
| Bastion infrastructure      | Bring your own bastion jump server, or Privileged Access Gateway, with privileged access management software | Virtual Servers (VSI)                                                                                                                                                      | Bastion host for administrative access and privileged management services                                                                                                                                                                                                                                                                                                        |
{: caption="Table 1. Architecture decisions for compute" caption-side="bottom"}
