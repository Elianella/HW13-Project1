## Automated ELK Stack Deployment

**The files in this repository were used to configure the network depicted below.**

 <img src="https://github.com/Elianella/HW13-Project1/blob/main/Images/Diagram.png"> 

These files have been tested and used to generate a live _ELK_ deployment on _Azure_. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as _Filebeat_.

- <a href="https://github.com/Elianella/HW13-Project1/blob/main/ansible/install-elk.yml">Elk Install</a>
- <a href="https://github.com/Elianella/HW13-Project1/blob/main/ansible/pentest.yml">DVWA</a>
- <a href="https://github.com/Elianella/HW13-Project1/blob/main/ansible/filebeat/roles/filebeat-playbook.yml">FileBeat</a>
- <a href="https://github.com/Elianella/HW13-Project1/blob/main/ansible/metricbeat/roles/metricbeat-playbook.yml">MetricBeat</a>

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
- _Filebeat_ monitors the log files that you specify _(audit logs, deprecation logs, gc logs, server logs, and slow logs)_, collects log events, and forwards them to Elasticsearch for indexing.
- _Metricbeat_ helps you monitor your servers by collecting metrics from the system and services running on the server.  It takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch.

The configuration details of each machine may be found below.
|   Name   |       Function      | IP Address | Operating System |
|:--------:|:-------------------:|:----------:|:----------------:|
| Jump Box |       Gateway       |  10.0.0.7  |      Ubuntu      |
|   Web-1  |      Web Server     |   10.0.05  |      Ubuntu      |
|   Web-2  |      Web Server     |  10.0.0.6  |      Ubuntu      |
|    Elk   | ElasticSearch Stack |  10.1.0.4  |      Ubuntu      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
