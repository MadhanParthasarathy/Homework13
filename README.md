# Homework13
Week 13
Project Information
what was required by the course as further proof of understanding and sharing of skills.

The network design below contains a intentionally vulnerable web application D*mm Vulnerable Web Application or DVWA and uses modern tools such as Elk for monitoring.

This design also contains elements of Docker, Ansible and Azure cloud services, including the use of High Availability (HA) technologies.

Introduction
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

This project also contains the following details:

Network Design Topology
Access Control Policies
ELK Configuration, including Configuration of monitoring software below
MetricBeat Setup
FileBeat Setup
Use of Ansible for Automated Deployment.
Network Design
The following design below is a representation of an Azure Cloud setup of the Elk stack, including the setup of a Load Balancer and use of network security groups to limit the flow of traffic using rule based control.

In this design, all traffic was restricted to each of our personal IPv4 public IP addresses.

Network Design

Resources
Virtual Machines

x4 Ubuntu based machines (tested using Ubuntu Server LTS 20.04)
x1 client workstation, or a device capable of displaying a browser.
Networking Requirements

NAT or Bridged Network
Traefik Reverse Proxy for HTTP traffic (or a Azure Load Balancer and NSG rule)
Virtual Machine Specifications

x1 VM with 2vCPUs and at least 4Gb Memory.
x2 VMs with 2vCPUs and 2Gbs Memory
x1 VM with 1vCPU and 2Gbs Memory
Knowledge and Skills This project is designed to help new cyber security professionals log and monitor internal systems, including. the below are assumed skills

Intermediate Linux directory navigation and diagnostic skills.
Understanding of virtualization software and technologies, such as containerization and hypervisors
Network Access Policies The machines on the internal network (vNet) are not exposed to the public Internet.

Using the diagram above and the table below, the only allowed port will be SSH for external access, this is additionally secured using a SSH key for an extra layer of security.

Network Addresses

The below table contains the IP address information for each virtual machine, including its function and operating system.

Name	Function	IP Address	Operating System
Web-1	DVWA with FileBeat and MetricBeat Monitoring	10.0.0.6	Ubuntu 18.04
Web-2	DVWA with FileBeat and MetricBeat Monitoring	10.0.0.7	Ubuntu 18.04
Elk Stack	Elk Stack Monitoring Host	10.1.0.4	Ubuntu 18.04
Jump-Box	Ansible configuration host	10.0.0.5	Ubuntu 18.04
Firewall Rules

Public NSG Rules

Name	Public Traffic Allowed	Allowed IP Addresses
Jump Host	Yes (SSH)	20.211... (Home IP Address)
Elk Server	Yes (Port 5601)	20.70... (Home IP Address)
Internal NSG Rules

The below rules are allowed internal traffic.

Name	Allowed IP Addresses	Allowed Ports
Web-1	10.0.0.4, 10.0.0.16 (Jump Host)	SSH
Web-2	10.2.0.4, 10.0.0.16 (Jump Host)	SSH
Elk Stack	10.1.0.4 (Jump Host)	5601
Jump Host		SSH
Ansible Setup
In this project, all configuration was performed using Ansible scripts in the Ansible folder above. This is also secured by using SSH keys for each of the host machines on the virtual network.

Ansible is used to automate deployments of network infrastructure and applications, it has various applications and use cases.

For this project the steps are as follows

Create an SSH Key on your home machine with ssh-keygen
Create 4 New Virtual Machine with Ubuntu (Web-1, 2, Elk Stack and Jump Host) 2.1. Create a availability set for both web machines to allow for additional redundancy.
Connect both Web virtual machines to the same virtual network (vNet)
Connect Jump Host to web network
Install Docker on Jump Host
Import cyberx/ansible docker container using docker pull
Start and access the Ansible container using docker attach
Setup an SSH key on the Ansible container to be imported on Web 1 and 2
Elk Setup
Using the Ansible playbook, edit the Ansible host file and include your elk machine ip in the elk servers.

Provision the new docker container using the project1-elk-server.yml file and ansible-playbook <filepath>

The following screenshot displays the end result of running docker ps after successfully configuring the ELK instance.

Elk Docker PS Command
  
![elk text](Images/"elk setup.PNG")
  
Monitoring with MetricBeats and FileBeat
This ELK server is configured to monitor the following machines:

10.0.0.6
10.0.0.7
We have installed the following Beats on these machines:

Web-1
Web-2
Using the system module of Elk and MetricBeat. this has been configured to monitor for system events and record all logs from the /var/log/* directory. this includes authentication events, CPU, memory and storage use.

you can find an example of the end result for MetricBeat here.



and FileBeat here.

