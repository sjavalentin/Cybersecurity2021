## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/sjavalentin/Cybersecurity2021/blob/386b43783470eddcf02b77e9991ce8d866b8de64/Diagrams/Network%20Diagram.jpg "Diagrams/Network Diagram.jpg")


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **yml** file may be used to install only certain pieces of it, such as Filebeat.

	- ELK install
	- [Filebeat playbook](https://github.com/sjavalentin/Cybersecurity2021/blob/386b43783470eddcf02b77e9991ce8d866b8de64/Ansible/filebeat-playbook.yml)
	- [Metricbeat playbook](https://github.com/sjavalentin/Cybersecurity2021/blob/386b43783470eddcf02b77e9991ce8d866b8de64/Ansible/metricbeat-playbook.yml)


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly **available**, in addition to restricting **access** to the network.

**If an attacker attacks the DVWA container with enough traffic, they may be able to trigger a Denial of Service on the machine. Load balancers are in place to protect from DDos attacks. They help ensure environment availability through distribution of incoming data to webservers. Jumpboxes allow for more easy administrations of multiple systems and provide an additional layer between the outside and internal assets.**

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **logs** and system **metrics**.

**Filebeat monitors the logs for any information in the file system that has been modified and when a file has been modified. 
Metricbeat takes the metrics and statistics  that it collects and ships them to the output you specify, such as Elasticsearch or Logstash.**

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name    	| Function   	| IP Address 	| Operating System 	|
|---------	|------------	|------------	|------------------	|
| JumpBox 	| Gateway    	| 10.0.0.4   	| Linux            	|
| Web-1   	| Server  	| 10.0.0.5   	| Linux            	|
| Web-2   	| Server  	| 10.0.0.6   	| Linux            	|
| ELK     	| Server 	| 10.1.0.4   	| Linux            	|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the **JumpBox provisioner** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

	- **Personal IP**


Machines within the network can only be accessed by the **JumpBox**. The Elk machine can have access from **personal IP** address through **port 5601**.	


A summary of the access policies in place can be found in the table below.

| Name    	| Publicly Accessible 	| Allowed IP Addresses 	|
|---------	|---------------------	|----------------------	|
| JumpBox 	| Yes                 	| Personal IP           |
| Web-1   	| No                  	| 10.0.0.4             	|
| Web-2   	| No                  	| 10.0.0.4             	|
| ELK     	| Yes                  	| Personal IP           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because **services running can be limited, system installation and update can be streamlined, and process become more replicable.**

The playbook implements the following tasks:
- Installs docker.io
- Install pip3
- Install Docker python pip module
- Use sysctl module to increase memory
- Configure container to start with the following port mappings 
	- 5601:5601
	- 9200:9200
	- 5044:5044


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name  | IP Address |
|-------|------------|
| Web-1 | 10.0.0.5   |
| Web-2 | 10.0.0.6   |


We have installed the following Beats on these machines:

	- *Filebeat*
	- *Metricbeat*


These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

- *Filebeat forwards and centralizes log data from your target machines. It monitors the log files that you specify and collects the log events, then forwards them to the elk server. 
- *Metricbeat collects the machine metrics and statistical data, such as CPU usage, memory usage and inbound/outbound traffic and sends the data to the ELK server. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the *playbook YML* files to *Ansible Control node* folder.
- Update the *hosts* files to include *webservers and elk IP addesses*
- Edit hosts files to update and make run ansible playbook on a specific machine, and specify which machine to install the ELK server on versus which to install Filebeat.
- Run the playbook, and navigate to *Kibana* to check that the installation worked as expected.
- Check that ELK server is running: http://[ELK IP]/app/kibana#/home

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._