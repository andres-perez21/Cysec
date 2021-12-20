# Cysec


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

•	TODO: Enter the playbook file.

This document contains the following details:

•	Description of the Topology

•	Access Policies

•	ELK Configuration 

•	Beats in Use

•	Machines Being Monitored

•	How to Use the Ansible Build

Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting disallowed access to the network.

•	Load balancers help protect against DDoS attacks. An advantage of the jump box is to be easily accessible, protected single access point into the virtual network. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the and system matrix.

•	Filebeat watches for any file changes in locations that you have set and indexes them. 

•	Metric beat records the metric data on a target server or data related to services running on a server. 

The configuration details of each machine may be found below. 


|     Name        |     Function                  |     IP Address                |     Operating System    |
|-----------------|-------------------------------|-------------------------------|-------------------------|
|     Jump Box    |     Gateway/Administration    |     10.0.0.4                  |     Linux               |
|     Web-1       |     DVWA                      |     10.0.0.5                  |     Linux               |
|     Web-2       |     DVWA                      |     10.0.0.6                  |     Linux               |
|     Elk         |     IDS                       |     20.112.79.200/10.1.0.5    |     Linux               |

Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Machines within the network can only be accessed by Jump-Box-Provisioner (10.0.0.4)

•	The only machine that can access the Elk server is the Jump-Box_Provisioner as well (10.0.0.4)

A summary of the access policies in place can be found in the table below.

|     Name        |     Publicly Accessible    |     Allowed IP   Addresses    |
|-----------------|----------------------------|-------------------------------|
|     Jump Box    |     No                     |     Personal Host IP          |
|     Web-1       |     No                     |     10.0.0.4                  |
|     Web-2       |     No                     |     10.0.0.4, 10.0.0.5        |
|     Elk         |     No                     |     10.0.0.4                  |
		
		
Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because reduces that repetitive task which reduces errors. 
The playbook implements the following tasks:
•	The playbook first installs docker.io, python3-pip, and the docker module on all webservers that have been selected in the host file.
•	The playbook will then increase the virtual memory and allocates that to the ELK Server.
•	After, the docker ELK container is installed and launched.
•	Finally, it will confirm the container is installed, configured and up and running using system command. 



The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
 
 

Target Machines & Beats

This ELK server is configured to monitor the following machines:
•	Web-1 10.0.0.5
•	Web-2 10.0.0.6
We have installed the following Beats on these machines:
•	Filebeats and Metricbeats were installed to create logfiles to monitor. They were added to Logstash for processing and visualized in Kibana to be analyzed. 
These Beats allow us to collect the following information from each machine:
•	Filebeats collects system log information and stores it in a designated location. Filedbeat will index the last line of the index registry. If the network were to fail, and then rebooted, Filebeat would return to the last point before failure. 
•	Metricbeat collects metric data, i.e., CPU usage or uptime of the system. Metricbeat can also monitor other beats on the system.  

Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:
•	Copy the ansible-playbook file to the node.
•	Update the host file to include the IP addresses of the WebServers and the Elk Server. 
•	Run the playbook, and navigate to Kibana site for the Elk server to check that the installation worked as expected. (http://20.112.79.200:5601/app/kibana#/home)
