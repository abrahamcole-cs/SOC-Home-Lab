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

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_20_48_40" src="https://github.com/user-attachments/assets/e3954955-f358-4797-9182-23ba23fc5caf" />

---

### Figure 4.2 – Proxy Configuration

No HTTP proxy was required for this lab environment, so the proxy configuration was left blank.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_20_54_59 proxy" src="https://github.com/user-attachments/assets/3a854676-baf3-4c89-bc0d-ddb1ee95abc3" />

---

### Figure 4.3 – Installer Update

Allowed Ubuntu to download the latest version of the installer before continuing the installation process. Updating the installer ensures the latest fixes and installation improvements are applied.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_20_55_53 update server" src="https://github.com/user-attachments/assets/6d127675-6c10-4f5c-abb8-6de8eb1704ea" />

---

### Figure 4.4 – Server Profile Configuration

Configured the server with the following information:

- Hostname: **ubuntuwatchtowerlive**
- Username: **defender__cole**

This server will later host the centralized monitoring and security infrastructure.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_00_00" src="https://github.com/user-attachments/assets/92dd1586-7293-410b-8e75-e18b5807140f" />

---

### Figure 4.5 – OpenSSH Server Installation

Enabled the **OpenSSH Server** package during installation.

Installing OpenSSH allows the server to be managed remotely from another machine without requiring direct access through VirtualBox.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_00_35 ssh" src="https://github.com/user-attachments/assets/a3f570c8-dabd-4b17-ba05-4d3aa5772a66" />

---

### Figure 4.6 – Ubuntu Server Installation Complete

Ubuntu successfully completed installation and configured all required system packages.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_00_52 complete intall tower" src="https://github.com/user-attachments/assets/441bf22e-77ae-4977-ba78-f01fff3a4e11" />

---

### Figure 4.7 – First Boot

After rebooting, Ubuntu successfully initialized all required system services and completed the boot process.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_01_47 reboot" src="https://github.com/user-attachments/assets/5b97489b-0d86-4bd6-9290-1a6599636afb" />

---

### Figure 4.8 – Initial Login

Successfully authenticated using the administrator account created during installation.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_11_40 login" src="https://github.com/user-attachments/assets/5e342422-9254-47aa-9760-6f5806849808" />

---

### Figure 4.9 – Ubuntu Server Dashboard

Verified successful login and confirmed the operating system version, network configuration, and system health.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_14_50 login success" src="https://github.com/user-attachments/assets/06644500-525c-4d44-a9bc-8bc51e9828db" />

---

### Figure 4.10 – Verify Network Interfaces

Executed the following command to display all available network interfaces.

```bash
ip a
```

Confirmed the server received both NAT and Host-Only IP addresses, allowing internet connectivity and communication with other virtual machines.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_21_15_54 IP A -NetworkInterfaces-" src="https://github.com/user-attachments/assets/230debc8-dac0-4d40-9361-32ad22f014f2" />

---

## Outcome

Successfully deployed and configured the Ubuntu Server **SOC Watchtower**, including the installation of Ubuntu Server, creation of the administrator account, configuration of the system hostname, and installation of the OpenSSH Server package.

Verified that the operating system was installed successfully, confirmed the server booted correctly, and identified the available network interfaces using the `ip a` command.

The SOC Watchtower is now prepared for virtual network configuration, remote administration, and the deployment of centralized security monitoring tools in the next phase of the project.


# Step 5 - Configure the DevOps Workstation (Ubuntu Desktop)

The Ubuntu Desktop virtual machine was configured to serve as the **DevOps Workstation**, providing a graphical Linux environment for administering the SOC infrastructure. This workstation will be used to manage virtual machines, remotely administer the SOC Watchtower, and support future deployment and testing of security monitoring tools.

---

### Figure 5.1 – Begin Ubuntu Desktop Installation

Selected **Install Ubuntu** to begin deploying the Ubuntu Desktop operating system.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_20_20 Installation" src="https://github.com/user-attachments/assets/d1d12960-3d9a-4b1a-8783-49725cf91600" />

---

### Figure 5.2 – Select Installation Options

Configured the installation using the following options:

- **Minimal Installation** to reduce unnecessary software and resource usage.
- **Download updates while installing Ubuntu** to ensure the system was current immediately after installation.
- **Install third-party software** to improve hardware compatibility and multimedia support.

These options provide a lightweight workstation while maintaining compatibility with enterprise hardware and future software installations.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_21_37  Minimal   better Hardware support" src="https://github.com/user-attachments/assets/74a442f0-d0af-4e02-aca2-f648482223aa" />

---

### Figure 5.3 – Configure Storage

Selected **Erase disk and install Ubuntu**.

Since this virtual machine uses a dedicated virtual hard disk within Oracle VirtualBox, erasing the disk only affects the virtual machine and does not modify the host operating system.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_22_37 Erase disk" src="https://github.com/user-attachments/assets/12206816-8e0a-42a4-80d9-2a3f7833c641" />

---

### Figure 5.4 – Configure User Profile

Created the administrator account for the DevOps workstation.

Configured:

- Display Name: **DEV Cole**
- Hostname: **dev-VirtualBox**
- Username: **dev**

This account will be used to administer the workstation and perform future system management tasks.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_24_01 Login setup" src="https://github.com/user-attachments/assets/8320b85a-9eca-447e-b4d8-b3e752224f0b" />

---

### Figure 5.5 – Ubuntu Desktop Installation

Ubuntu Desktop copied the required system files and completed the installation process.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_25_17 instal confirg" src="https://github.com/user-attachments/assets/7d65287a-db05-4851-bddb-4e11c1e3ae3a" />

---

### Figure 5.6 – First Login

Successfully logged into the Ubuntu Desktop environment and verified that the operating system installed correctly.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_33_58 Succesfull login creation" src="https://github.com/user-attachments/assets/bdf95890-eb69-48f6-96fe-2a27049a6a43" />

---

### Figure 5.7 – Verify Network Interfaces

Executed the following command to verify the workstation's network configuration.

```bash
ip a
```

Confirmed that both NAT and Host-Only network adapters were assigned valid IP addresses, allowing communication with the host computer and the remaining virtual machines.

<img width="1280" height="800" alt="VirtualBox_Dev Ops WorkStation DSKTOP_27_06_2026_21_35_17 network interfaces" src="https://github.com/user-attachments/assets/732550f3-5301-42b5-97d6-8d951de8edda" />

---

## Outcome

Successfully deployed and configured the Ubuntu Desktop **DevOps Workstation**.

Verified successful installation of the operating system, configured the administrator account, and confirmed network connectivity by validating the assigned network interfaces.

The DevOps Workstation is now prepared to remotely administer the SOC Watchtower, manage the virtual lab environment, and support the deployment and testing of future security monitoring solutions.


# Step 6 - Configure the Windows 10 Workstation

The Windows 10 virtual machine was configured to serve as the primary monitored Windows endpoint within the Blue Team SOC lab. This workstation will later generate Windows event logs, Sysmon telemetry, PowerShell activity, and security events that will be collected and analyzed by the SOC Watchtower.

---

### Figure 6.1 – Begin Windows 10 Installation

Booted the Windows 10 Enterprise installation media and verified the installer launched successfully.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_21_36_44" src="https://github.com/user-attachments/assets/0aad7edd-fc42-4c3c-92f1-3b4a8e12ecb5" />

---

### Figure 6.2 – Select Windows Edition

Selected **Windows 10 Pro (64-bit)** for deployment.

Windows 10 Pro provides enterprise management capabilities and administrative features commonly used in business environments, making it appropriate for a cybersecurity lab.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_21_37_44 windows 10 pro versio" src="https://github.com/user-attachments/assets/1740eba6-21ce-4bed-92ed-3658c3032e3c" />
---

### Figure 6.3 – Configure Storage

Selected the unallocated virtual disk and allowed Windows Setup to automatically create the required system partitions.

Because the workstation is installed on a dedicated VirtualBox virtual disk, these partitions only affect the virtual machine and do not modify the host operating system.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_21_38_47 create windows partion" src="https://github.com/user-attachments/assets/fb9e53d0-c53c-42c9-b15e-7598afb893d0" />

---

### Figure 6.4 – Windows Installation

Windows copied the required installation files, installed system components, and completed the operating system deployment.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_21_46_31 setup" src="https://github.com/user-attachments/assets/1af28eb2-504f-4748-8a5a-eb82d621c596" />

---

### Figure 6.5 – Initial Device Configuration

Selected **Limited Experience** instead of signing in with a Microsoft account.

Using a local account simplifies administration within the isolated lab environment and better reflects systems commonly encountered during enterprise troubleshooting and security investigations.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_21_58_10 limited ex for personal use" src="https://github.com/user-attachments/assets/dea926b2-fd64-4d7a-a78b-dcaaba5bcb6c" />

---

### Figure 6.6 – Configure Local Administrator Account

Created the local workstation account.

**Computer Name**

- DesignerWorkstation

This workstation will later serve as the monitored Windows endpoint for security monitoring exercises.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_21_58_43 DesignerWorkstation" src="https://github.com/user-attachments/assets/c94203fc-ba05-450d-83e4-26c53f1261c1" />

---

### Figure 6.7 – Configure Privacy Settings

Disabled optional privacy, telemetry, advertising, and tracking features that are unnecessary within the isolated virtual lab.

Reducing unnecessary background services creates a cleaner environment for observing system activity generated during future security testing.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_22_00_00 TurnTracking Off" src="https://github.com/user-attachments/assets/8286f061-a0df-4601-8e17-95dbe520103e" />

---

### Figure 6.8 – Successful Windows Installation

Verified successful installation and confirmed that Windows booted correctly into the desktop environment.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_22_02_07 Success Creation" src="https://github.com/user-attachments/assets/f7f50b61-0cbc-40d1-9e7c-006bfaa24246" />

---

### Figure 6.9 – Verify Network Configuration

Executed the following command to verify the workstation's assigned network interfaces.

```powershell
ipconfig
```

Confirmed that both NAT and Host-Only network adapters received valid IP addresses, allowing internet connectivity while enabling communication with the remaining virtual machines.

<img width="1024" height="768" alt="VirtualBox_WindowWorkstation_27_06_2026_22_03_07 network Adapters" src="https://github.com/user-attachments/assets/b3e26bb4-38aa-4fda-abc2-e9339c6e7435" />

---

## Outcome

Successfully deployed and configured the Windows 10 workstation.

Verified the operating system installation, configured a local administrator account, applied privacy settings appropriate for an isolated lab environment, and confirmed the workstation's network configuration.

The Windows workstation is now prepared for deployment of Sysmon, Elastic Agent, endpoint telemetry collection, and future attack simulations within the Blue Team SOC environment.
---

# Step 7 - Configure Remote Administration & Validate Network Connectivity

After completing the operating system installations, the next objective was to verify communication between all systems within the virtual lab.

The SOC Watchtower (Ubuntu Server) was remotely accessed from the host computer using **OpenSSH**, allowing administration without interacting directly with the VirtualBox console.

Network connectivity was then validated between every virtual machine to ensure the environment was properly configured for future centralized monitoring and log collection.

---

### Figure 7.1 – Establish Remote SSH Session

Connected to the SOC Watchtower from the Windows host using OpenSSH.

```powershell
ssh defender__cole@192.168.56.104
```

During the initial connection, SSH prompted for host verification before adding the server's fingerprint to the local **known_hosts** file.

After authentication, a secure remote shell session was successfully established.

<img width="1367" height="448" alt="Screenshot 2026-06-27 222459" src="https://github.com/user-attachments/assets/3565f07d-01e3-4013-8342-6f9903eb3344" />

---

### Figure 7.2 – Verify Network Interfaces

Verified that the SOC Watchtower was assigned both NAT and Host-Only network adapters.

```bash
ip a
```

Confirmed that the server received:

- NAT Adapter: `10.0.2.15`
- Host-Only Adapter: `192.168.56.104`

These interfaces provide internet connectivity while allowing communication between virtual machines.

<img width="1390" height="405" alt="Screenshot 2026-06-27 222531" src="https://github.com/user-attachments/assets/c5bc6c6f-96b4-43b9-bd82-3ba1e88c39c6" />

---

### Figure 7.3 – Test Connectivity to the Host Computer

Performed an ICMP connectivity test between the SOC Watchtower and the Windows host computer.

The initial ping request failed because Windows Defender Firewall was blocking inbound ICMP Echo Requests.

<img width="800" height="600" alt="VirtualBox_SOC WatchTower LIVESERVER_27_06_2026_22_14_01 PING Ubuntu desktop" src="https://github.com/user-attachments/assets/2b2bd7db-4061-468b-af91-4bb7c8fa243b" />

---

### Figure 7.4 – Enable ICMP Echo Requests

The initial connectivity test indicated that the Windows host was blocking inbound ICMP Echo Requests.

To allow the SOC Watchtower to communicate with the host system, Windows Defender Firewall was configured to permit inbound ICMPv4 traffic.

#### Step 1 – Open Windows Defender Firewall

Opened **Windows Defender Firewall** from the Windows Control Panel.

<img width="626" height="85" alt="Screenshot 2026-06-28 002615" src="https://github.com/user-attachments/assets/fd205daf-babf-4ddc-85d8-0e3e381d6cf2" />

---

#### Step 2 – Open Advanced Settings

Selected **Advanced settings** to launch **Windows Defender Firewall with Advanced Security**.

<img width="229" height="37" alt="Screenshot 2026-06-28 002508" src="https://github.com/user-attachments/assets/5b5c21e6-9201-4259-a1eb-092202604c12" />
---

#### Step 3 – Navigate to Inbound Rules

Selected **Inbound Rules** to view and manage incoming firewall rules.

<img width="142" height="19" alt="Screenshot 2026-06-28 002531" src="https://github.com/user-attachments/assets/d7c1e4e0-e4ad-4065-a94f-a1891c568878" />

---

#### Step 4 – Enable ICMPv4 Echo Requests

Located and enabled the **File and Printer Sharing (Echo Request – ICMPv4-In)** inbound firewall rule.

This rule allows the Windows host computer to respond to ICMP Echo Requests (ping) from other systems on the Host-Only network, enabling connectivity testing between the host computer and the SOC Watchtower.

<img width="223" height="33" alt="Screenshot 2026-06-28 002547" src="https://github.com/user-attachments/assets/ab33350d-fbee-4766-b106-09dfbaf4bdc6" />

---

### Figure 7.5 – Verify Host Connectivity

Repeated the ping test after enabling the firewall rule.

The host computer successfully responded to ICMP requests, confirming communication between the SOC Watchtower and the host operating system.

<img width="1428" height="593" alt="Screenshot 2026-06-27 222555" src="https://github.com/user-attachments/assets/eb29e19a-db8c-40fa-a4e0-01da312134da" />

---

### Figure 7.6 – Verify Virtual Machine Connectivity

Tested communication between the SOC Watchtower and the remaining virtual machines.

Successfully verified:

- Ubuntu Desktop (DevOps Workstation)
- Windows 10 Workstation

During testing, the Windows workstation initially failed to respond because its Windows Defender Firewall was also blocking ICMP Echo Requests.

After enabling the same inbound firewall rule on the Windows workstation, all systems communicated successfully.

#### Figure 7.6.1 – Ping Ubuntu Desktop

Verified successful ICMP communication between the SOC Watchtower and the Ubuntu Desktop DevOps Workstation.
<img width="800" height="115" alt="defender" src="https://github.com/user-attachments/assets/36c2e0d8-a5b9-48f2-be60-e98f77766ae2" />
#### Figure 7.6.2 – Ping DevOps Workstation

Confirmed successful communication between the SOC Watchtower and the DevOps Workstation over the Host-Only network.

<img width="591" height="148" alt="Screenshot 2026-06-28 004114" src="https://github.com/user-attachments/assets/8aa7a4d1-9df9-46ba-991c-ecd74abd955c" />
#### Figure 7.6.3 – Initial Windows 10 Connectivity Failure

Attempted to communicate with the Windows 10 workstation. The request failed because Windows Defender Firewall was blocking inbound ICMP Echo Requests.

<img width="593" height="56" alt="Screenshot 2026-06-28 004406" src="https://github.com/user-attachments/assets/f5bcc28c-d26f-4b3c-a0b6-946a649878e7" />
#### Figure 7.6.4 – Successful Windows 10 Connectivity

After enabling the **File and Printer Sharing (Echo Request – ICMPv4-In)** inbound firewall rule on the Windows 10 workstation, the SOC Watchtower successfully communicated with the endpoint.

<img width="579" height="110" alt="Screenshot 2026-06-28 004411" src="https://github.com/user-attachments/assets/8f4bba40-f9b5-479a-8156-6204fdcd7e23" />

---

## Outcome

Successfully configured secure remote administration using OpenSSH and validated network connectivity across the Blue Team SOC lab.

Resolved Windows Defender Firewall restrictions by enabling the **File and Printer Sharing (Echo Request – ICMPv4-In)** inbound rule on both the host computer and Windows workstation, allowing successful ICMP communication between all systems.

The virtual lab now supports reliable communication between every machine, providing the foundation required for centralized logging, endpoint monitoring, and future security operations exercises.

## Outcome

Successfully designed, deployed, and documented a fully functional Blue Team Security Operations Center (SOC) home lab using VirtualBox.

The lab consists of three interconnected virtual machines that simulate a small enterprise environment:

- **Ubuntu Server 22.10** configured as the **SOC Watchtower** for centralized monitoring and remote administration.
- **Ubuntu Desktop 22.10** configured as a Linux endpoint (DevOps Workstation).
- **Windows 10 Enterprise** configured as a monitored Windows endpoint.

Throughout the deployment process, the following objectives were successfully completed:

- Installed and configured all virtual machines from official operating system images.
- Designed an isolated virtual network using both **NAT** and **Host-Only** adapters.
- Assigned and verified network interfaces using Linux and Windows networking tools.
- Enabled **OpenSSH** on the Ubuntu Server for secure remote administration.
- Established remote SSH connectivity from the Windows host to the SOC Watchtower.
- Verified communication between the host computer and all virtual machines using ICMP connectivity testing.
- Diagnosed and resolved Windows Defender Firewall restrictions by enabling **File and Printer Sharing (Echo Request – ICMPv4-In)** on both the Windows host and Windows virtual machine.
- Documented each deployment phase with screenshots and technical explanations to create repeatable infrastructure documentation.

This project establishes the foundation for a production-style Blue Team environment and prepares the lab for more advanced security operations, including:

- Elastic Stack (ELK) deployment
- Centralized log collection
- Syslog configuration
- Windows Event Forwarding (WEF)
- Sysmon deployment
- Endpoint telemetry collection
- SIEM rule creation
- Threat detection engineering
- Incident response investigations
- Digital forensics exercises
- Malware analysis
- Attack simulation using Atomic Red Team and MITRE ATT&CK techniques

The environment now provides a stable platform for continuing hands-on cybersecurity labs while developing practical experience with enterprise security monitoring, log analysis, network visibility, and Security Operations Center (SOC) workflows.
