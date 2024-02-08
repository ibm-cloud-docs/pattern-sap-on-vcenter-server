---

copyright:
  years: 2024
lastupdated: "2024-02-05"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment. When you are planning your network design, consider enterprise connectivity, latency, throughput, resiliency, and security requirements.

When you deploy SAP to VMware® vCenter Server® on {{site.data.keyword.Bluemix_notm}}, keep in mind a few key networking considerations:

- Network bandwidth: SAP applications can be very demanding in terms of network bandwidth, so it's important to make sure that you have sufficient bandwidth that is allocated to your SAP environment. {{site.data.keyword.Bluemix_notm}} offers various networking options, including {{site.data.keyword.dl_full_notm}}, which provides up to 10 GB of bandwidth between {{site.data.keyword.Bluemix_notm}} and your existing data center.
- Network security: SAP applications often contain sensitive data. It is important to make sure that your SAP environments are secure and properly isolated. As a security best practice, isolate production from nonproduction workloads. It’s also a best practice to isolate by application tiers, for example, separating application from database. {{site.data.keyword.Bluemix_notm}} and VMware® vCenter Server®(VCS) on {{site.data.keyword.Bluemix_notm}} enables the creation of logically isolated environments and application tiers. {{site.data.keyword.Bluemix_notm}} that uses vCenter Server offers various security features, including next generation firewalls, network segmentation, intrusion detection and prevention capability, and encryption. Use a layered security approach to provide isolation and segmentation between your SAP environments and your application tiers by using add-on firewalls and [NSX-T](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design) included in the vCenter Server offering.

In addition to the general networking considerations, there are a few VMware specific networking tools for SAP deployments on VMware on {{site.data.keyword.Bluemix_notm}}:

- VMware NSX-T: VMware NSX-T provides network virtualization that is used to isolate, create, and manage networks for SAP applications on VMware. It's used to provide network isolation and segmentation through the creation of vxLANs on the overlay network. {{site.data.keyword.Bluemix_notm}} for VMware® vCenter Server® includes VMware NSX-T.
- VMware HCX: VMware HCX can be used to provide a migration solution that can be used to migrate SAP applications from on-premises to {{site.data.keyword.Bluemix_notm}}.

## VMware networking
{: #networking-design}

A VMware® vCenter Server® on {{site.data.keyword.Bluemix_notm}} deployment uses both an Underlay and Overlay network.

### Underlay network
{: #networking-underlay}

Separating different types of traffic is required to provide security isolation and to reduce contention and latency. VLANs are used to segment physical network functions. vCenter Server uses three VLANs. Two for private traffic and one for public network traffic.

| VLAN | Designation | Traffic type                              |
|----------|-----------------|-----------------------------------------------|
| VLAN1    | Public          | Available for internet ingress and egress traffic |
| VLAN2    | Private A       | ESXi host management and vxLAN                |
| VLAN3    | Private B       | Storage and vMotion                           |
{: caption="Table 1. VMware vCenter Server on {{site.data.keyword.Bluemix_notm}} VLANs" caption-side="bottom"}

### Overlay network
{: #networking-overlay}

The overlay is the VMware network specific to the VMware deployment implemented by NSX-T. It's up to the customer to design the network overlay based on their micro-segmentation, vxLAN, and isolation requirements. The {{site.data.keyword.Bluemix_notm}} vCenter Server automation deploys an example topology by following the model that is illustrated in Figure 1. This topology includes single Tier-0 and Tier-1 gateways and a few NSX-T overlay segments as a starting point.

Figure 1 illustrates a baseline VCS network deployment.

-   VMware is deployed with both public and private connectivity or only private connectivity based on the network preference selection. 
-   The vCenter Server instance can be deployed with various SAP certified {{site.data.keyword.baremetal_short}} hardware options. Initial deployment includes one consolidated cluster or separate management and workload clusters. The solution can be expanded after the initial deployment by adding more SAP Certified hosts to existing clusters, or by adding new clusters.
-   Clusters can have multiple datastores. {{site.data.keyword.filestorage_full_notm}} (NFS), can have one or more LUNs with different performance and size characteristics. Volumes can be expanded as needed.
-   The automation deploys a vCenter Server appliance on the management or consolidated cluster. vCenter Server has an IP address from the {{site.data.keyword.Bluemix_notm}} classic infrastructure provided 10/8 address space.
-   The automation deploys three VMware NSX-T managers and a cluster is formed which uses NSX-T virtual IP for high availability (HA). NSX-T managers have an IP address from the {{site.data.keyword.Bluemix_notm}} classic infrastructure provided 10/8 address space.
-   The automation deploys an active directory for authentication and name resolution. Select between a single Windows virtual server instance in {{site.data.keyword.Bluemix_notm}} IaaS hypervisor or two highly available dedicated Windows server VMs (with bring your own license) on the VMware management cluster.
-   The automation deploys four edge nodes in the deployment and forms two NSX-T edge clusters; the services edge cluster and workload edge cluster.
-   The services edge cluster is used to host services in the Tier-0 Gateway, which provides network connectivity services for the management components.
-   The workload edge cluster hosts the workload Tier-0 and Tier-1 Gateways. A predefined example overlay network topology with one Tier-1 Gateway is provided by the automation. It can be customized to meet requirements by changing or deleting example segments or by adding new segments to separate the SAP application tier from the database tier.

![A diagram of a computer description that's automatically generated](./sap-on-vmware-network.svg){: caption="Figure 1: Baseline vCenter Server architecture diagram" caption-side="bottom"}

For detailed explanations of VMware Network deployment options, see [Architecture patterns for the vCenter Server deployment default connectivity options](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-nsx-t-topology-overview).

For a list of all the networking considerations, see [Network design considerations](/docs/sap?topic=sap-networking-design-considerations).
{: #note}
