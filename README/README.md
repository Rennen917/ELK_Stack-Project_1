## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 -Update the path with the name of your diagram](Images/ELK Network.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  (Ansible Playbooks install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly dynamic in addition to restricting access to the network.
     
-What aspect of security do load balancers protect? What is the advantage of a jump box?

[A load-balancer has features and policy controls to stop bad traffic from ever reaching the main application, two main examples being (rate limiting) and (URL filtering). Both software and physical Load-balancers work on layers 4-7 of the OSI model (transportation, session application, presentation).]

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.

 -What does Filebeat watch for? [Filebeat watches and monitors the log files or locations that users specify also it collects log events and forwards them to either Elasticsearch or Logstash for indexing.]
 
-What does Metricbeat record? [Metricbeat is similar to Filebeat it is whats known as a lightweight shipper that periodically collects metrics from the operating system and from services running on the server.]

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |Web Server| 10.1.0.5   | Linux            |
| Web-2    |Web Server| 10.1.0.6   | Linux            |
|ELK-VM-MK1|Web Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 -Add whitelisted IP addresses
[Only the Jump Box machine can accept connections from the internet through (Port 22). Access to this machine is only allowed from the following IP addresses.(My IP)]

-Machines within the network can only be accessed by [The three machines within this network can only be accessed by the provisioned Jump Box. This provisioning allows for only my personal
IP to gain access to the ELK project VM which works off of (Port 5601). Machines outside of this network can only gain access by remote access through the Jump Box within the Ansible container.]

 -Which machine did you allow to access your ELK VM? What was its IP address?

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1 10.0.0.2    |
| Web-1    | No                  | MY IP                |
| Web-2    | No                  | MY IP                |
| ELK-VM   | SSH-No/HTTP-yes     | MY IP                |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

-What is the main advantage of automating configuration with Ansible?

[I used ansible to automate all 3 of the VM's. I didn't perform any configuration manually which is an advantage because Ansible allows for universal changes to be made within any of the VM's associated with Ansible. This helps with stability between the machines and fluidty with the playbook established.]
[A main advantage of the automation factor with Ansible is its use of roles. The roles provide the groundwork for various tasks. The Ansible roles basically simplify the writing of complex playbooks.]

The playbook implements the following tasks:

 -In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

[The VMs can be built in 5 steps. First you Install docker.io.Then you Install python3-pip. Third you Install Docker module E.g.
Elk Instalation: Fourth by creating a new vNet which we needed to be located in the same resource group. Most of the settings stayed the same after that it entailed adding Peering. This established the connection between all vNets. This was important for allowing traffic to pass between the virtual networks.
Install Docker: Finally you had to create a playbook that installed Docker and configured the containers (-name: Insatll Docker python module)]

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

-Update the path with the name of your screenshot of docker ps output](Images/Sudo Docker ps -a.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 
-List the IP addresses of the machines you are monitoring.

[The ELK server is configured to monitor the following machines:(ELK-VM-MK1 10.1.0.4) (JumpBoxProvisioner 10.0.0.4) (Web-1 10.1.0.5) (Web-2 10.1.0.6)]

We have installed the following Beats on these machines:

 -Specify which Beats you successfully installed.

[I successfully installed Filebeat on my Web-1,Web-2 and ELK-VM-MK1]

These Beats allow us to collect the following information from each machine:

 -In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.

[Filebeat watches and monitors log files the log events and locations that users specify, Example: Harvesters and inputs.]

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

[- Edit the /etc/ansible/ansible.cfg command line remote_user=username (mine is bluesysadmin) to indicate the remote account being used to execute playbooks.]
[- Update the (/etc/ansible/hosts) file to include the groups we want to install packages on.]
[- Run the playbook, and navigate to (JumpBoxProvisioner)to check that the installation worked as expected.]

   -Answer the following questions to fill in the blanks:
 -Which file is the playbook? Where do you copy it?

[The anisble.cfg file is the playbook and you copy it to the /etc/ansible directory.]

 -Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

[I updated the (install-Elk.yml) file to make Ansible run the playbook on a specific machine to specify which machine to install the ELK server on versus which to install Filebeat on. I used specific IP's of the servers.]

 -Which URL do you navigate to in order to check that the ELK server is running?

[To make sure my ELK-VM-MK1 was running I navigated to http://20.46.242.239:5601/app/kibana#/home/tutorial/systemLogs and verified that Kibana was recieving data.]

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._