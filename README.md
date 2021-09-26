## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](Project_1.draw.io.PNG) 

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.
- Load balancers protect system from attacks such as DDoS attacks that threaten the availablity of the application. 
- Along with a Load Balancer, using a Jump Box has benefits as well. It prevents all of the servers from being exposed to the public.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.  
Filebeat Monitors the log files or locations specified, collects log events.    
Metricbeat monitors your server by collecting metrics, statistics, and running services  

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    |Web Server| 10.0.0.5   | Linux            |
| Web-2    |Web Server| 10.0.0.6   | Linux            |
| ELKVM    |ELK Stack | 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 136.36.14.156

Machines within the network can only be accessed by the ansible container.
- JumpBox 10.0.0.4  

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 136.36.14.156        |
| ELKVM    | Yes                 | 136.36.14.156        |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because rather than having to do it all manually all the tasks needed for configuration at once in a playbook. Playbooks can be used repeatedly as well if configuration is needed on another machine.  

The playbook implements the following tasks:
- Install Docker
- Install python
- Increase virtual memory
- Download image
- Launch container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps output](\Diagrams\docker_ps_output.png) 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5   
- 10.0.0.6  

We have installed the following Beats on these machines:
- Filebeat  
- Metricbeat  

These Beats allow us to collect the following information from each machine:  
- Filebeat collects log data, monitors log files, collects log events, and sends them to Elasticsearch or Logstash. An example would be the logs produced that monitor the HTTP traffic across the server.  
- Metricbeat collects metrics and statistics on your system or server. An example would be statistics that monitor general health of the system, such as CPU usage, or apache server status  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the `install_elk.yml` file to the `/etc/ansible/` directory.
- Update the _____ file to include...
- 

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

- _Which URL do you navigate to in order to check that the ELK server is running?


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._  

- Navigate to the ansible folder  
`cd /etc/ansible`

- To make the playbook install_elk.yml run on a specific machine you need to edit the /ansible/hosts file. Here you make groups, an example the elk group, adding the machines ip to the group. This way when you run a playbook with ansible, you can specify which group to run them on. 
Edit the hosts file, place ELKVM in a group  
`nano hosts`
`[elk]`
`10.1.0.4 ansible_python_interpreter=/usr/bin/python3`

- Run the playbook  
`ansible-playbook install_elk.yml`

- Connect to the VM  
`ssh RedAdmin@20.150.211.49`

- Check that the container is running  
`docker ps`

- Run the playbook, and navigate to http://20.150.211.49:5601/app/kibana to check that the installation worked as expected.
