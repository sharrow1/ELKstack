## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagrams\Network_Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  - [Webserver playbook](Ansible/DVWA.yml)
  - [ELK playbook](Ansible/Elk.yml)
  - [Combined Beats playbook](Ansible/CombinedBeats.yml)
  - [Filebeat playbook](Ansible/Filebeat.yml)
  - [Metricbeat playbook](Ansible/Metricbeat.yml)

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
-  Load balancers protect the availability of the network by balancing traffic between multiple destinations, if one is overloaded or drops offline for any reason the other can help keep the resource available.  
- The biggest advantage to a jump box is only having to open an ssh connection from select sources in your firewall, which saves on monitoring resources.

 Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- The stack uses filebeat for logs and log events
- The stack uses metricbeat to record system metrics such as cpu load and memory usage.

The configuration details of each machine may be found below.
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Ubuntu 18.04     |
| Elk1     | Elkstack | 10.2.0.4   | Ubuntu 18.04     |
| Web1     | Webserver| 10.1.0.9   | Ubuntu 18.04     |
| Web2     | Webserver| 10.1.0.8   | Ubuntu 18.04     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- 154.21.23.76

Machines within the network can only be accessed by jumpbox,  at IP 10.1.0.4.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      | Yes                 |  154.21.23.76        |
| Internal jump | No                  |  10.1.0.4            |
| 80 to LB      | Yes                 |  154.21.23.76        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of it's scalability.

The playbook implements the following tasks:
- The playbook first downloads and installs docker, python3.pip and the pip docker module
- Then the playbook increases its virtual memory and makes it available to the system
- Then the elk container is downloaded and launched
- Finally docker is enabled

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="Images\docker ps.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1: 10.1.0.9
- Web2: 10.1.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- We can use Filebeat to monitor logs to check for system issues or new files added to the system.  Metricbeat is used to collect system utilization logs such as CPU and network usage.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the beats.yml file to /etc/ansible/playbooks/.
- Update the hosts file to include your target machines
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- Playbooks are yaml files located in: `/etc/ansible/playbooks/`
- To run ansible on a specific machine add it to the ansible hosts file, located in /etc/ansible/hosts. I created an elk and dvwa group to install the relevant packages to the correct machines.

- _Which URL do you navigate to in order to check that the ELK server is running?
`http://<vmIPaddress>:5601/app/kibana`
### Commands to install stack:

````
- ssh redadmin@jumpboxip
- sudo docker container list -a
- sudo docker start [ansible container id]
- sudo docker attatch [ansible container id]
- cd /etc/ansible/playbooks
- vim elk.yml #copy elk.yml from repo
- ansible-playbook ekl.yml
- repeat for filebeat and metricbeat
