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

Downloaded the operating system images required to build the Blue Team SOC lab environment.

The following operating systems were selected:

- **Ubuntu Server 22.10 LTS** – Centralized monitoring server (SOC Watchtower)
- **Ubuntu Desktop 22.10 LTS** – Linux endpoint for security monitoring
- **Windows 10 Enterprise** – Windows endpoint for telemetry collection and future threat simulations
  
<img width="1900" height="949" alt="Screenshot 2026-06-27 232816" src="https://github.com/user-attachments/assets/4d20814b-87e7-4d62-902f-b888565ba9ba" />
<img width="1895" height="890" alt="Screenshot 2026-06-27 232845" src="https://github.com/user-attachments/assets/61074dfe-da56-4700-a29c-da976709f43e" />

<img width="1767" height="388" alt="Screenshot 2026-06-27 233349" src="https://github.com/user-attachments/assets/f6d405a7-44a7-40f1-b9ac-3fa4b16a780f" />



Ubuntu **22.10 LTS** was selected because it is a Long-Term Support (LTS) release that closely aligns with operating systems commonly deployed in enterprise environments. Using an LTS release provides long-term security updates, stability, and compatibility with modern security tools that will be installed later in the project.

This operating system selection establishes a realistic foundation for deploying enterprise security monitoring solutions such as Elastic Stack, Kibana, Elastic Agent, and Sysmon.




*(Insert ISO download screenshot here.)*

---

<h3>Step 3 - Create Virtual Machines</h3>

<p>
Created three virtual machines that simulate a small enterprise environment. Each virtual machine serves a specific role within the SOC lab.
</p>

<ul>
  <li><strong>Ubuntu Server</strong> – SOC Watchtower (Monitoring Server)</li>
  <li><strong>Ubuntu Desktop</strong> – Dev OPs Workstation Endpoint</li>
  <li><strong>Windows 10</strong> – Monitored Windows 10 Endpoint</li>
</ul>

<p>
Each virtual machine was configured with dedicated CPU, memory, storage, and networking resources to support future security monitoring and centralized log collection.
</p>

<img width="1913" height="982" alt="Screenshot 2026-06-27 204652" src="https://github.com/user-attachments/assets/c87667e0-6cfe-4f7c-a920-fa58c931e1e2" />

<p><em>Figure 1. Oracle VirtualBox displaying the three virtual machines that make up the Blue Team SOC lab infrastructure.</em></p>
---

### Step 4 - Configure Virtual Networking

Configured the virtual network using NAT, Host-Only, and Internal Network adapters to enable communication between all systems while maintaining isolation from the physical network.

Validated successful communication between machines.

**Screenshot**

*(Insert network configuration screenshot here.)*

---

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
