
# Linux Labs

### Lab Project - 6

#### Objective: Linux SSH Connectivity Labs

#### DURATION: 2 - 3 Hourse

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### Lab 1: Basic SSH Connectivity

#### Objective:
•	Learn how to set up and use SSH for basic remote access.

#### Tasks:

     1.	Install OpenSSH Server:
      
      o	Install the OpenSSH server package on a Linux machine (if not already installed).
      
      o	For Ubuntu/Debian-based systems:

bash

Copy code

sudo apt update

sudo apt install openssh-server

      o	For CentOS/RHEL-based systems:

bash

Copy code

sudo yum install openssh-server

     2.	Start and Enable SSH Service:

      o	Start the SSH service and enable it to start at boot.

bash

Copy code

sudo systemctl start ssh

sudo systemctl enable ssh

     3.	Check SSH Service Status:

      o	Verify that the SSH server is running.

bash

Copy code

sudo systemctl status ssh

     4.	Verify SSH Port:
      
      o	Ensure SSH is running on port 22 (default port).

bash

Copy code

sudo netstat -tuln | grep :22

     5.	Connect to the Remote Server via SSH:

      o	From another machine, connect to the SSH server using:

bash

Copy code

ssh username@server_ip

      o	Replace username with a valid user on the remote server and server_ip with the IP address of the server.

     6.	Log Out of SSH Session:

      o	Use the exit command to end the SSH session.

#### Outcome:
You will have established a basic SSH connection and learned how to install and start the SSH server on a Linux machine.
________________________________________
#### Lab 2: SSH Key-Based Authentication

#### Objective:
•	Learn how to configure SSH key-based authentication for more secure and password-less login.

#### Tasks:

     1.	Generate SSH Key Pair:

      o	On your local machine, generate a new SSH key pair using ssh-keygen.

bash

Copy code

ssh-keygen -t rsa -b 4096

      o	Follow the prompts to save the key to a default location (~/.ssh/id_rsa) and optionally set a passphrase.

     2.	Copy Public Key to the Remote Server:

      o	Use ssh-copy-id to copy the public key to the remote server.

bash

Copy code

ssh-copy-id username@server_ip
     
     3.	Test Key-Based Authentication:
      
      o	Attempt to SSH into the remote server. You should be logged in without needing to enter the password.

bash

Copy code

ssh username@server_ip

     4.	Disable Password Authentication (optional):

      o	For additional security, you can disable password-based login on the server by modifying the SSH configuration file (/etc/ssh/sshd_config).

#Set PasswordAuthentication to no.

bash

Copy code

sudo nano /etc/ssh/sshd_config

PasswordAuthentication no

      o	Restart the SSH service:

bash

Copy code

sudo systemctl restart ssh

     5.	Test SSH Connection After Disabling Password Authentication:

      o	Try to SSH into the server again. You should only be able to connect using the SSH key.

#### Outcome:
You will have configured SSH key-based authentication, improving security by avoiding password-based login.
________________________________________
#### Lab 3: SSH Configuration and Security

#### Objective:
•	Learn how to harden and secure your SSH configuration.

#### Tasks:

     1.	Change Default SSH Port:
      
      o	Edit the SSH configuration file (/etc/ssh/sshd_config) to change the default port from 22 to another port (e.g., 2222).

bash

Copy code

sudo nano /etc/ssh/sshd_config

Port 2222

      o	Restart the SSH service:

bash

Copy code

sudo systemctl restart ssh

      o	Test the connection by specifying the new port:

bash

Copy code

ssh username@server_ip -p 2222

     2.	Disable Root Login via SSH:

      o	Modify /etc/ssh/sshd_config to disable direct root login.

bash

Copy code

sudo nano /etc/ssh/sshd_config

PermitRootLogin no

      o	Restart the SSH service:

bash

Copy code

sudo systemctl restart ssh

     3.	Limit SSH Access to Specific Users or Groups:

      o	Use the AllowUsers or AllowGroups directive in /etc/ssh/sshd_config to allow only specific users or groups to log in via SSH.

bash

Copy code

sudo nano /etc/ssh/sshd_config

AllowUsers user1 user2

#or

AllowGroups sshusers

      o	Restart the SSH service:

bash

Copy code

sudo systemctl restart ssh

     4.	Enable SSH Rate Limiting with Fail2Ban:

      o	Install fail2ban to block IP addresses that attempt too many failed SSH login attempts.

bash

Copy code

sudo apt install fail2ban
      
      o	Enable and start the service:

bash

Copy code

sudo systemctl enable fail2ban

sudo systemctl start fail2ban

     5.	Test Security Configurations:

      o	Test that root login is disabled, specific users/groups can log in, and the new SSH port is working correctly.

      o	Attempt SSH connections with invalid passwords to check if fail2ban blocks the IP after multiple failed attempts.

#### Outcome:
You will have configured a secure SSH environment by changing default settings, restricting access, and adding fail2ban protection.
________________________________________
#### Lab 4: SSH Tunneling and Port Forwarding

#### Objective:
•	Learn how to set up SSH tunneling for secure communication between two systems.

#### Tasks:

     1.	Local Port Forwarding:
      
      o	Forward a local port to a remote server. For example, if you have a web server running on port 80 on a remote system, you can forward it to a local port:

bash

Copy code

ssh -L 8080:localhost:80 username@server_ip

      o	After establishing the connection, you can access the remote web server by navigating to http://localhost:8080 on your local browser.
     
     2.	Remote Port Forwarding:
      
      o	Forward a remote port to a local system. For example, if you want to access a service running locally on port 3306 from a remote server, you can use:

bash

Copy code

ssh -R 3306:localhost:3306 username@server_ip

     3.	Dynamic Port Forwarding (SOCKS Proxy):

      o	Set up SSH to create a SOCKS proxy for secure browsing.

bash

Copy code

ssh -D 1080 username@server_ip

      o	Configure your browser to use the SOCKS proxy on port 1080 to securely browse the web.

     4.	Test the Port Forwarding:

      o	For local and remote port forwarding, test the service by connecting to the local forwarded port (e.g., a web server or database).

      o	For SOCKS proxy, verify browsing through the secure tunnel.

#### Outcome:
You will understand and be able to implement SSH tunneling to securely forward ports and set up a SOCKS proxy.
________________________________________
#### Lab 5: SSH Agent and Forwarding

#### Objective:
•	Learn to use SSH agent forwarding for accessing remote servers that require authentication via SSH keys.

#### Tasks:
     
     1.	Start the SSH Agent:

      o	Start the SSH agent on your local machine.

bash

Copy code

eval $(ssh-agent -s)

     2.	Add SSH Key to the Agent:
      
      o	Add your private key to the SSH agent.

bash 

Copy code

ssh-add ~/.ssh/id_rsa
     
     3.	Enable SSH Agent Forwarding:

      o	On your local machine, configure ~/.ssh/config to enable agent forwarding.

bash

Copy code

Host *

  ForwardAgent yes

     4.	Access Remote Server with SSH Agent Forwarding:
      
      o	SSH into the first server and then SSH from that server to a second server. The SSH agent on your local machine will be forwarded, allowing you to use the SSH key for the second connection without needing to copy it over.
      
      o	Example:

bash

Copy code

ssh username@first_server_ip

ssh username@second_server_ip

     5.	Verify SSH Agent Forwarding:

      o	Check if agent forwarding is enabled by running the following on the second server:

bash

Copy code

ssh-add -l

#### Outcome:
You will understand how to use SSH agent forwarding to securely access multiple systems without copying SSH keys.
________________________________________
#### Conclusion:
These SSH connectivity labs cover everything from basic setup to advanced configurations such as key-based authentication, security hardening, SSH tunneling, and agent forwarding. By completing these labs, you'll gain hands-on experience with SSH, which is essential for remote administration, system security, and networking tasks.


