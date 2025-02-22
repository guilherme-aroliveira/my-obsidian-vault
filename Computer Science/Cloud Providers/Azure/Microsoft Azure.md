Azure region --> area in a single Country where it's infrastructure can be deployed. Example: East US, West US, East US2, West US2.

Availability zones --> groups of data centers (same as AWS)

Azure Components
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

Tenant --> one Active Directory --> management group (default - root) --> subscriptions --> Resource Groups --> Resources 

Azure Networking Components

Azure Virtual Machines