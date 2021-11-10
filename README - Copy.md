## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Elk Deployment Diagram](https://drive.google.com/file/d/1SdAkdIedJS60YqbYH1-PNQrRn1MVoAfY/view?usp=sharing)

The following files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

Click Link to view [ElkPlayBook](https://docs.google.com/document/d/1vMusWICrrrCwiz38tOSiwu0Y9bDw8ir9aBFiqgAFPRo/edit?usp=sharing)

Click Link to view [FilebeatPlayBook](https://docs.google.com/document/d/1h_wC04IJgCAggkhUdcfUrct9aqpFVnBflAWfgTbqfcQ/edit?usp=sharing)

Click Link to view [MetricBeatPlayBook](https://docs.google.com/document/d/19ENDVzMKCAqhpy8mBKDVSI5kZ5n6zhTB6H6Igw12lls/edit?usp=sharing)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
The advantage of having a load balancer is that you are able to provide services using HTTP/HTTPS with out having an open SSH port to the internet.  A jump box can be created that is only accessible from select IP addresses, and would require a user to connect through the SSH protocol.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and the metrics of the system.
Filebeats can be used to watch for log directories or specific log files. 
Metricbeat is able to help you monitor servers as it collects metrics from the system and services running on the server.  

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address   | Operating System |
|----------|-----------|--------------|------------------|
| Jump Box | Gateway   | 10.0.0.4     | Linux            |
| Web 1    | Server    | 10.0.0.5     | Linux            |
| Web 2    | Server    | 10.0.0.6     | Linux            |
| Elk      | Log Server| 10.1.0.4     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
     67.182.212.206

Machines within the network can only be accessed by the Jump Box.
The Jump Box can SSH to the Elk through port 22

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      | Yes                 | 67.182.212.206       |
| Load Balancer | Yes                 | Any                  |
| Web 1         | No                  | 10.0.0.5             |
| Web 2         | No                  | 10.0.0.6             |
| ELK Server    | Yes                 | 67.182.212.206       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The main advantage of automating configuration with Anislbe is that the program does all the work allowing a person to configure multiple containers quicker than if they had to do it themselves.  

The playbook implements the following tasks:

To use Docker module:  name:Install docker.io apt:update_cache:yes name:docker.io state:present

To use Pip module:  name:Install pip3 apt:force_apt_get:yes name:python3-pip state:present 

To use Python:  name: Install Docker python module pip: name: docker state: present 

To use command module:  name: Increase virtual memory command: sysctl -w vm.max_map_count=262144

To use sysctll module:  name: Use more memory sysctl:name:vm.max_map_count valeu:"262144"state:present reload:yes

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[DockContainerModule](https://github.com/Slywon/Project1/blob/1f8dae9316bac26186d349730800ec62de433a0b/Docker_container_module_screenshot)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
