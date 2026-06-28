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


---

### Step 2 - Download Operating System Images

Downloaded the required ISO images:

- Windows 10
- Ubuntu Server
- Ubuntu Desktop

These operating systems will simulate enterprise endpoints and the centralized monitoring server.

**Screenshot**

*(Insert ISO download screenshot here.)*

---

<h3>Step 3 - Create Virtual Machines</h3>

<p>
Created three virtual machines that simulate a small enterprise environment. Each virtual machine serves a specific role within the SOC lab.
</p>

<ul>
  <li><strong>Ubuntu Server</strong> – SOC Watchtower (Monitoring Server)</li>
  <li><strong>Ubuntu Desktop</strong> – Monitored Linux Endpoint</li>
  <li><strong>Windows 10</strong> – Monitored Windows Endpoint</li>
</ul>

<p>
Each virtual machine was configured with dedicated CPU, memory, storage, and networking resources to support future security monitoring and centralized log collection.
</p>

<img src="https://i.imgur.com/a/tIxA4rG" width="900">

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
