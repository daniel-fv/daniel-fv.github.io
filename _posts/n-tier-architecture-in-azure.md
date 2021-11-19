https://www.linkedin.com/post/edit/6679756946112843776/

With over hundreds of Azure services, sometimes it can be difficult to choose the appropriate service for the right task. Should we go with the Infrastructure as a Service (IaaS) route or should we implement Platform as a Service (PaaS) in Azure? When building applications, should we go the with the traditional N-tier architecture or could we build it using the more recently popular microservices architecture?

Fortunately, Microsoft has published an architecture style guide in the Azure Architecture Center that can help us in selection the most appropriate Azure service depending on what we are trying to accomplish. I will try to summarize when to use each according to the architecture style.

The architectures I will cover below are:

N-tier
Microservices
Web-queue-worker
Event-Driven
Big Compute
Big data
1- N-tier architecture
N-tier divides an application into layers. Practically IaaS, this style can be implemented using traditional Virtual Machines (VMs) or as PaaS for some of the tiers.

Example of a N-tier application
Running simple website applications like a CRM, ERP or a Wordpress site could be implemented using this architecture. It provides the benefit of migrating on-premises infraestructure to Azure easily with minimal refactoring.








Add alt text
No alt text provided for this image
Each layer is physically separated according to the services it provides. Each of these tiers is running two or more Virtual Machines in a scale set or availabiltiy set in Azure. This helps with scalability (in case we need to add more VMs if demand increases) and with resiliency (in case a VM fails for some reason) helping us achieve high availability for the application and also helps with security (as we should only allow access to a lower layer from a higher layer and not expose inner layers to the internet).

Components of N-tier architecture
Load Balancer - to split the traffic between VMs in each tier.
Network Virtual Appliance (NVA) - Firewall application running in a VM like Sophos XG Firewall using the Web Application Firewall (WAF) feature.
Web tier - VMs running Apache, nginx or Microsoft IIS web servers.
Business tier (optional) - depending on the application, we may need this middle tier to perform additional actions before we serve data to the end user or use it as some type of cache for the data.
Data tier - we need to choose a database that supports replication to achieve the high availability of running multiple VMs. For example, Microsoft SQL Server, Apache Cassandra (NoSQL), MySQL or MariaDB running replication or in a cluster.
Jump box - VM on the network used for us to log in from the internet to our infraestructure and from there log in to our other VMs. We should only allow management traffic to our internal VMs from this jump box.
Azure services used in a N-tier architecture
Because mostly we will be running IaaS, we will use Azure Virtual Machines to run the OS and install on our own the required software (web server, database, etc), not many other Azure services will be used essentially besides a load balancer.

Azure Virtual Machines running Linux or Windows.
Load Balancer - We could use the following as load balancers: Azure Front Door, Traffic Manager, Application Gateway, Azure Load Balancer. Comparison of Azure load balancers for more information.
PaaS alternatives for N-tier architecture
We could replace many of the tiers with PaaS managed solutions in Azure and it could help us to manage more easily the application. This saves us time and resources as we no longer would need to manage individual VMs, keeping their OS updated, or doing any maintanance on the individual instances.

Instead of using VMs, we can use some of these Azure services for these specific functions of the architecture:

Web Application Firewall - instead of running our own NVA inside a VM we could use the following services as WAF: Azure Application Gateway, Azure Front Door, and Azure Content Delivery Network (CDN). With some of these we could also take advantage of combining the load balancer with a WAF. Note: Azure Firewall is a basic firewall service that doesn't provide protection against web exploits and vulnerabilities, so it is not recommended to use it for that purpose.
Web servers could be replaced with Azure Web Apps. As it is a managed service, we do not need to worry about load balancers and scalability, the service will load balance automatically and we can increase or decrease instances if the demand requires it. No need to worry about configuring web servers. The service supports web apps running .NET, Node.js, PHP, Python or Ruby.
Databases - VMs running Microsoft SQL Server, MySQL or MariaDB can be replaced with managed versions in Azure: Azure SQL, Azure Database for MySQL or Azure Database for MariaDB. We would not need to worry about setting up replication or clusters as these services provide high availability by default with a 99.99% SLA.
2- Microservices architecture


