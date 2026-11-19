# Experiment 3: Basic Network Traffic Analysis with Wireshark

## Objective

To capture and examine network packets using Wireshark to detect suspicious activity or cleartext credentials in a simulated network.

## Procedure

### Step 1: Configure the Kali Linux and Metasploitable machines

Open the Kali Linux and Metasploitable virtual machines and configure both to use a Host-only Adapter. Use ifconfig to identify their IP addresses and ping the Metasploitable IP from Kali to verify connectivity.

# Commands:
```bash
ifconfig
ping <Metasploitable-IP>
```

![Step 1 Screenshot](images/step_1.jpg)

### Step 2: Identify the network interface and scan the target

Use ip a on Kali Linux to identify the active network interface, such as eth0. Then perform an Nmap scan against the Metasploitable IP to identify open ports and services.

# Commands:
```bash
ip a
nmap -sS -Pn <Metasploitable-IP>
```

![Step 2 Screenshot](images/step_2.jpg)

### Step 3: Start Wireshark and configure packet capture

Launch Wireshark and select the eth0 interface. Apply a capture filter for the Metasploitable IP address and start capturing network traffic.

# Capture Filter: host (Metasploitable-IP)

![Step 3 Screenshot](images/step_3.jpg)

### Step 4: Generate HTTP and FTP traffic

While Wireshark is capturing, generate traffic from a Kali terminal by accessing the Metasploitable web service and connecting to its FTP service.

Log in to the FTP service using the available lab credentials.

# Commands:
```bash
curl http://<Metasploitable-IP>
ftp <Metasploitable-IP>
```

![Step 4.1 Screenshot](images/step_4.1.jpg)

![Step 4.2 Screenshot](images/step_4.2.jpg)

### Step 5: Identify and inspect FTP packets

Return to Wireshark and locate the captured FTP packets generated during the FTP session. Select an FTP packet and use Follow → TCP Stream to inspect the communication.

![Step 5 Screenshot](images/step_5.jpg)

### Step 6: Analyze the TCP stream

Examine the followed TCP stream to observe the FTP communication, including the credentials transmitted in cleartext.

![Step 6 Screenshot](images/step_6.jpg)

## Result

The experiment demonstrated network traffic capture and analysis using Wireshark, revealing cleartext FTP credentials in the captured TCP stream.
