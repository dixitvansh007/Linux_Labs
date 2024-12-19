
# Linux Labs

### Lab Project - 2

#### Objective: Shell scripting for Automation labs

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### DURATION: 2 - 3 Hourse

#### Lab 1: Automating System Backup
#### Objective:
•	Learn to create a shell script that automates the process of backing up files and directories.
#### Tasks:
    1.	Create a Backup Script:
     o	Create a script called backup.sh to automate the backup of a directory.

bash

Copy code

nano backup.sh
  
     o	Add the following content to the script:

bash

Copy code

#!/bin/bash

#Source directory to backup

SRC_DIR="/home/user/data"

#Destination directory where backups will be stored

BACKUP_DIR="/home/user/backups"

#Date format for the backup filename

DATE=$(date +%F)

#Backup filename

BACKUP_FILE="backup_$DATE.tar.gz"


#Create a backup

tar -czf $BACKUP_DIR/$BACKUP_FILE $SRC_DIR

echo "Backup of $SRC_DIR completed successfully and stored in $BACKUP_DIR/$BACKUP_FILE"

    2.	Make the Script Executable:

bash

Copy code

chmod +x backup.sh

    3.	Run the Backup Script:
     o	Run the script to create a backup:

bash

Copy code

./backup.sh

    4.	Schedule the Backup Using Cron:
     o	Open the crontab file to schedule a daily backup.

bash

Copy code

crontab -e
     
     o	Add the following cron job to run the backup script every day at 2 AM:

bash

Copy code

0 2 * * * /path/to/backup.sh

#### Outcome:
You will automate the backup of files using a shell script, and schedule it to run daily using cron.
________________________________________
#### Lab 2: Automating System Updates
#### Objective:
•	Automate system package updates using a shell script to ensure the system is always up to date.
#### Tasks:
    1.	Create the Update Script:
     o	Create a script called auto_update.sh to automate system updates for Debian-based systems (e.g., Ubuntu) or Red Hat-based systems (e.g., CentOS).

bash

Copy code

nano auto_update.sh
     
     o	Add the following content for Debian/Ubuntu:

bash

Copy code

#!/bin/bash

#Update package list

sudo apt update

#Upgrade installed packages

sudo apt upgrade -y

#Clean up unused packages

sudo apt autoremove -y

echo "System update completed."

    o	For Red Hat/CentOS, replace the content with:

bash

Copy code

#!/bin/bash

#Update package list and upgrade packages

sudo yum update -y

#Clean up unused packages

sudo yum autoremove -y

echo "System update completed."

    2.	Make the Script Executable:

bash

Copy code

chmod +x auto_update.sh
    
    3.	Run the Update Script:
     o	Run the script to perform an update:

bash

Copy code

./auto_update.sh

    4.	Schedule Automatic Updates Using Cron:
     o	Open the crontab file to schedule the update script to run weekly.

bash

Copy code

crontab -e

     o	Add the following cron job to run the script every Sunday at 3 AM:

bash

Copy code

0 3 * * SUN /path/to/auto_update.sh

#### Outcome:
You will automate the process of keeping your system updated by creating a shell script and scheduling it to run automatically using cron.
________________________________________
#### Lab 3: Automating Disk Space Monitoring
#### Objective:
•	Automate disk space monitoring and send an alert when disk space usage exceeds a threshold.
#### Tasks:
    1.	Create a Disk Space Monitoring Script:
     o	Create a script called disk_space_monitor.sh to check disk usage and send an email alert if usage exceeds 80%.

bash

Copy code

nano disk_space_monitor.sh
     
     o	Add the following content:

bash

Copy code

#!/bin/bash

#Set the threshold for disk space usage

THRESHOLD=80

#Get the current disk usage percentage

DISK_USAGE=$(df / | grep / | awk '{ print $5 }' | sed 's/%//g')

#Check if disk usage is above the threshold

if [ $DISK_USAGE -gt $THRESHOLD ]; then

echo "Warning: Disk usage is above $THRESHOLD%. 

Current usage: $DISK_USAGE%" | mail -s "Disk Space 

Alert" user@example.com

else

echo "Disk usage is below $THRESHOLD%. Current usage: $DISK_USAGE%"

fi

    2.	Make the Script Executable:

bash

Copy code

chmod +x disk_space_monitor.sh

    3.	Run the Script:
    
     o	Run the script to check disk usage:

bash

Copy code

./disk_space_monitor.sh

    4.	Schedule the Monitoring Script Using Cron:

     o	Open the crontab file to schedule the script to  run every day at 6 AM:

bash

Copy code

crontab -e
     
     o	Add the following cron job:

bash

Copy code

0 6 * * * /path/to/disk_space_monitor.sh

#### Outcome:
You will automate disk space monitoring and set up an email alert when disk usage exceeds a predefined threshold.
________________________________________
#### Lab 4: Automating Log Rotation
#### Objective:
•	Automate the process of rotating logs to avoid disk space issues.
#### Tasks:
    1.	Create a Log Rotation Script:
     o	Create a script called log_rotation.sh to rotate log files in a directory.

bash

Copy code

nano log_rotation.sh
     
     o	Add the following content:

bash

Copy code

#!/bin/bash

#Directory where logs are stored

LOG_DIR="/var/log/myapp"

#Backup directory for rotated logs

BACKUP_DIR="/var/log/myapp/backup"

#Log file to rotate

LOG_FILE="myapp.log"

#Create backup directory if it doesn't exist

mkdir -p $BACKUP_DIR

#Rotate the log file by renaming it with a timestamp

mv $LOG_DIR/$LOG_FILE $BACKUP_DIR/$LOG_FILE-$(date +%F-%T)

#Create a new empty log file

touch $LOG_DIR/$LOG_FILE

#Set permissions on the new log file

chmod 644 $LOG_DIR/$LOG_FILE

echo "Log rotation completed."

    2.	Make the Script Executable:

bash

Copy code

chmod +x log_rotation.sh

    3.	Run the Script:
     o Run the script to perform log rotation:

bash

Copy code

./log_rotation.sh

    4.	Schedule Log Rotation Using Cron:
     o	Open the crontab file to schedule the log rotation to run every day at midnight:

bash

Copy code

crontab -e

     o	Add the following cron job:

bash

Copy code

0 0 * * * /path/to/log_rotation.sh

#### Outcome:
You will automate log file rotation and archiving to ensure that log files do not consume excessive disk space.
________________________________________
#### Lab 5: Automating User Account Management

#### Objective:
•	Automate the process of adding and removing users in Linux.
#### Tasks:
    1.	Create a Script to Add Users:
     o	Create a script called add_user.sh to automate adding a user to the system.

bash

Copy code

nano add_user.sh

     o	Add the following content:

bash

Copy code

#!/bin/bash

#Check if username is provided

if [ -z "$1" ]; then

echo "Error: Please provide a username."

exit 1

fi

#Add user to the system

sudo useradd $1

#Set password for the new user

echo "Enter password for user $1:"

sudo passwd $1

echo "User $1 has been added successfully."

    2.	Make the Script Executable:

bash

Copy code

chmod +x add_user.sh

    3.	Run the Script:
     
     o	Run the script to add a new user:

bash

Copy code

./add_user.sh newuser

    4.	Create a Script to Remove Users:
     o	Create a script called remove_user.sh to automate removing a user.

bash

Copy code

nano remove_user.sh

     o	Add the following content:

bash

Copy code

#!/bin/bash

#Check if username is provided

if [ -z "$1" ]; then

echo "Error: Please provide a username."

exit 1

fi

#Remove user from the system

sudo userdel $1

echo "User $1 has been removed successfully."

    5.	Run the Script to Remove a User:

bash

Copy code

./remove_user.sh newuser

#### Outcome:
You will automate user account management, including adding and removing users via shell scripts.
________________________________________
#### Lab 6: Automating File Cleanup
#### Objective:
•	Automate the deletion of old files in a directory to free up disk space.
#### Tasks:
    1.	Create a Cleanup Script:
     o	Create a script called file_cleanup.sh to remove files older than 30 days.

bash

Copy code

nano file_cleanup.sh

     o	Add the following content:

bash

Copy code

#!/bin/bash

#Directory to clean up

TARGET_DIR="/home/user/temp"

#Find and delete files older than 30 days

find $TARGET_DIR -type f -mtime +30 -exec rm -f {} \;

echo "Old files have been deleted from $TARGET_DIR."

    2.	Make the Script Executable:

bash

Copy code

chmod +x file_cleanup.sh

    3.	Run the Cleanup Script:
     o	Run the script to clean up old files:

bash

Copy code

./file_cleanup.sh

    4.	Schedule the Cleanup Script Using Cron:
     o	Open the crontab file to schedule the cleanup script to run weekly.

bash

Copy code

crontab -e

     o	Add the following cron job:

bash

Copy code

0 3 * * SUN /path/to/file_cleanup.sh

#### Outcome:
You will automate the cleanup of old files to keep the system free of unnecessary data.
________________________________________
#### Conclusion:
By completing these Shell Scripting for Automation Labs, you will be able to automate many system administration tasks such as backups, system updates, log rotations, disk space monitoring, and user management. These skills are essential for increasing efficiency and minimizing human error in managing Linux systems
