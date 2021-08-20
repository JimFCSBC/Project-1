## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagrams/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.
  filebeat-playbook.yml
  filebeat-config.yml
This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.

What aspect of security do load balancers protect?
The aspect of security load balancers protect, by off-loading, protects organizations from DDoS attacks. It also helps by preventing over-tasked servers.


What is the advantage of a jump box?
As the name would imply, a jump box is literally a 'jumping off', or starting point. Sysadmins securely connect here first, prior to starting potentially harmful network connected processes.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

What does Filebeat watch for?
Filebeat watches for log files or locations that users specify, collecting log events, and forwarding them to Elasticsearch or Logstash for indexing. It is a lightweight shipper for forwarding and centralizing log data, and is installed as an agent on the server.


What does Metricbeat record?
Metricbeat records stats and metrics from the operating system and services running on a server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|   | Name     | Function | IP Address                              | Operating System |   |
|---|----------|----------|-----------------------------------------|------------------|---|
|   | -------- | -------- | --------------------------------------- | ---------------- |   |
|   | Jump Box | Gateway  | 20.51.234.166(Public)/10.0.0.4(Private) | Linux            |   |
|   | ELK-VM   | Server   | 20.98.136.181(Public)/10.1.0.4(Private) | Linux            |   |
|   | Web-1    | Server   | 10.0.0.5                                | Linux            |   |
|   | Web-2    | Server   | 10.0.0.6                                | Linux            |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jump Box___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- Local machine's ip address 

Machines within the network can only be accessed by __Jump Box Provisioner___.

- Which machine did you allow to access your ELK VM? The Jump Box 
- What was its IP address? 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
| -------- | ------------------- | -------------------- |
| Jump Box | Yes                 | Local IP             |
| ELK-VM   | No                  | 10.0.0.4             |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- _TODO: What is the main advantage of automating configuration with Ansible?
- _It can expedite complex tasks required for multi-tier IT infrastructure creation.

The playbook implements the following tasks:

- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
The playbook (Elk-install.yml) implements the following tasks:
  - The first step installs Docker.
  - Next, Python3-pip installs.
  - Following step installs Docker module under pip.
  - Next, the VM's virtual memory gets increased with sysctl.
  - After which a docker elk container is downloaded and launched.
  - Lastly, the Docker service is configured to start upon bootup.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- _TODO: List the IP addresses of the machines you are monitoring
  - Web-1 (10.0.0.5)
  - Web-2 (10.0.0.6)

We have installed the following Beats on these machines:

- _TODO: Specify which Beats you successfully installed_
  - Metricbeat
  - Filebeat
  

These Beats allow us to collect the following information from each machine:

  - Metricbeat collects machine metrics, while filebeat collects log files from remote machines. 
  - Filebeat collects log files from modules like apache, mysql, nginx, etc.
  - Metricbeat records metrics, e.g. Memory and CPU usage, etc .._

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ___filebeat-config.yml__ file to __/etc/ansible__.
- Update the ___filebeat-config.yml__ file to include ELK private IP 10.1.0.4 in lines 1106 and 1806
- Run playbook, then logon to ELK-VM to check results of the installation.

_TODO: Answer the following questions to fill in the blanks:_

- _Which file is the playbook?
- filebeat-playbook.yml
-  Where do you copy it?_
- /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine?
- /etc/ansible/hosts
-   How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  - Create 2 groups in hosts file. Name one group "Elk" including the Elk-VMs IP. Name the other group "webservers" and include IPs of web VMs where Filebeat will be installed.

- _Which URL do you navigate to in order to check that the ELK server is running?
- http://20.85.211.96:5601

