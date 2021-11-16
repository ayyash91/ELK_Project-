# ELK_Project

## Automated ELK Stack Deployment


The files in this repository were used to configure the network depicted below.

<img src="/Diagrams/ELK_Network.png" >


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.


  https://github.com/ayyash91/ELK_Project-/blob/main/Ansible/filebeat-playbook.yml


## This document contains the following details:


* Description of the Topology
* Access Policies
* ELK Configuration
     - Beats in Use
     - Machines Being Monitored
* How to Use the Ansible Build





## Description of the Topology


The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.


Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

<strong>What aspect of security do load balancers protect?</strong> 
         
* Load Balancer distributed the traffic efficiency across the network which helps in mitigating denial of service attacks (DDoS). 
* Load Balancer also had health probe function. This function check regularly to make sure the machine behind the load balancer is functioning before sending traffic to them. If one machine had an issue then the load balancer start sending the traffic to the other machine. 

<strong>What is the advantage of a jump box?</strong>

* Jump box prevents VMs to be exposed to the public network and restrict access to the machines securely only to the administrator from the Jump box


 


    
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system traffic.


<strong>What does Filebeat watch for?</strong>

* Filebeat collect file system and log files and monitors any change that occurs to the system


<strong>What does Metricbeat record?</strong>

* Collect metrics from your systems and services and send them to Elasticsearch for visualization and chart generating. 


The configuration details of each machine may be found below.



|  Name | Function  | IP Address  | Operation system  |
|---|---|---|---|
| Jump box  | Gateway / Ansible  | 10.0.0.4  | Linux Ubuntu 18.04.01  |
| Web-1  | Web Server used to run DVWA  |  10.0.0.7 | Linux Ubuntu 18.04.01  |
| Web-2  |  Web Server used to run DVWA | 10.0.0.8  |  Linux Ubuntu 18.04.01 |
| Elk  | Run Elk Container and Kibana  | 10.1.0.4  | Linux Ubuntu 18.04.01  |


## Access Policies


* The machines on the internal network are not exposed to the public Internet.

* Only the Jump Box Provisioner machine can accept connections from the Internet. 

* Access to this machine is only allowed from the following IP addresses: 93.85.243.49


* Machines within the network can only be accessed by the Jump-box-Provisioner.


<strong>Which machine did you allow to access your ELK VM?</strong>

* Jump Box


<strong>What was its IP address?</strong> 

* 13.68.194.231
















A summary of the access policies in place can be found in the table below.




| Name  | Public Accessible  | Allowed IP Address  |
|---|---|---|
|  Jump Box | Yes via Port 22  | 93.85.243.49  |
| Web-1  |  No | 10.0.0.4  |
|  Web-2 | No  |  10.0.0.4 |
| ELK  | Yes via port 5601  |  93.85.243.49 |
| Load Balancer  | Yes via port 80  | 93.85.243.49  |


	
	







## Elk Configuration


Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces human error and simplifies the process of configuration of multiple machines


The playbook implements the following tasks:


* Install docker.io the docker engine. used for running containers
* Install python3 for ELK machine 
* Install python client for docker. Required by ansible to control the state of Docker containers.
* Increase the virtual memory for the ELK machine by 262144 
* Download the ELK docker image with restart police always so there is no need for the elk container to start manually every time 
* Finally, enable docker on the boot so we don’t have to start it manually every time we turn on our VM 


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


<img src="/images/docker-ELK.png" >






Target Machines & Beats
This ELK server is configured to monitor the following machines:


* Web-1 with IP Address 10.0.0.7
* Web-2 with IP Address 10.0.08 


We have installed the following Beats on these machines:


* Filebeat 
* Metricbeat 


These Beats allow us to collect the following information from each machine:


Filebeat collects log information about the file system and which file has been changed in the system. On the other hand, metric beats show information about the operation system and the status of the CPU usage, memory usage, network IO  


## Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned. SSH into the control node and follow the steps below:


*  Copy the `filebeat-config.yml` file to `/etc/ansible/files/filebeat-config.yml`


* Update the filebeat-config.yml to include host “10.1.0.4.9200” with username “elastic” and password “changeme” and setup.kibana host to “10.1.0.4:5601” 


* Run the playbook, and navigate to http://23.99.89.109:5601/app/kibana#/home/tutorial/systemLogs and click on check data from the browser to check that the installation worked as expected.




<strong>Which file is the playbook?</strong>


* `filebeat-playbook.yml`


 <strong>Where do you copy it?</strong>


* `/etc/ansible/roles/filebeat-playbook.yml`








<strong>Which file do you update to make Ansible run the playbook on a specific machine?</strong>


* `/etc/ansible/hosts` 


<strong>How do I specify which machine to install the ELK server on versus which to install Filebeat on?</strong>


* By adding the private ip address of web-1 and web-2 to the file host under [webservers]


* Adding the private ip address of the elk vm under [elk] 


<storng>Which URL do you navigate to in order to check that the ELK server is running?</strong>


* http://23.99.89.109:5601/app/kibana


Command we use to download, update and run playbook:


To download playbook we use the command:

`curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml`
	



To update files we use the nano command 


* `nano hosts` 
* `nano playbook_file.yml`


To run the playbook we use the command: 


* `ansible-playbook playbook_file.yml`
