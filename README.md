🔍 Local Network Reconnaissance Using Nmap & Wireshark
📘 Objective
Gain foundational network security skills by scanning your local network for open ports and analyzing traffic. This helps you understand which devices are exposed, what services they're running, and potential security risks.

🛠 Tools Required
Nmap – Network scanning and port discovery

Wireshark – Packet analysis tool (optional but recommended)

🚦 Part 1: Scan Your Local Network Using Nmap
✅ Step-by-Step Guide
1. Install Nmap
Download and install from the official site:
➡️ https://nmap.org/download.html

Ensure you install the CLI version (and optionally Zenmap GUI).

2. Find Your Local IP Range
Run the following:

On Windows:

bash
Copy
Edit
ipconfig
On macOS/Linux:

bash
Copy
Edit
ifconfig
Note the IPv4 address and subnet mask.
Example: 192.168.181.237 with mask 255.255.255.0 → Subnet: 192.168.181.0/24

3. Run the Nmap Scan
Open Command Prompt as Administrator and run:

bash
Copy
Edit
nmap -sS 192.168.181.0/24
-sS: Stealth TCP SYN scan

/24: Scans all 254 hosts in your subnet

Optionally, increase verbosity:

bash
Copy
Edit
nmap -sS -T4 -v 192.168.181.0/24
4. Analyze the Results
Example output:

text
Copy
Edit
Nmap scan report for 192.168.181.110
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.181.237
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
7070/tcp open  realserver
8000/tcp open  http-alt
8089/tcp open  unknown
Interpretation:

Port 53: DNS server (possibly a router or Pi-hole).

Ports 135, 139, 445: Common on Windows — for file/printer sharing.

Ports 7070, 8000, 8089: Could be local apps, web servers, or custom services.

5. Save Scan Output
bash
Copy
Edit
nmap -sS 192.168.181.0/24 -oN local_scan.txt
📡 Part 2: Analyze Network Traffic with Wireshark (Optional)
✅ Step-by-Step Guide
1. Install Wireshark
Download from:
➡️ https://www.wireshark.org/download.html
Install Npcap when prompted.

2. Launch Wireshark and Start Capture
Open Wireshark (preferably as Administrator).

Choose your active network interface (Wi-Fi or Ethernet).

Click Start Capture (blue shark fin icon).

3. Run Nmap While Capturing
In another window, run your nmap scan. Wireshark will capture all related traffic.

4. Use Display Filters
Some useful filters:

Purpose	Filter
Show TCP traffic	tcp
Filter specific IP	ip.addr == 192.168.181.237
Only SYN packets	tcp.flags.syn == 1 && tcp.flags.ack == 0
Show DNS traffic	dns

5. Stop and Save Capture
Click the red square (stop button) to stop.

Save your capture as .pcapng or .pcap file.

⚠️ Security Notes
Port	Risk Description
135/139/445	SMB-related; can be exploited if not secured or patched
7070/8089	Rarely used; verify they are legitimate
8000	Often development-related — restrict to localhost if possible

✅ Outcome
Identified active devices and open ports

Gained hands-on experience using Nmap and Wireshark

Learned to interpret basic network-level activity

Understood basic risks in exposed services


