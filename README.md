## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(Images/NETWORKDIAGRAM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  - my-playbook.yml
  - ELK-VM.yml
  - Ansible.cfg
  - filebeat-config.yml
  - filebeat-playbook.yml
  - metricbeat-config.yml
  - metricbeat-playbook.yml
  - hosts

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? Load balancers protect the network security and its traffic. It also precents against DDoS attacks. What is the advantage of a jump box? A jump box allows you to access and manage your devices in a set security area.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the applications and system logs.
- What does Filebeat watch for? Filebeat monitors logs and locations
- What does Metricbeat record? Metricbeat monitors the servers.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JumpBox  | Gateway  | 10.0.0.4   | Linux            |
| Web 1    |   VM     | 10.0.0.5   | Linux            |
| Web 2    |   VM     | 10.0.0.6   | Linux            |
| Web 3    |   VM     | 10.0.0.7   | Linux            |
|ELK-SERVER|   VM     | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses: 68.251.57.208

Machines within the network can only be accessed by JumpBox SSH.
- Which machine did you allow to access your ELK VM? JumpBox What was its IP address? 138.91.143.216

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 138.91.143.216 & 10.0.0.4    |
| Web 1    | No                  | 10.0.0.5             |
| Web 2    | No                  | 10.0.0.6             |
| Web 3    | No                  | 10.0.0.7             |     
|ELK-SERVER| Yes                 | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? The main advantage is efficiency when you have to make changes. It allows you to make a change on one machine and it will transfer to all the rest that are connected.

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- First, we create a new virtual network with a different region than our original machine in Azure and add it to the same resource group as our original machine. We then create a peering to connect the two. 
- Next, we create a new virtual machine that has 2vCPUs and 4DiB of memory into our new virtual network. Then, we add the IP address of our new virtual machine to the Ansible hosts file in the JumpBox.
- Afterwards, we create a playbook that will install Docker.io, python3-pip, Docker Python Module, and create a container. Once completed, we will run the playbook and the container will launch. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/dockerps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring: 10.0.0.4, 10.0.0.5, 10.0.0.6, 10.0.0.7, 10.1.0.4

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed: Filebeat & Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
- Filebeat monitors logs and locations. It collects log files, location files, and log events. An example would be any input. Metricbeat monitors manipulated information in system files. An example would be an Elasticsearch cluster or any data with numbers.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible configuration file to /etc/ansible to run playbooks.
- Update the Ansible host file to include all internal IP addresses of your web servers and ELK server.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? The ELK-VM.yml is the playbook and is copied to /etc/ansible
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? The file that needs to be updated is ELK-VM.yml and in order to specify, you use the IP address of the designated server.
- _Which URL do you navigate to in order to check that the ELK server is running? http://[ELK-SERVER-ip]:5601/app/kibana/home
