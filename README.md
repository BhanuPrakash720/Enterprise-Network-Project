# Enterprise-Network-Project
Got it\! You want the screenshots placed right where their relevant configuration or verification step is described, for immediate context. This is an excellent way to make your `README.md` highly understandable.

I will remove the detailed screenshot descriptions from the final "Visuals & Verification Screenshots" section and instead, integrate each screenshot placeholder directly into its respective "Step-by-Step Configuration" or "Step-by-Step Process" section. The final "Visuals" section will be a brief summary and reminder to replace the placeholders.

Here's the updated `README.md` template:

-----

### How to Create Your `README.md` on GitHub

Since you've just created your GitHub account and repository, here's the simplest way to add this comprehensive `README.md` file to your project:

1.  **Navigate to Your Repository:** Go to `github.com` and log in. Click on your project repository (e.g., `Enterprise-Network-Project`).
2.  **Add a New File:** On your repository's main page, you'll see an "Add file" dropdown or a prominent "Add README" button if you haven't added one yet. Click "Add file" then select "Create new file."
3.  **Name the File:** In the file name field, type `README.md`. GitHub will automatically recognize this name and render its content on your repository's homepage.
4.  **Paste the Content:** Copy the entire markdown content I provide below and paste it into the large text area.
5.  **Commit the New File:** Scroll down, add a short, descriptive commit message (e.g., "Initial project README with Phase 1 setup and design details"), and click the "Commit new file" button.

That's it\! Your repository will now have a detailed `README.md` visible on its main page.

-----

````markdown
# Enterprise Network Infrastructure Project: Phase 1 - Core Network Infrastructure & Initial Configuration

![Project Status](https://img.shields.io/badge/Phase%201%20Complete-Core%20Setup-green)
![Learning Objectives](https://img.shields.io/badge/Focus-GNS3%2C%20Topology%2C%20IP%20Addressing%2C%20Basic%20Device%20Config-blueviolet)
![License](https://img.shields.io/badge/License-MIT-blue.svg) ## Table of Contents

* [Project Overview](#project-overview)
* [Phase 1: Core Network Infrastructure & Initial Configuration](#phase-1-core-network-infrastructure--initial-configuration)
    * [Learning Objectives](#learning-objectives)
    * [Implementation Steps](#implementation-steps)
        * [1. GNS3 Installation & Environment Setup](#1-gns3-installation--environment-setup)
        * [2. Network Topology Design (Conceptual)](#2-network-topology-design-conceptual)
        * [3. IP Addressing Plan](#3-ip-addressing-plan)
        * [4. GNS3 Project Setup](#4-gns3-project-setup)
        * [5. Basic Device Setup & SSH Hardening](#5-basic-device-setup--ssh-hardening)
        * [6. VLANs and Trunking Implementation](#6-vlans-and-trunking-implementation)
        * [7. Inter-VLAN Routing Configuration](#7-inter-vlan-routing-configuration)
        * [8. DHCP Server Configuration](#8-dhcp-server-configuration)
        * [9. Basic IP Connectivity Testing & STP Verification](#9-basic-ip-connectivity-testing--stp-verification)
* [Visuals & Verification Screenshots Overview](#visuals--verification-screenshots-overview)
* [Next Steps](#next-steps)

---

## Project Overview

This repository documents the phased development of a robust, secure, and automated enterprise network infrastructure, simulated using **GNS3**. The overarching goal is to build a full-scale corporate network, implement various security measures, automate common network tasks, and set up proactive monitoring.

This document specifically covers **Phase 1: Core Network Infrastructure & Initial Configuration**. This foundational phase focuses on setting up the simulation environment, designing the network topology, and configuring the core connectivity components including basic device settings, secure remote access, VLANs, trunking, inter-VLAN routing, and DHCP.

---

## Phase 1: Core Network Infrastructure & Initial Configuration

This phase details the entire process of laying down the groundwork for our enterprise network. From setting up the GNS3 simulation environment to establishing fundamental network services and initial security.

### Learning Objectives

Before diving into the practical implementation, this phase aims to solidify understanding of:

* **Networking Fundamentals:** OSI Model, TCP/IP, IPv4 addressing, and subnetting.
* **Cisco IOS Basics:** Navigating the Command Line Interface (CLI), basic device configuration (hostname, password, enable secret), and managing configurations.
* **VLANs:** Concepts of Virtual Local Area Networks, **802.1Q trunking**, and **access ports**.
* **Spanning Tree Protocol (STP):** Its purpose, basic operation, and how it ensures a loop-free Layer 2 topology.
* **IP Routing:** Understanding **static routes** and **default routes**.
* **DHCP:** The Dynamic Host Configuration Protocol's client-server process (DORA) and how to configure **DHCP pools** on Cisco devices.
* **SSH & Security:** The importance of **SSH (Secure Shell)** for encrypted remote management and initial security hardening measures like **strong passwords** and **banner warnings**.

### Implementation Steps

#### 1. GNS3 Installation & Environment Setup

This section covers getting GNS3 and its associated VM installed and integrated for simulating realistic network environments.

1.1. **Check PC Specifications:**
    Before starting, ensure your computer has sufficient resources. GNS3 can be resource-intensive:
    * **CPU:** Multi-core processor (Intel i5/i7/i9 or AMD Ryzen 5/7/9 recommended).
    * **RAM:** Minimum 8 GB; 16 GB or more is highly recommended for complex topologies.
    * **Disk Space:** At least 20-50 GB free, depending on your device images.
    * **Virtualization:** Crucially, ensure virtualization (Intel VT-x or AMD-V) is enabled in your BIOS/UEFI settings.

1.2. **Download GNS3 & GNS3 VM:**
    * **GNS3 Software:** Download the GNS3 client for your OS from the official GNS3 website ([www.gns3.com/software/download](www.gns3.com/software/download)). A free account is typically required.
    * **GNS3 VM:** From the same page, download the GNS3 VM image for your chosen virtualization software (VMware Workstation Player/Pro or VirtualBox).

1.3. **Install GNS3 and GNS3 VM:**
    * **GNS3 Client (Windows Example):** Run the installer, following on-screen prompts. Install recommended tools like `Npcap` and `Wireshark` for packet capturing. Select "Local GNS3 VM" for initial setups.
    * **GNS3 VM (VMware Workstation Player/Pro Example):** Open VMware, go to `File > Open`, select the downloaded GNS3 VM `.ova` file, import it, and power it on. Note its IP address.

1.4. **Integrate GNS3 & GNS3 VM:**
    * Launch the GNS3 client. The Setup Wizard should appear automatically.
    * Choose "Run appliances in a virtual machine" and click "Next."
    * Select your GNS3 VM. GNS3 should detect the running VM.
    * Confirm server settings (Host, Port).
    * Click "Finish." A green indicator in the GNS3 client window signifies a successful connection.

1.5. **Source and Import Cisco IOS Images:**
    * **Note:** Cisco IOS images are proprietary and require proper licensing or access. This guide assumes you have legally sourced these images.
    * **Recommended Images:**
        * **Routers:** `Cisco CSR1000v` (feature-rich, resource-intensive) or `vIOS-L3` (lighter).
        * **Layer 3 Switch:** `Cisco IOL L3` or `vIOS-L3`.
        * **Layer 2 Switch:** `Cisco IOL L2` or `vIOS-L2`.
    * **Importing:** In GNS3, use `File > Import appliance` for `.gns3a` files. For raw `.bin` or `.image` files (e.g., for Dynamips or Qemu VMs), go to `Edit > Preferences > Qemu VMs` or `IOS routers`, click `New`, and follow the template creation wizard.

#### 2. Network Topology Design (Conceptual)

This is the blueprint of our network. It's crucial to sketch this out conceptually before building it in the simulator.

* **Headquarters (HQ) Network:**
    * **Edge Router (R1 - HQ-EDGE):** Connects the internal network to the simulated Internet.
    * **Core Layer 3 Switch (L3S1 - HQ-CORE):** Central point for inter-VLAN routing, high-speed backbone.
    * **Distribution Layer 2 Switches (L2S1 - HQ-DIST-A, L2S2 - HQ-DIST-B):** Aggregate connections from the access layer, providing redundancy.
    * **Access Layer 2 Switches:** `L2S3 - HQ-ACC-HR` (for HR VLAN), `L2S4 - HQ-ACC-IT` (for IT VLAN), `L2S5 - HQ-ACC-FIN` (for Finance VLAN).
* **Branch Office Network:**
    * **Branch Router (R2 - BRANCH-RTR):** Connects the Branch office to the HQ network (via simulated WAN link to HQ-EDGE).
    * **Branch Switch (L2S6 - BRANCH-SW):** Provides local connectivity for devices in the Branch office.
* **Interconnects:** Define all physical connections between devices (e.g., Internet to HQ-EDGE, HQ-EDGE to HQ-CORE, HQ-EDGE to BRANCH-RTR, and all inter-switch connections using high-speed trunk links).

#### 3. IP Addressing Plan

A well-structured IP addressing plan is crucial for scalability and manageability. We will use the `10.0.0.0/8` private address space for this project.

* **VLANs and Subnets:**
    * **VLAN 10 - HR:** `10.10.10.0/24` (Gateway: `10.10.10.1`)
    * **VLAN 20 - IT:** `10.10.20.0/24` (Gateway: `10.10.20.1`)
    * **VLAN 30 - Finance:** `10.10.30.0/24` (Gateway: `10.10.30.1`)
    * **VLAN 99 - Management:** `10.10.99.0/24` (Gateway: `10.10.99.1`)
    * **Branch LAN (VLAN 40):** `10.20.0.0/24` (Gateway: `10.20.0.1`)
* **Inter-Device Links:**
    * **HQ-EDGE to HQ-CORE:** `10.0.0.0/30` (`.1` on HQ-EDGE, `.2` on HQ-CORE)
    * **HQ-EDGE to BRANCH-RTR (WAN):** `10.0.0.4/30` (`.5` on HQ-EDGE, `.6` on BRANCH-RTR)

#### 4. GNS3 Project Setup

Now, we translate the conceptual design into our GNS3 workspace.

1.  **Launch GNS3 & Create New Project:** Open the GNS3 application, go to `File > New blank project`, give your project a descriptive name (e.g., "HQ_Branch_Network_Project"), and ensure the "Run this project on" setting points to your configured GNS3 VM.
2.  **Add Devices:** On the left-hand GNS3 toolbar, click the "Browse devices" icon. Drag and drop all the planned devices (Cloud, HQ-EDGE, HQ-CORE, Distribution switches, Access switches, Branch Router, Branch Switch, and a few **VPCS** (Virtual PC) devices to act as end-hosts for testing VLANs later) onto your workspace.
3.  **Connect Devices:** Use the "Add a link" icon (cable icon) to connect devices based on your conceptual design. Carefully match interface mappings (e.g., Cloud to HQ-EDGE's GigabitEthernet0/0, HQ-EDGE's GigabitEthernet0/1 to HQ-CORE's GigabitEthernet0/1). Once all devices are placed and connected, save your project (`File > Save project`).

**Visuals for Initial Setup:**

* **Network Topology Diagram (Conceptual)**
    * *Purpose:* The blueprint of your network design, illustrating device roles, interconnections, and the overall structure.
    * ![Conceptual Network Topology Diagram](images/conceptual_topology.png)
    * *(Replace this placeholder with your actual diagram from Draw.io or Lucidchart. Save it as `conceptual_topology.png` in an `images` folder within your repository.)*

* **Initial GNS3 Workspace with Devices Connected**
    * *Purpose:* Shows the physical layout of devices and connections in GNS3, reflecting the initial topology setup.
    * ![Initial GNS3 Workspace with Devices Connected](images/gns3_initial_workspace.png)
    * *(Replace this placeholder with your actual screenshot of your GNS3 project. Save it as `gns3_initial_workspace.png` in the same `images` folder.)*

#### 5. Basic Device Setup & SSH Hardening

This step configures fundamental settings on all network devices, establishes secure remote access, and implements initial security hardening measures.

1.  **Console Access:** Start all devices in GNS3 (green play button) and open a console connection to each device. This is your initial point of interaction.
2.  **Hostname Configuration:** Assign a unique and descriptive hostname to each device.
    ```cli
    enable
    configure terminal
    hostname HQ-EDGE-R1  # Example: Use HQ-CORE-L3SW1, BRANCH-R1, etc.
    exit
    ```
3.  **Basic Password Security:** Implement strong, encrypted passwords for privileged EXEC mode and console access.
    ```cli
    configure terminal
    enable secret yourStrongEnablePassword  # Use a strong, complex password
    line console 0
    password yourConsolePassword # Use a strong password
    login
    exit
    ```
4.  **SSH Hardening (Crucial for Secure Remote Access):** Secure your remote management access using **SSHv2**. This involves generating cryptographic keys, specifying the SSH version, and creating local user accounts.
    ```cli
    configure terminal
    ip domain name yourcompany.local # Use a descriptive domain name
    crypto key generate rsa modulus 2048 # Generate 2048-bit RSA keys for strong encryption
    ip ssh version 2 # Enforce SSH version 2 only
    username admin privilege 15 secret yourstrongpassword # Create a local admin user with highest privilege
    line vty 0 4 # Access virtual terminal lines (0 to 4 means 5 simultaneous sessions)
    transport input ssh # Allow ONLY SSH connections
    login local # Use local user accounts for authentication
    exit
    ```

**Verification Screenshot for SSH Configuration:**

* **SSH Configuration Output**
    * *Device:* One of your routers (e.g., HQ-EDGE-R1).
    * *Command Output:* `show running-config | section ssh` or `show ip ssh`.
    * *Purpose:* Demonstrates successful SSH configuration, including key generation and version enforcement.
    * ![SSH Configuration Output](images/ssh_config_output.png)
    * *(Replace this placeholder with your actual screenshot of the CLI output.)*

5.  **Disable Insecure Telnet Explicitly:** While `transport input ssh` often implies disabling Telnet, explicitly ensuring it's not active is a good security practice.
    ```cli
    configure terminal
    line vty 0 4
    no transport input telnet # Ensure Telnet is explicitly removed if present/enabled
    exit
    ```
6.  **Banner Warnings (Message Of The Day):** Configure a legal warning banner that is displayed to anyone attempting to access the device.
    ```cli
    configure terminal
    banner motd # Unauthorized access to this system is prohibited # # Use a unique delimiter like '#'
    exit
    ```

**Verification Screenshot for Banner Warning:**

* **Banner Warning**
    * *Device:* Any device after configuration.
    * *Output:* Console access displaying the banner message.
    * *Purpose:* Confirms your legal warning banner is active.
    * ![Banner Warning](images/banner_warning.png)
    * *(Replace this placeholder with your actual screenshot of the console output.)*

7.  **Save Configuration:** Always save your running configuration to startup configuration. This ensures your changes persist across device reloads or power cycles.
    ```cli
    copy running-config startup-config
    ```

#### 6. VLANs and Trunking Implementation

This part involves logically segmenting your network into different departments using VLANs and enabling communication between switches through trunk links. This is a critical step in building a scalable and secure network.

1.  **VLAN Creation (on all Layer 2 and Layer 3 switches):** You need to create the necessary VLANs on all your Cisco IOSvL2 switches (Access, Distribution, Branch).
    ```cli
    enable
    configure terminal
    vlan 10
     name HR
    vlan 20
     name IT
    vlan 30
     name Finance
    vlan 99
     name Management
    # On L2S6-BRANCH-SW (Branch Switch):
    vlan 40
     name Branch
    exit
    ```
    (Note: On the Cisco 7200 router, VLANs are implicitly defined via sub-interfaces in the next step.)

**Verification Screenshot for VLAN Creation:**

* **`show vlan brief` Output**
    * *Device:* Any Cisco IOSvL2 switch (e.g., L2S1-DIST-A).
    * *Command Output:* `show vlan brief`.
    * *Purpose:* Demonstrates that you have successfully created all the defined VLANs (HR, IT, Finance, Management, Branch) on your switches.
    * ![show vlan brief Output](images/show_vlan_brief.png)
    * *(Replace this placeholder with your actual screenshot of the CLI output.)*

2.  **Access Port Assignment (on Access Switches - L2S3-HR, L2S4-IT, L2S5-FIN, L2S6-BRANCH):** Identify ports connecting to simulated end-user devices (VPCS), configure them as access ports, and assign them to the correct VLAN.
    * **Example for HQ-ACC-HR (L2S3-HR), assuming PC connects to FastEthernet0/1:**
        ```cli
        configure terminal
        interface FastEthernet0/1  # Or GigabitEthernet0/1, match your topology
         switchport mode access
         switchport access vlan 10  # Assigns this port to the HR VLAN
         no shutdown
        exit
        ```
    * Repeat for:
        * `L2S4-IT`: Ports connected to IT PCs -> `switchport access vlan 20`
        * `L2S5-FIN`: Ports connected to Finance PCs -> `switchport access vlan 30`
        * `L2S6-BRANCH`: Ports connected to Branch PCs -> `switchport access vlan 40`

3.  **Trunk Configuration (on all inter-switch links and switch-to-router links):** Identify interfaces connecting switches to other switches or to the HQ-CORE router and configure them as trunk ports.
    * **On Cisco IOSvL2 Switches (Access, Distribution, Branch):** For any interface that connects to another switch or to the HQ-CORE router:
        ```cli
        configure terminal
        interface GigabitEthernet0/X  # Replace X with the correct interface number
         switchport mode trunk
         switchport trunk native vlan 99 # Sets VLAN 99 as the native VLAN (best practice)
         switchport nonegotiate # Optional: Disables DTP for security/stability
         no shutdown
        exit
        ```
    * Apply this to the following links:
        * `L2S3-HR <-> L2S1-DIST-A`
        * `L2S4-IT <-> L2S1-DIST-A`
        * `L2S5-FIN <-> L2S2-DIST-B`
        * `L2S1-DIST-A <-> L3S1-HQ-CORE`
        * `L2S2-DIST-B <-> L3S1-HQ-CORE`
        * `L2S6-BRANCH-SW <-> R2-BRANCH-RTR`
    * **Special Case: Trunk configuration on HQ-CORE (L3S1 - Cisco 7200 Router):** For the physical interface(s) of your HQ-CORE router that connect to the Distribution switches, ensure they are enabled and have no IP address assigned yet. Inter-VLAN routing configuration on sub-interfaces will follow.
        ```cli
        configure terminal
        interface GigabitEthernet0/1  # Replace with the actual interface connected to L2S1/L2S2
         no ip address
         no shutdown
        exit
        ```

**Verification Screenshot for Trunk Configuration:**

* **`show interfaces trunk` Output**
    * *Device:* One of your Distribution Layer 2 switches (e.g., L2S1-DIST-A).
    * *Command Output:* `show interfaces trunk`.
    * *Purpose:* Confirms active trunk links, showing 802.1Q encapsulation and allowing traffic for the expected VLANs to pass through.
    * ![show interfaces trunk Output](images/show_interfaces_trunk.png)
    * *(Replace this placeholder with your actual screenshot of the CLI output.)*

4.  **Save Configuration:**
    ```cli
    copy running-config startup-config
    ```

#### 7. Inter-VLAN Routing Configuration

Now that VLANs are segmented, this step implements **Inter-VLAN Routing** to allow seamless communication between devices in different VLANs.

1.  **Configure Inter-VLAN Routing on HQ-CORE (L3S1 - Cisco 7200 Router):** This router will be the default gateway for your HR, IT, Finance, and Management VLANs. We'll use the **Router-on-a-Stick** method.
    ```cli
    enable
    configure terminal

    # Ensure the physical interface connected to the Distribution Switches is 'no ip address' and 'no shutdown'
    interface GigabitEthernet4/0 # Replace with the actual interface (e.g., Gig0/1 or Fa0/0)
     no ip address
     no shutdown
    exit

    # Create sub-interfaces for each VLAN and assign gateway IPs
    interface GigabitEthernet4/0.10 # Sub-interface for VLAN 10 (HR)
     encapsulation dot1Q 10
     ip address 10.10.10.1 255.255.255.0
     no shutdown
    exit

    interface GigabitEthernet4/0.20 # Sub-interface for VLAN 20 (IT)
     encapsulation dot1Q 20
     ip address 10.10.20.1 255.255.255.0
     no shutdown
    exit

    interface GigabitEthernet4/0.99 # Sub-interface for VLAN 99 (Management - Native VLAN)
     encapsulation dot1Q 99 native # Matches switch trunk configuration
     ip address 10.10.99.1 255.255.255.0
     no shutdown
    exit

    interface GigabitEthernet0/5.30 # Sub-interface for VLAN 30 (Finance) - Example assuming Gig0/5
    encapsulation dot1Q 30
    ip address 10.10.30.1 255.255.255.0
    no shutdown
    exit
    ```

**Verification Screenshot for Inter-VLAN Routing Configuration:**

* **`show ip interface brief` Output**
    * *Device:* Your L3S1 - HQ-CORE (Cisco 7200 router).
    * *Command Output:* `show ip interface brief`.
    * *Purpose:* Displays all physical interfaces and, crucially, your newly configured sub-interfaces along with their assigned IP addresses and status, confirming your inter-VLAN routing setup.
    * ![show ip interface brief Output](images/show_ip_interface_brief.png)
    * *(Replace this placeholder with your actual screenshot of the CLI output.)*

2.  **Configure Inter-VLAN Routing on BRANCH-RTR (R2 - Cisco 7200 Router):** This router will be the default gateway for your Branch VLAN(s).
    ```cli
    enable
    configure terminal

    # Ensure the physical interface connected to the Branch Switch (L2S6) is 'no ip address' and 'no shutdown'
    interface GigabitEthernet4/0 # Replace with the actual interface
     no ip address
     no shutdown
    exit

    # Create sub-interface for the Branch VLAN and assign gateway IP
    interface GigabitEthernet4/0.40 # Sub-interface for VLAN 40 (Branch)
     encapsulation dot1Q 40
     ip address 10.20.0.1 255.255.255.0
     no shutdown
    exit
    ```

3.  **Configure Default Gateways on VPCS (Simulated PCs):** Set the default gateway on each simulated PC (VPCS) to point to the correct sub-interface IP address.
    * **For HR PC (connected to L2S3):** `PC> ip 10.10.10.10 255.255.255.0 10.10.10.1`
    * **For IT PC (connected to L2S4):** `PC> ip 10.10.20.10 255.255.255.0 10.10.20.1`
    * **For Finance PC (connected to L2S5):** `PC> ip 10.10.30.10 255.255.255.0 10.10.30.1`
    * **For Branch PC (connected to L2S6):** `PC> ip 10.20.0.10 255.255.255.0 10.20.0.1`

4.  **Save Configuration:**
    ```cli
    copy running-config startup-config
    ```

#### 8. DHCP Server Configuration

This step automates the assignment of IP addresses, subnet masks, default gateways, and DNS server information to devices within your HR, IT, and Finance VLANs, making network management more efficient.

1.  **Access Global Configuration Mode on HQ-CORE (L3S1):**
    ```cli
    enable
    configure terminal
    ```

2.  **Exclude Gateway and Static IP Addresses from DHCP Pools:** Prevent the DHCP server from handing out IP addresses already assigned statically or reserved for servers.
    ```cli
    ip dhcp excluded-address 10.10.10.1 10.10.10.9 # For HR VLAN 10
    ip dhcp excluded-address 10.10.20.1 10.10.20.9 # For IT VLAN 20
    ip dhcp excluded-address 10.10.30.1 10.10.30.9 # For Finance VLAN 30
    ```

3.  **Create DHCP Pool for HR VLAN 10:**
    ```cli
    ip dhcp pool HR_VLAN_POOL
     network 10.10.10.0 255.255.255.0
     default-router 10.10.10.1
     dns-server 8.8.8.8 8.8.4.4
    exit
    ```

4.  **Create DHCP Pool for IT VLAN 20:**
    ```cli
    ip dhcp pool IT_VLAN_POOL
     network 10.10.20.0 255.255.255.0
     default-router 10.10.20.1
     dns-server 8.8.8.8 8.8.4.4
    exit
    ```

5.  **Create DHCP Pool for Finance VLAN 30:**
    ```cli
    ip dhcp pool Finance_VLAN_POOL
     network 10.10.30.0 255.255.255.0
     default-router 10.10.30.1
     dns-server 8.8.8.8 8.8.4.4
    exit
    ```

6.  **Save Your Configuration:**
    ```cli
    end
    copy running-config startup-config
    ```

**Verification & Testing Your DHCP Configuration:**

1.  **Verify DHCP Pool Configuration on the HQ-CORE Router:**
    ```cli
    show ip dhcp pool
    ```
    * **Expected Output:** Detailed information for `HR_VLAN_POOL`, `IT_VLAN_POOL`, and `Finance_VLAN_POOL` with correct "Network," "Default router," and "DNS servers."

**Verification Screenshot for DHCP Pool Configuration:**

* **`show ip dhcp pool` Output**
    * *Device:* HQ-CORE (L3S1 - Cisco 7200 router).
    * *Command Output:* `show ip dhcp pool`.
    * *Purpose:* Displays DHCP pool configurations, confirming the defined networks, default routers, and DNS servers.
    * ![show ip dhcp pool Output](images/show_ip_dhcp_pool.png)
    * *(Replace this placeholder with your actual screenshot of the CLI output.)*

2.  **Test IP Address Assignment on VPCS (Simulated PCs):**
    * Go to each of your simulated PCs (HR PC, IT PC, Finance PC) and instruct them to obtain an IP address via DHCP.
    * For each VPCS:
        ```cli
        PC> ip dhcp
        ```
    * **Observe Output:** The VPCS should display messages indicating it's acquiring a lease and then confirm the assigned IP address, subnet mask, default gateway, and DNS servers.

**Verification Screenshot for DHCP Client Details:**

* **DHCP Client Details (`show ip` on VPCS)**
    * *Device:* Any VPCS after obtaining an IP via DHCP (e.g., HR PC).
    * *Command Output:* `show ip`.
    * *Purpose:* Confirms the PC successfully obtained its IP address, subnet mask, default gateway, and DNS servers from DHCP.
    * ![DHCP Client Details](images/dhcp_client_details.png)
    * *(Replace this placeholder with your actual screenshot of the VPCS output.)*

#### 9. Basic IP Connectivity Testing & STP Verification

This final step for Phase 1 aims to thoroughly test IP connectivity between all devices and verify that Spanning Tree Protocol (STP) is operating correctly to ensure a loop-free network.

#### Part 1: Client VM/PC Setup & DHCP Test (Re-verification)

Objective: Re-verify that your client devices are correctly acquiring IP addresses from the DHCP server configured on HQ-CORE, now that all configurations are in place. (Steps and commands already detailed in Phase 8).

#### Part 2: Intra-VLAN & Inter-VLAN Connectivity Tests

Objective: Confirm that devices can communicate both within their own VLANs and, more importantly, between different VLANs via Inter-VLAN routing.

1.  **Intra-VLAN Connectivity Test (Example: HR to HR):**
    * From your HR PC (e.g., 10.10.10.10), `ping` another device within the same HR VLAN (if applicable, e.g., `ping 10.10.10.11`).
    * **Expected Result:** Successful pings. This confirms your access port configurations and basic Layer 2 forwarding within the VLAN.

2.  **Inter-VLAN Connectivity Test (Example: HR to IT, IT to Finance):**
    * From HR PC: `ping 10.10.20.10` (IT PC), `ping 10.10.30.10` (Finance PC).
    * From IT PC: `ping 10.10.30.10` (Finance PC).
    * **Expected Result:** All pings should be successful. This confirms your Inter-VLAN routing configuration on HQ-CORE and the trunking between your switches and the router.

**Verification Screenshot for Inter-VLAN Ping:**

* **Successful Ping (Inter-VLAN)**
    * *Device:* One of your VPCS (e.g., HR PC).
    * *Command Output:* `ping 10.10.30.10` (HR PC pinging Finance PC).
    * *Purpose:* Demonstrates successful IP connectivity between devices in different VLANs, proving inter-VLAN routing and trunking are functional.
    * ![Successful Ping (Inter-VLAN)](images/inter_vlan_ping.png)
    * *(Replace this placeholder with your actual screenshot of a successful inter-VLAN ping command.)*

#### Part 3: STP Verification

Objective: Ensure that STP is correctly preventing loops and that your Root Bridge is correctly elected.

1.  **Access Device:** Log in to one of your Layer 2 switches (e.g., L2S1-DIST-A, or any switch where you have configured STP).
2.  **Verify Spanning Tree Summary:**
    ```cli
    enable
    show spanning-tree summary
    ```
    * **Expected Output:** This command provides a quick overview. Look for "Root bridge is (your HQ-CORE-L3SW1)" (or relevant core switch). Confirm all VLANs are included in the STP instance and observe port states (e.g., how many are forwarding, blocking).

**Verification Screenshot for Spanning Tree Summary:**

* **`show spanning-tree summary` Output**
    * *Device:* One of your Distribution Layer 2 switches (e.g., L2S1-DIST-A).
    * *Command Output:* `show spanning-tree summary`.
    * *Purpose:* Provides an overview of STP, indicating the Root Bridge, included VLANs, and port states, ensuring a loop-free topology.
    * ![show spanning-tree summary Output](images/show_spanning_tree_summary.png)
    * *(Replace this placeholder with your actual screenshot of the CLI output.)*

3.  **Verify Spanning Tree per VLAN (Optional, but good for detailed check):**
    ```cli
    show spanning-tree vlan 10
    show spanning-tree vlan 20
    show spanning-tree vlan 30
    show spanning-tree vlan 99
    ```
    * **Expected Output:** For each VLAN, confirm the Root Bridge, the role of each port (Root, Designated, Blocked), and the state of each port (Forwarding, Blocking). Ensure no critical active links are unexpectedly in a blocking state.

4.  **Save All Device Configurations:** After completing all your tests and verifications, save the running configuration to the startup configuration on all your network devices (routers and switches). This ensures your hard work persists through reboots.
    ```cli
    end
    copy running-config startup-config
    ```

---

## Visuals & Verification Screenshots Overview

Throughout this document, screenshots are embedded directly after their corresponding configuration or verification steps to provide immediate visual context. Please ensure you replace all placeholder images with your actual screenshots to fully document your project. All images should be placed in an `images/` folder within your repository's root directory.

---

## Next Steps

With Phase 1 complete, we've established a robust core network infrastructure with basic configurations, secure access, and essential services like VLANs, inter-VLAN routing, and DHCP.

The next phases of this project will delve into:

* **Phase 2: Routing Protocols & Network Security (ACLs & NAT):** Implementing dynamic routing and advanced security measures.
* **Phase 3: VPN & Initial Monitoring Setup:** Establishing secure site-to-site VPNs and configuring network monitoring.
* **Phase 4: Automation, Documentation & Final Polish:** Developing automation scripts and compiling comprehensive project documentation.

Stay tuned for updates as the project progresses!

---
````
