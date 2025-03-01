Azure region --> area in a single Country where it's infrastructure can be deployed. Example: East US, West US, East US2, West US2.

Availability zones --> groups of data centers (same as AWS)
##### <span style="color: #689d6a">Azure Components</span>

- Azure Tenant --> represents a single organization and provides a unique identity within the Azure ecosystem. any new organization receives a domain that ends with: `.omicrosoft.com` A domain is associated with a tenant and can be customized
- Azure Active Directory --> dedicated directory that includes users, groups, and applications that all tenants get when they onboard to Azure. This directory is used to manage identity and access management functions for tenant resources.
	- One organization can create multiple Active Directories, but they don't have any link to each other --> it's isolated with other Active Directories
	- Management Groups --> allows to have a high level grouping (business units) in the organization. Allows to define policies, role based access control (RBAC).
		- Logical containers that you use for one or more subscriptions. You can define a hierarchy of management groups, subscriptions, resource groups, and resources to efficiently manage access, policies, and compliance through inheritance.
		- Management groups can be nested
		- Subscriptions --> A logical container for the resources. Each Azure resource is associated with only one subscription. Creating a subscription is the first step in adopting Azure. The billing happens at the subscription level. pay as you go model --> you only pay for the resources created under the subscription.
			- approaches: Only 1 sub for one project (small project), create multiple sub for a single project (big project). --> multiple according the environment: Example: Ecomm-dev, Ecomm-uat, Ecomm-prod.
- Resource Groups --> Logical containers that you use to group related resources in a subscription. Each resource can exist in only one resource group. Resource groups allow for more granular grouping within a subscription. They're commonly used to represent a collection of assets that are required to support a workload, application, or specific function within a subscription.
- Resources --> An entity that's managed by Azure. Examples include Azure Virtual Machines, virtual networks, and storage accounts.

Without a resource group, resources cant be deployed. 

The metadata of the resources will reside resource group region even if the resources are created in another region.

Tenant --> one Active Directory --> management group (default - root) --> subscriptions --> Resource Groups --> Resources 

Azure Resource Manager is the only layer in Azure which helps the user to do deployment. Deployments of any resources in Azure, has to be done via the Azure Resource Manager.
##### <span style="color: #689d6a">Azure Networking Components</span>

Azure Virtual Network --> service that provides the fundamental building block for your private network in Azure (just as the VPC on AWS)
An instance of the service (a virtual network) enables many types of Azure resources to securely communicate with each other, the internet, and on-premises networks.
allows to create a private network in Azure, provides isolation to resources, enables secure communication within network and with outside resources, handles the inbound and outbound traffic, connects to other Azure VNets and to on-prem networks
(10.0.0.0 - 10.0.0.255) --> range of the internal IP addresses for the network
whenever a resource is deployed, there will always be a private IP address that will be assigned to it --> It's network interface card that gets the private IP address.
public IP address are optional.

NIC --> allows VM to communicate with outside network

One virtual network can have up to 3000 subnets

firewall --> can only be assigned at the VNet level

Network Security Group (NSG) --> set of rules that helps to handle the inbound and outbound traffic (just like Security Groups on AWS).
- can be assigned at the subnet level or at the NIC (VM) level (allows to have more control, but creates maintenance issues)
- NSG at subnet level but not at VM level (controlling traffic for all VMs, no maintenance issues)

Azure Load Balancing options: Azure Load Balancer,  Azure Application Gateway, Azure Traffic Manager, Azure Front Door

3-tier architecture
##### <span style="color: #689d6a">Azure Virtual Machines</span>

Multiple NICs (Network Interface Card) can be assigned to a VM.