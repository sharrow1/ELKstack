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
- What aspect of security do load balancers protect? What is the advantage of a jump box?_Load balancers protect the availability of the network by balancing traffic between multiple sources.  The biggest advantage to a jump box is only having to open an ssh connection from select sources in your firewall.

 Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- What does Filebeat watch for? Filebeat monitors logs and log events
- What does Metricbeat record? Metricbeat records system metrics such as cpu load and memory usage.

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

Machines within the network can only be accessed by jumpbox, 10.1.0.4.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      | Yes                 |  154.21.23.76        |
| Internal jump | No                  |  10.1.0.4            |
| 80 to LB      | Yes                 |  154.21.23.76        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The primary advantage to ansibile is it's scalability

The playbook implements the following tasks:
- The playbook first downloads and installs docker, python3.pip and the pip docker module
- Then the playbook increases its virtual memory and makes it available to the system
- Then the elk container is downloaded and launched
- Finally docker is enabled

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1: 10.1.0.9
- Web2: 10.1.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the beats.yml file to /etc/ansible/playbooks.
- Update the hosts file to include your target machines
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_Playbooks are located in: 
`/etc/ansible/playbooks/`
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ To run ansible on a specific machine add it to the ansible hosts file, generally located in /etc/ansible/hosts. I created an elk and dvwa group to install the relevant packages to the correct machines.

- _Which URL do you navigate to in order to check that the ELK server is running?
`http://\<vmIPaddress>:5601/app/kibana`

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._