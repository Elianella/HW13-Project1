## Automated ELK Stack Deployment

**The files in this repository were used to configure the network depicted below.**

 <img src="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/Images/Diagram.png"> 

These files have been tested and used to generate a live _ELK_ deployment on _Azure_. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as _Filebeat_.

- <a href="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/Elk/install-elk.yml">Elk Install</a>
- <a href="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/DVWA/pentest.yml">DVWA</a>
- <a href="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/filebeat/roles/filebeat-playbook.yml">FileBeat</a>
- <a href="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/metricbeat/roles/metricbeat-playbook.yml">MetricBeat</a>

**This document contains the following details:**
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

_Load balancing_ ensures that the application will be highly available and reliable, in addition to restricting access to the network.
- A _Jumpbox_ or _Jump Server_ serves as a gateway to gain entry into a remote network. 
  - This helps us to open only one port instead of several ports to connect different virtual machines present in the cloud. 
  - Many times the primary mode of access is ssh and without the key access is forbidden.
  - The _Jumpbox_ can be kept inside a specific subnet (Jumpbox Subnet) with high monitoring capabilities as a security improvement.
- A _Loadbalancer_ distributes network traffic across multiple servers.
  - This ensures no single server bears too much demand. By spreading the work evenly, _load balancing_ improves application responsiveness.
  - If necessary, _load balancers_ remove  unhealthy servers from the pool until they are restored.
  - This increases high availability and helps prevent overloads as well as distributed denial-of-service (DDoS) attacks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- _Filebeat_ monitors changes on the log files that you specify _(audit logs, deprecation logs, gc logs, server logs, and slow logs)_, collects log events, and forwards them to Elasticsearch for indexing.
- _Metricbeat_ helps you monitor your servers by collecting metric data from the system and services running on the server.  It takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch.

The configuration details of each machine may be found below.
|   Name   |       Function      | IP Address | Operating System |
|:--------:|:-------------------:|:----------:|:----------------:|
| Jump Box |       Gateway       |  10.0.0.7  |      Ubuntu      |
|   Web-1  |      Web Server     |  10.0.0.5  |      Ubuntu      |
|   Web-2  |      Web Server     |  10.0.0.6  |      Ubuntu      |
|    Elk   |      Monitoring     |  10.1.0.4  |      Ubuntu      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Jump Box_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 138.91.188.251

Machines within the network can only be accessed by Jump Box.
- **Public IP:** 138.91.147.29
- **Private IP:** 10.0.0.7

A summary of the access policies in place can be found in the table below.

|      Name     |   Publicly Accessible   | Allowed IP Addresses |
|:-------------:|:-----------------------:|:--------------------:|
|    Jump Box   |           Yes           |    138.91.188.251    |
|     Web-1     |            No           |           -          |
|     Web-2     |            No           |           -          |
|      ELK      |           Yes           |    51.141.184.242    |
|      ELK      |           Yes           |      10.1.0.0/16     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It allows for full automation and implementation of various configurations of a specific server or multiple machines, reducing configuration errors.

The playbook implements the following tasks:
- **Install Docker.io:** Docker Engine, used for running containers.
- **Install Python3_PIP:** Package used to install Python software.
- **Increase Virtual Memory:** This configures the target VM to use more memory, Elk container will not run without this setting.
- **Docker Container Module:** Tells the previous PIP module to install the necessary docker component modules.
- **Download and Launch Elk Container:** This downloads the ELK Docker container and initializes it with the specified ports being published.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/Images/docker-ps.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- **10.0.0.5** - Web-1
- **10.0.0.6** - Web-2

We have installed the following Beats on these machines:
- **Filebeat**
- **Metricbeat**

These Beats allow us to collect the following information from each machine:
- _Filebeat_ monitors the log files or locations specified by collecting log events, and then forwarding them to elasticsearch for indexing.
- _Metricbeat_ allows us to collect various metrics and statistics from the operating system and various processes running on the specified servers and ships them to the output that you specify, like Elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml to roles directory /etc/ansible/roles/.
- Update the hosts file to include the IPs of each machine on each group (web so that Ansible knows wich machines need to be run on a given playbook.
- Run the playbook, and navigate to Kibana (http://[Host IP]:5601/app/kibana) to check that the installation worked as expected.


**Bonus**
- ssh azdmin@138.91.147.29 (connect to Jump Box)
- sudo docker container start [name of container] (start ansible container)
- sudo docker container attach [name of container] (run ansible container)
- curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb
sudo dpkg -i metricbeat-7.6.1-amd64.deb (using metricbeat as an example)
- nano /etc/ansible/hosts
  -  edit hosts by adding the machines for elk group
<img src="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/Images/hosts.png">

- ansible-playbook metricbeat-playbook.yml
- check your installation is working by visiting in a browser: http://51.141.184.242:5601/app/kibana#/home/tutorial/dockerMetrics
  - you should see something like this:
<img src="https://github.com/Elianella/HW13-Project1/blob/main/Scripts/ansible/Images/Metricbeat-dashboard.png">
