# Lab Manual: Phishing Simulation Using Gophish

## Experiment Title
Phishing Simulation Using Gophish

## Aim
To understand how phishing campaigns are designed and executed by creating and running a simulated phishing attack using Gophish in a controlled lab environment.

## Objectives
- Understand the anatomy of a phishing campaign (sending profile, landing page, email template, target group).
- Install and configure Gophish in an isolated lab environment.
- Design a phishing email template and a fake landing page.
- Launch a simulated campaign against test accounts and analyze results.
- Understand detection and defense mechanisms against phishing.

## Prerequisites / Theory

### What is Phishing?
Phishing is a social engineering attack in which an attacker impersonates a trusted entity to trick a victim into revealing sensitive information (credentials, financial data) or executing malicious actions (clicking a link, downloading a file).

### What is Gophish?
Gophish is an open-source phishing framework designed for security awareness training and authorized penetration testing. It allows security teams to:
- Create email templates and sending profiles
- Build landing pages that mimic real login portals
- Manage target groups
- Launch campaigns and track results (opens, clicks, submitted data, reported emails)

### Ethical and Legal Note
> **Warning:** Phishing simulations must only be conducted on systems and accounts you own or have **explicit written authorization** to test. Running this experiment against third-party accounts, public email addresses, or without authorization is illegal and against the policies of most institutions. This lab is to be performed strictly on isolated/sandboxed accounts created for this exercise (e.g., a local mail server or disposable test mailboxes).

## Tools and Software Required
| Tool | Purpose |
|------|---------|
| Gophish (latest release) | Phishing campaign framework |
| Virtual Machine (Kali Linux / Ubuntu) | Isolated lab environment |
| Mailtrap / local SMTP server (e.g., `smtp4dev`, `MailHog`) | Sandboxed email delivery (no real-world sending) |
| Web Browser | Accessing Gophish admin panel and landing page |
| Test email accounts | Simulated victims |

## System Setup

### Step 1: Prepare the Lab Environment
1. Set up an isolated VM (no direct internet-facing mail relay).
2. Install a local SMTP testing tool such as **MailHog** or **smtp4dev** so no real emails leave the lab network.

### Step 2: Install Gophish
```bash
# Download the latest Gophish release (Linux example)
wget https://github.com/gophish/gophish/releases/download/vX.X.X/gophish-vX.X.X-linux-64bit.zip
unzip gophish-vX.X.X-linux-64bit.zip
cd gophish
chmod +x gophish
./gophish
```

### Step 3: Access the Admin Panel
1. Gophish starts an admin interface, by default at:
   ```
   https://127.0.0.1:3333
   ```
2. Retrieve the auto-generated admin password from the terminal output on first run.
3. Log in and immediately change the default password.

## Procedure

### Step 1: Configure a Sending Profile
1. Navigate to **Sending Profiles → New Profile**.
2. Enter the local SMTP server details (e.g., MailHog running on `localhost:1025`).
3. Save the profile and send a test email to confirm connectivity.

### Step 2: Create a Landing Page
1. Navigate to **Landing Pages → New Page**.
2. Import or design an HTML page that mimics a benign login portal (e.g., a test "company portal" page created for this lab — **do not clone real production login pages**).
3. Enable **Capture Submitted Data** to log form submissions (for analysis only, within the sandbox).
4. Optionally enable a redirect to an "awareness" page after submission.

### Step 3: Create an Email Template
1. Navigate to **Email Templates → New Template**.
2. Write a subject line and body that simulates a common pretext (e.g., "Password Expiry Notice", "IT Security Update").
3. Insert the Gophish tracking tag (`{{.TrackingURL}}`) so link clicks can be logged.
4. Save the template.

### Step 4: Create a Target Group
1. Navigate to **Users & Groups → New Group**.
2. Add the test/sandbox email accounts created specifically for this lab (first name, last name, email).

### Step 5: Launch the Campaign
1. Navigate to **Campaigns → New Campaign**.
2. Select the email template, landing page, sending profile, and target group created above.
3. Set the launch date/time.
4. Launch the campaign.

### Step 6: Monitor Results
1. Open the campaign dashboard to observe real-time results:
   - Emails sent
   - Emails opened
   - Links clicked
   - Data submitted
2. Export the results as a report (CSV/PDF) from the dashboard.

## Observations
Record the following in a results table:

| Metric | Count | Percentage |
|--------|-------|------------|
| Emails Sent | | |
| Emails Opened | | |
| Links Clicked | | |
| Credentials Submitted | | |
| Emails Reported (if applicable) | | |

## Analysis
- Identify which pretext/template had the highest click rate.
- Discuss why certain users may have fallen for the simulated attack (urgency, authority, curiosity).
- Correlate results with common phishing psychology principles (social proof, scarcity, fear).

## Defense and Mitigation Discussion
- Importance of **Security Awareness Training** based on simulation results.
- Role of **email authentication protocols**: SPF, DKIM, DMARC in reducing phishing delivery success.
- Browser/email client warnings and link-scanning tools.
- Incident reporting workflow for suspected phishing.

## Conclusion
Summarize how the simulated campaign demonstrated the lifecycle of a phishing attack (template → delivery → landing page → data capture) and how organizations can use such controlled simulations to measure and improve employee resilience against real phishing threats.


## References
- Gophish Official Documentation: https://docs.getgophish.com/
- OWASP Phishing Guidance
