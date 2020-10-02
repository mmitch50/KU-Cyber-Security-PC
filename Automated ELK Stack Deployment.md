### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- What aspect of security do load balancers protect? ***Load Balancing plays an important security role as computing moves evermore to the cloud. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. (avinetworks.com)*** 
- What is the advantage of a jump box? ***A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments. (csoonline.com) The jump box also allows for the administrator to control and configure other servers via ssh. This also provides a layer of security because the jump box sits in front of other back-end servers limiting access to the back-end servers.***

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- What does Filebeat watch for? ***Filebeat collects data about the file system.***
- What does Metricbeat record? ***Metricbeat collects machine metrics, such as uptime.***

The configuration details of each machine may be found below.

| Name          | Function         | IP Address     | Operating System                     |
| ------------- | ---------------- | -------------- | ------------------------------------ |
| Jump Box      | Gateway          | 10.0.0.4       | Linux/Ansible                        |
| Web-1         | Web Server       | 10.0.0.5       | Linux/DVWA                           |
| Web-2         | Web Server       | 10.0.0.6       | Linux/DVWA                           |
| Web-3         | Web Server       | 10.0.0.7       | Linux/DVWA                           |
| Elk Stack     | Monitoring Stack | 10.1.0.4       | Linux/Elasticsearch/Logstash/Kilbana |
| Load Balancer | Load Balance     | 168.62.198.225 | Linux                                |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load Balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- ***168.62.198.225***

Machines within the network can only be accessed by the Jump Box using .ssh.
- Which machine did you allow to access your ELK VM? ***The Jump Box***
- _What was its IP address? **40.83.255.1(public), 10.0.0.4 (private)**

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
| ------------- | ------------------- | -------------------- |
| Jump Box      | Yes                 | 24.255.194.212       |
| Web-1         | No                  | 10.0.0.4             |
| Web-2         | No                  | 10.0.0.4             |
| Web-3         | No                  | 10.0.0.4             |
| Elk Stack     | Yes                 | 10.0.0.4             |
| Load Balancer | Yes                 | 168.62.198.225       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? ***Ansible automates and simplifies repetitive, complex, and tedious operations. (www.openio.io)***

The playbook implements the following tasks:

TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

- ***Install docker.io***
- ***Install python3-pip***
- ***Install docker module***
- ***Increase virtual memory***
- ***Use more memory***
- ***Download and launce docker elk container***

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](C:\Users\magni\Documents\KU Cyber Security\Homework Folder\Week 13 Cyber\Sebp-Elk Screen Shot.jpg)

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


![TODO: Update the path with the name of your screenshot of docker ps output] C:\Users\magni\Documents\KU Cyber Security\Homework Folder\Week 13 Cyber\Sebp-Elk Screen Shot.jpg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

List the IP addresses of the machines you are monitoring

- ***Web-1 (10.0.0.5)***
- ***Web-2 (10.0.0.6)***
- ***Web-2 (10.0.0.7)***

We have installed the following Beats on these machines:

Specify which Beats you successfully installed

- ***Filebeats***
- ***Metricbeats***

These Beats allow us to collect the following information from each machine:

TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.

- ***Filebeat is often used to collect log files from very specific files, such as those generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQL databases.***
- ***Metricbeat collects machine metrics, such as uptime and CPU usage.***

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ***install-elk.yml*** file to ***/etc/ansible/install-elk.yml***.
- Update the ***/etc/ansible/hosts*** file to include ***Elk host***.
- Run the playbook, and navigate to ***docker ps*** to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_

​	   Which file is the playbook?

-  ***install-elk.yml***

  Where do you copy it? 

- ***/etc/ansible/install-elk.yml***

  Which file do you update to make Ansible run the playbook on a specific machine? 

- ***/etc/ansible/hosts***

  How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

- ***When you modify the /etc/ansible/hosts file you add Elk as a hosts along with it's ip address. The Elk server is it's own server inside of it's own security group. Filebeat is a log collection tool that's installed on a web server to collect logs. Those logs are then sent over to the Elk Stack server to be displayed among other things.***

  Which URL do you navigate to in order to check that the ELK server is running?

- ***52.165.184.110:5601/app/kibana***

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files ect. ***ansible-playbook /etc/ansible/install-elk.yml***