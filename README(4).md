
# Linux Labs

### Lab Project - 5

#### Objective: Linux Sudo Access  

#### DURATION: 2 - 3 Hourse

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### Lab 1: Introduction to sudo
#### Objective:
•	Understand how sudo works and gain basic experience using it.

#### Tasks:
    
    1.	Check for sudo Installation:
     
     o  Verify that sudo is installed on your system.

bash

Copy code

which sudo

     o	If it is not installed, you can install it using the following command:

#On Ubuntu/Debian:

bash

Copy code

sudo apt install sudo

#On CentOS/RHEL:

bash

Copy code

sudo yum install sudo

    2.	Verify sudo Access for Current User:
     
     o	Check whether the current user has sudo privileges by running a command that requires superuser permissions, such as:

bash

Copy code

sudo whoami

     o	This should return root if the user has sudo access.

    3.	Execute Commands with sudo:

     o	Run a simple system command with sudo to confirm access. For example, try updating the system package list:

bash

Copy code

sudo apt update    # Ubuntu/Debian

sudo yum update    # CentOS/RHEL

    4.	Exit the sudo Session:

     o	After running the command, exit the root session by simply typing exit or waiting for the session timeout.

#### Outcome:
You will have learned how to check if sudo is installed, verify sudo access, and run commands with sudo.
________________________________________
#### Lab 2: Configuring Sudo Access

#### Objective:
•	Learn how to configure sudo access for specific users by editing the sudoers file.
#### Tasks:
    
    1.	Open the Sudoers File Safely:
     
     o	Use visudo to edit the sudoers file, which is the correct and safest way to modify sudo permissions.

bash

Copy code

sudo visudo

    2.	Grant Sudo Access to a User:

     o	Add a new user to the sudoers file by adding the following line under the user section:

bash

Copy code

username  ALL=(ALL)  ALL

     o	Replace username with the actual username you want to grant sudo access to.

    3.	Grant Sudo Access to a Group:
     
     o	To grant sudo access to all members of a specific group (e.g., admin or sudo), you can add:

bash

Copy code

%groupname  ALL=(ALL)  ALL

     o	Replace groupname with the group you want to grant sudo access to.

    4.	Apply the Changes:

     o	Save and exit the visudo editor (Ctrl+X, then Y to confirm, and Enter to save).
     
     o	The changes will take effect immediately.
    
    5.	Test the New User’s Sudo Access:
     
     o	Log in as the newly added user or use su to switch to that user:

bash

Copy code

su - username

     o	Test sudo access by running:

bash

Copy code

sudo whoami

#### Outcome:
You will be able to grant and manage sudo access for specific users and groups.
________________________________________
#### Lab 3: Understanding and Configuring Sudo Permissions

#### Objective:
•	Understand how to control specific sudo permissions (what commands a user can run with sudo).
#### Tasks:
    
    1.	Limit Sudo Access to Specific Commands:
    
     o	Open the sudoers file and add a rule that only allows a user to run specific commands. For example:

bash

Copy code

username ALL=(ALL) /usr/bin/apt, /usr/bin/dpkg

     o	This allows the user to run only apt and dpkg with sudo.

    2.	Set NOPASSWD for Certain Commands:
     
     o	You can configure sudo to not ask for a password for specific commands. Add the following line in the sudoers file:

bash

Copy code

username ALL=(ALL) NOPASSWD: /usr/bin/apt, /usr/bin/dpkg

     o	This allows the user to run apt and dpkg without entering a password.

    3.	Restrict Access to Only Certain Users:

     o	You can also configure sudo to only allow certain users to execute certain commands. For example:

bash

Copy code

username ALL=(ALL) /usr/bin/apt

%admin  ALL=(ALL) /usr/bin/apt

     o	This allows username and all users in the admin group to run apt.

    4.	Apply the Changes and Test:
     
     o	Save the sudoers file and exit.
     
     o	Test the restricted access by running only the permitted commands as the user.

#### Outcome:
You will learn how to restrict and customize sudo permissions to enhance security.
________________________________________
#### Lab 4: Sudo Logs and Auditing

#### Objective:
•	Learn how to view and manage sudo logs to track user activity.
#### Tasks:

    1.	Check Sudo Logs:
     
     o	By default, sudo logs all commands run to /var/log/auth.log (on Ubuntu/Debian) or /var/log/secure (on CentOS/RHEL).

     o	View the sudo logs by running:

bash

Copy code

sudo cat /var/log/auth.log    # Ubuntu/Debian

sudo cat /var/log/secure      # CentOS/RHEL

    2.	Search for Sudo Commands:

     o	Use grep to search for sudo-related logs:

bash
 
Copy code

sudo grep 'sudo' /var/log/auth.log

    3.	Configure Logging Level:

     o	You can configure the logging level of sudo by modifying the sudoers file.

     o	Add a line to the sudoers file to set the logging level (optional):

bash

Copy code

Defaults logfile="/var/log/sudo.log"

    4.	View the Sudo Log File:

     o	You can now monitor the sudo log file to track all sudo commands used by different users:

bash

Copy code

sudo tail -f /var/log/sudo.log

#### Outcome:
You will have learned how to track and audit sudo usage, which is crucial for security and accountability.
________________________________________
#### Lab 5: Sudo Timeout and Tuning

#### Objective:
•	Learn how to configure the sudo session timeout to improve security.

#### Tasks:
    
    1.	Set the sudo Timeout:
     
     o	The sudo session timeout can be controlled by setting the timestamp_timeout parameter in the sudoers file.

     o	To configure the timeout (in minutes), edit the sudoers file:

bash

Copy code

Defaults timestamp_timeout=10

     o	This means sudo will prompt for a password every 10 minutes.

    2.	Disable the Timeout:

     o	To disable the timeout entirely, set the timeout to 0:

bash

Copy code

Defaults timestamp_timeout=0

    3.	Test the Timeout Configuration:

     o	Run a sudo command and wait for the specified timeout duration. After the timeout, sudo should prompt you for the password again.

    4.	Set a Negative Timeout:
     
     o	If you set timestamp_timeout to -1, sudo will ask for the password every time a sudo command is executed:

bash

Copy code

Defaults timestamp_timeout=-1

#### Outcome:
You will learn how to adjust the timeout settings for sudo, which is important for managing the security of long-running sessions.
________________________________________
#### Lab 6: Troubleshooting Sudo Issues

#### Objective:
•	Learn how to troubleshoot common sudo access issues.

#### Tasks:

    1.	Check User's Group Membership:
     
     o	Verify that the user is part of the correct group (sudo or wheel) by running:

bash

Copy code

groups username

    2.	Verify Permissions in the Sudoers File:

     o	Check for syntax errors in the sudoers file by running:

bash

Copy code

sudo visudo

     o	Ensure that there are no conflicting rules or misconfigurations.
    
    3.	Check Sudo Log for Errors:
     
     o	If a user cannot execute sudo, check the logs for any errors related to authentication.

    4.	Test with Another User:
    
     o	If one user cannot use sudo, try using another user with sudo access to determine if the problem is user-specific.

#### Outcome:
You will gain skills in diagnosing and fixing common sudo configuration problems.
________________________________________
#### Conclusion:
These Sudo Access Labs will equip you with a deep understanding of how to configure, manage, and troubleshoot sudo access on a Linux system. You’ll be able to securely provide limited administrative access, audit user activity, and ensure proper use of system resources. These skills are fundamental for any system administrator responsible for maintaining Linux environments.

