# Day 4: Introduction to Amazon VPC & Network Security

## Overview
Built and inspected a custom Amazon Virtual Private Cloud (`Lab-vpc`) in `us-west-2` using the **VPC and more** wizard, and verified routing, network access control, and security group behavior across public and private subnets.

## Architecture & Resource Summary
- **Region:** `us-west-2` (US West - Oregon)
- **VPC:** `Lab-vpc` (`vpc-045263245387b4ecf`, CIDR: `10.0.0.0/16`)
- **Public Subnet:** `Lab-subnet-public` (`10.0.25.0/24`)
  - Associated with a public route table containing `10.0.0.0/16` (`local`) and `0.0.0.0/0` routed to the attached **Internet Gateway** (`Lab-igw` / `igw-0592c233c2363531a`).
  - Hosts the **NAT Gateway** (launched in the public subnet so it has a public IP and path to the IGW).
- **Private Subnet:** `Lab-subnet-private` (`10.0.50.0/24`)
  - Associated with a private route table containing `10.0.0.0/16` (`local`) and `0.0.0.0/0` routed to the **NAT Gateway** for outbound internet access without direct inbound internet exposure.

## Key Networking & Security Takeaways
- **Public vs. Private Subnet:** A subnet is public when its route table directs internet-bound traffic (`0.0.0.0/0`) to an **Internet Gateway**; routing `0.0.0.0/0` to a **NAT Gateway** keeps instances private while allowing outbound access.
- **Local Route (`10.0.0.0/16`):** Enables internal communication across the VPC CIDR block without leaving the VPC.
- **Security Groups (Stateful):** Operate at the instance/ENI level and automatically allow return traffic for permitted inbound/outbound rules.
- **Network ACLs / NACLs (Stateless):** Operate at the subnet level, evaluate rules in ascending order (`100`, etc., down to `*` default deny), and require explicit rules for both directions since return traffic is not automatically tracked.
