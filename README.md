# Blue Team SOC Home Lab - Infrastructure Deployment

## Objective

The objective of this project was to design and deploy the foundational infrastructure for a Blue Team Security Operations Center (SOC) home lab. This included creating a virtual environment with Windows and Linux endpoints, configuring enterprise-style networking, validating communication between systems, and enabling remote administration of the monitoring server. This infrastructure will serve as the foundation for future projects involving centralized logging, SIEM deployment, endpoint monitoring, threat detection, and incident response.

---

## Skills Learned

- Deployed and configured multiple virtual machines using Oracle VirtualBox.
- Installed and configured Windows 10, Ubuntu Desktop, and Ubuntu Server.
- Designed and configured virtual networking using NAT, Host-Only, and Internal Network adapters.
- Verified connectivity between systems using ICMP (ping).
- Configured SSH for secure remote administration of the Ubuntu Server.
- Developed practical Linux server administration skills.
- Improved understanding of enterprise network architecture and endpoint communication.
- Gained experience troubleshooting virtual networking and connectivity issues.

---

## Tools Used

### Virtualization

- Oracle VirtualBox

### Operating Systems

- Windows 10
- Ubuntu Server
- Ubuntu Desktop

### Networking

- NAT Networking
- Host-Only Networking
- Internal Networking
- ICMP (Ping)
- SSH

### Administration

- Linux Terminal
- Windows Command Prompt

---

# Lab Architecture

```
                     Host Computer
                           │
                  Oracle VirtualBox
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        │                  │                  │
 Windows 10 VM      Ubuntu Desktop VM    Ubuntu Server VM
 (Monitored Host)   (Monitored Host)      (SOC Watchtower)
                           │
                  SSH Remote Management
```

---

## Steps

### Step 1 - Install Oracle VirtualBox

Installed Oracle VirtualBox to provide the virtualization platform used to build the SOC environment.


<img width="1496" height="924" alt="Screenshot 2026-06-27 232056" src="https://github.com/user-attachments/assets/b5cc6a73-6e90-425b-8bc9-3533bea9fb81" />
---

### Step 2 - Download Operating System Images

Downloaded the operating system images required to build the Blue Team SOC home lab environment.

The following operating systems were selected:

- **Ubuntu Server 22.10** – Centralized monitoring server (SOC Watchtower)
- **Ubuntu Desktop 22.10** – Linux endpoint for monitoring and future security testing
- **Windows 10 Enterprise** – Enterprise Windows endpoint used for endpoint telemetry collection, log generation, and future attack simulations

To obtain the Windows 10 Enterprise ISO directly from Microsoft's website, I used the browser's **Developer Tools** to emulate a mobile device. Microsoft provides a direct ISO download option when the site is accessed from a mobile or tablet browser, eliminating the need for the Media Creation Tool. This allowed me to download the official Windows 10 Enterprise installation image for use in the lab.

### Windows 10 Enterprise Download Process

**Figure 2.1** – Opened the Microsoft Windows download page and launched the browser's **Developer Tools (Inspect Element)**.

<img width="1900" height="949" alt="Opened Developer Tools" src="https://github.com/user-attachments/assets/4d20814b-87e7-4d62-902f-b888565ba9ba" />

---

**Figure 2.2** – Enabled **Device Toolbar** (mobile/tablet emulation) to access Microsoft's direct Windows 10 Enterprise ISO download page.

<img width="1895" height="890" alt="Enabled Device Emulation" src="https://github.com/user-attachments/assets/61074dfe-da56-4700-a29c-da976709f43e" />

---

**Figure 2.3** – Successfully accessed the official Windows 10 Enterprise ISO download page and selected the Windows 10 Enterprise edition for download.

<img width="1767" height="388" alt="Windows 10 Enterprise Download" src="https://github.com/user-attachments/assets/f6d405a7-44a7-40f1-b9ac-3fa4b16a780f" />

> **Outcome:** Successfully downloaded the official Windows 10 Enterprise ISO, Ubuntu Server 22.10, and Ubuntu Desktop 22.10 installation images required to build the Blue Team SOC home lab infrastructure.



Ubuntu **22.10 LTS** was selected because it is a Long-Term Support (LTS) release that closely aligns with operating systems commonly deployed in enterprise environments. Using an LTS release provides long-term security updates, stability, and compatibility with modern security tools that will be installed later in the project.

This operating system selection establishes a realistic foundation for deploying enterprise security monitoring solutions such as Elastic Stack, Kibana, Elastic Agent, and Sysmon.




<img width="1404" height="858" alt="Screenshot 2026-06-27 233757" src="https://github.com/user-attachments/assets/4a15f88d-08ab-46c6-a124-07cb59ab037a" />

---

<h3>Step 3 - Create Virtual Machines</h3>

<p>
Created three virtual machines to simulate a small enterprise environment. Each virtual machine serves a dedicated role within the Blue Team SOC lab, allowing the separation of monitored endpoints from the centralized monitoring infrastructure.
</p>

<ul>
  <li><strong>Ubuntu Server</strong> – SOC Watchtower (Centralized Monitoring Server)</li>
  <li><strong>Ubuntu Desktop</strong> – DevOps Workstation used to administer and manage the SOC infrastructure.</li>
  <li><strong>Windows 10 Enterprise</strong> – Monitored Windows endpoint used to generate telemetry, security events, and future attack simulations.</li>
</ul>

<p>
Each virtual machine was configured with dedicated CPU, memory, storage, and networking resources to closely resemble a small enterprise environment. This architecture establishes the foundation for centralized logging, endpoint monitoring, and future threat detection exercises.
</p>

<hr>

<h4>Figure 3.1 – DevOps Workstation Configuration</h4>

<p>
Configured the Ubuntu Desktop virtual machine, which will serve as the primary administrative workstation for managing the SOC infrastructure.
</p>

<img width="900" alt="DevOps Workstation Configuration" src="https://github.com/user-attachments/assets/56998fbe-e080-4b24-93de-36aa18da2f31" />

<br><br>

<h4>Figure 3.2 – SOC Watchtower Configuration</h4>

<p>
Configured the Ubuntu Server virtual machine, which will function as the centralized monitoring server responsible for hosting the future Elastic Stack and SIEM components.
</p>

<img width="900" alt="SOC Watchtower Configuration" src="https://github.com/user-attachments/assets/59806968-5fbe-41d5-a5f1-22da662d6923" />

<br><br>

<h4>Figure 3.3 – Windows 10 Enterprise Configuration</h4>

<p>
Configured the Windows 10 Enterprise virtual machine, which will serve as the monitored Windows endpoint for endpoint telemetry collection, event logging, and future security testing.
</p>

<img width="900" alt="Windows 10 Enterprise Configuration" src="https://github.com/user-attachments/assets/65bf7c34-2e86-426e-9588-f46eb9febf92" />

<hr>

<p>
<strong>Outcome:</strong> Successfully created and configured all three virtual machines required for the Blue Team SOC lab. The environment is now prepared for network configuration, operating system installation, and the deployment of centralized monitoring tools in subsequent phases.
</p>

## Step 4 - Install and Configure the SOC Watchtower (Ubuntu Server)

The Ubuntu Server virtual machine was configured to serve as the **SOC Watchtower**, which will act as the centralized monitoring server throughout the remainder of the lab.

During installation, the server was configured with a dedicated hostname, administrative account, OpenSSH Server, and networking settings to enable remote administration and future deployment of the Elastic Stack.

---

### Figure 4.1 – Select Installation Language

Selected **English** as the installation language before beginning the Ubuntu Server installation.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.2 – Proxy Configuration

No HTTP proxy was required for this lab environment, so the proxy configuration was left blank.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.3 – Installer Update

Allowed Ubuntu to download the latest version of the installer before continuing the installation process. Updating the installer ensures the latest fixes and installation improvements are applied.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.4 – Server Profile Configuration

Configured the server with the following information:

- Hostname: **ubuntuwatchtowerlive**
- Username: **defender__cole**

This server will later host the centralized monitoring and security infrastructure.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.5 – OpenSSH Server Installation

Enabled the **OpenSSH Server** package during installation.

Installing OpenSSH allows the server to be managed remotely from another machine without requiring direct access through VirtualBox.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.6 – Ubuntu Server Installation Complete

Ubuntu successfully completed installation and configured all required system packages.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.7 – First Boot

After rebooting, Ubuntu successfully initialized all required system services and completed the boot process.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.8 – Initial Login

Successfully authenticated using the administrator account created during installation.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.9 – Ubuntu Server Dashboard

Verified successful login and confirmed the operating system version, network configuration, and system health.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.10 – Verify Network Interfaces

Executed the following command to display all available network interfaces.

```bash
ip a
```

Confirmed the server received both NAT and Host-Only IP addresses, allowing internet connectivity and communication with other virtual machines.

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

### Figure 4.11 – Connectivity Testing

Validated communication between the SOC Watchtower and other systems using ICMP.

Successful connectivity tests included:

- Host Computer
- Ubuntu Desktop (DevOps Workstation)
- Windows 10 Workstation

During testing, the Windows workstation initially failed to respond due to Windows Firewall blocking ICMP requests.

After enabling ICMP Echo Requests within Windows Defender Firewall, connectivity was successfully established.

<img width="900" src="https://github.com/user-attachments/assets/..." />

<img width="900" src="https://github.com/user-attachments/assets/..." />

<img width="900" src="https://github.com/user-attachments/assets/..." />

<img width="900" src="https://github.com/user-attachments/assets/..." />

---

## Outcome

Successfully deployed and configured the Ubuntu Server SOC Watchtower, enabled secure remote administration through OpenSSH, verified network interfaces, and confirmed communication with all virtual machines.

The monitoring server is now prepared for deployment of the Elastic Stack, centralized log collection, and future security monitoring activities.

### Step 5 - Install Ubuntu Server

Installed Ubuntu Server to serve as the centralized monitoring server that will later host the SOC monitoring stack.

Configured:

- Administrative account
- Network settings
- System updates

Verified successful installation.

**Screenshot**

*(Insert Ubuntu Server screenshot here.)*

---

### Step 6 - Install Ubuntu Desktop

Installed Ubuntu Desktop to simulate a monitored Linux workstation.

Verified successful installation and desktop functionality.

**Screenshot**

*(Insert Ubuntu Desktop screenshot here.)*

---

### Step 7 - Install Windows 10

Installed Windows 10 to represent an enterprise Windows endpoint that will later generate security events for monitoring.

Verified successful installation.

**Screenshot**

*(Insert Windows installation screenshot here.)*

---

### Step 8 - Verify Network Connectivity

Performed connectivity testing using ICMP (ping).

Verified:

- Endpoint communication
- Host communication
- Proper virtual network configuration

**Screenshot**

*(Insert successful ping screenshot here.)*

---

### Step 9 - Configure SSH Remote Access

Configured SSH on the Ubuntu Server and successfully connected remotely from the host machine.

This allows remote administration of the monitoring server without direct console access.

**Screenshot**

*(Insert SSH terminal screenshot here.)*

---

## Outcome

Successfully deployed the foundational infrastructure for a Blue Team SOC home lab consisting of multiple virtual machines, enterprise-style virtual networking, and remote server administration.

This environment is now ready for the next phase of the project, which will include:

- Elastic Stack
- Kibana
- Elastic Agent
- Sysmon
- Centralized log collection
- Endpoint telemetry
- Detection engineering
- Threat hunting
- Incident response
