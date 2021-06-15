# Project-1
ElkStack:Web1:Web2:Jump-Box-Provisioner
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  -install-elk.yml
  -
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

- A jumpbox or bastion server serves as a gatway to gain entry into a remote network. Many times the primary mode of access is ssh and without the key access is forbidden
- A loadbalancer is meant to serve as a specific point of access for a service that is served by multiple machines. This allows high availability models to function properly

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- Filebeat is meant primarily to watch for system logs and forward any changes to the Elasticsearch Host
- Metricbeat is used only for gathering metrics and system resources usage for display in Elasticsearch

The configuration details of each machine may be found below.

| Name    | Function            | IP Address | Operating System |
|---------|---------------------|------------|------------------|
| JumpBox | Gateway             | 10.0.0.4   | Ubuntu           |
| Web1    | Web Server          | 10.0.0.5   | Ubuntu           |
| Web2    | Web Server          | 10.0.0.6   | Ubuntu           |
| ELK     | ElasticSearch Stack | 10.2.0.4   | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 20.94.252.40

Machines within the network can only be accessed by the Jumpbox Provisioner
- Jumpbox Provisioner
    -PublicIP: 20.94.252.40
    -PrivateIP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Addresses                       |
|---------|---------------------|--------------------------------------------|
| JumpBox | Yes                 | 20.94.252.40; 10.0.0.4; 10.0.0.5; 10.0.0.6 |
| Web1    | No                  | 10.0.0.5                                   |
| Web2    | No                  | 10.0.0.6                                   |
| ELK     | Yes                 | ElkStackVM1-ip; 10.2.0.4                   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It allows for full automation of a specific server and reduces configuration errors

The playbook implements the following tasks:
  -Install Docker: Installs the core docker code to the remote server
  -Install Python3_pip: Pip is an installation module that allows for additional docker modules to be installed easier
  -Docker Module: Tells the previous PIP module to install the necessary docker component modules
  -Increase Memory/Use More Memory: A common issue with the ELK Docker image is to little memory. This help fix the issue to allow the server to launch
  -Download and Launch ELK Container: This downloads the ELK docker container and initializes it with the specified ports being published

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.4
- 10.0.0.5
- 10.0.0.6
- 10.2.0.4

We have installed the following Beats on these machines:
- We have installed Filebeat and Metricbeat on the following Systems: Web1, Web2, ELK

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml
- Update the hosts file to include the attribute, such as ELK, then include your destination IP of the ELK server
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.
