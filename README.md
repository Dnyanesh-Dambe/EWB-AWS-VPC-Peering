# AWS VPC Peering Project

**Student:** Dnyanesh Dattatray Dambe      
**Batch:** AWS Batch 1
**Course:** AWS Architect Associate, EWB Courses
**Region:** Asia Pacific (Sydney) ap-southeast-2

## Overview
Two VPCs connected with VPC peering so two private EC2 servers can talk
over private IPs. One public bastion host in VPC A is used for SSH access.

## Architecture
[Architecture](docs/AWS VPC Peering Network Architecture.png)

| Resource | CIDR / IP |
|---|---|
| ewb-vpc-a | 10.10.0.0/16 |
| ewb-a-public | 10.10.1.0/24 |
| ewb-a-private | 10.10.2.0/24 |
| ewb-vpc-b | 10.20.0.0/16 |
| ewb-b-private | 10.20.1.0/24 |
| ewb-bastion | 10.10.1.10 (public IP) |
| ewb-app-a | 10.10.2.10 |
| ewb-app-b | 10.20.1.10 |

## What I built
- VPC A with a public and a private subnet, an internet gateway and route tables
- VPC B with a private subnet and no internet gateway
- Security groups with least-privilege inbound rules
- VPC peering with routes on both sides
- SSH access to private servers through the bastion using ProxyJump

## Test results
| Test | Result |
|---|---|
| Baseline ping before peering | 100% packet loss |
| App-A to App-B ping | 0% packet loss |
| App-B to App-A ping | 0% packet loss |
| SSH to App-B through bastion | Success |
| Controlled failure (ICMP rule removed) | Ping failed, then recovered |

Screenshots are in the `screenshots/` folder.

## Report
Full report: [report/Dnyanesh_EWB_VPC_Peering.pdf](report/Dnyanesh_EWB_VPC_Peering.pdf)

## Cleanup
All resources were deleted after the project to avoid charges.
