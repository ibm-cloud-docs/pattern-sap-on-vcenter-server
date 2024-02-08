---

copyright:
  years: 2024
lastupdated: "2024-02-06"

subcollection: pattern-sap-on-vcenter-server

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Security design
{: #security-design}

Apply security at all layers of the solution for in-depth defense that depend on the requirements. For example, at the network edge, vLANs, vxLANs, at every compute instance, and at the application and database layers. In addition, protect data both in transit and at rest according to data classification. Controls eliminate the need for direct access to the environment. When direct access is needed, monitor and log all access.

It's a best practice to isolate, secure, manage, and monitor all ingress and egress traffic to the environment and to centralize these functions. It’s recommended that security and isolation are established by using a combination of the {{site.data.keyword.vsrx_full}} firewall and workload isolation by using NSX-T™. This is in addition to the cloud account-level protection provided in {{site.data.keyword.iamshort}}.

Implementation of firewalls at the network edge can secure and route public traffic to the {{site.data.keyword.Bluemix_notm}} environment and over the private customer network.

Each of the vxLANs in the VMware network design should be isolated by implementing rulesets to allow only the required traffic to specific cloud and VMware resources.

Enable logging to facilitate the firewall activity analysis if needed to meet security intrusion prevention and intrusion detection requirements.

Any traffic, public and private, should route through the network edge {{site.data.keyword.vsrx_full}} for routing, isolation, and logging.

To restrict, log, and monitor administrative access to the environment, a bastion host is recommended on a private VLAN for all administrative access. In addition, all bastion access and activity should be logged and monitored through Privileged Access Management (PAM) services.

Security is a shared responsibility between the cloud provider and customer at both the infrastructure and application layers.
