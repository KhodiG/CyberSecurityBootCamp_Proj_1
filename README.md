## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/KhodiG/CyberSecurityBootCamp_Proj_1/blob/main/Images/Network_Diagram.PNG?raw=true

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  https://github.com/KhodiG/CyberSecurityBootCamp_Proj_1/tree/main/Ansible

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?_
	
	The load balancer can help protect the web servers from suspicious traffic and potential attacks.
	The JumpBox allows an admin to access the webservers from a single node that can be monitored and secured.
	
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
-What does Filebeat watch for?_
	
	Collects data about the file system

-What does Metricbeat record?_
	
	Collects machine metrics

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box | Gateway  | 10.0.0.1   | Linux            |
| Web1     | Server   | 10.0.0.7   | Linux            |
| Web2     | Server   | 10.0.0.8   | Linux            |
| ElkVM    | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Add whitelisted IP addresses_
	
	The JumpBox only accepts conenctions from my Home IP address.

Machines within the network can only be accessed by _____.
-Which machine did you allow to access your ELK VM? What was its IP address?_
	
	The Elk machine can only be accessed by my JumpBox

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses       |
|----------|---------------------|----------------------------|
| Jump Box | No                  | Home IP Address (ssh)      |
| Web1     | Yes                 | Any (http) 10.0.0.4 (ssh)  |
| Web2     | Yes                 | Any (http) 10.0.0.4 (ssh)  |
| ElkVM    | No			 | 10.0.0.4 (ssh)             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-What is the main advantage of automating configuration with Ansible?_
	
	Makes deploying new machines quick and easy  while making sure that they are set up correctly and the same way every time.

The playbook implements the following tasks:
- Install: docker.io
- Install: python3-pip
- Install: docker module
- Increase virtual memory
- Use more memory
- Download and launch docker elk container
- Enable Docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/KhodiG/CyberSecurityBootCamp_Proj_1/blob/main/Images/Elk761.PNG?raw=true

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_
	
	10.0.0.7
	10.0.0.8

We have installed the following Beats on these machines:
Specify which Beats you successfully installed_
	
	FileBeat
	MetricBeat

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
	
	FileBeat: Monitors log files specified, collects log events and forwards them to desired locations for indexing. It will show things like unique visitors, what OS they're using, avg bytes, etc.
	
	MetricBeat: Periodically collects metric data from servers such as CPU or memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
	
	/etc/ansible/file/filebeat-configuration.yml
	
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
	
	You can use the host file in the ansible folder to organize your machine into groups, then designate which groups install which containers in the .yml
	
- _Which URL do you navigate to in order to check that the ELK server is running?
- 
	https://20.38.34.142:5601/app/kibana
