---

copyright:
  years: 2024
lastupdated: "2024-02-05"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Compute design
{: #compute-design}

{{site.data.keyword.ibm_cloud_sap}} on VMware uses SAP Certified infrastructure. The servers are available and offered in different profiles that define CPU and RAM combinations suitable and certified for SAP workloads.

SAP certifies only specific server profiles in {{site.data.keyword.Bluemix}}. It's critical that the appropriate profiles are chosen from the {{site.data.keyword.Bluemix_notm}} catalog. The range of SAP HANA certified profiles available on VMware on {{site.data.keyword.Bluemix_notm}} cover most customer use cases for the SAP HANA database service.

[{{site.data.keyword.Bluemix_notm}} vCenter Server](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) gives you maximum flexibility to build your own {{site.data.keyword.IBM}}-hosted environment that uses VMware-compatible hardware and the right set of VMware components that fit your business needs and expertise.

VMware® vCenter Server® is a hosted private cloud that delivers the VMware vSphere stack as a service. The VMware environment is built on a minimum of three {{site.data.keyword.baremetal_long}}, shared Endurance NFS storage, and it includes the automatic deployment and configuration of an easy to manage logical edge firewall that is powered by VMware NSX-T™. Also, add-on components can be selected for firewalls and resiliency.

New deployments of vCenter Server multizone instances are not supported.
{: note}

For a comprehensive list of VMware best practices, see [SAP HANA VMware best practices and reference architecture guide](https://core.vmware.com/resource/sap-hana-vmware-vsphere-best-practices-and-reference-architecture-guide){: external}.

## VMware compute deployment considerations
{: #deploy-considerations}

Review the VMware compute considerations for deploying {{site.data.keyword.ibm_cloud_sap}}.

SAP Application Performance Standard (SAPS) sizing considerations:

-   SAP provides a sizing tool to help customers determine the required SAPS for their SAP workloads. This information can be used to size the appropriate VMware hosts and ESXi clusters. For more information, see [Sizing process for SAP Systems](/docs/sap?topic=sap-sizing&interface=ui).
-   Each vCPU on a VMware ESXi host = \~1000 SAPS
-   Oversubscription in VMware refers to the method when more resources than are available on the physical host can be assigned to the virtual servers supported by that host.
    -   **For Netweaver**, host oversubscription is possible.
        -   Heavy workload: 1:1 – 2:1
        -   Medium workload: 4:1 – 8:1
        -   Light workload: 16:1
    -   **For HANA**: You can’t use oversubscription.
-   VMware overhead: VMware is a Type 2 hypervisor and therefore does have a small overhead of CPU/RAM that is used for running ESXi on the Bare Metal servers. This CPU/RAM overhead is then available for virtual machines to use. On average this overhead is 10%, and is expected by VMware-SAP in virtualized environments.  Factor it into the overall sizing calculations.

For additional information on sizing and VMWare overhead, see [Compute Profiles of SAP-certified VMware on Classic Infrastructure](/docs/sap?topic=sap-compute-os-design-considerations#compute-vmware).

VMware virtual SAP HANA sizing gets performed like the physically deployed SAP HANA systems. The major difference is that an SAP HANA workload needs to fit into the compute and RAM maximums of a VM and that the costs of virtualization (RAM and CPU costs of ESXi) need to get considered when planning an SAP HANA deployment. If an SAP HANA system exceeds the available resources (virtual or physical deployments), the VM can get moved to a new host with more memory or higher performing CPUs. After the migration to this new host, the VM must be shut down, and the VM configuration must be changed to reflect these modifications. If a single host is not able to satisfy the resource requirements of an SAP HANA VM, then scale-out deployments or SAP HANA extension nodes can be used.

Check out the following documentation for information about the variety of SAP certified server profiles for deployment of SAP NetWeaver and SAP HANA on VMware on {{site.data.keyword.Bluemix_notm}}.

* [NetWeaver VMware server profiles](/docs/sap?topic=sap-nw-iaas-offerings-profiles-vmware)

* [SAP HANA VMware server profiles](/docs/sap?topic=sap-hana-iaas-offerings-profiles-vmware)

### VMware® vCenter Server® cluster sizing
{: #sizing-instance-vcenter}

You can scale out or decrease the capacity of your VMware® vCenter Server® instance according to your business needs by adding [VMware ESXi servers](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers) that use the {{site.data.keyword.Bluemix_notm}} console. The new hosts and extra capacity are automatically added to the cluster.

VMware® vCenter Server® instances are deployed with a consolidated cluster for VMware vSphere® 7 in which all the VMware® management components and user workloads run. You can order a separate workload cluster or a gateway cluster, or both. For more information, see [Additional clusters (optional)](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters).

SAP HANA is an “in-memory” database so memory sizing must be considered. If an SAP HANA database size exceeds 12 TB of memory for VMs, or Bare Metal, PowerVS (with a range of profiles up to 22.5 TB) is the recommended landing zone and is covered in the [{{site.data.keyword.powerSys_notm}}](/docs/pattern-sap-on-powervs?topic=pattern-sap-on-powervs-overview) pattern.  Therefore, if the required memory for SAP HANA requires a {{site.data.keyword.powerSys_notm}} deployment, the application layer must also be on {{site.data.keyword.powerSys_notm}}, not VMware on {{site.data.keyword.Bluemix_notm}}.

Best practice for a distributed SAP installation is to have all nodes in the same location, for example, the same Availability Zone or Datacenter. Deviation from this setup can cause latency and timeouts, which can render an SAP system unresponsive. SAP does not support the application layer and database to be deployed across different locations and zones. The application and database layers must exist in the same availability zone.

Databases typically experience growth over time so database size and expected data growth rates should be considered when you plan database deployments.
{: tip}

## SAP AnyDB
{: #anydb-design}

Database is a customer choice, although S/4HANA requires the use of the HANA DB. AnyDB refers to any non-SAP HANA, SAP supported database. SAP supports: {{site.data.keyword.IBM}} Db2, Oracle, Microsoft SQL Server, SAP Max DB, SAP ASE on VMware in {{site.data.keyword.Bluemix_notm}}.

Deploying SAP AnyDB on {{site.data.keyword.Bluemix_notm}} is similar to infrastructure deployments in on-premises data centers. The information that is provided from SAP and the Relational data base management system providers can be used. The following links contain design considerations for each database:

* [IBM Db2](/docs/sap?topic=sap-anydb-ibm-db2)

* [Microsoft SQL Server](/docs/sap?topic=sap-anydb-ms-sql-server)

* [SAP Max DB](/docs/sap?topic=sap-anydb-sap-maxdb)

* [SAP ASE](/docs/sap?topic=sap-anydb-sap-ase)

In general, Oracle is not a recommended option for SAP on VMware in {{site.data.keyword.Bluemix_notm}} due to licensing issues that can be effectively cost handled by deploying SAP and Oracle in an {{site.data.keyword.powerSysFull}} SAP environment. In a VMware environment, multiple hosts are typically clustered together, enabling virtual machines to move freely between the hosts by vMotion, Distributed Resource Scheduler (DRS), VMware HA, and VMware Fault Tolerance. In a vSphere cluster, there are two distinct Oracle licensing scenarios to consider. In the first scenario, all the hosts in the cluster are fully licensed to run the Oracle product (fully licensed clusters). In the second scenario, only a subset of the hosts in the cluster are licensed for Oracle (partially licensed clusters). Licensing a partial subset of hosts might minimize the benefits of DRS, vMotion, and VMware HA. Also, licensing the entire SAP cluster or establishing a separate Oracle cluster can be cost prohibitive.
