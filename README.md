# AWS-VPC-Traffic-Mirroring Lab
Hands-on lab using AWS VPC Traffic Mirroring to capture and analyze ICMP and HTTP traffic between EC2 instances using tcpdump and Session Manager.

This project demonstrates how to configure AWS VPC Traffic Mirroring to capture and analyze network traffic between EC2 instances.  
It covers identifying network interfaces, setting up traffic mirror targets, filters, and sessions, and verifying captured traffic.

![image](https://github.com/user-attachments/assets/ff764df3-36fa-4442-9409-74663f082724)


## Project Overview
- **VPC Setup** with a public subnet
- **Three EC2 Instances**:
  - **Client** (10.0.0.10): Sends traffic
  - **Server** (10.0.0.20): Receives traffic
  - **Target** (10.0.0.30): Captures mirrored traffic
- **Security Groups** configured to allow required ICMP and HTTP traffic.
- **Traffic Mirroring** configured for packet capture and analysis.
  
## Steps Performed
### 1. Identified Network Interfaces
- Retrieved the Elastic Network Interface (ENI) IDs for Server and Target EC2 instances.

### 2. Configured Traffic Mirror Target
- Created a Traffic Mirror Target using the Target instance's ENI.
![Screenshot ](https://github.com/user-attachments/assets/186e8da6-2044-4b79-9690-3a6e1e119bd2)

### 3. Configured Traffic Mirror Filter
- Created a filter to capture:
  - **Inbound ICMP traffic** from subnet (10.0.0.0/24) to the Server (10.0.0.20).
  - Later updated to also capture **HTTP traffic** (TCP port 80).
![Screenshot ](https://github.com/user-attachments/assets/e901baed-a672-4712-a352-5962a20c8aeb)
![Screenshot ](https://github.com/user-attachments/assets/da86c6cb-50bc-4c36-847d-edce37744069)

### 4. Created Traffic Mirror Session
- Established a session linking the Server’s ENI (source) to the Target’s ENI (target) using the created filter.
![Screenshot ](https://github.com/user-attachments/assets/e6382eb6-8e86-43b1-8e2a-934dfcb77ec5)

### 5. Captured and Verified Mirrored Traffic
- Used AWS Systems Manager Session Manager to access EC2 terminals.
- Installed and used `tcpdump` on the Target instance to monitor and capture mirrored traffic.
![Screenshot (19)](https://github.com/user-attachments/assets/560b9c56-ae40-42c5-842c-d72adb6ec06b)
![Screenshot (23)](https://github.com/user-attachments/assets/8b38ebdd-cbbd-4041-a912-27e819bc6f87)
![Screenshot (24)](https://github.com/user-attachments/assets/b605e5fb-186b-4904-9dd9-f8d7f2e2d843)

### 6. Saved Captured Traffic
- Saved packet captures into `.pcap` files for future analysis with tools like Wireshark.
![Screenshot (25)](https://github.com/user-attachments/assets/c82c1527-4762-4945-b9af-a517e9e5b29e)

## Key Concepts
- **Source**: ENI to monitor (Server)
- **Target**: ENI to send mirrored traffic (Target)
- **Filter**: Defines which traffic to mirror (ICMP and HTTP)
- **Session**: Binds source, target, and filter together

## Technologies Used
- AWS VPC
- AWS EC2
- AWS Systems Manager Session Manager
- AWS Traffic Mirroring
- `tcpdump`
- Linux CLI

## Lessons Learned
- Configuration of AWS Traffic Mirroring.
- Real-time packet capture and network traffic analysis.
- Importance of precise security group rules for mirrored traffic.
- Using filters to dynamically control captured traffic.

## Future Improvements
- Automate Traffic Mirroring setup with AWS CloudFormation or Terraform.
- Use Amazon Kinesis Data Firehose to stream mirrored traffic for real-time analytics.
  
## License
This project was completed as part of a cloud security hands-on learning initiative.  
Feel free to fork and expand upon it for educational purposes.

