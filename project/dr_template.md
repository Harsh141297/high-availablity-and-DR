# Infrastructure

## AWS Zones
1] Primary Region: us-east-2
2] Secondary Region: us-west-1

## Servers and Clusters

### Table 1.1 Summary
| Asset                         | Purpose                           | Size         | Qty | DR                                                     |
|-------------------------------|-----------------------------------|--------------|-----|--------------------------------------------------------|
| Web Servers (EC2)              | Host web application              | t3.micro      | 3   | Auto-scaling across regions                            |
| Database (RDS - Aurora)        | Store application data            | db.t3.small   | 2   | Multi-AZ deployment for failover (primary and secondary in two different regions) |
| Load Balancer (ELB)            | Distribute incoming traffic       | Standard     | 1   | Configured across regions                               |
| Monitoring and Logging         | Monitor infrastructure            | Standard     | 2   | Redundant setup                                        |
| Elastic Kubernetes Cluster     | Managed Kubernetes Cluster        | Standard     | 2   | Primary and secondary in two different regions          |
| VPC                           | Private network                    | Standard     | 2   | Primary and secondary in two different regions          |

### Descriptions

1] Web Servers:
Purpose: Hosts the web application. The web servers are responsible for handling incoming HTTP requests and serving the application content.
Size: t3.micro
Qty: 3
DR: The web servers are configured for auto-scaling across availability zones to ensure fault tolerance and handle variable traffic loads. They are stateless, allowing for easy replication.

2] Database (RDS - Aurora):
Purpose: Stores application data. The RDS Aurora database is a managed relational database service optimized for high availability and fault tolerance.
Size: db.t3.small
Qty: 2
DR: The database is set up in a Multi-AZ deployment configuration, ensuring automatic failover to a standby instance in case of a primary instance failure. Regular database backups are configured to Amazon S3 for data durability.

3] Load Balancer (ELB):
Purpose: Distributes incoming traffic. The Elastic Load Balancer (ELB) evenly distributes incoming application traffic across multiple web servers to ensure availability and prevent overloading of any single server.
Size: Standard
Qty: 1
DR: The load balancer is configured to distribute traffic across multiple availability zones, providing load balancing and failover support. Health checks are configured to monitor the status of backend instances.

4] Monitoring and Logging:
Purpose: Monitors infrastructure health and logs events. Monitoring and logging systems are crucial for identifying issues, analyzing performance, and maintaining visibility into the health of the entire infrastructure.
Size: Standard
Qty: 2
DR: Two redundant monitoring and logging systems are set up to ensure continuous monitoring. This redundancy helps in maintaining operational visibility even in the event of a failure in one of the systems.

5] Elastic Kubernetes Cluster:
Purpose: Managed Kubernetes Cluster.
Size: Standard
Qty: 2
DR: Primary and secondary clusters are established in two different regions to ensure high availability and fault tolerance.

6] VPC:
Purpose: Private network.
Size: Standard
Qty: 2
DR: Primary and secondary VPCs are established in two different regions to ensure a private and isolated network infrastructure.

### DR Plan
#### Pre-Steps:
Identify the target AWS region.
Document load balancer endpoints of the database and web servers.

#### Steps:
Trigger failover in the primary region's database cluster.
Update application configurations to point to the secondary region's database.
Scale up the number of web server instances based on demand.
Update DNS records to point to the new region's load balancer.
Activate redundant monitoring systems in the new region.
Verify the logs and metrics are streaming correctly.
