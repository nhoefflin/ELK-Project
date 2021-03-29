# ELK-Project
Automated ELK Stack Deployment - Azure


## Automated ELK Stack Deployment

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting traffic to the network.
- The primary function of a load balancer is to spread workloads across multiple servers to prevent overloading servers, optimize productivity and maximize uptime. Load balancing also provides the ability to add and remove instances without causing any disruption to incoming traffic.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system files.
- Filebeat will monitor the VMs by generating and organizing log files. Specifically, it logs information about the file system, including which files have changed and when.
- Metricbeat will monitor the VMs by periodically collecting metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name       | Function | IP Address | Operating System |
|------------|----------|------------|------------------|
| Jump-Box   | Gateway  | 10.0.0.4   | Linux            |
| Web-1      | Client   | 10.0.0.5   | Linux            |
| Web-2      | Client   | 10.0.0.6   | Linux            |
| Web-3      | Client   | 10.0.0.7   | Linux            |
| ELK-Server | Gateway  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- <My_Public_IP>

Machines within the network can only be accessed by SSH from the Jump-Box VM.
- Jump-Box can access the ELK-Server private IP: 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump-Box   | Yes                 | 52.173.31.22         |
| ELK-SERVER | No                  | 10.1.0.4             |
| Web-1      | No                  | 10.0.0.5             |
| Web-2      | No                  | 10.0.0.6             |
| Web-3      | No                  | 10.0.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- We can make updates to our server without disrupting incoming traffic.

The playbook implements the following tasks:
- Install docker.
- Install pip3.
- Install docker python module.
- Download and launch docker elk container.

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
 - https://github.com/nhoefflin/ELK-Project/blob/main/Images/Install-elk.png
 - https://github.com/nhoefflin/ELK-Project/blob/main/Images/Docker-ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.7
- ELK-SERVER 10.1.0.4
  - https://github.com/nhoefflin/ELK-Project/blob/main/Images/Network-Interfaces.png


We have installed the following Beats on these machines:
- Filebeat, which will monitor the VMs by generating and organizing log files. Specifically, it logs information about the file system, including which files have changed and when
- Metricbeat, which will monitor the VMs by periodically collecting metrics from the operating system and from services running on the server.

The playbook below installs Filebeat on the target hosts.
- https://github.com/nhoefflin/ELK-Project/blob/main/Ansible/filebeat-playbook.yml

The playbook below installs Metricbeat on the target hosts.
  - https://github.com/nhoefflin/ELK-Project/blob/main/Ansible/metricbeat-playbook.yml

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible.
- Update the hosts file to include each VM client IP address (10.0.0.5-10.0.0.7)
    - 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
    - 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
    - 10.0.0.7 ansible_python_interpreter=/usr/bin/python3
    - [elk]
- Run the playbook and navigate to 10.0.0.5 and curl localhost/setup.php to check that the installation worked as expected.
- Check to make sure that the ELK server is running:
  - Public IP address on port 5601 (40.114.0.106:5601/app/kibana#/home)
  - Kabana Application



To download and run the playbooks, use the following commands:
  - ansible-playbook filebeat-playbook.yml from /etc/ansible.
  - ansible-playbook metricbeat-playbook from /etc/ansible.
