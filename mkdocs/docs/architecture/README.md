# Microservices Architecture

## Infrastructure Design
<a href="../img/microservices_infrastructure_design.png" target="_blank">
  <img src="../img/microservices_infrastructure_design.png" alt="Microservices Infrastructure Design">
</a>

## Infrastructure Resources

### Network/Transport

* **VPC**
> Development, Stage, and Production Environments will be in different VPCs since they don't need access to each environment's resources and for security purposes. AWS Organizations can be created for both production and non-production environments for additional security upon access and to efficiently monitor billing of resources.

* **Public Subnet**
> Resources placed in public subnet will be limited for security purposes.
Bastion host(jump server), elastic load balancer, and nat gateway will be in public subnet.

* **Private Subnet**
> Development, Stage, and Production EC2 instances, elasticache, and RDS instances will be in the private subnet since these resources do not need direct access and will be accessible only from bastion host.

* **Nat Gateway**
> This resource allows services to have outbound internet access without having the security of these services compromised by disabling inbound internet access.

* **Cloudfront**
> This resource wll be used in front of assets and static site not just to encapsulate URLs but also for secure data transfer since cloudfront can enable SSL connection and supports the use of WAF(Web Application Firewall), Geo Restriction, and AWS Shield to block attacks from hackers such as DDOS. Also since cloudfront has edge location globally, better performance should be expected.
*Note*: Cloudfront can also be used in front of ELB/ALB too for performance and security purposes although cloudfront has a history of downtimes, this is still a debatable approach in terms of reliability.

* **Elastic Load Balancer**
> Services will be accessible for ports 443/80 behind load balancer since services will be in private subnet yet require public access. Also ELB is beneficial on preventing DDOS attack and auto scaling of instances. The load balancer will be cross-zonal for high availability.

### Application

* **EKS**
