---

copyright:
  years: 2024
lastupdated: "2024-02-06"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Resiliency design
{: #resiliency-design}

Resiliency is the ability of a workload to meet a specific target Service Level Objective (SLO), Service Level Availability (SLA), or recover from a service disruption and still meet the required SLA. Resiliency needs to be considered at both the infrastructure and application layers across the entire solution. Resiliency covers three primary areas: backup, disaster recovery, and high availability.

## Backup design
{: #backup-design}

When you back up SAP deployed to VMware on {{site.data.keyword.Bluemix_notm}}, take the following into consideration.

- **Backup frequency and retention:** Consider how often the data needs to be backed up, and how long to retain the data. The retention period drives storage decisions so the most cost-effective storage should be used for long-term, infrequently used backups.
- **Backup type:** There are two main types of backups: full backups and incremental backups. Full backups back up all of your data and use more storage. Incremental backups back up only the data that changed since the last full backup. Incremental backups are typically faster and more efficient than full backups, but they require a full backup first.
- **Backup location:** Where are backups stored? Backup location might depend on specific business and regulatory compliance requirements and determine where data can be backed based on geography. Choose a backup location that is secure and follows compliance and regulatory rules.
- **Backup size:** Consider the largest database size for full backups with room for addition growth. Also, it’s recommended to complement the backup solution with daily production snapshots.

## High availability (HA) design
{: #ha-design}

High availability is the resource availability in a solution throughout the stack, built in by design, to withstand individual component failures in the system.

When deploying SAP to VMware® vCenter Server® on {{site.data.keyword.Bluemix_notm}}, various HA technologies can be used:

- **VMware vMotion:** VMware vMotion allows live migration running VMs between hosts without downtime. This can be used to avoid downtime due to planned or unplanned hardware maintenance.
- **VMware vSphere HA:** VMware vSphere HA automatically restarts failed VMs on other hosts in the cluster. This can help to minimize downtime due to hardware failures.
- **SAP HANA System Replication (HSR):** SAP HSR is a high-availability solution for SAP HANA databases. It replicates data synchronously between two nodes, so that if a failure occurs, the secondary node can take over immediately.

## Disaster recovery (DR) design
{: #dr-design}

Disaster recovery (DR) is the infrastructure, application layers, and accompanying set of policies and procedures to enable the recovery or continuation of vital technology infrastructure and applications following a natural or human-induced disaster.

When you deploy SAP to VMware® vCenter Server® on {{site.data.keyword.Bluemix_notm}}, you can use various DR strategies:

- **Replicating your data to a secondary region:** Disaster Recovery requires replicating data to a secondary region in {{site.data.keyword.Bluemix_notm}}, so that if a disaster occurs in one region, workloads can quickly failover to the secondary region within specified Recovery Time Objective(RTO) and Recovery Point Objective(RPO) requirements. The technology choices that are used consider the RTO and RPO requirements. Typically, as RTO and RPO service level objectives decrease, a “near real time” replication solution is needed.
- **Disaster recovery services and software:** Third-party disaster recovery software is available, selection dependent on RTO and RPO SLAs that can aid with DR scenarios. This software replicates data to an alternative {{site.data.keyword.Bluemix_notm}} region and provides the tools for infrastructure and application recovery in a disaster.

Both HA and DR can be enabled by using several technologies and approaches, which depends on the RPO, RTO, and SLA requirements.

SAP doesn't support the application layer and database to be deployed across different zones or colocations. The application and database layers must exist in the same {{site.data.keyword.Bluemix_notm}} availability zone.
{: important}

A combination of SAP Native Database Backup tools can be used to deliver the HANA resiliency services such as:

-   DBACOCKPIT
-   SAP HANA COCKPIT
-   “Backint” for SAP Database backups

## Resiliency for infrastructure and application
{: #infra-app-resiliency}

Resiliency needs to be considered for both the infrastructure and application levels.

### Infrastructure
{: #infra-resiliency}

- A single instance of VMware® vCenter Server® provides a 99.9% availability.
- New multizone instances are no longer supported.
- Clients might implement instances in a different region for DR in an active or standby scenario.
- VMware vMotion, VMware Distributed Resource Scheduler (DRS), and VMware HA capabilities can be used to achieve operational performance and availability. For more information, see [SAP note 2937606](https://launchpad.support.sap.com/#/notes/2937606){: external}.

### Application
{: #application-resiliency}

- Client and service providers might choose to configure SAP and database clusters for HA and DR purposes to achieve >99.7% SLA.
- If a deployment requires an SAP SLA greater than 99.5%, a cluster for SAP and databases should be implemented.

For more information about recovery time and other considerations, see[Storage impacts on Recovery Time](/docs/sap?topic=sap-storage-design-considerations#storage-performance-backup-rto) and [Additional storage resiliency considerations](/docs/sap?topic=sap-storage-design-considerations#storage-performance-backup-rto).
