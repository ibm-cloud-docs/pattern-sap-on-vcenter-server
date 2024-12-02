---

copyright:
  years: 2024
lastupdated: "2024-02-08"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Migration design
{: #migration-design}

Several migration scenarios are available and the most straight-forward is a direct homogeneous migration that is also known as the “lift-and-shift”. With the Lift and Shift migration method, the Infrastructure, and SAP versions remain the same. For example, on-premises SAP NetWeaver ABAP 7.0 running on VMware to the same environment on the cloud. Migration from on-premises to another infrastructure platform or SAP version, the heterogeneous migration, can become more complex, especially when combined with a database conversion or application server upgrade. For a list of migration options and tools, see [FAQ of Moving SAP Workloads](/docs/sap?topic=sap-faq-moving-sap-workloads#faq-moving-sap-workloads-overview).

## Types of SAP migration
{: #sap-migration-types}

There are two types of SAP migration categories. 

1. Homogeneous: The target has the same operating system (OS) and software versions as the source.

2. Heterogeneous: The target has a different OS, software, database type, or version than the source.

The following tables summarize various approaches for a homogeneous and heterogeneous migration that are all dependent on client environments and preferences.

## Homogeneous migration
{: #homogeneous-migration}


| Migration method | Technique summary | Advantages and concerns | Associated tools |
| -------------- | -------------- | -------------- | -------------- |
| Virtual machine (VM) Backup and Restore                     | Use specialty tools to back up entire SAP instances as virtual machine images and restore to VMware as Virtual server instances.                                                 | Lift and shift operation.                                                                                                                                                                 | Rackware Migration Management                                                                                                                                                                           |
|                                                             |                                                                                                                                                                                    | Ensure that tooling can support delta replication after the point in time move.                                                                                                                |                                                                                                                                                                                                             |
|                                                             |                                                                                                                                                                                    | Depending on the tools used, post migration adjustments can be necessary to mesh with the target environment in terms of the network and system addressing, interface enablement, and so on.          |                                                                                                                                                                                                             |
| Database Backup and Restore                                 | Backup the source database by using native DBMS tools. Restore the backup copy to a "shell" copy of the source system prebuilt on VMware on {{site.data.keyword.Bluemix_notm}}, by using identical versions of the software.  | Time to transfer large database backups can be an issue.                                                                                                                                  | SAP software to build a "shell" system \n Veeam                                                                                                                                            |
|                                                             |                                                                                                                                                                                    | The target needs the same or compatible vendor software to restore from backups files received.                                                                                                    |                                                                                                                                                                                                             |
| Fresh Build and Copy the Config                             | Build a fresh copy of the SAP system on VMware and copy and reenter the configuration parameters as required.                                                                              | Good for applications and middleware servers that do not require data transfer. The risk of error introduction if postinstallation manual procedures are applied to reproduce exact configuration. | SAP software to build "shell” system                                                                                                                                                                       |
| Database Replication or Continuous Data Protection (CDP) Tools | Establish replication between source replication and target database that is constructed on VMware on {{site.data.keyword.Bluemix_notm}}.                                                                           | Verify that the replication is supported between the source version of the database and the target version across the distances involved                                                      | SAP software to build a "shell" system \n Vendor specific database tools to configure and administer database replication, for example, SQL Always on replication, SAP HANA System Replication, Oracle DataGuard, and so on. |
{: caption="Homogeneous migration" caption-side="bottom"}

## Heterogeneous migration
{: #heterogeneous-migration}


| Migration method | Technique summary | Advantages and concerns | Associated tools |
| -------------- | -------------- | -------------- | -------------- |
| System copy that uses [SWPM](https://support.sap.com/en/tools/software-logistics-tools/software-provisioning-manager.html){: external}                                                     | Move or replatform to a different CPU Architecture, OS, or database. Uses the system                                                                                                                                                                             | Commonly used to change database server in preparation for a more significant move, for example, a move to SAP HANA DB with a classical migration approach                                                  | Copy Import and export of Software Provisioning Manager (SWPM)                                                                                                |
| SAP import and export                                                                                                                                                              | Export database from source system to target on {{site.data.keyword.Bluemix_notm}}. Transfer the export to {{site.data.keyword.Bluemix_notm}} and import into a prebuilt "shell" version of the same system and applying variations to software as required.                                                         | Time to transfer export across a network is a concern if the database is large. Using SAP import and export procedures eliminates concern about having compatible backup and restore software at the source and target. | SAP software to build "shell" system; Aspera (optional) to expedite transfer of SAP export                               |
| Standard [Database Migration Option(DMO) migration](https://support.sap.com/en/tools/software-logistics-tools/software-update-manager/database-migration-option-dmo.html){: external} from on-premises to {{site.data.keyword.Bluemix_notm}} | Use SAP Software Update Manager(SUM) or DMO to migrate and upgrade application or database software and associated data from source location across the network to a "shell" target system on VMware on {{site.data.keyword.Bluemix_notm}}.                                                                  | The technique supports upgrade of application or database software. The time to run SUM and DMO across a network can be lengthy if the source database is large or the network connection is slow or unreliable.    | SAP software to build "shell" system; SAP SUM or DMO migration tool                                                         |
| Two-Step Migration: Lift and Shift migration model followed by SUM or DMO transformation                                                                                                         | Perform a Lift and Shift Migration of the source system to {{site.data.keyword.Bluemix_notm}}. Build a shell target system in {{site.data.keyword.Bluemix_notm}} that has applied the necessary variations in software. Perform a SUM or DMO procedure within {{site.data.keyword.Bluemix_notm}} to migrate and transfer the data to the new system.  | Two-Step migration approach can take a long time to run. It is easier and faster to run a SUM or DMO procedure this way because the source and target systems are colocated.                           | SAP software to build a "shell" system \n Aspera (optional) to expedite Lift and Shift migration transfer \n SAP SUM or DMO migration tool  |
| Partner Tools [SNP Cockpit](https://www.snpgroup.com){: external}                                                                                              | Build a "shell" target system in VMware that has required software levels. Use SNP tools to analyze source system and transfer a subset of configuration, data, or technical debt from the source system across the network to the target system.      | Supports application modernization and simplifies migration by using custom tooling. Requires a robust network connection to accomplish the migration and transformation to the VMware-resident target system.| SAP installation software \n SNP CrystalBridge through {{site.data.keyword.IBM}} Consulting \n SNP Cockpit through {{site.data.keyword.IBM}} Consulting                   |
{: caption="Heterogeneous migration" caption-side="bottom"}
