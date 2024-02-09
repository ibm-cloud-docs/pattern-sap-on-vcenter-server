---

copyright:
  years: 2024
lastupdated: "2024-01-31"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}

The objective of this pattern is to provide an {{site.data.keyword.IBM}} solution design for the deployment of SAP to VMware® vCenter Server®(VCS) on {{site.data.keyword.Bluemix_short}} to:

-   Accelerate and simplify solution design by providing a standard {{site.data.keyword.Bluemix_notm}} deployment architecture reference solution for SAP on VMware in {{site.data.keyword.Bluemix_notm}} following the [IBM Architecture Framework](/docs/architecture-framework?topic=architecture-framework-intro).
-   Provide a prescriptive, end to end enterprise-class solution design. The design includes diagrams, component architecture decisions, and rationale for cloud component selection for a secure, resilient SAP on VMware in {{site.data.keyword.Bluemix_notm}}.
-   Ensure requirements are met from performance, system availability, and security perspectives.

This document does not cover SAP configuration and SAP component deployment scenarios. It is limited to vCenter Server (VCS) on {{site.data.keyword.Bluemix_notm}} infrastructure options that support SAP workload deployment.

It supports the deployment of SAP Business Applications Running on SAP NetWeaver, SAP HANA or SAP AnyDB, and other SAP products using other technologies such as SAP Content Server, or newer applications such as SAP Data Intelligence.

The strong partnership between VMware, {{site.data.keyword.IBM}}, and SAP enables customers to operate their SAP workload in {{site.data.keyword.Bluemix_notm}} on VMware in a fully certified and dedicated environment which is a unique offering in {{site.data.keyword.Bluemix_notm}}.

## Benefits of SAP-Certified Infrastructure
{: #benefits-SAP}

{{site.data.keyword.Bluemix_notm}} SAP-Certified Infrastructure provides the flexibility to run SAP workloads in the {{site.data.keyword.Bluemix_notm}} and the ability to quickly address issues such as:

-   Moving SAP workloads to the cloud
-   Rapidly expanding or contracting capacity
-   Supplementing an existing private cloud architecture

Enterprise-class, mission critical workloads need to be resilient and provide High Availability (HA) and Disaster Recovery (DR) capabilities. This pattern can be used as a guide to meet typical customer requirements and provide a base reference solution for a secure and resilient SAP NetWeaver and SAP HANA or SAP NetWeaver and SAP AnyDB deployment to vCenter Server (VCS) on {{site.data.keyword.Bluemix_notm}}. It illustrates a single-zone, multi-region design which can provide both HA and DR to meet typical customer requirements.

The simplest variation of this pattern assumes that the customer is moving existing SAP workloads to vCenter Server (VCS) on {{site.data.keyword.Bluemix_notm}}. The move could be due to one of the following examples:

-   A new VMware setup on {{site.data.keyword.Bluemix_notm}}
-   Migration of existing primary and/or secondary VMware workloads from on-premise or other locations to vCenter Server (VCS) on {{site.data.keyword.Bluemix_notm}}
-   An extension of customers on premise VMware and SAP installation for DR purposes

The {{site.data.keyword.Bluemix_notm}} for VMware offerings enable existing VMware virtualized datacenter clients running SAP to house their SAP workloads on {{site.data.keyword.Bluemix_notm}}. This permits use cases like capacity expansion and contraction into the cloud, migration to the cloud, DR, backup, and the ability to stand up a dedicated cloud environment for development, testing, or production.

## Understanding the design 
{: #design-SAP}

This design serves as a baseline architecture providing the foundation for other internal or vendor specific components to be added in as required by specific use cases.

There are two variations of VMware available from {{site.data.keyword.Bluemix_notm}} that support SAP: build your own VMware vSphere (VSS) or use an automated build and configuration Virtual Center Server (VCS) according to VMware best practices. For more information, see:

-  [VMware vSphere (VSS)](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview) manual to build your own {{site.data.keyword.IBM}}-hosted VMware environment by customizing and ordering the VMware-compatible hardware based on your selected VMware components.
-   [vCenter Server](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) (VCS) is a dedicated, fully automated VMware Software Defined Data Center setup and configuration, which includes optional BYOL, configuration of different VMware components (such as VMware NSX, VMware Aria Operations, Aria Operations for Logs, Aria Operations for Networks) and access to advanced VMware capabilities (such as VMware HCX)

The target landing zone for the workloads for this pattern is a {{site.data.keyword.Bluemix_notm}} for VMware vCenter Server(VCS), single zone instance deployed in two regions to support resiliency requirements.

This solution pattern does not include automated DR orchestration. A more complete resiliency solution depends on the actual customer requirements, application design, and incident management service level agreements, and is out of the scope for this document.
{: note}

Global System Integrator (GSI) or Managed Service Provider (MSP) services can be optionally added to build and manage the cloud environment or SAP application and associated “bolt-ons” deployed on the VMware cluster.

<!--This pattern documents the target VMware environment for SAP deployment and the architecture decisions made to meet specific customer requirements. For more information on how to select the best fit components to meet other customer requirements see the VMware Pattern Architecture assets (WIP by Dwarka) noted in the references section. -->

The following documentation in this guide provides architecture, design considerations, and guidance for deploying the infrastructure to support SAP workloads, including:

-   SAP Business Applications such as SAP S/4HANA or SAP BW/4 HANA
-   SAP Technical Applications such SAP HANA database server and SAP NetWeaver application server
