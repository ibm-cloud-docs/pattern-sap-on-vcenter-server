---

copyright:
  years: 2024
lastupdated: "2024-02-05"

subcollection: pattern-sap-on-vcenter-server
keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for resiliency
{: #resiliency-architecture}

The following tables summarize the resiliency architecture decisions for SAP on {{site.data.keyword.Bluemix_notm}} VMware Cloud Foundation (VCF) for Classic.

## Architecture decisions for high availability (HA)
{: #resiliency-architecture-high-availability}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| High availability for SAP HANA       | Provide 99.97% availability for SAP HANA DB   | SAP HANA System Replication (HSR)                                                  | Enabling HANA HSR addresses SAP HANA outage reduction due to planned maintenance, faults, and disasters. It supports a recovery point objective (RPO) of 0 seconds and a recovery time objective (RTO) measured in minutes. |
| High availability Infrastructure | Provide 99.9% availability for infrastructure | HA solution on a single zone with an application SLA of 99.9% with VMotion enabled | Minimize cost, implementation and maintenance complexity, potential latency and maximize value with IBM solutions.                                                                                                          |
{: caption="High availability architecture decisions" caption-side="bottom"}

## Architecture decisions for disaster recovery (DR)
{: #resiliency-architecture-disaster-recovery}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Disaster recovery for application and infrastructure  | DR capability in secondary region \n  DR with Recovery Point Objective \< 15 min and Recovery Time Objective \< 4 hours. | Veeam Continuous Data Protection (CDP) implemented in both primary and secondary regions                   | Support for databases (SAP HANA , Oracle or MSSQL) \n  Veeam service seamlessly integrates directly with VMware Cloud Foundation (VCF) for Classic on {{site.data.keyword.Bluemix_notm}} to help achieve high availability. This service provides recovery points and time objectives for SAP application servers. Controls both the backups and restores of all virtual machines (VMs) for SAP applications directly from the Veeam console. |
| Disaster recovery for SAP HANA                    | SAP HANA disaster recovery capability in secondary region                                         | SAP HANA System Replication (HSR) AnyDB database native tools for replication | Continuous replication of data from a primary to a secondary system in a separate region, including in-memory loading, system replication facilitates rapid failover in the event of a disaster                                                                                                                                                                               |
{: caption="Disaster recovery architecture decisions" caption-side="bottom"}

## Architecture decisions for backup
{: #resiliency-architecture-backup}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Backup for SAP              | Back up of NetWeaver and SAP HANA data | SAP NW file level backup  \n SAP NW storage snapshot  \n SAP SAP HANA file level backup  \n SAP SAP HANA storage snapshot | Minimize cost and operational ease using SAP Native tools like DBACOCKPIT, SAP HANA COCKPIT, backint will be used to take SAP Database backup. |
| Backup for Infrastructure   | Infrastructure backups                 | Veeam                                                                                                         | Veeam is SAP HANA Certified Automated provisioning as an add-on to vCenter Server                                                              |
{: caption="Backup architecture decisions" caption-side="bottom"}
