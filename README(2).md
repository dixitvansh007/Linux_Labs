
# Linux Labs
 
### Lab Project - 3
#### Objective: Linux process management lab
#### DURATION: 2 - 3 Hourse

#### PRE-REQUISITES: 
Oracle VirtualBox or VMWare, Ubuntu installed.

#### Lab 1 : Process Exploration and Identification
####	Objective: 
Understand how processes work in Linux, and how to identify and explore running processes.
#### Task:
    1.	List Running Processes:
    
     # Use ps, top, or htop to list all running processes on the system.
    
     # Understand the difference between ps, top, and htop, and experiment with their options (e.g., ps aux, top -u <username>).
    
    2.	Find a Specific Process:
    
     # Use pgrep to find the PID (process ID) of a specific running process like apache2 or nginx.
     
     # Use pstree to view a tree of processes and their parent-child relationships.

    3.	Investigate Process Details:

     # Use lsof to identify files opened by a process.
     
     # Check the memory usage and CPU time of a process using ps -eo pid,etime,%mem,%cpu,comm.
#### Outcome:
This lab will help you become familiar with the tools and techniques used to explore and gather information about running processes in Linux.
________________________________________
#### Lab 2 : Process Control and Termination
#### Objective: 
Learn how to control, pause, resume, and terminate processes in Linux.
#### Task:
    1.	Send Signals to Processes:
    
     # Use kill to send signals to processes. Try sending a SIGTERM and SIGKILL to terminate a process by PID.
    
     # Use kill -s STOP <PID> and kill -s CONT <PID> to stop and resume a process.
    
    2.	Send Custom Signals:
    
     # Send a SIGINT signal to a running process (e.g., when running a program in the terminal, use Ctrl+C or kill -s SIGINT <PID>).
    
    3.	Test Process Termination:
     
     # Start a process, for example, sleep 300, then find its PID and try to terminate it using kill or kill -9.
#### Outcome: 
You will gain experience in controlling the execution of processes and understand how to manage them using different signals.
________________________________________
#### Lab 3 : Managing Background and Foreground Processes
#### Objective: 
Learn how to run processes in the background and manage jobs effectively.
#### Task:
    1.	Run a Process in the Background:
     
     # Start a process in the background using &, e.g., sleep 100 &.
     
     # Use jobs to see a list of background jobs.

    2.	Bring a Process to the Foreground:
     
     # Use the fg command to bring a background process to the foreground.
    
    3.	Pause and Resume a Process:
     
     # Pause a background process using Ctrl+Z and resume it in the background with the bg command.
    
    4.	Control Multiple Jobs:
     
     # Start multiple jobs in the background and manage them with jobs, fg, and bg.
#### Outcome: 
This lab will help you practice managing processes in the background and foreground, useful for multitasking on the command line.
________________________________________
#### Lab 4 : Monitoring System Performance and Resource Usage
#### Objective: 
Learn how to monitor system resources and analyze processes consuming system resources.
#### Task:
    1.	Monitor CPU Usage:
     
     # Use top or htop to monitor CPU usage in real-time.
     
     # Look for processes consuming high CPU and analyze them.

    2.	Monitor Memory Usage:
     
     # Use free or vmstat to check system memory usage.
     
     # Use ps aux --sort=-%mem to find processes using the most memory.
    
    3.	Disk Usage and I/O Monitoring:

     # Use iotop or dstat to monitor real-time disk I/O usage by processes.
    
    4. Check Process Limits:
     
     # Use ulimit to check and modify user limits on processes (e.g., maximum number of open files).
#### Outcome: 
You will learn to use various monitoring tools to keep track of system performance, identify resource hogs, and improve system efficiency.
________________________________________
#### Lab 5 : Managing Daemons and Background Services

#### Objective: 
Learn how to manage background services and daemons in Linux.
#### Task:
    1.	Start and Stop Services:
     
     # Use systemctl to start, stop, and restart system services (e.g., systemctl start apache2, systemctl stop nginx).

    2.	Enable/Disable Services on Boot:

     # Use systemctl enable and systemctl disable to manage whether a service starts on boot.
 
    3.	Check Service Status:
     
     # Use systemctl status to check the status of a service (e.g., systemctl status apache2).
 
    4.	Managing Logs for Services:

     # Use journalctl to check logs for systemd services.
     
     # Filter logs for specific services or time periods to troubleshoot issues.

#### Outcome: 
This lab will give you hands-on experience with managing system services and daemons, which is crucial for server administration.
________________________________________
#### Lab 6 : Process Scheduling and Prioritization

#### Objective: 
Learn how to control process priority and manage process scheduling.

#### Task:

    1.	Change Process Priority (Nice Value):

     # Use nice to start a new process with a custom priority level (e.g., nice -n 10 command).
     
     # Use renice to change the priority of an already running process by its PID (e.g., renice -n -5 <PID>).

    2.	Scheduling Processes:
     
     # Use at to schedule a one-time task (e.g., at 09:00 to run a script).
     
     # Use cron to schedule recurring tasks by adding entries to /etc/crontab or using crontab -e for user-specific jobs.
    
    3.	Monitor Process Execution Time:
     
     # Use time to measure the execution time of a command or script.

#### Outcome: 
You will learn how to manage process priority and scheduling, useful for optimizing resource allocation and automation of tasks.
________________________________________
#### Lab 7 : Investigating and Debugging Stuck Processes

#### Objective: 
Learn how to identify and debug processes that are stuck or unresponsive.

#### Task:
    1.	Check for Stuck Processes:
    
     # Use ps or top to identify processes that are stuck in a specific state, like D (uninterruptible sleep).
    
    2.	Trace Process Execution:
     
     # Use strace to trace the system calls made by a process (e.g., strace -p <PID>).

    3.	Analyze Process Core Dumps:
    
     # Set up core dumps for processes by configuring /etc/security/limits.conf.
     
     # Use gdb to analyze the core dump of a crashed process.

    4.	Terminate or Kill a Stuck Process:
  
     # Use kill -9 to forcefully terminate a stuck process.

     # Investigate logs (e.g., /var/log/syslog) for additional clues.

#### Outcome: 
This lab will help you practice troubleshooting and debugging stuck or unresponsive processes, a critical skill in system administration.
________________________________________
#### Lab 8 : Containerized Processes with Docker

#### Objective: 
Manage processes within Docker containers and understand container lifecycle.
#### Task:
    
    1.	Start a Docker Container:
     
     # Use docker run to start a container from an image (e.g., docker run -d nginx).
    
    2.	Monitor Processes Inside Containers:
     
     # Use docker exec to run commands like top or ps inside a running container to view its processes.
    
    3.	Stop and Restart Containers:
     
     # Use docker stop and docker restart to manage containerized processes.
    
    4.	Debugging a Stuck Container:
    
     # Use docker logs to view logs and diagnose issues in a container.
    
     # Check container resource usage using docker stats.

#### Outcome: 
You will gain practical experience managing processes inside Docker containers, an essential skill for modern application deployment.
________________________________________
#### Lab 9 : Process Resource Usage and Optimization

#### Objective: 
Optimize processes to improve system performance and reduce resource usage.

#### Task:
    
    1. Analyze Resource Usage:
     
     # Use ps aux --sort=-%mem or top to find the processes consuming the most memory and CPU.
    
    2. Optimize Memory Usage:
     
     # Identify memory leaks or inefficient memory usage with valgrind or smem.
    
    3. Optimize CPU Usage:
    
     # Use cpulimit or nice to adjust CPU resource allocation for specific processes.
    
    4. Tune System Parameters:
     
     # Tune kernel parameters related to process management using sysctl (e.g., sysctl -w vm.swappiness=10).

#### Outcome: 
You will learn to optimize resource usage by fine-tuning processes and system parameters for improved performance.
________________________________________
#### Conclusion:
These Linux process management labs will provide you with practical, hands-on experience in managing processes, monitoring system resources, debugging issues, and optimizing performance. Each lab mimics real-life tasks and will help you develop critical skills for system administration and troubleshooting.
