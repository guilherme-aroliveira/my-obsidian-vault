VPC isolates the instances on a network level, It's like a private network in the cloud.

EC2-Classic --> is basically one big network where all AWS customers could launch their instances in

For smaller to medium steps, one VPC (per region) will be suitable. 

AN instance launched in one VPC can never communicate with an instance in another VPC using their private IP addresses. 

Private Subnets (Private IP Addresses) can'þ be used on the internet, They are only to be used privately within a VPC or in a home network or office netwoek. There are only a few privae subnets. Ex: `10.0.0.0/8`, `172.16.0.0/16` (range that Amazon buy default uses), `192.168.0.0/16`. 
/24 irá apenas suportar 256 hosts.
é a aprtir od enredeço da vpc que serão criadas as subnets que irão segrerar o tráfego.
o ultimo octeto é reservado para rede

tenancy --> 

tags são utilizadas para identificar sobre qual projeto um determinado recurso pertence.


Instances started in subnet main-public-3 will have IP address `10.0.3.x`, and an instance launched in main-private -1 will have an IP address `10.0.0.4.x`. 

É a subnet que irá fornecer um endereço IP para a máquina criada. 

Cada resurco que estiver na subnet publica terá um endereço IP publico e é possivel acessar de qualquer lugar do mundo. A rota de uam subnet publcia irá para um subnet gatweay.

subnet publica geralmente irá rodar os load labancer (ALB e NLB) --> ponto de entrada do trafego publico.

Um subnet private que irá para o nat gateway (é criado na subnet publica) --> o nat gateway irá rotear para o internet gateway. Todos os recursos que estão na subnet privada terão um ip privada com endereço da vpc.

All public subnets are connecyted to an internet gateray. Thsese isntances will also have a publixc Ip address, alloing them to be reachavle from the internet.

intances in the subnets don't get a public Ip address, so they will not be reachable from teh internet --> they can have a NAT Gateway to that will allow to communicate outside.

Typically public subnets are used for intetnet-facing services/applications

Databases, caching services, and backends all go into the private subnets.

If  a Load Balancer (LB) is used, it will typically be puted in the public subnet and the instances and the instances serving an application in the private subnets.

`instance_tenancy` --> it means every instance that is launched will have the default tenancy. It can have multiple instances on one physical piece of hardware. 

`enable_dns_support` and `eable_dns_hostnames` --> only the intances gies an internal host name and domain name. 

A security group is a just like a firewall, managed by AWS.

Extra EBS storage volume --> extra volumes can be used for log files, anu real data that is put on the instance. That data will be persisted until AWS is instructed to rmove it. 

`user_data` --> can be used to do any customization at launch:
- extra software can be installed
- prepard the isntance t joina a cluster
- execute commands / scripts
- mount volumes
- is only executed at the creation of the instance

Private IP (static ip) will be auto-assinede to EC2 istances.  By pecifiyn the pirvate IP, this makes sure that EC2 instance will always have the same internal IP.
o que determina uma subnet ser publica ou privada são as rotas.


To use public ip address, just use EIPs (Elastic IP address). It's a public, static IP address than can eb attached to an instance.

Steps to create an RDS instance:
- create a subnet group --> allows to specifu in what subnet tah database will be in (e.g us-east01a)
- Create a Parameter group --> allows to psecifu parameters to change setggins in the database
- Create a securitu group that allows incoming traffic to the RS instance
- Create the RDS instance(s) itself

intergat geatway é um cpomonente de alta disponibilidade que permite um componente dentro da VPC possa comunicar com algo externo (ex: site do google) e receber trafego de entrada (Ex: um cliente consegue chegar por um IP publico atraǘes do internet gateway)

o internet gateway deve ser adicionado (attach) em uma vpc --> todo os componenetes dentro da vpc poderão utilizar o internet gwteway.

tobela de rotemanento definem as regras das rotas --> deve-se configurada uma roda de saída (Ex: nat gateway)

Para obter alta disponibilidade no nat gateway ele devera rodar em mais de uma subnet.
nat gaeway precisa de um ip elastico (Ip estático)

Elastic beandstalck is AWS platform as a swrvice solution. It's a platform where it can launch an app without having to maintain the underlying infrastructure. 
The user is still reponsible for the EC2 instance, but AWS will provide updates that the user can supply --> the update can be applied manually or automatically

Elastic beanstalk can hanlde application scaling, underlying it uses a lod balancer and an autoscaling grup to achieve it.
scaling evenrt can be scaheduled or enable autoscaling based on a metric. It'ß similar to Heroku.
The support plataform are: PHP, Java, .Net, NodeJS, Python, Ruby, Go an Docker

When an Elastic Beanstalsk environment is deployed it creates a CNAME (hostname that) that it can be used as endpoint.
Once Elastic Beanstalk  is running, the application can be deployed on it by using the EB Command line utility

>[!example] Example - AWS Beanstalk
>```hcl 
>resource "aws_elastic_beanstalk_application" "app" {
>  name = "app"
>  description = "prod"
>}
> 
>resource "aws_elastic_beanstalk_environment" "app_prod" {
>  name = "app-prod"
>  application = aws_elastic_beanstalk_application.app.name
>  solution_stack_name = ""
>  
>  setting {
>    namespace = "aws:ec2:vpc"
>    name = "VPCId"
>    value = var.vpc_id
>  }
>}
>```

There's a soft limit of number of ENIs that a user can have per region. 