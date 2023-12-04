# Infrastructure

## AWS Zones
1] us-east-2
2] us-west-1

## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Web Servers | Host web application | t3.micro | 3 | Auto-scaling across zones |

| Database (RDS - Aurora) | Store application data | db.t3.small | 2 | Multi-AZ deployment for failover |

| Load Balancer (ELB) | Distribute incoming traffic | Standard | 1 | Configured across zones |

| Monitoring and Logging | Monitor infrastructure | Standard | 2 | Redundant setup |



### Descriptions
Descriptions
### 1]Web Servers:

Purpose: Hosts the web application. The web servers are responsible for handling incoming HTTP requests and serving the application content.
Size: t3.micro
Qty: 3
DR: The web servers are configured for auto-scaling across availability zones to ensure fault tolerance and handle variable traffic loads. They are stateless, allowing for easy replication.

### 2] Database (RDS - Aurora):

Purpose: Stores application data. The RDS Aurora database is a managed relational database service optimized for high availability and fault tolerance.
Size: db.t3.small
Qty: 2
DR: The database is set up in a Multi-AZ deployment configuration, ensuring automatic failover to a standby instance in case of a primary instance failure. Regular database backups are configured to Amazon S3 for data durability.

### 3] Load Balancer (ELB):

Purpose: Distributes incoming traffic. The Elastic Load Balancer (ELB) evenly distributes incoming application traffic across multiple web servers to ensure availability and prevent overloading of any single server.
Size: Standard
Qty: 1
DR: The load balancer is configured to distribute traffic across multiple availability zones, providing load balancing and failover support. Health checks are configured to monitor the status of backend instances.

### 4] Monitoring and Logging:

Purpose: Monitors infrastructure health and logs events. Monitoring and logging systems are crucial for identifying issues, analyzing performance, and maintaining visibility into the health of the entire infrastructure.
Size: Standard
Qty: 2
DR: Two redundant monitoring and logging systems are set up to ensure continuous monitoring. This redundancy helps in maintaining operational visibility even in the event of a failure in one of the systems.


## DR Plan
### Pre-Steps:
- Identify target AWS region.
- Load balancer endpoints of DB and servers.

## Steps:

1] Trigger failover in the primary region's database cluster.
2] Update application configurations to point to the secondary region's database.
3] Scale up the number of web server instances based on demand
4] Update DNS records to point to the new region's load balancer.
5] Activate redundant monitoring systems in the new region.
6] Verify the logs and metrics are streaming correctly.