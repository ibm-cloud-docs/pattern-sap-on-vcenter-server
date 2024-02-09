---

copyright:
  years: 2024
lastupdated: "2024-01-30"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for storage
{: #storage-decisions}

The following tables summarize the storage architecture decisions for SAP on {{site.data.keyword.Bluemix_notm}} VMware® vCenter Server®.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Primary storage           | Primary file storage for VCenter Server  | Use a mix of IOPs Network File Storage (NFS) for production workloads and reduce cost storage when high IOPs are not required | vSAN is not certified for SAP workloads \n Cost and performance optimization                                                                               |
| Backup storage            | Backup storage for resiliency purposes   | Network File Storage (NFS) \n {{site.data.keyword.cos_full_notm}}                                                                          | {{site.data.keyword.cos_full_notm}} for reduce costs \n Combine NFS and {{site.data.keyword.cos_full_notm}} for long-term needs \n {{site.data.keyword.cos_full_notm}} is used as a cost optimized option for backups  |
| Archive storage           | Archive storage for backups              | {{site.data.keyword.cos_full_notm}}                                                                                     | Low cost                                                                                                                                                |
{: caption="Table 1. Architecture decisions for storage" caption-side="bottom"}
