## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!NETWORK DIAGRAM(Images/ELK NETWORK.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly distributed, in addition to restricting access to the network.
-The main purpose of load balancing is to prevent any single server from getting overloaded and possibly breaking down. The jumpbox acts as a main point of control for your other VMs. A jump server is hardened and monitroed in
a seperate secutiy zone and allows management and access of other devices.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system data.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat records data about Elasticsearch and ships it to the monitoring cluster.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     |   Function    | IP Address | Operating System |
|----------|---------------|------------|------------------|
| Jump Box | Gateway       | 10.0.0.1   | Linux            |
| DVWA-1   |   VM          | 10.0.0.2   | Linux            |
| DVWA-2   |   VM          | 10.0.0.3   | Linux            |
| ELK VM   |Data Aggregator|162.11.12.13| Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Home IP Address: 173.2.193.223

Machines within the network can only be accessed by the Jumpbox's Ansible Container.
-Which machine did you allow to access your ELK VM? 
Jumpbox VM 
What was its IP address? 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |  Yes                | 173.2.193.223        |
| DVWA-1   |  NO                 | 10.0.0.1             |
| DVWA-2   |  NO                 | 10.0.0.1             |
| ELK VM   |  NO                 | JUMPBOX IP           |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-Using ansible playbooks allows us to automatically configure one or many servers at once.

The playbook implements the following tasks:
- Install Docker
- Install Python-pip
- Install Docker Module
- Increase Virtual Memory
- Publish The Ports ELK Runs On

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/Docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-DVWA-1 : 10.0.0.2             
-DVWA-2 : 10.0.0.3             

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:
-Filebeat plays the role of the logging agent and shipping the logs to the ELK Server for data consumption. An example would be Apache Access Logs.
-Metricbeat holds onto incoming data and then ships those metrics to Elasticsearch or Logstash. An example of data shipped is CPU and RAM consumption.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to ./etc/ansible/.
- Update the hosts file to include the Web Servers you will be running the playbook on.
- Run the playbook, and navigate to DVWA-IP:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Copies ./ansible/playbook.yml to ./etc/
- _Which file do you update to make Ansible run the playbook on a specific machine?
The Hosts File
 How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
By specifying the ansible hosts it will run against in the playbook
- _Which URL do you navigate to in order to check that the ELK server is running?
ELK-SERVER-IP:9200 for Elasticsearch Interface and port 5601 for Kibana Interface

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._