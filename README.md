# Project
linux and ansible scripts
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted above.~/Project/diagrams/’network diagram.png’



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.



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
What aspect of security do load balancers protect? What is the advantage of a jump box? Load balancers protect against denial of service attacks; the load balancer analyzes the traffic coming in and determines what server to send the traffic to. This distributes the traffic evenly and prevents a server from getting overloaded with traffic. The jump box allows private access to servers because you need private ips to connect to the other machines.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
What does Filebeat watch for? Filebeat watches for changes to the files, it generates and organizes log files. 
What does Metricbeat record? Metricbeat records metrics from the operating system and services running on the server. Metricbeat uses Elasticsearch or Logstash which lets you visualize the metrics and statistics that it generates from the OS and running services.

The configuration details of each machine may be found below.

| Name 	| Function | IP Address | Operating System |
| jump box | gateway                     | 10.0.0.4 | Linux (ubuntu 18.04) |   |
| web-1    | web server used to run DVWA | 10.0.0.7 | Linux (ubuntu 18.04) |   |
| web-2    | web server used to run DVWA | 10.0.0.8 | Linux (ubuntu 18.04) |   | 
| ELK      | Run ELK container & Kibana  | 10.1.0.4 | Linux (ubuntu 18.04) |   |


Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Add whitelisted IP addresses 76.205.178.251, 10.0.0.8, 10.0.0.7

Machines within the network can only be accessed by jump box vm.
Which machine did you allow to access your ELK VM? What was its IP address? Jump box 20.187.116.44

A summary of the access policies in place can be found in the table below.

| Name 	| Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| jumpbox        | yes                | 76.205.178.251 |
|----------------|--------------------|----------------|
| web-1          | no                 | 10.0.0.7       |
| web-2          | no                 | 10.0.0.8       |
| ELK            | yes via (port5601) | 76.205.178.251 |
| Load Balancer  | yes via (port 80)  | 76.205.178.251 |


Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it prevented having to configure ELK manually and streamlined the process. It allowed more control over what was being installed and performed on the machine. No coding skills are necessary to use playbooks. You can orchestrate the entire application environment no matter where it is deployed.

The playbook implements the following tasks:
THe elk playbook installs docker.io on the elk virtual machine
Python is installed on the ELK VM
ELK requires more virtual memory so this tasks increases memory
Downloads installs and executes the docker elk container on the ELK VM.
This enables docker on boot so you dont have to manually start docker when you turn your vm back on.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Screen shot of 'docker ps' can be found in the ansible folder.

Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.7
web-2 10.0.0.8
We have installed file beat and metricbeat on the following machines web-1, web-2, and the elk server.

These Beats allow us to collect the following information from each machine:
Filebeat collects log information about the file system and specifies which files have been changed and when a file was changed to either elasticsearch or Logstash. Connecting to kibana will allow you to check the logs for any changes that have been made to the file system while showing the time interval of your choosing. Metricbeat shows statistics for every process running on your system including memory, CPU usage, file system, Network IO disk IO stats. View this data collected by connecting to kibana while machines are running, select the system you want to review and from there you can see the metrics of the system.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files/filebeat-config.yml.
- Update the filebeat-config.yml file to include host 10.1.0.4:5601
- Run the playbook, and navigate to kibana (ELK GUI interface) to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Filebeat-playbook.yml Where do you copy it? /etc/ansible/files/filebeat.playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? Filebeat-config.yml this is the file you update to run the playbook. We had to add elk server private ip to the host file then we are able to add filebeat and metricbeat.
- _Which URL do you navigate to in order to check that the ELK server is running? http://136.35.167.114:5601/app/kibana

# Cloud Network
This is a collection of Linux Scripts and Ansible Scripts from my CyberClass.

Most of the scripts are used to configure cloud servers with different docker containers.

The final setup was 4 servers running vulnerable DVWA containers along with a jump box and a server running an ELK stack container.
