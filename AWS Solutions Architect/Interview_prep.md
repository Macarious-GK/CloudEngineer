# Networking (VPC)
## VPC
- We have IGW & Nat Gateway (has elastic IP)
- Public Subnets (VMs with public Ip & private IP)
- Private Subnets (VMs with private IP)

- Connection from VM-public to client
    - IGW used to translate the public accessed ip to the vm private IP
    - No direct connection between the VM and client
    - 2 way communication can be started

- Connection from VM-private to google
    - vm send request to nat gateway 
    - Nat do its magic and  replace source ip
    - nat use IGW to talk to google
    - and the connection goes back
    - Only one way connection, only the private vm can init the connect (security)
    - Nat keep a `mapping entry` to keep track of its connections

- Security Groups:
    - Allow rules only — everything else is implicitly denied.
- NACL:
    - Can explicitly allow or deny traffic


## NATing
- `SNAT` changes the ***source IP*** address of a packet as it leaves your network. (*MASQUERADE*)
- `DNAT` changes the ***destination IP*** address of a packet as it enters your network.

## Firewall stateful VS statless
- `Stateful`: When a connection is allowed through the firewall in either direction, return traffic matching session table is also allowed
    - ex: if allow tcp port 80, the response will be allowed even it not explicitly defined

- `Statless`: Does not track connection state. Each packet is evaluated independently based only on rules.
    - ex: if allow tcp port 80 the response will not be permitted unless an explicit defined incoming rule.

# Security In Cloud
- Secure network(sg, nacl, firewall rules)
- secure access (RBAC, Identity federation)
- Secure app secrets & Config (Secret Manager)
- Encryption in rest & Transient (KMS, AWS Certificate Manager)
- Logs/metircs (cloud Trail)


# Resilience VS Fault tolerance VS High Availability VS Reliability

***`Durability = Data does not get lost.`***

***`Reliability = system  perform its intended function correctly over time.`*** 

***`Resilience = system  recover quickly from failures and return to normal operation.`***

***`Scalability = System can grow when demand increases.`***

***`High availability = system recovers quickly from failures, but might have a brief disruption(Downtime).`***

***`Fault tolerance = Continuous operation under failure & Zero DownTime`***

--- 

| Concept               | Meaning (Simple)                 | AWS Example                |
| --------------------- | -------------------------------- | ---------------------------|
| **Durability**        | Data never gets lost             | S3                         |
| **Reliability**       | Works correctly over time        | Lambda                     |
| **Resilience**        | Recovers from failures           | Auto Scaling Group         |
| **Scalability**       | Grows with traffic               | DynamoDB                   |
| **High Availability** | Minimal downtime during failover | RDS Multi-AZ               |
| **Fault Tolerance**   | Zero downtime under failure      | S3, DynamoDB Global Tables |


# Observability
<div style="text-align: center;"><img src="./observability.png" alt="three-tier design" width="1000 " height="450" style="border-radius: 15px;"></div>  

# CloudWatch
- Collection of monitoring tools 
<div style="text-align: center;"><img src="./CloudWatch.png" alt="three-tier design" width="900 " height="350" style="border-radius: 15px;"></div>

- Logs, Metrics, Events, Alarms, Dashboards
- **Logs**
    - We can have Logs, Logs Groups, Log Streams
- **Metrics**
    - Create Custom metrics and define resolution (intervale to connect data)
    - not all ec2 metrics are tracked without an agent (need to install cloudwatch agent on Ec2)
- **EventsBridge**:
    - Event
    - Producer
    - Event Bus (Place that contain events)
    - Rules (determine what events to deliver)
    - Targets (the target consume events)
    - common use case: (Trigger DB Backup everyday)
<div style="text-align: center;"><img src="./eventbridge.png" alt="three-tier design" width="800" height="400" style="border-radius: 15px;"></div>

- **Alarm**:
    - state (OK, ALARM, INSUFFICIENT)
    - Condition (define threshold -> `Static & Anomaly`)
    - Action (Notifications, ASG, EC2 Actions)

# CLoudTrail
- Monitor API calls and Actions
- we use it to identify:
    - who User, UserAgent
    - Where Source IP Address
    - When EventTime
    - What Region, resource

- It tracks Management Events (Default) , Data Events