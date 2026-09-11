# Cybersecurity Testing Lab Environment Setup

This repository details the re-configuration and customisation of a multi-OS virtual lab built on Oracle VirtualBox for cybersecurity and ethical hacking practice.

---

## 1. Environment Architecture

The environment relies on a custom NAT Network subnet to allow isolated inter-VM communications alongside outbound internet access.

| Virtual Machine | Operating System | IP Address | Subnet Mask | Default Gateway | Network Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Attacker Machine** | Kali Linux | `10.0.0.2` | `255.255.255.0` (`/24`) | `10.0.0.1` | Custom NATNetwork |
| **Target Machine 1** | Windows 10 | `10.0.0.10` | `255.255.255.0` (`/24`) | `10.0.0.1` | Custom NATNetwork |
| **Target Machine 2** | Android 9.0 R2 | `10.0.0.9` | `255.255.255.0` (`/24`) | `10.0.0.1` | Custom NATNetwork |

---

## 2. VirtualBox Network Configuration

### Step 1: Create Custom NAT Network
1. Open **Oracle VirtualBox Manager**.
2. Navigate to **Tools** > **Network** > **NAT Networks** tab[cite: 1].
3. Click **Create** and configure the subnet properties[cite: 1]:
   * **Network Name**: `NatNetwork`[cite: 1]
   * **IPv4 Prefix**: `10.0.0.0/24`[cite: 1]
   * **Enable DHCP**: Checked[cite: 1]

---

## 3. Virtual Machine Adapter Settings

### Kali Linux VM Settings
1. Select the **Kali Linux VM** and open **Settings** > **Network**[cite: 1].
2. Enable **Adapter 1** and select[cite: 1]:
   * **Attached to**: `NAT Network`[cite: 1]
   * **Name**: `NatNetwork`[cite: 1]
   * **Promiscuous Mode**: `Allow All`[cite: 1]

### Windows 10 Target VM Settings
1. Select the **Windows 10 VM** and navigate to **Settings** > **Network**[cite: 1].
2. Enable **Adapter 1** and configure[cite: 1]:
   * **Attached to**: `NAT Network`[cite: 1]
   * **Name**: `NatNetwork`[cite: 1]
   * **Promiscuous Mode**: `Allow All`[cite: 1]

### Android Target VM Settings
1. Open **Settings** > **Display** on the Android VM[cite: 1].
2. Set **Graphics Controller** to `VBoxVGA` and uncheck **Enable 3D Acceleration** to prevent display rendering conflicts[cite: 1].

---

## 4. In-OS IP Assignment & Connectivity Testing

### Kali Linux Manual Configuration
1. Open Network Settings in Kali Linux and configure **Wired connection 1** under **IPv4 Settings**[cite: 1]:
   * **Method**: `Manual`[cite: 1]
   * **Address**: `10.0.0.2`[cite: 1]
   * **Netmask**: `24`[cite: 1]
   * **Gateway**: `10.0.0.1`[cite: 1]
   * **DNS Server**: `8.8.8.8`[cite: 1]

2. Verify interface assignment and WAN connectivity via terminal[cite: 1]:
   ```bash
   ip a
   ping -c 4 8.8.8.8
