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

[DockerContainerModule](https://github.com/Slywon/Project1/blob/1f8dae9316bac26186d349730800ec62de433a0b/Docker_container_module_screenshot)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Successfully configuring ELK instance looks like this](https://github.com/Slywon/Project1/blob/febdf4f2adcfc61561fefd70fed5134d32722f04/screenshotsuccessfulconfigelkinstance.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6

We have installed the following Beats on these machines:
 FileBeat
 MetricBest 

These Beats allow us to collect the following information from each machine:
FileBeat allows the monitoring of log directories or even specific log files, tags the files, then sends them to Elasticsearch or Logstash to be indexed.  
MetricBeat does as the name suggests and collects metrics on the system for example CPU usage which is used to monitor the health of your system.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to your web VMs.
- Update the /etc/ansible/hosts file to include the IP addresses of the ELK server, VM, and webservers.  
- Run the playbook, and navigate to http://20.83.226.255:5601/app/kibana to check that the installation worked as expected.

Follow up questions.

Filebeat-config.yml is the playbook and you would copy it from /etc/ansible/files/filebeat-config.yml to /etc/filebeat/filebeat.yml

The file you update to make Ansilbe run the playbook on a specific machine is:  filebeat-config.yml -- specify the machine to install by navigating to the host files and updating them with the IP addresses of webservers as well as the Elk server and select which group to run in Ansible.  

You would naviagate to http://20.83.226.255:5601/app/kibana in order to check that the Elk server is running.  

