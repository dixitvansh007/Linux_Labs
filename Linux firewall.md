
# Linux Labs

### Lab Project - 8

#### Objective: 
Linux environment management lab

#### DURATION: 4 - 5 Hourse

### Pre-requisites

1. A Linux machine (Ubuntu, CentOS, Debian, or any other distribution).

2. Administrative privileges (root or sudo).

3. Basic knowledge of network services and firewall configuration.

#### Task Objective
The objective of this lab task is to configure a firewall using `iptables` to control network traffic, securing a Linux server from unauthorized access while allowing necessary services to function.

#### Lab Task Steps

#### Part 1: Setup and Verify Networking Configuration
1. **Check network interfaces:**
   - Run `ip addr` or `ifconfig` to identify your network interfaces. Typically, your interface may be `eth0`, `ens33`, `enp0s3`, etc.
   
2. **Verify connectivity:**
   - Make sure you can reach the internet and other machines in your local network:
     - `ping 8.8.8.8` (Google DNS server)
     - `ping <your_gateway_ip>`
     - `ping <another_machine_in_the_network>`
   
3. **Confirm that `iptables` is installed:**
   - Run `iptables --version` to ensure that `iptables` is installed. If not, install it:
     - `sudo apt install iptables` (on Ubuntu/Debian)
     - `sudo yum install iptables` (on CentOS/RHEL)

#### Part 2: Configure a Basic Firewall

1. **Set default policies:**
   - By default, we want to deny all incoming traffic and allow outgoing traffic. This can be set as follows:
   
   ```bash
   sudo iptables -P INPUT DROP      # Block all incoming traffic
   sudo iptables -P FORWARD DROP    # Block forwarding
   sudo iptables -P OUTPUT ACCEPT   # Allow all outgoing traffic
   ```

2. **Allow established connections:**
   - To maintain established connections (like active SSH sessions), you need to allow the related and established connections:
   
   ```bash
   sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
   ```

3. **Allow SSH access (port 22):**
   - You need to allow SSH traffic to connect remotely to the system. This is done by allowing inbound traffic on port 22:
   
   ```bash
   sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
   ```

4. **Allow HTTP/HTTPS (ports 80, 443):**
   - If your server will serve web pages, open HTTP and HTTPS ports:
   
   ```bash
   sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT   # Allow HTTP
   sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT  # Allow HTTPS
   ```

5. **Allow ICMP (ping) requests:**
   - You can allow ICMP traffic for ping functionality:
   
   ```bash
   sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
   ```

6. **Save your rules:**
   - To ensure the firewall rules persist after reboot, save the iptables rules:
   
   ```bash
   sudo iptables-save > /etc/iptables/rules.v4   # For Debian/Ubuntu
   sudo service iptables save                    # For CentOS/RHEL
   ```

#### Part 3: Test Firewall Rules

1. **Test SSH connection:**
   - From another machine, try to SSH into your Linux server. It should work if port 22 is open.
   - `ssh user@<server-ip>`

2. **Test web server access (if applicable):**
   - If you allowed HTTP/HTTPS, try accessing the server from a browser:
     - `http://<server-ip>` for HTTP
     - `https://<server-ip>` for HTTPS (if SSL is configured)

3. **Test ping:**
   - From another machine, ping the server to ensure ICMP traffic is allowed.
     - `ping <server-ip>`

#### Part 4: Enhance Security (Optional)

1. **Block all incoming traffic by default, but allow specific IP ranges:**
   - You can restrict access to the server to specific IP ranges, for example:
   
   ```bash
   sudo iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT    # Allow local network
   sudo iptables -A INPUT -s <trusted-ip> -j ACCEPT        # Allow a specific trusted IP
   sudo iptables -A INPUT -j DROP                         # Block everything else
   ```

2. **Log dropped packets:**
   - You can enable logging to monitor dropped packets:
   
   ```bash
   sudo iptables -A INPUT -j LOG --log-prefix "Dropped Packet: "
   ```

3. **Rate limiting (Optional):**
   - To prevent brute-force attacks on services like SSH, you can limit the number of connections:
   
   ```bash
   sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m limit --limit 5/minute -j ACCEPT
   ```

#### Part 5: Monitor and Manage Firewall

1. **View current firewall rules:**
   - Check the current rules using:
   
   ```bash
   sudo iptables -L
   ```

2. **Flush all rules (reset firewall):**
   - If you want to reset the firewall to its default state (deny all traffic):
   
   ```bash
   sudo iptables -F
   ```

3. **Delete a specific rule:**
   - If you need to delete a specific rule, use:
   
   ```bash
   sudo iptables -D INPUT -p tcp --dport 80 -j ACCEPT
   ```

### Lab Task Completion Criteria:
- You should have successfully set up the firewall with basic rules allowing SSH, HTTP/HTTPS, and ICMP while denying all other traffic.
- You should be able to test and verify that only the allowed traffic can reach the server.
- Bonus if you can configure logging or rate limiting.

Let me know if you need any specific instructions or configurations for your task!


#### Here's a detailed lab task focused on **port blocking**, **IP allowance**, **IP range configuration**, and **protocol allowance** using `iptables` for firewall management. This will help you learn how to manage network traffic based on ports, specific IP addresses, IP ranges, and protocols.

---

### **Lab Task: Configuring Port Blocking, IP Allowance, IP Range, and Protocol Allowance using `iptables`**

#### **Objective:**
- Block/allow specific ports.
- Permit traffic from specific IP addresses.
- Allow traffic only from certain IP ranges.
- Allow/deny specific network protocols.

---

### **Prerequisites:**
1. A Linux machine (Ubuntu, CentOS, or any distribution).
2. Administrative privileges (root or sudo).
3. Basic networking knowledge and the ability to use the terminal.

### **Steps for the Lab Task:**

---

### **1. Verify Current Networking and Firewall Configuration**

1. **Check IP addresses and network interfaces:**
   Run the following command to get a list of network interfaces and their IP addresses.
   ```bash
   ip addr
   ```

2. **Verify if `iptables` is installed:**
   Check if `iptables` is available on your system.
   ```bash
   iptables --version
   ```

3. **Check current `iptables` rules:**
   List all existing rules in the firewall.
   ```bash
   sudo iptables -L
   ```

---

### **2. Block Specific Ports**

You can block incoming traffic on specific ports using `iptables`.

1. **Block incoming traffic on port 80 (HTTP):**
   - This will block all HTTP traffic from reaching your server.
   ```bash
   sudo iptables -A INPUT -p tcp --dport 80 -j DROP
   ```

2. **Block incoming traffic on port 443 (HTTPS):**
   - This will block all HTTPS traffic.
   ```bash
   sudo iptables -A INPUT -p tcp --dport 443 -j DROP
   ```

3. **Verify the changes:**
   - List the rules to ensure that the ports are blocked.
   ```bash
   sudo iptables -L
   ```

4. **Test port blocking:**
   - From a different machine, try to access the blocked port using `curl` or a browser. 
   - You should not be able to reach the server on ports 80 or 443.

---

### **3. Allow Traffic from Specific IP Addresses**

You can allow or deny traffic based on specific IP addresses.

1. **Allow SSH (port 22) only from a specific IP address (e.g., `192.168.1.100`):**
   ```bash
   sudo iptables -A INPUT -p tcp -s 192.168.1.100 --dport 22 -j ACCEPT
   ```

2. **Block SSH access from all other IP addresses:**
   ```bash
   sudo iptables -A INPUT -p tcp --dport 22 -j DROP
   ```

3. **Verify the changes:**
   - List the rules again to confirm the changes.
   ```bash
   sudo iptables -L
   ```

4. **Test the configuration:**
   - Try to SSH into the server from `192.168.1.100` — it should work.
   - Try from any other IP — it should be blocked.

---

### **4. Allow Traffic from a Specific IP Range**

You can also allow traffic from a specific range of IPs. For example, if you want to allow access to your server from a range of IP addresses within the `192.168.1.0/24` subnet:

1. **Allow traffic from the IP range `192.168.1.0/24`:**
   ```bash
   sudo iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 22 -j ACCEPT
   ```

2. **Block traffic from all other IP ranges:**
   ```bash
   sudo iptables -A INPUT -p tcp --dport 22 -j DROP
   ```

3. **Verify the rules:**
   ```bash
   sudo iptables -L
   ```

4. **Test the configuration:**
   - Try accessing the server from an IP within the `192.168.1.0/24` range — it should work.
   - Try accessing from an outside range — it should be blocked.

---

### **5. Allow Specific Protocols (TCP, UDP, ICMP)**

You can allow or block specific network protocols (e.g., TCP, UDP, ICMP).

1. **Allow all incoming ICMP (Ping) requests:**
   ```bash
   sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
   ```

2. **Allow incoming UDP traffic on port 53 (DNS):**
   ```bash
   sudo iptables -A INPUT -p udp --dport 53 -j ACCEPT
   ```

3. **Allow incoming TCP traffic on port 22 (SSH):**
   ```bash
   sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
   ```

4. **Block UDP traffic:**
   - Block all UDP traffic.
   ```bash
   sudo iptables -A INPUT -p udp -j DROP
   ```

5. **Verify the changes:**
   List the rules again to ensure all protocols and ports are configured as needed.
   ```bash
   sudo iptables -L
   ```

6. **Test the configurations:**
   - Test ICMP by pinging the server.
   - Test UDP and TCP services using tools like `nc`, `ping`, or `curl` to ensure proper functionality.

---

### **6. Allow Specific IP and Port Combinations**

You can also allow specific combinations of IP and port.

1. **Allow traffic from `192.168.1.100` to port 22 (SSH):**
   ```bash
   sudo iptables -A INPUT -p tcp -s 192.168.1.100 --dport 22 -j ACCEPT
   ```

2. **Allow traffic from `192.168.1.0/24` to port 80 (HTTP):**
   ```bash
   sudo iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 80 -j ACCEPT
   ```

3. **Block all other IP addresses from accessing port 80:**
   ```bash
   sudo iptables -A INPUT -p tcp --dport 80 -j DROP
   ```

---

### **7. Save and Make `iptables` Rules Persistent**

Once you have configured your firewall rules, make them persistent across reboots.

1. **On Debian/Ubuntu:**
   Save the rules to a file to persist them across reboots.
   ```bash
   sudo iptables-save > /etc/iptables/rules.v4
   ```

2. **On CentOS/RHEL:**
   ```bash
   sudo service iptables save
   ```

---

### **8. Flush All Rules and Reset Firewall**

If you want to reset the firewall to a clean state, you can flush all existing rules.

1. **Flush all `iptables` rules:**
   ```bash
   sudo iptables -F
   ```

2. **Verify that all rules are removed:**
   ```bash
   sudo iptables -L
   ```

---

### **Conclusion:**

By completing this lab task, you have learned how to:
- Block and allow specific ports.
- Allow traffic from particular IP addresses.
- Configure access based on IP ranges.
- Manage firewall rules for specific protocols like TCP, UDP, and ICMP.

You can continue enhancing this configuration by adding more complex rules, logging dropped packets, and creating custom chains to manage traffic in a more fine-grained manner.