# Frank
CS bootcamp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Red Team Virtual Network with Elk Server]("C:\Users\frank\Frank\Diagram\Red Team Virtual Network with Elk Server.png")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above or select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - "C:\Users\frank\Frank\Ansible\ansible.cfg.txt"
  - "C:\Users\frank\Frank\Ansible\hosts.txt"
  - "C:\Users\frank\Frank\Ansible\install-elk.yml.txt"
  - "C:\Users\frank\Frank\Ansible\filebeat-config.yml.txt"
  - "C:\Users\frank\Frank\Ansible\filebeat-playbook.yml.txt"
  - "C:\Users\frank\Frank\Ansible\metricbeat-config.yml.txt"
  - "C:\Users\frank\Frank\Ansible\metricbeat-playbook.yml.txt"

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized access to the network and preventing DOS attacks.  Load balancers distribute traffic evenly between multiple servers and thereby keeping the servers/data available for the company.  

A Jump Box limits the traffic from the internet and prevents unauthorized access to the servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system logs.  Threats such as changes to the file systems, increased CPU usage and any declined login attemp can be easily reviewed and escalated if neccesary.    

The configuration details of each machine may be found below.


| Name                 | Function   | IP Address              | Operating System |
|----------------------|------------|-------------------------|------------------|
| Jump Box Provisioner | Gateway    | 20.83.61.176/ 10.0.0.4  | Linux            |
| Web-1                | Web Server | 10.0.0.5                | Linux            |
| Web-2                | Web Server | 10.0.0.6                | Linux            |
| Web-3                | Web Server | 10.0.0.7                | Linux            |
| ElkServer            | Monitoring | 20.230.101.99/ 10.1.0.4 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Gateway machine can accept connections from the Internet. Access to this machine is only allowed from the IP address 63.124.141.112.

Machines within the network can only be accessed by SSH through the JumpBoxProvisioner at 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump Box Provisioner | Yes                 | 63.124.141.112       |
| Web-1                | No                  | 10.0.0.4             |
| Web-2                | No                  | 10.0.0.4             |
| Web-3                | No                  | 10.0.0.4             |
| ElkServer            | Yes                 | 63.124.141.112       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it quicker and consistent.  All configuration would be the same and changes can easily be made if needed.

The playbook implements the following tasks:
- Install Docker
- Install Python3-pip
- Install the Docker using pip
- Increase virtual memory
- Download and launch the elk:761 docker web container and allow ports 5601:5601, 9200:9200 and 5044:5044
- Enable Docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker PS]("C:\Users\frank\Frank\Images\Docker PS.png")

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name  | IP Address |
|-------|------------|
| Web-1 | 10.0.0.5   |
| Web-2 | 10.0.0.6   |
| Web-3 | 10.0.0.7   |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

Filebeat is used to collect log data files on remote machines.  Metricbeat is used to collect the metrics of the system such as memory and CPU usage.  These files will be sent to the ELk server to be stored and reviewed through Kobana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the playbook files to Ansible Control Node.
	- mkdir files within /etc/ansible
	- git clone https://github.com/eddie12frank/Frank/blob/main/Ansible/install-elk.yml.txt/.git
	- cp filebeat-playbook.yml.txt /etc/ansible/files
	- cp metricbeat-playbook.yml.txt /etc/ansible/files

- Update the hosts file to include the ELK Server.
	- nano /etc/ansible/hosts
![Update Host File]("C:\Users\frank\Frank\Images\Update Host File.png")
	
- Run the playbook, and navigate to kibana to check that the installation worked as expected.
	- cd /etc/ansible
	- ansible-playbook install_elk.yml 
	- ansible-playbook install_filebeat.yml 
	- ansible-playbook install_metricbeat.yml 

-Check Kibana to verify installation succeeded
	- website: http://20.230.101.99:5601/app/kibana



