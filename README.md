## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/B-Sayer/GT_Project_1/blob/a6104d6a27e8abb9d4d280827c466bf129f9932b/Diagrams/diagram_filename.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/B-Sayer/GT_Project_1/blob/2652b4f59d6a0048408312defdd464829c728e71/Ansible/ansible_config.yml
  - https://github.com/B-Sayer/GT_Project_1/blob/2652b4f59d6a0048408312defdd464829c728e71/Ansible/ansible_elk.yml
  - https://github.com/B-Sayer/GT_Project_1/blob/2652b4f59d6a0048408312defdd464829c728e71/Ansible/filebeat-playbook.yml
  - https://github.com/B-Sayer/GT_Project_1/blob/2652b4f59d6a0048408312defdd464829c728e71/Ansible/install-elk.yml
  - https://github.com/B-Sayer/GT_Project_1/blob/2652b4f59d6a0048408312defdd464829c728e71/Ansible/metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- The load balancers can protect against Distributed Denial-of-Service attacks (DDoS Attacks). The jumpbox enables control of all traffic by forcing it into one center point, i.e. the jumpbox.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat enables the monitoring of log files or locations that are specified. Logs are collected and forwarded to either Elasticsearch or Logstash for indexing.
- Metricbeat collects metrics and statistics, routing them to a specified output such as Logstash or Elasticsearch.

The configuration details of each machine may be found below.

| Name     | Function   |  IP Address   | Operating System |
|----------|------------|---------------|------------------|
| Jump Box | Gateway    | 23.96.107.167 | Linux            |
| Web 1    | Webserver  |  10.0.0.5     | Linux            |
| Web 2    | Webserver  |  10.0.0.6     | Linux            |
| ELK-VM   | ELK Server |  10.1.0.4     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Home Network IP Addresses

Machines within the network can only be accessed by the Jump-Box-Provisioner.

- Jump-Box-Provisioner: 23.96.107.167 vis SSH port 22. Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses                                  |
|----------|---------------------|-------------------------------------------------------|
| Jump Box | Yes/No              | Home Network IP Addresses                             |
| Web 1    | No                  | Jump-Box: 23.96.107.167 LB: 20.106.163.202            |
| Web 2    | No                  | Jump-Box: 23.96.107.167 LB: 20.106.163.202            |     
| ELK-VM   | No                  | Jump-Box: 23.96.107.167 Web1: 10.0.0.5 Web2: 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible is able to easily and quickly deploy multi-tier apps by creating Ansible Playbooks. These playbooks allow the direct application to VMs, configuring them based on what is specified in the Ansible Playbook. A huge advantage is the ability to re-use these playbooks to configure future VMs.

The playbook implements the following tasks:
- Increase Memory/Use More Memory
- Install docker.io
- Install python3-pip
- Install docker
- Download and launch ELK Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/B-Sayer/GT_Project_1/blob/befeed3efe393813559f8fda7ab2a5589efdc54f/Diagrams/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1: 10.0.0.4
- Web 2: 10.0.0.5
- ELK-VM: 10.1.0.4

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors specified machines, collecting logs such as audit logs, deprecation logs, and server logs.
- Metricbeat monitors specified machines, collecting metrics from the operating system and services such as CPU, Memory, File System, Disk IO, Network IO, and statistics on      running processes.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/install-elk.yml.
- Update the hosts file to include your Webserver IP's and ELKServer IP's. Be sure to specify the correct host in your ansible playbook.
- Run the playbook, and navigate to HTTP://<ELKServer_Public_IP>:5601 to check that the installation worked as expected.

### Commands the User will need to run
Put install-elk.yml under /etc/ansible
Edit the hosts file in /etc/ansible and include the correct IP address with ansible_python_interpreter=/usr/bin/python3 under the correct []

Run install-elk.yml by typing command: ansible-playbook install-elk.yml

Now visit HTTP://<ELKServer_Public_IP>:5601

Run the filebeat-playbook.yml and metricbeat-playbook.yml in the /etc/ansible folder by using ansible-playbook, filebeat-playbook.yml, and ansible-playbook / metricbeat-playbook.yml
