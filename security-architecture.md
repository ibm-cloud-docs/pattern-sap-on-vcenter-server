---

copyright:
  years: 2024
lastupdated: "2024-02-06"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for security
{: #security-architecture}

The following tables summarize the security architecture decisions for SAP on {{site.data.keyword.Bluemix_notm}} VMware Cloud Foundation (VCF) for Classic.

## Security architecture decisions for data
{: #security-architecture-data}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Data: Encryption at Rest          |                                                                                                                                                                       |                                                                         |                                                                                                                                                             |
|  Primary Storage                   | Ability to encrypt data at rest                                                                                                                                       | Endurance Network File Storage(NFS) with VMware vSphere encryption                    | VMware vSphere encryption applies to all types of VMware storage, including NFS.                                                                            |
|  Backup storage and archive storage | Ability to encrypt backups                                                                                                                                            | {{site.data.keyword.cos_full_notm}} encryption                                         | By default, all objects that are stored in {{site.data.keyword.cos_full_notm}} are encrypted by using randomly generated keys and an all-or-nothing-transform (AONT).  |
| SAP HANA data encryption           | Ability to encrypt SAP HANA data at rest                                                                                                                          | SAP HANA Data Volume Encryption (DVE)                                   | DVE encrypts SAP HANA data at the persistence layer, protecting data stored on disk from unauthorized access at operating system level.                     |
| Data: Encryption in transit       | Ability to encrypt data while in transit, to servers, between servers, and any attached storage secure management and production VMs while at-rest or in-transit. | FTPs and HTTPs protocols (client to server) VMware vSphere® encryption | Secure client requests over HTTPs and FTPs \n Secure management and production VMs while at-rest or in-transit.                                                     |
{: caption="Data architecture decisions" caption-side="bottom"}

## Security architecture decisions for Identity and Access
{: #security-architecture-identity-and-access}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Identity and Access Management(IAM) | Securely authenticate users for platform services and control access to resources consistently across {{site.data.keyword.Bluemix_notm}} | {{site.data.keyword.iamshort}}(IAM)                                                                                                                 | Use IAM access policies to assign users, service IDs, and trusted profiles access to resources within the {{site.data.keyword.Bluemix_notm}} account.                                                                              |
| Privileged Identity and Access Management | Privileged access management (PAM) services for administrative purposes                                         | Bring you own bastion host with PAM software that is deployed on underlay private Vlan 2FA authentication through [{{site.data.keyword.IBM}} security verify](https://www.ibm.com/products/verify-identity){: external}  | Securely access remote resources over the private network for management purposes; bastion accessed by SSH. Session recording that tracks all activities, successful or not, to note any potential threats |
{: caption="Identity and access architecture decisions" caption-side="bottom"}

## Security architecture decisions for core network protection
{: #security-architecture-core-network-protection}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Core Network Protection   | Strict separation of duties \n Isolated security zones between environments \n Isolated, private cloud environment  | NSX-T™ (Overlay) \n {{site.data.keyword.vsrx_full}} with content security bundle (Underlay)  | A design combination that uses both NSX-T™ and {{site.data.keyword.vsrx_full}} to isolate VLANas and network traffic \n Separate VLANs and NSX-T™ VXLANs and the use of firewall capabilities. |
{: caption="Core network protection architecture decisions" caption-side="bottom"}

## Security architecture decisions for threat detection
{: #security-architecture-threat-detection}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- |-------------- |
| Threat detection          | Boundary protection: The highest level of isolation from external network threats intrusion prevention and detection at all ingress and egress \n Unified Threat Management (UTM) Firewall  | {{site.data.keyword.vsrx_full}} with content security bundle  | Advanced FW Features (Intrusion Prevention System(IPS) and Intrusion Detection System(IDS), Unified Threat Management(UTM), Policy Routing, SSL Proxy)  |
{: caption="Threat detection architecture decisions" caption-side="bottom"}
