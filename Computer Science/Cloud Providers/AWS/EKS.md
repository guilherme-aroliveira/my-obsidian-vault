AWS EKS --> Amazon Elastic Container Service for Kubernetes is a highly available, scalable and secure Kubernetes Service.

Kubernetes can run on any public cloud providers (or even on-premises)

AWS EKS providers managed Kubernetes master nodes
the master nodes are multi-AZ to provide redundancy
the master nodes will scale automatically when necessary

O cluster de EKS (Kubernetes) necessita que pelo menos duas subnets sejram criadas em diferentes zonas de disponibilidades (availability zones) --> para obter alta disponibilidades.

with any managed service, master nodes can't be created. The master nodes do not host any application or workloads. it can't ssh or access them, because in managed Kubernetes services, the master node are maintained by the service provider. 

>[!note]
>O ideal para qualquer projeto que envolve Alta Disponibilidade é que tenha  3 AZs (Availabilit Azones) --> mais de um ponto de falha

Cada Pod dentro do cluster de kubernetes na AWS irá consumir um endereço IP. Então é interessante colocar um range maior em cada subnet. 

O cluster de EKS terá um apontamento para as subnet publicas, para que se possa criar um endpoint de acesso externo.

A subnet privada será utilizada para rodar os managed node groups (worker nodes) --> EC2 que contem os Pods do cluster de kubernetes.

Se o controle de ingress para Kubernetes da AWS for utilizado, ele irá identificar quais  são as subnets publicas e privadas para criar os load balancer publicos e privados, baseados nas tags: `kubernetes.io/role/internal-elb` -> para private subnets e `kubernetes.io/role/elb` -> para subnets publicas.

As subnets devem ser padronidazas com tags especificas para o cluster de kubernetes --> veja documentação da AWS.

Uma IAM role deve ser criada para fornecer permissões que o cluster de Kubernetes necessita. É a policy que fornece a permissão, sendo atrelada a uma role --> Amazon Kluter Policy. Deve ser cirada um role atrelada à essa policy.
Managed Policy são policies padrão da AWS.

AWS EKS - setup
- Step 1: Provision an EKS Cluster
	- EKS Cluster
	- IAM Roles
	- Security Groups
	- VPC
- Step 2: Deploy worker nodes
	- Launch Configuration
	- Auto Scaling Group
	- IAM Roles
	- Security Groups
- Setup 3: Connect to EKS
	- ~/.kube/config
	- ConfigMap
	- kubectl
	- Heptio auth


Criação do cluter de EKS
pre-requisits:
- eks cluster role
- iam role for node group
- vpc
- ec2 key pair key which can be used to ssh to the worker nodes

seleciona a vpc
seleciona as subnets publica --> para endpoint publico
configura o cluster endpoint access como publico e privado --> requisição externa. retorna um IP publico, e requisição dentro da VPC retorna um IP privado.
seleciona os logs do control plane
add-ons --> Amaon VPC CNI --> implementa a parte de rede dos Pods
CoreDNS --> resolve buscas DNS dentro do cluster
kube-proxy --> cria as regras de IPtables

`nc -v <api server endpoint> 443`

`aws eks update-kubeconfig --region us-east-1 --name <cluster_name>` -> --> adiciona um novo contexto

`kubectl config use-context <context>` --> altera para um novo contexto


criar um role com as seguintes policies: `AamazonEKSWorkerNodePolicy`, `AmazomnEC2ContainerRegistryReadOnly` --> para que seja feito o pull das imagens do ECR, e a `AmazonEKS_CNI_Policy` --> para realizar as configurações da interfaces de rede.

Criar um manage node group para adicionar o node ao cluster. Adiciona um nome e as roles para o node
aba compute --> Node groups --> Add node group 
seleciona as AMI Linux --> tipo de instancia --> scaling configuration --> select private subnets --> configure ssh

OIDC Provider --> é utilizado para trazer um funcionalidade dentro do cluster chamada de IAM role for service account --> há uma serviço account de um pod, e é possível restringir o acesso desse pod com a role do IAM.
Todas as aplicaçõas que rodam nbo EKS precisam de OIDC pata ter acesso de IAM role.

AWS Load Balancer Controller --> utilizado para a criação dos ingress do cluster de kubernetes.

aws eks --region us-west-2 update-kubeconfig --name example-voting-app
kubectl get nodes
access the application using the load balancer IP address

aws sts get-caller-identity