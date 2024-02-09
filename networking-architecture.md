---

copyright:
  years: 2024
lastupdated: "2024-02-05"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for networking
{: #networking-architecture}

The following table summarizes the network architecture decisions for SAP on {{site.data.keyword.Bluemix_notm}} VMware® vCenter Server®.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| From Cloud to enterprise                                   | The connectivity that's needed between client and {{site.data.keyword.Bluemix_notm}}                                                                           | Redundant {{site.data.keyword.dl_full_notm}} Connect Connections                                                                                      | Preferred depending on the security requirements. Lower cost than {{site.data.keyword..dl_short}} Dedicated                                                                                                                            |
| From Managed Service Providers (MSPs)                       | Secure and encrypted connectivity between MSPs and {{site.data.keyword.Bluemix_notm}}                                                                  | Site to site VPN that uses {{site.data.keyword.vsrx_full}} firewall as the Cloud VPN termination point                                                    | Private and encrypted network connectivity for managed services                                                                                                                                                   |
| Bring Your own IP (BYOIP) and Edge Gateway                                         | The capability that's needed for a customer to provide isolation, security, and edge routing services                                    | {{site.data.keyword.vsrx_full}} with content security bundle                                                                            | Required to control traffic and VPN connections. Provides the first layer of defense and enable higher performance for NSX-T™ but carrying key functions on a dedicated device. North South Traffic (Underlay) |
| Network segmentation and isolation                             | The ability to provide network isolation across workloads                                                                      | {{site.data.keyword.vsrx_full}} \n NSX-T™                                                                                                   | {{site.data.keyword.vsrx_full}} can provide isolation of the underlay network NSX-T™ provides segmentation and isolation of the overlay network                                                                                    |
| Cloud-native connectivity (to cloud services)              | Ability to connect to cloud services over the private network                                                              | Cloud service endpoints | Communicate with {{site.data.keyword.Bluemix_notm}} services over the private network by using private endpoint                                                                                                                            |
| Cloud landing-zone connectivity classic to VPC or PowerVS | If needed to connect to non-SAP workloads that are running in {{site.data.keyword.Bluemix_notm}} VPC, other regions or PowerVS                               | {{site.data.keyword.tg_full_notm}}(TGW) \n Global Transit Gateway(TGW)                                                                                    | Use TGW to connect separate VPCs (Edge or workload) and Classic (if needed). Global transit gateway to connect to environments in other regions for resiliency data replication purposes.                        |
| Load balancing (Public)                                    | Load balancing over the public network across two regions if an outage (DR) for failover to the other region. | {{site.data.keyword.cis_short}}                                                                                                   | Public load balancing for resiliency needs as described in the SAP best practices. CIS also provides DDoS services.                                                                                                         |
| Load Balancing (Private)                                   | Load balancing workloads across multiple workload instances over the private network                                       | SAP Web Dispatcher \n NSX-T™                                                                                                       | SAP Web Dispatcher forwards incoming HTTP and HTTPS requests to SAP application servers. NSX-T™ can load balance VMware inter-application server requests across hosts.                                     |
| Domain Name System (DNS)                                   | Ability to resolve DNS names on site                                                                                       | IBM continues to forward the DNS to client DNS Servers onsite                                                        | Service necessary to manage network changes associated with vHOSTNAME in highly available deployments.                                                                                                         |
{: caption="Table 1. Architecture decisions for network" caption-side="bottom"}
