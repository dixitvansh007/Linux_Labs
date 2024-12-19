
# Linux Labs

### Project - 1 

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### DURATION: 2 - 3 Hourse

#### 1. Create a New User

#### Objective: 
Learn how to create a new user on a Linux system.

#### Task:
    1.	Use the useradd command to create a new user, e.g., john.
    2.	Set a password for the new user using passwd.
    3.	Verify the new user by checking the /etc/passwd file.
•	Expected Outcome: You will learn how to add users and set passwords for them.
   
#### 2. Add a User to a Group
#### Objective: 
Learn how to manage user groups in Linux.
#### Task:
    1.	Create a new group (e.g., developers) using groupadd.
    2.	Add an existing user (e.g., john) to the group using usermod.
    3.	Verify that the user is added to the group by using the groups command.

•	Expected Outcome: You will learn to add users to groups and understand group management.

#### 3. Modify User Information
#### Objective: Learn how to modify user attributes.
#### Task:
    1.	Modify the home directory for user john using usermod.
    2.	Change the default shell for john to /bin/bash.
    3.	Change the user’s full name using the chfn command.
    4.	Verify the changes using grep john /etc/passwd.

•	Expected Outcome: You will practice modifying user information.
#### 4. Delete a User
#### Objective: 
Learn how to safely remove users from the system.
#### Task:
    1.	Delete the user john using the userdel command.
    2.	Ensure the user's home directory and files are removed by using userdel -r.
    3.	Verify the deletion by checking the /etc/passwd file.

•	Expected Outcome: You will learn how to remove a user and associated files.
#### 5. Create a System User
#### Objective: Learn how to create system users.
#### Task:
    1.	Create a system user for an application (e.g., www-data for web server users).
    2.	Ensure that the system user has no login shell and that no home directory is created by using useradd -r.
    3.	Verify the user is created with no login shell by inspecting /etc/passwd.

•	Expected Outcome: You will understand how to create system users that are not meant for interactive logins.
#### 6. Managing User Permissions
#### Objective: Learn how to manage file permissions for users.
#### Task:
    1.	Create a new user alice.
    2.	Create a directory /home/alice_data and set it as rw for the owner, r for the group, and no permissions for others.
    3.	Add alice to the group that has access to this directory.
    4.	Verify the permissions using ls -l.

•	Expected Outcome: You will learn how to manage file and directory permissions based on user groups.
#### 7. Password Aging and Expiry
#### Objective: Learn how to set password policies for users.
#### Task:
    1.	Set a password expiration period of 90 days for user alice using chage.
    2.	Set a warning period to notify the user 7 days before the password expires.
    3.	Verify the changes using chage -l alice.
    
•	Expected Outcome: You will learn how to set and manage password expiration and aging policies.
#### 8. Lock and Unlock User Accounts
#### Objective: 
Learn how to lock and unlock user accounts.
#### Task:
    1.	Lock the user account alice by using the passwd -l command.
    2.	Verify that the account is locked by trying to log in as alice.
    3.	Unlock the account using the passwd -u command.
    4.	Verify the account is unlocked by trying to log in again.

•	Expected Outcome: You will understand how to temporarily disable and re-enable user accounts.
#### 9. Create and Manage Sudo Access
#### Objective: 
Learn how to provide and manage administrative privileges for users.
#### Task:
    1.	Add a user bob to the sudo group, allowing bob to execute commands as root.
    2.	Test by logging in as bob and running a command with sudo.
    3.	Optionally, restrict bob’s sudo access by editing the /etc/sudoers file using visudo (e.g., allow only apt-get commands).

•	Expected Outcome: You will learn how to grant and restrict sudo access.
#### 10. Set Up User Environment Variables
#### Objective: 
Learn how to set and customize user environment variables.
#### Task:
    1.	Modify the .bashrc file for a user (alice) to set a custom environment variable (e.g., MYVAR=HelloWorld).
    2.	Have the user log out and log back in, then check the environment variable using echo $MYVAR.

•	Expected Outcome: You will practice setting environment variables that affect user sessions.

#### 11. Create and Manage User Quotas
#### Objective: 
Learn to set disk usage limits for users.
#### Task:
    1.	Enable disk quotas on a specific file system (/home).
    2.	Set a soft and hard limit for user alice (e.g., 1 GB for soft, 1.5 GB for hard).
    3.	Test the quota by attempting to exceed the disk usage limit.
    4.	Verify the user’s quota using the quota command.

•	Expected Outcome: You will understand how to limit user disk space usage on a per-user basis.

#### 12. Configure User Shells
#### Objective: 
Learn how to configure a specific shell for users.
#### Task:
    1.	Create a user eve and set their default shell to /bin/zsh using usermod -s /bin/zsh.
    2.	Verify that eve’s default shell is set to Zsh by checking /etc/passwd.
    3.	Log in as eve and confirm the shell is now Zsh.

•	Expected Outcome: You will learn how to change a user’s login shell and verify the change.
 
#### 13. Automate User Creation with a Script
#### Objective: 
Write a script to automate the creation of users and groups.

#### Task:
    1.	Write a Bash script that takes a username and a group as input.
    2.	Create the user, create the group if it does not exist, and add the user to the group.
    3.	Set a default password for the new user and notify the administrator by email.

•	Expected Outcome: You will automate user and group management tasks, which is useful for system administration.

#### 14. User Account Audit
#### Objective: 
Learn how to audit user accounts.
#### Task:
    1.	Write a script to list all users who have not logged in for the past 90 days.
    2.	Optionally, send an email alert for these inactive accounts.
    3.	Disable inactive accounts by locking them (passwd -l).

•	Expected Outcome: You will practice auditing user activity and manage inactive accounts.

#### 15. Check and Modify User File Permissions
#### objective: 
Learn to manage file permissions and ownership for users.
#### Task:
    1.	Create a file /home/alice/important_file.txt.
    2.	Change the ownership of the file to the user alice using chown.
    3.	Set the file permissions so that only alice has read and write access, while others have no access.
    4.	Verify the permissions using ls -l.

•	Expected Outcome: You will gain experience in changing file ownership and setting permissions.
________________________________________
#### Conclusion
These Linux user management tasks provide hands-on experience with essential administrative tasks, including user creation, group management, permissions, password policies, and user auditing. Completing these tasks will help you develop strong skills in managing users and securing your Linux systems.



