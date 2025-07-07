---
copyright:
  years: 2024
lastupdated: "2024-09-23"
authors:
  - name: Esteban Arias

version: 1.0

subcollection: pattern-sap-on-vcenter-server

keywords:
---
{{site.data.keyword.attribute-definition-list}}

# Deploying SAP to VMware Cloud Foundation (VCF) for Classic on IBM Cloud
{: #sap-on-vcf}

This guide outlines deploying a target landing zone for the workloads for this pattern is a {{site.data.keyword.Bluemix_notm}} for VMware Cloud Foundation (VCF) for Classic, the design provides with a primary site and recovery site both deployed in different IBM Cloud regions and using a single zone.

This solution pattern does not include automated DR orchestration. A more complete resiliency solution depends on the actual customer requirements, application design, and incident management service level agreements, and is out of the scope for this document.

## Before you begin
{: #sap-on-vcf-prereqs}

You need the following items to deploy and configure this reference architecture:

* An [IBM Cloud account](https://cloud.ibm.com/registration).
* [Required IAM access policies](https://github.com/terraform-ibm-modules/terraform-ibm-web-app-mzr-da/tree/main/solutions/e2e#required-iam-access-policies).
* An [IBM Cloud API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui) for the user or service ID with the correct IAM access policies.
* Review [IBM Cloud general requirements](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts)
* Review [VCF automated instances requirements](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req).

## Provision Architecture
{: #provision-sap-on-vcf}

1. First time order requirements [VCF automated](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-completing_checklist)
2. Provision a primary instance [VCF automated](https://cloud.ibm.com/infrastructure/vmware-solutions/console/ordernew/dedicated/vcs_nsx_t), for software version information and hardware profiles review the Design considerations and architecture decisions section in this document. This primary instance uses the following specifications:
    - Automated VCF instance provision in one of the available regions (for instance Dallas, Washington DC, Montreal, Toronto, Sydney, London, Frankfurt, or Tokyo.)
    - Deploy separated workload clusters and gateway cluster along with a consolidated management cluster, notice that a minimum number of three bare metal servers is required for the consolidated management cluster and two for the workload and gateway clusters.
    - CPU models requirements for the clusters depend on customer specifications, it is recommended to use SAP-Certified hardware.
    - Select NFS storage according to the sizing requirements.
    - Networking type must public and private with uplink speed of 10 GB and new VLANs (except if specific requirements indicate otherwise)
    - vCenter (one applicance per region)
    - NSX Manager (one cluster per region)
    - VMware Aria Operations™ for Logs (One cluster per region and the use log forwarding/filtering between regions.)
    - VMware Aria Operations Manager
    - AD/DNS/NTP - HA VMs (Two highly available dedicated Windows Server VMs on the consolidated cluster)
    - Veeam (single Veeam Backup and Replication instance with a bare metal server in each region.) with default specifications.
    - Juniper vSRX with default specifications, this applicance will be hosted in the Gateway cluster
    - vSphere 8 is not supported for SAP-certified Cascade Lake servers.


3. Provision a secondary instance, there is parameter in the ordering form that allows for the selection of the primary instance [Secondary instance](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure). This secondary instance uses the following specifications:
    - Linked to the primary instance SSO site name
    - Same DNS domain as primary instance
    - DNS and AD replication setup between the AD virtual machines on the primary and secondary instances
    - VMware vCenter Server® on the secondary instances is set up with Enhanced Linked Mode (ELM) to the vCenter Server on the primary instance
    - Automated VCF instance provision in one of the available regions (for instance Dallas, Washington DC, Montreal, Toronto, Sydney, London, Frankfurt, or Tokyo.)
    - Deploy separated workload clusters and gateway cluster along with a consolidated management cluster, notice that a minimum number of three bare metal servers is required for the consolidated management cluster and two for the workload and gateway clusters.
    - CPU models requirements for the clusters depend on customer specifications, it is recommended to use SAP-Certified hardware.
    - Select NFS storage according to the sizing requirements.
    - Networking type must public and private with uplink speed of 10 GB and new VLANs (except if specific requirements indicate otherwise)
    - vCenter (one applicance per region)
    - NSX Manager (one cluster per region)
    - VMware Aria Operations™ for Logs (One cluster per region and the use log forwarding/filtering between regions.)
    - VMware Aria Operations Manager
    - AD/DNS/NTP - HA VMs (Two highly available dedicated Windows Server VMs on the consolidated cluster)
    - Veeam (single Veeam Backup and Replication instance with a bare metal server in each region.) with default specifications.
    - Juniper vSRX with default specifications, this applicance will be hosted in the Gateway cluster
    - vSphere 8 is not supported for SAP-certified Cascade Lake servers.

4. For steps two and three, the process starts automatically and users receive confirmation that the order is in progress, when the instance is ready status changes to Available. [Check Status](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure)

5. On VMware VCF for Classic automated instance in IBM Cloud workloads are deployed and run on a VMware NSX overlay network. NSX topology is deployed automatically and could be reused or customized as required. Notice that overlay networks are not advertized to IBM cloud classic infrastructure network. Networking operations require that a suitable tunnel is established between on prem / consumer devices and overlay workloads running in the cloud. The tunnel is established netween NSX T0 and customer routers through direct link. [IPsec over Direct Link with NSX](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-nsx-t-direct-link-ipsec)

6. Production workloads must be protected by appropiate disaster recovery plans and procedures, this architectural pattern uses use VMware Cloud Foundation for Classic Automated and Veeam® Backup and Recovery for VMware vSphere. [Detailed Veeam steps](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)

## Additonal Services
{: #additonal-sap-on-vcf}

You can add additional services onto the VMware Cloud Foundation (VCF) for Classic.  The addtional services include:

1. [Caveonix RiskForesight](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
2. [F5 Big-IP](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)
3. [FortiGate Virtual Appliance](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations)
4. [VMware HCX](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations)
5. [IBM Security Services for SAP](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-managing-ss-sap)
6. [Juniper vSRX](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview)
7. [KMIP for VMware](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations)
8. [Red Hat OpenShift for VMware](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview)
9. [Veeam](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
10. [VMware Arias Operations and Operations for Logs](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)
11. [Zerto](https://cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr)
