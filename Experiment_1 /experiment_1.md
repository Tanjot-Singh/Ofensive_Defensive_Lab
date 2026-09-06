# EXPERIMENT NO. 1

## Title

**Cybersecurity Lab Ecosystem with Kali Linux (Attacker) and Metasploitable 2 (Victim) for Scanning Vulnerabilities in a Network using Nmap and Nessus**

## Aim

To set up a cybersecurity lab environment using **Kali Linux as the attacker machine** and **Metasploitable 2 as the victim machine**, and to identify open ports, running services, and known vulnerabilities using **Nmap and Nessus**.

## Objectives

* To understand the basic cybersecurity lab environment.
* To identify active hosts and open ports in a network.
* To identify services running on the target machine using Nmap.
* To perform vulnerability assessment using Nessus.

## Requirements

* Kali Linux
* Metasploitable 2
* VirtualBox
* Nmap
* Nessus

## Theory

**NMAP (Network Mapper)** is a network reconnaissance tool used to scan networks to find active hosts or devices and identify open ports and services running on them.

Nmap can be used to:

* Identify active hosts.
* Identify open ports.
* Identify services running on open ports.
* Determine the operating system of a target machine.

**Nessus** is a vulnerability assessment tool used to detect known vulnerabilities in systems and services.

In this experiment, Kali Linux acts as the **attacker machine**, while Metasploitable 2 acts as the **victim/test machine**. Nmap is first used for reconnaissance, followed by Nessus to identify known vulnerabilities.

## Procedure

### Step 1: Check Kali Linux Configuration

Open the Kali Linux terminal and execute:

```bash
cat /etc/os-release
```

**Purpose:** To check which Linux distribution and version is running.

Test internet connectivity using:

```bash
ping google.com
```

**Purpose:** To test internet connectivity and DNS resolution.

Update the package index:

```bash
sudo apt update
```

**Purpose:** To refresh the package index from the configured repositories.

Install the required Linux kernel headers:

```bash
sudo apt install linux-headers-generic
```

**Purpose:** To install the Linux kernel header files matching the currently running kernel.

### Step 2: Identify the Target Machine

Determine the IP address of the Metasploitable 2 virtual machine and ensure that Kali Linux and Metasploitable 2 can communicate with each other.

For this experiment, the target IP used is:

**192.168.1.26**

### Step 3: Perform Nmap Scanning

To scan particular ports such as port 80 and 443:

```bash
nmap -sT -p 80,443 192.168.1.26
```

This performs a TCP connect scan on the specified ports.

To perform a stealth SYN scan:

```bash
nmap -sS 192.168.1.26
```

The `-sS` option performs a SYN scan and is commonly referred to as a stealthy scan.

To identify the operating system of the target:

```bash
nmap -O 192.168.1.26
```

This attempts to determine the operating system running on the target machine.

To view the Nmap help/manual:

```bash
nmap -help
```

### Step 4: Install and Start Nessus

Install the Nessus Debian package using:

```bash
sudo dpkg -i Nessus-10.9.3-debian10_amd64.deb
```

Start the Nessus service:

```bash
/bin/systemctl start nessusd
```

Fetch the Nessus challenge code:

```bash
sudo /opt/nessus/sbin/nessuscli fetch --challenge
```

After this, complete the required Nessus account settings and configuration.

### Step 5: Perform Vulnerability Assessment

Open the Nessus interface and configure a scan for the Metasploitable 2 target.

Enter the target IP address:

**192.168.1.26**

Start the vulnerability scan and analyze the vulnerabilities detected by Nessus.

## Observations

1. Nmap identified the open ports on the target machine.
2. The services associated with the open ports could be identified.
3. Nmap was also used to obtain information about the operating system.
4. Nessus detected known vulnerabilities associated with the services running on the target system.
5. The results demonstrate how reconnaissance can be followed by vulnerability assessment.

## Result

The cybersecurity lab environment was successfully established using **Kali Linux as the attacker** and **Metasploitable 2 as the victim**. Nmap was successfully used to identify open ports, services, and operating-system information, while Nessus was used to identify known vulnerabilities on the target machine.
