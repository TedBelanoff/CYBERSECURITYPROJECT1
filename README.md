## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

![Update the path with the name of your diagram](images/FileBeat Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - ansible/Elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly distributed, in addition to protecting from exessive requests to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Load balancers prevent excessive requests to a single machine (DDos attacks) by keeping the traffic distributed. A JumpBox provides a standard environment that allows
for a common security policy and access groups across a set of virtual machines.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the traffic quantity and system stability. It also monitors file system changes.
- _TODO: What does Filebeat watch for?_ FileBeat detects changes in a machine's file system.
- _TODO: What does Metricbeat record?_ MetricBeat detects changes in a system's metrics (ex: traffic quantity, CPU usage statistics).

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name        | Function  | IP Address                       | Operating System |
|-------------|-----------|----------------------------------|------------------|
| Jump Box    | Gateway   | 10.0.0.4 (and 13.68.154.26)      | Linux            |
| RedTeam-Web1| DVWA      | 10.0.0.5                         | Linux            |
| RedTeam-Web2| DVWA      | 10.0.0.6                         | Linux            |
| RedTeam-Web3| DVWA      | 10.0.0.7                         | Linux            |
| ELKVM       | ELK Server| 10.1.0.4 (and 104.215.101.147)   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK/Kibana machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 74.72.253.235

Machines within the network can only be accessed by the jumpbox (RedTeam-JumpBox).
-Which machine did you allow to access your ELK VM? The Jumpbox
 What was its IP address? 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses |
|--------------|---------------------|----------------------|
| Jump Box     | Yes                 | 74.72.253.235        |
| RedTeam-Web1 | No                  | 10.0.0.4             |
| RedTeam-Web2 | No                  | 10.0.0.4             |
| RedTeam-Web3 | No                  | 10.0.0.4             |
| ELKVM        | Yes                 | 74.72.253.235        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
	Ansible allows many commands to be executed uniformly on multiple machines with a single command. Large ansible scripts could save a lot of time.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Specify elkservers as the installation point (based on the [elkservers] tag in the host file
- Increase memory size
- Install docker
- Install pip3
- Install docker python

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


![Update the path with the name of your screenshot of docker ps output](images/docker_screenshot.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: 
	RedTeam-Web1 (10.0.0.5)
	RedTeam-Web2 (10.0.0.6)
	RedTeam-Web3 (10.0.0.7)

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
I installed FileBeat-oss-7.9.3. I tried installing other versions but they were not compatible with my elasticsearch version.

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects/records changes in internal computer file structure.

Metricbeat collects usage statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to the new VM.
- Update the hosts file to include the new VM in the appropriate servers category
- Run the playbook, and navigate to the new VM to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? The playbook is the .YML file that specifies install instructions.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
	You update the hosts file in order to specify which machines to run various functions on. You can specify the different types of computers by changing the server tags (repeated in the playbook files)
	in the hosts file. For example, my elk installation is in the [elkservers] group while the FileBeat playbook installs on the VMs in the [webservers] group.
- _Which URL do you navigate to in order to check that the ELK server is running?
	The public IP (port 5601) of the Elk VM. This should work provided that you have allowed access on the Elk VM to this port. 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
