Zones --> data centers isolados de uma mesma região, sendo que cada região possui três zonas (zones). 

>[!note]
>A escolha da região vai depender da aplicação e geografia na qual será utilizada para o deploy da aplicação.

Há tipos de infra estrutura que estão disponíveis em cada uma da regiões. Not all the regions are identical within a region, not all the zones are identical. There are some differences even if the region is the same.

A VPC network is a global resource, but individual subnets are regional resources. Example: A single VPC can be created and it can have 2 subnets which are in two different regions, for example, one in Brazil and other in Portugal. 

>[!info]
>The network that connects all its data center is really fast, and the latency of cross data centers is very low.

App Engine --> platform mas a service, it ha 2 flavors: the standard edition and the app engine flexible 
- standard --> powered internally by a proprietary tech (container based). Can drop down to zero instances.
- flexible --> powered by infrastructure as a service (internally it uses dedicated compute resources). Its like a kubernetes control engine minus the control plane. It always maintain at least 1 instance in the infrastructure. 

Cloud Functions --> serverless, unit of work, could be an upload of a document

Knative --> 

Cloud Bigtable --> fully manage NoSQL database that supports the popular open-source Apache HBase 1.0 API.

Datastore (Cloud Firestore) --> like MongoDB, like documents and collections of documents. 

Firestore

Compute Egine
network tags is the equivalent of securitu groups en AWS

Intance Groups --> like an autoscaling group
if differentes subnets are created, it needs to have different intances groups  
Ex: In a region with 4 subnets which each have an intance, it needs to have 4 instance groups.
With Autoscaling off it just maitains the numbers of intances defined --> it's ok for a fixed incoming requests per second 
core principle  --> create a group of identical VM instances.
