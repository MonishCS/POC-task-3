# POC-task-3
FIREWALL AND NETWORKS SECURITY:

✅ Setup:

step 1: Installing & Configuring a Basic Web Server

# Update system and install Apache web server
      ┌──(monish㉿vbox)-[~]
      └─$ sudo apt install -y apache2

# Enable Apache to start on boot
      ┌──(monish㉿vbox)-[~]
      └─$ sudo systemctl enable apache2

# Start Apache service
      ┌──(monish㉿vbox)-[~]
      └─$ sudo systemctl start apache2

# Verify Apache is running
      ┌──(monish㉿vbox)-[~]
      └─$ sudo systemctl status apache2 
      
   apache2.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/apache2.service; enabled; preset: >
   Active: active (running) since Tue 2025-03-18 11:45:11 IST; 30s ago

# Disable UFW to allow all traffic (Very Insecure!)
     ┌──(monish㉿vbox)-[~]
     └─$ sudo ufw disable  
   
   Firewall stopped and disabled on system startup

✅ Exploitation: 

step 2: Brute-Force Attack on SSH

# Check open ports on the system
     ┌──(monish㉿vbox)-[~]
     └─$ sudo netstat -tulnp

# Scan for open ports using Nmap
     ┌──(monish㉿vbox)-[~]
     └─$ sudo nmap -sS -A localhost   

# Check ports are open
      ┌──(monish㉿vbox)-[~]
      └─$ nc -zv localhost 80
      localhost [178.0.0.9] 80 (http) open

✅ Mitigation: 

 step 3: Hardening the System with UFW & iptables

# Enable UFW firewall
      ┌──(monish㉿vbox)-[~]
      └─$ sudo ufw enable           
Firewall is active and enabled on system startup

# Allow only SSH (22) and HTTP (80)
      ┌──(monish㉿vbox)-[~]
      └─$ sudo ufw allow 22/tcp

# Set default UFW rules to block other traffic
      ┌──(monish㉿vbox)-[~]
      └─$ sudo ufw default deny incoming
sudo ufw default allow outgoing

Be sure to update your rules accordingly
Be sure to update your rules accordingly

# Verify UFW rules
       ┌──(monish㉿vbox)-[~]
       └─$ sudo ufw status verbose       
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

# Implement iptables rules to further restrict access
        ┌──(monish㉿vbox)-[~]
        └─$sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT


# Save iptables rules
        ┌──(monish㉿vbox)-[~]
        └─$ sudo netfilter-persistent save                    
run-parts: executing /usr/share/netfilter-persistent/plugins.d/15-ip4tables save
run-parts: executing /usr/share/netfilter-persistent/plugins.d/25-ip6tables save

📌 SUMMARY:









