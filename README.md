# Virtual-Network-Deployment
Deployment of a jump box, webservers, and ELK stack in Azure. This involved cloud security, logging, and monitoring


The files in this repository were used to configure the network depicted below.

Virtual-Network-Deployment/Project1.NetworkDiagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the pentest.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting unrestricted access to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system metrics. Filebeat is responsible for the log data, while Metricbeat will be collecting system statistics, and mertrics.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address | Operating System | 
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |   
| Web1     | Server     | 10.0.0.5   | Linux            |   
| Web2     | Server     | 10.0.0.6   | Linux            |   
| Elk      | Monitoring | 10.2.0.3   | Linux            |  

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
66.30.15.27

The Jump-Box-Provisioner is the only way to access any of the machines within the network. - 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses            |
|----------|---------------------|---------------------------------|
| Jump Box | Yes                 | 66.30.15.27, 10.0.0.5, 10.0.0.6 |
| Web1     | No                  | 10.0.0.4                        |
| Web2     | No                  | 10.0.0.4                        |
| Elk      | No                  | 10.0.0.4                        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows us to deploy multiple at the same time. It is also easier, and prevents human error.

The playbook implements the following tasks:
- Installing Docker and Python3-pip and sets them as the default docker modules
- Increase allocated memory
- Downloads and launches the elk image to the specified container
- Confirms ELK ports
- Enables Docker service to enable upon booting


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
- These Beats allow us to collect the following information from each machine:
- Filebeat generates log files on the machine it is installed on. Filebeat also has the capability to forward data to Logstash or Elasticsearch.
- Metricbeat is responsible for the collection of metrics, and statistics of a system. Metricbeat takes the information it collects and ships it to a specified output, in this case, Logstash and Elasticsearch.


### Using the Playbook
- In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

- SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml as well as metricbeat-playbook.yml file to the /etc/ansible directory
- Update the hosts file to include your machines IP address. Set the IP addresses of the machines you are trying to configure.
- Run the ansible playbook. Check your ELK VM for installation validation.

In Depth Configuration:
- Modify the following files
  - ansible.cfg
    - set user
  - metricbeat-config.yml
    - set hosts 
  - filebeat-config.yml
    - set hosts
- Modify the hosts file 
 - update the IP address of the servers you want to monitor [webservers] 
 - update IP address of the ELK stack [elk]
- Run pentest playbook to deploy dockers to webservers
- Run filebeat and metricbeat playbooks to deploy services to ELK VM
- ssh into ELK vm and "sudo docker ps" to confirm docker is running
- Another way to confirm the deployment was succesful is to navigate to your Kibana dashboard. (http://[elk.external.ip]:5601/app/kibana)
