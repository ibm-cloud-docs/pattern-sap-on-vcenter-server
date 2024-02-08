---

copyright:
  years: 2024
lastupdated: "2024-02-08"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Storage design
{: #storage-design}

SAP solutions want to make sure that there is enough available storage to accommodate the existing environment and allow for more data growth for primary, backup, and archive storage. You need to choose the appropriate SAP Certified profile to meet primary storage and growth requirements for workloads.

## VMware® vCenter Server® storage Considerations
{: #storage-considerations}

Storage considerations for SAP on {{site.data.keyword.Bluemix_notm}} for VMware® vCenter Server® include:

-   **Performance:** SAP workloads are typically I/O-intensive, so it is important to choose storage that can provide the required performance. {{site.data.keyword.Bluemix_notm}} vCenter Server offers attached Network File Storage (NFS) for use with SAP on VMware deployments. NFS is the only option that is supported for SAP NetWeaver, SAP HANA, and SAP AnyDB. VMware vSAN storage is not permitted. The {{site.data.keyword.Bluemix_notm}} allows up to 96 vSphere ESXi hosts to connect to a single endurance NFS export.

    - Network File Storage (NFS) is available in four performance tiers of 0.25, 2, 4, and 10 input and output operations per second Input-Output Operations per second (IOPS) and GB to support varying application needs. After an NFS share is ordered, it can be resized or reconfigured to allow for more or less IOPS. Also, storage can be [added or removed](/docs/sap?topic=sap-vmware-sddc-set-up-infrastructure#vmware-sddc-adding-network-storage) after provisioning.

    - Network file storage is designed to support the storing and retrieving of massive amounts of files and is ideal for computing operations that need higher IOPS. This storage is hosted in the same data center as your {{site.data.keyword.Bluemix_notm}} VMware environment. It is designed to support the storing and retrieving of massive amounts of files and is ideal for computing operations that need high IOPS, with Flash Storage, allowing near-limitless scalability. This can be replicated to other data centers over the {{site.data.keyword.Bluemix_notm}} private network.

-   **Availability:** SAP workloads are also mission-critical, so it is important to choose storage that is highly available. NFS is highly available and provides 99.9% availability. {{site.data.keyword.cos_full_notm}}, used for backups and archival can also be easily replicated to more regions if needed.
-   **Capacity:** SAP workloads can be large. It is important to choose storage that can provide the required capacity. As a result, you can select and attach (through the VCS automation) NFS storage ranging in size from 20 GB to a maximum of 24 TB.
-   **Cost:** Storage can be a significant cost factor for SAP deployments, so it is important to choose storage that is cost-effective by using a mix of IOPS tiers and {{site.data.keyword.cos_full_notm}}.

Storage must be provisioned on NFS storage. VMware vSAN storage for SAP NetWeaver, SAP HANA, and SAP AnyDB is not permitted. For more information, see [SAP Note 2161991 - VMware vSphere configuration guidelines](https://launchpad.support.sap.com/#/notes/2161991){: external} and [SAP Note 2718982 - SAP HANA on VMware vSphere and vSAN](https://launchpad.support.sap.com/#/notes/2718982){: external}.
