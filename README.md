## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

AZURE_server_W12.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

Install-elk.yml to install and configure the interaction between the machines and the elk server.
filebeat-playbook.yml to install and launch the Filebeat service on the target machines.
Metricbeat.yml to install and configure Metricbeat on the target machines.

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly AVAILABLE, in addition to restricting overprocessing to the network.
The load balancers ensure that all processing from the network is partitioned out as well as restricting the amount of data that faces outward onto the public.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics of the network and system logs.
Filebeat: Provides the system logs for the machines.
Metricbeat: Monitors the metrics for each VM in the network including CPU usage and load, memory availability as well as input and output for the network.

The configuration details of each machine may be found below.

| Name     | Function  |IP Address | Operating System |
|----------|-----------|-----------|------------------|
| Jump Box | Gateway   | 10.1.0.4  | Linux (Ubuntu)   |
| Web 1    |DVWA Server| 10.1.0.7  | Linux (Ubuntu)   |
| Web 2    |DVWA Server| 10.1.0.8  | Linux (Ubuntu)   |
| Web 3    |DVWA Server| 10.1.0.9  | Linux (Ubuntu)   |
| Elk 1    | ELK Stack | 10.3.0.1  | Linux (Ubuntu)   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox and the Elk machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
  - Only the personal ip addresses for the developer of this network is allowed to access the public IPs for the Jumpbox machine.
  - Only ther personal ip addresses for the developer of this network are allowed to access the Kibana open port for the Elk server machine.
 
Machines within the network can only be accessed by Jumpbox.
  - The Jumpbox and the Elk machines can access the DVWM servers.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses  |
|----------|---------------------|-----------------------|
| Jumpbox  | Yes                 |Personal workstation ip| 
| Web1     | No                  | 10.0.1.4              |
| Web2     | No                  | 10.0.1.4              |
| Web3     | No                  | 10.0.1.4              |
| Elk      | Yes                 |Personal workstation ip|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is an easily understandable python language that doesnt require code to be built from the ground up. It uses docker engines and functions to partition out a protocol for the engines to follow.

The playbook implements the following tasks:
- Install ELK
  - Installs Docker using the apt command
  - Installs python 3 using the apt command
  - Configures VMs to use more memory using the sysctl comman
  - Pushes the docker container from the ELK machine

- Filebeat
  - Downloads and installs Filebeat using curl and dpkg
  - Pushes the filebeat playbook from the Elk machine.
  - Force enables the Filebeat module and starts it

- Metricbeat
  - Download and install .deb package for metricbeat
  - Copy metricbeat config file to VMs
  - Enable docker module for metricbeat
  - Setup and start metricbeat

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
  - Web1
  - Web2
  - Web3

We have installed the following Beats on these machines:
  - Filebeat
  - Metricbeat

These Beats allow us to collect the following information from each machine:
  - Filebeat - Collectes and centralizes system logs to reference and troubleshoot the machine.
  - Metricbeat - Collects and centralizes Machine performance information throughout usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook files to /etc/ansible/role.
- Update the /etc/ansible/hosts file to include the ip addresses of both the elkservers and the webservers.
- Run the playbook, and navigate to (public_ip_of_elk):5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
  - The install-elk.yml file is the playbook.
  - The /etc/ansible/hosts file is the config file to make sure the playbooks run at certain machines.
  - The public ip followed by :5601 is the url for the elk server.
