

# Creating and Configuring a Network Load Balancer in AWS

<img width="1537" height="888" alt="Screenshot 2025-11-01 125641" src="https://github.com/user-attachments/assets/813fb3ba-d98a-47d2-a5ce-038ae8c1f08c" />



## 📋 Overview

This repository documents my hands-on lab experience creating and configuring a Network Load Balancer (NLB) in AWS. The lab was completed through Whizlabs and demonstrates practical skills in AWS networking, load balancing, and high availability architecture.

**Lab Source:** [Whizlabs - Creating and Configuring a Network Load Balancer in AWS](https://www.whizlabs.com/labs/creating-and-configuring-a-network-load-balancer-in-aws)

## 🎯 Objectives

- Create and configure an AWS Network Load Balancer
- Set up EC2 instances as target resources
- Configure target groups with health checks
- Implement load balancing across multiple availability zones
- Test and verify load distribution and failover capabilities

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Internet Gateway                      │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ▼
        ┌─────────────────────────────┐
        │   Network Load Balancer     │
        │    (Layer 4 - TCP/UDP)      │
        └──────────┬──────────────────┘
                   │
        ┌──────────┴──────────┐
        │                     │
        ▼                     ▼
┌───────────────┐     ┌───────────────┐
│      AZ-1     │     │      AZ-2     │
│               │     │               │
│ ┌───────────┐ │     │ ┌───────────┐ │
│ │  EC2      │ │     │ │  EC2      │ │
│ │  Target 1 │ │     │ │  Target 2 │ │
│ └───────────┘ │     │ └───────────┘ │
└───────────────┘     └───────────────┘
```

## 🛠️ Technologies Used

- **AWS Services:**
  - Amazon EC2 (Elastic Compute Cloud)
  - Elastic Load Balancing (Network Load Balancer)
  - Amazon VPC (Virtual Private Cloud)
  - Security Groups
  - Target Groups

- **Protocols:** TCP/UDP (Layer 4)
- **Region:** [Specify your region, e.g., us-east-1]

## 📝 Implementation Steps

### 1. Environment Setup
- Created a VPC with public subnets across multiple availability zones
- Configured Internet Gateway and route tables
- Set up security groups with appropriate inbound/outbound rules


### 2. EC2 Instance Configuration
- Launched EC2 instances in different availability zones
- Installed and configured web servers (Apache/Nginx)
- Created custom index pages to identify each instance
- Applied security groups to allow traffic on required ports

### 3. Target Group Creation
- Created a target group with TCP protocol
- Configured health check parameters:
  - Health check protocol: TCP/HTTP
  - Health check port: [Your port]
  - Healthy threshold: [Number]
  - Unhealthy threshold: [Number]
  - Interval: [Seconds]
- Registered EC2 instances as targets
- <img width="1898" height="854" alt="Screenshot 2025-11-01 125738" src="https://github.com/user-attachments/assets/e55ff38c-68d8-46b0-b614-c8ececc76444" />


### 4. Network Load Balancer Configuration
- Created an internet-facing Network Load Balancer
- Selected multiple availability zones for high availability
- Configured listener rules:
  - Protocol: TCP
  - Port: [Your port, e.g., 80]
  - Default action: Forward to target group
- Enabled cross-zone load balancing (if applicable)
  <img width="1898" height="849" alt="Screenshot 2025-11-01 125911" src="https://github.com/user-attachments/assets/c482f2de-7fd1-4f43-bc73-d671d534a81b" />

<img width="1896" height="832" alt="Screenshot 2025-11-01 125853" src="https://github.com/user-attachments/assets/97aa289c-8e85-4441-af0c-b3737543b280" /> 
  <img width="1909" height="818" alt="Screenshot 2025-11-01 125940" src="https://github.com/user-attachments/assets/cd7c190a-ee84-4cf5-9526-1f96b7d4e126" />


### 5. Testing and Validation
- Verified NLB DNS name resolution
- Tested load distribution across instances
- Validated health checks and target status
- Simulated instance failure to test failover
- Measured response times and connection handling

## 🔍 Key Learnings

### Network Load Balancer Characteristics
- **Layer 4 Load Balancing:** Operates at the transport layer (TCP/UDP)
- **Ultra-low Latency:** Capable of handling millions of requests per second
- **Static IP:** Provides a static IP address per availability zone
- **Preserve Source IP:** Maintains client IP address to targets
- **Connection-based:** Routes connections rather than individual requests

### Performance Benefits
- Handles sudden traffic spikes effectively
- Supports long-lived TCP connections
- Minimal latency impact compared to Application Load Balancer
- Ideal for latency-sensitive applications

### High Availability Features
- Automatic failover to healthy targets
- Cross-zone load balancing for even distribution
- Health checks ensure traffic only goes to healthy instances
- Multi-AZ deployment for fault tolerance

## 📊 Results


- Successfully distributed traffic across  EC2 instances
- Health checks correctly identified unhealthy targets within [X] seconds
- Load balancer DNS name: (http://mynetwork-lb-5abc32802b19a1aa.elb.us-east-1.amazonaws.com/)

## 🔐 Security Considerations

- Security groups configured with least privilege principle
- Target instances only accept traffic from NLB security group
- TLS/SSL termination options available (if configured)
- VPC subnet isolation for enhanced security

## 💰 Cost Optimization Tips

- Delete resources after lab completion to avoid charges
- Use t2.micro instances for testing (free tier eligible)
- Monitor NLB hours and data processed
- Consider using Application Load Balancer if Layer 7 features are needed



## 📸 Screenshots


### Load Balancer Testing
<img width="1881" height="792" alt="Screenshot 2025-11-01 130350" src="https://github.com/user-attachments/assets/6d4b20ec-9593-4654-a004-5564855adde9" />
<img width="1894" height="642" alt="Screenshot 2025-11-01 130404" src="https://github.com/user-attachments/assets/22b97494-d42a-465c-b510-c869765db069" />
Showcasing that it is working on both the Apache and Nginx servers 
<img width="1537" height="888" alt="Screenshot 2025-11-01 125641" src="https://github.com/user-attachments/assets/147237ae-5561-4431-8887-52e1c1cf3bbb" />
Validation of being completed in its entirety 



## 🔗 Additional Resources

- [AWS Network Load Balancer Documentation](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/)
- [Elastic Load Balancing Best Practices](https://aws.amazon.com/architecture/well-architected/)
- [Network Load Balancer vs Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Dorien K**
- GitHub:(https://github.com/cantstayoffl1ne) 



## 🙏 Acknowledgments

- Whizlabs for providing the hands-on lab environment
- AWS Documentation and community resources

---

⭐ If you found this helpful, please consider giving it a star!


