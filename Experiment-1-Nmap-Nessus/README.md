# Experiment 1: Scanning for Vulnerabilities using Nmap and Nessus

## Objective

To use Nmap to identify open ports and Nessus to scan for known vulnerabilities on a test machine.

## Procedure

### Step 1: Configure the Kali Linux and Metasploitable machines

Open the Kali Linux virtual machine as the attacker machine and the Metasploitable virtual machine as the target machine. Configure the network adapter of both virtual machines to Host-only Adapter so that they can communicate with each other within the isolated lab network.

![Step 1 Screenshot](images/step_1.png)

### Step 2: Check the IP address and verify connectivity

Open a terminal in Kali Linux and use ifconfig to identify the IP address of the Kali machine. Then use the ping command with the Metasploitable IP address to verify that the two machines can communicate with each other.

# Commands used :
```bash
ifconfig
ping <Metasploitable-IP>
```

![Step 2 Screenshot](images/step_2.png)

### Step 3: Perform a basic Nmap scan

Use Nmap to scan the Metasploitable machine and identify the open ports and services running on the target.

# Commands used :
```bash
nmap <Metasploitable-IP>
```

The scan output can be used to understand the exposed services on the target.

![Step 3 Screenshot](images/step_3.png)

### Step 4: Download Nessus

Download the Nessus vulnerability scanner required for performing vulnerability assessment of the target machine.

![Step 4 Screenshot](images/step_4.jpeg)

### Step 5: Install and configure Nessus

Install Nessus on the system and complete the required initial setup. After installation, open the Nessus web interface and prepare it for vulnerability scanning.

![Step 5 Screenshot](images/step_5.jpeg)

### Step 6: Scan the target and review the vulnerabilities

Configure Nessus to scan the Metasploitable target and review the scan results after completion. The dashboard displays the vulnerabilities detected on the target along with their severity levels.

![Step 6 Screenshot](images/step_6.png)

## Result

The experiment was successfully performed using Nmap and Nessus. Nmap was used to identify the open ports and services on the Metasploitable target, while Nessus was used to assess the target for known vulnerabilities and display the detected security issues.
