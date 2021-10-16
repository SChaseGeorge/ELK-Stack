# ELK-Stack
Cybersecurity Bootcamp project

The files in this repository were used to configure the network depicted below.

 (Diagrams/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the GitHub file may be used to install only certain pieces of it, such as Filebeat.

- install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will have high availability, in addition to restricting access to the network.

- The load balancer protects the network from availability attacks such as DDoS (distributed denial-of-service) attacks. 
- The jump box is the connection point to the rest of the machines, using a jump box makes securing the entire network easy because as the single point of access to the internal network it is easily monitored and controlled to prevent unwanted access. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.

 - Filebeat monitors log files and collects log events when changes occur, it can be set to monitor specific logs and then it sends the logs to Logstash.

- Metricbeat records metrics from the operating system such as CPU and memory usage as well as information about services running on the system. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function        | IP Address | Operating System |
|----------|-----------------|------------|------------------|
| Jump Box | Gateway         | 10.0.0.7   | Linux            |
| Elk VM   | Hosts ELK Stack | 10.1.0.4   | Linux            |
| Web 1    | Hosts DVWA      | 10.0.0.8   | Linux            |
| Web 2    | Hosts DVWA      | 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 174.51.15.176

Machines within the network can only be accessed by ssh from the Jump box.

- The machine that has access to the ELK VM is the Jump box with IP 10.0.0.7  

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 174.51.15.176        |
| ELK VM   | No                  | 10.0.0.7             |
| Web 1    | No                  | 10.0.0.7             |
| Web 2    | No                  | 10.0.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for scalability and easy implementation. Automating the configuration means that installing ELK stack on a new system will be extremely easy and streamlined. 


The playbook implements the following tasks:
- Install Docker
- Install python3 
- Increase virtual memory 
- Use more memory
- Download and launch docker elk container
- Enable service on boot 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/Docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 10.0.0.8
- Web2 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat and Metricbeat have been installed on both machines 

These Beats allow us to collect the following information from each machine:

- Filebeat and Metricbeat are used to collect information such as log events, system file changes and monitor CPU and memory. Filebeat can be used to collect log information on specific files or more brand log events, on example of this is audit logs and server logs. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to the sensible container.
- Update the Ansible hosts file to include the group elk and the IP address of the VM you want it to run on, you want the ELK stack to run on the ELK VM so you put that IP and you want Filebeat to run on Web1 and Web2 so you put in there IP addresses to specify which machine to run on. 
- Run the playbook, and navigate to the ELK VM to check that the installation worked as expected by running docker ps.
- Go to http://your -ELK-VM-External-IP:5601/app/kibana to ensure that the ELK sever is up and running. 
