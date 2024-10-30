# Steps to Build the Lab

## Table of Contents
- [1. Planning Phase](#1-planning-phase)
- [2. Downloading and Installing VirtualBox](#2-downloading-and-installing-virtualbox)
- [3. Building a pfSense VM](#3-building-a-pfsense-vm)
- [4. Installing pfSense](#4-installing-pfsense)
- [5. Configuring pfSense](#5-configuring-pfsense)
- [6. Importing Kali](#6-importing-kali)
- [7. ](#7-)
- [8. ](#8-)
- [9. ](#9-)
- [10. ](#10-)
- [11. ](#11-)
- [12. ](#12-)
- [13. ](#13-)
- [14. ](#14-)

---

## 1. Planning Phase
- Create a network diagram to visually represent your lab.
- [View Network Diagram](https://github.com/A9u3ybaCyb3r/Virtual-Network-Penetration-Testing-Lab/blob/main/Building%20The%20Lab/Empire%20Net%20Diagram.drawio.pdf)

---

## 2. Downloading and Installing VirtualBox
1. Visit [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads) and download the appropriate version for your operating system.  
   ![Download VirtualBox](https://github.com/user-attachments/assets/f291de59-ca36-44c4-93c0-dbb21030192f)

2. Install the VirtualBox Extension Pack.  
   ![Install Extension Pack](https://github.com/user-attachments/assets/40457f5e-4417-4b4b-b642-f0c4c704617e)

3. Open VirtualBox and navigate to **File > Tools > Extension Pack Manager**.  
   ![Extension Pack Manager](https://github.com/user-attachments/assets/67c5e941-0cbf-4dc1-95e9-8ef9ffa4d88d)

4. Click **Install**, select the downloaded extension pack, and follow the prompts.  
   ![Install Extension](https://github.com/user-attachments/assets/2d202300-7d52-43c7-baa2-291f35362450)
   ![Installation Complete](https://github.com/user-attachments/assets/230cf88a-54de-4522-858b-991670742f14)

---

## 3. Building a pfSense VM
1. **Download pfSense**:
   - Visit [pfSense Downloads](https://www.netgate.com/downloads) and download the latest version.  
     ![Choose Latest Version](https://github.com/user-attachments/assets/b1c3be2d-a7dd-437d-af8d-3af6658d3056)

2. **Extract the ISO File**:
   - Use 7-Zip or a similar tool to extract the downloaded file.  
     ![Extract with 7-Zip](https://github.com/user-attachments/assets/b395d9a3-6e1c-4d7d-a32f-352084f731eb)

3. **Create a New Machine**:
   - Open VirtualBox, click **New**, and configure the VM with a name, location, and the ISO image.  
     ![Create New Machine](https://github.com/user-attachments/assets/a1bed139-45f7-4864-9d89-74ef542fc0cc)
     ![VM Configuration](https://github.com/user-attachments/assets/fa7194ac-cf8c-44f5-882e-62213f7dc89d)

4. **Configure VM Settings**:
   - Modify the boot order to match the image below. Uncheck **Floppy Disk**.  
     ![Change Boot Order](https://github.com/user-attachments/assets/f69d55aa-465c-4616-a2cb-ceac898494ef)

   - Disable audio and USB support.  
     ![Disable Audio](https://github.com/user-attachments/assets/0677dd7d-2d4d-4383-8697-01d8fe5b8c04)  
     ![Disable USB](https://github.com/user-attachments/assets/96c4257b-b5aa-416e-a86a-2f23360f1d0c)

   - **Configure Network Interfaces**:
     - **Adapter 1 (WAN)**:  
       ![WAN Adapter](https://github.com/user-attachments/assets/7ba13507-0c08-4ce8-a7a5-48591123ad08)
     - **Adapter 2 (LAN)**:  
       ![LAN Adapter](https://github.com/user-attachments/assets/924e9715-78d5-45ba-8176-7dcb7d878862)
     - **Adapter 3 (ISOLATED)**:  
       ![ISOLATED Adapter](https://github.com/user-attachments/assets/7f6f4678-f46f-4344-8b99-9b39a45d55cf)
     - **Adapter 4 (AD-LAB)**:  
       ![AD-LAB Adapter](https://github.com/user-attachments/assets/7fe81f34-1f06-443e-bbaf-251de2fc6024)

5. **Start the VM**.

---

## 4. Installing pfSense
1. Start the VM and press **Enter** to begin installation.  
   ![Start VM](https://github.com/user-attachments/assets/e8207eaf-82db-4e52-a6e0-5efb4512622d)

2. Select **Install pfSense** and choose **Auto (ZFS)** for the file system.  
   ![Select Auto ZFS](https://github.com/user-attachments/assets/fe0a64bc-c58a-4771-bacf-3412eccc69d3)

3. Use the default configuration for installation.  
   ![Default Configuration](https://github.com/user-attachments/assets/3ef9e02b-aa6d-49f4-92c3-d64d3539a813)

4. Choose **Stripe - No Redundancy**, select the disk, and proceed.  
   ![Choose Disk](https://github.com/user-attachments/assets/e26bf8a4-d30c-4f8b-bad7-b3c3c93121a4)

5. Once the installation completes, select **Reboot**.  
   ![Reboot](https://github.com/user-attachments/assets/2296c60c-d355-4902-9789-5f394ef42f15)

---

## 5. Configuring pfSense
1. When prompted about VLANs, enter **n**.  
   ![VLAN Setup](https://github.com/user-attachments/assets/f9a0cf84-ee71-4439-a54a-731c478bcf64)

2. Configure the interfaces:
   - **WAN Interface**:  
     ![WAN Interface](https://github.com/user-attachments/assets/4f3fe5fa-f812-4c77-a728-cb1f7fdd7b1d)
   - **LAN Interface**:  
     ![LAN Interface](https://github.com/user-attachments/assets/ade25300-b7de-45d2-952d-2bf19da796fe)
   - **ISOLATED Interface**:  
     ![ISOLATED Interface](https://github.com/user-attachments/assets/dc1363e8-5b9f-43e6-9833-e7629f46e538)
   - **AD_LAB Interface**:  
     ![AD_LAB Interface](https://github.com/user-attachments/assets/ea899840-4ee0-4bd5-9b48-8f6f6883aa5d)

3. Confirm the configuration by typing **y**.  
   ![Confirm Configuration](https://github.com/user-attachments/assets/4e4f7eef-f07d-41f7-a125-183)

## 6. Importing Kali  

Go to [Kali Official Website](https://kali.org/get-kali/)  

- Click on the image that says Virtual Machines and download the 64-bit version of Virtualbox.  
  ![VM Download Image](https://github.com/user-attachments/assets/ae2d558e-57a4-4d1a-8576-5ad25de659ec)  
  ![Download Details](https://github.com/user-attachments/assets/6430026d-9ca1-46db-9dd6-98e6d758617c)  

After downloading the file, extract it and hit the **Add** button on Virtualbox.  
![VirtualBox Add Button](https://github.com/user-attachments/assets/37ef160d-c250-4151-80df-bdfb038f063c)  

Then choose the `.vbox` extension file.  
![VBox File Selection](https://github.com/user-attachments/assets/5cf67d2e-ebd6-4c6e-ab83-f49f87a27b82)  

Right-click the machine and choose **Network settings**.  
![Network Settings](https://github.com/user-attachments/assets/465b1135-d2b9-4e79-aa75-f6eb9f315ed1)  

Change the network settings to the **pfSense LAN network** that you created.  
![LAN Network](https://github.com/user-attachments/assets/82294fe3-d42c-44cb-8982-732ef4d9e3aa)  

Increase your RAM if necessary. Mine is set to **8GB** because of the tools I use. You can do it under the machine settings.  
![RAM Settings](https://github.com/user-attachments/assets/9cf482b6-64c7-48be-8248-fe25ad5868eb)  

Click **OK** and start the machine. Use the default credentials:  
- **Username:** kali  
- **Password:** kali  

![Login Image](https://github.com/user-attachments/assets/919a0fe4-12fe-4847-acad-0180f51a77b8)  

Open the terminal to confirm you're on the LAN network. The IP Address should be `10.19.19.X/24`. You can later assign a specific IP.  
![Terminal View](https://github.com/user-attachments/assets/3507057e-d6df-423e-9fbe-bde723849657)  

---

## 7. Configuring the pfSense Firewall  

Log into the web portal from the Kali machine by navigating to:  
**https://10.19.19.1**  

If you encounter a warning, click **Advanced** and **Accept the Risk**.  
![Advanced Warning](https://github.com/user-attachments/assets/329900dc-3fec-47e3-8335-42b84cd7069a)  
![Accept the Risk](https://github.com/user-attachments/assets/2fbd799e-db1d-447b-8616-538c8b91f774)  

Default credentials:  
- **Username:** admin  
- **Password:** pfsense  

Click **Next** after logging in.  
![Login Success](https://github.com/user-attachments/assets/4157974c-affb-43d9-aa12-f745ad488560)  

Fill out the **Hostname** and **Domain**, uncheck **Override DNS**, and click **Next**.  
![Hostname and Domain Setup](https://github.com/user-attachments/assets/c3e8a9f6-c266-4412-a404-03931166ec10)  

---

## 8. Configure Interfaces  

### Isolated Interface  

1. Go to **Interfaces** and select **OPT1**.  
   ![Interface OPT1](https://github.com/user-attachments/assets/1d51f12c-c551-4c49-9543-464d5f1f9302)  

2. Set the description to **ISOLATED** and click **Save** and **Apply Changes**.  
   ![Isolated Description](https://github.com/user-attachments/assets/90a7eff1-1423-4d85-921b-a4c649c6f7aa)  

### AD_LAB Interface  

1. Go to **Interfaces** and select **OPT2**.  
   ![Interface OPT2](https://github.com/user-attachments/assets/f6b7f5cc-1410-4316-a3ba-df06c50e7cb6)  

2. Change the description to **AD_LAB**, save, and apply the changes.  
   ![AD_LAB Description](https://github.com/user-attachments/assets/4a1b57ba-2a69-43d3-a743-fde6276d0868)  

---

## 9. Optimize the DNS Resolver Service  

1. Navigate to **Services > DNS Resolver**.  
   ![DNS Resolver](https://github.com/user-attachments/assets/b0dd2a59-96fb-4496-8c93-423fd49f4bfe)  

2. Check both options, then click **Save** and **Apply Changes**.  
   ![DNS Options](https://github.com/user-attachments/assets/7b7612c2-1fde-463d-aa03-ebf2125d3aab)  

3. In the **Advanced Settings**, check both options and save the changes.  
   ![Advanced DNS Settings](https://github.com/user-attachments/assets/e7f537a4-9c21-4fe7-889b-68b01c09afa2)  

---

## 10. Give Kali a Static DHCP Lease  

1. Go to **Status > DHCP Leases**.  
   ![DHCP Leases](https://github.com/user-attachments/assets/1129d9f4-f090-470c-8a27-3202972cff1e)  

2. Add a static mapping for the Kali machine.  
   ![Static Mapping](https://github.com/user-attachments/assets/8e402467-88ac-4272-8336-7f0f00ad6c80)  

3. Set the IP address and click **Save** and **Apply Changes**.  
   ![Static IP](https://github.com/user-attachments/assets/a85398a6-99fe-4090-9bb2-7f5540b39e88)  

## 11. Configure the Firewall Rules

### Create an Alias for RFC1918

This alias will reference all private IPv4 spaces. Go to **Firewall > Aliases**.

![Alias for RFC1918](https://github.com/user-attachments/assets/d1132f04-0a9e-48d1-b6c2-102723e3c00b)

Click **Add** and fill out the form as shown. Then click **Save**.

![RFC1918 Form](https://github.com/user-attachments/assets/b4e2dcdc-e912-4bf3-be1d-097eddbdee25)

---

## Create an Alias for Kali

Click **Add**, Save, and Apply Changes.

![Kali Alias](https://github.com/user-attachments/assets/b9e15e1a-9c14-42e1-8096-26c560fe7891)

---

## Configure LAN Rules

Navigate to **Firewall > Rules** and click **LAN** to add a rule.

![LAN Rules](https://github.com/user-attachments/assets/00e87e94-4a92-49cb-84ea-bdbb97dbbe80)

Click **Add** and copy these rules.

![Add LAN Rule](https://github.com/user-attachments/assets/eb5af460-2933-4136-9018-fda3bd73f433)

Your configuration should look like this:

![LAN Configuration Complete](https://github.com/user-attachments/assets/388db847-7bf8-4421-8563-0153d522d6aa)

---

## Configure ISOLATED Rules

Go to the **ISOLATED** section and add a rule.

![Add ISOLATED Rule](https://github.com/user-attachments/assets/c5e09e3a-6633-4157-8d2f-fffcee1e5938)

Add another rule as shown:

![ISOLATED Rule 2](https://github.com/user-attachments/assets/fd4acef1-4374-4758-ac44-cbe094730803)

---

## Configure AD_LAB Rules

Click on **AD_LAB** and start adding rules.

![AD_LAB Rule 1](https://github.com/user-attachments/assets/354dc273-5e98-41d7-bd3d-1b39e246359d)

This rule blocks traffic to any private IP address. Add another rule above it to allow traffic to Kali.

![AD_LAB Rule 2](https://github.com/user-attachments/assets/21947bc9-1f65-4e6d-b362-3fd67ccc3039)

Final configuration should look like this:

![AD_LAB Rules Complete](https://github.com/user-attachments/assets/35cf63a4-ff61-4fcb-b5a1-bea349450758)

---

## Floating Rules Configuration

Go to **Firewall > Aliases** to add a port alias.

![Port Alias](https://github.com/user-attachments/assets/afd67561-4332-48a6-b4c0-eb89886cb4c3)

Add a rule in the Floating section.

![Floating Rule](https://github.com/user-attachments/assets/5ef5ef01-0caa-4954-a8f9-4917bf8ac593)

Configure two separators to organize your rules.

![Separators](https://github.com/user-attachments/assets/aa9127bd-e1c4-47ff-b04b-fd5d4f644dc9)

---

## Block Firewall Logins

Add a rule to block logins from ISOLATED and AD_LAB subnets.

![Block Logins Rule](https://github.com/user-attachments/assets/5240f215-a47b-4479-8a25-295e3a340417)

Apply changes and save your rules.

---

## Make System Tweaks to pfSense

Go to **System > Advanced > Networking**. Enable the required option and click **Save**.

![System Tweaks](https://github.com/user-attachments/assets/313f82d4-2e26-4f65-ad4f-f641c3c142bc)

---

## 12. Importing Vulnhub VMs to the Lab

Download Metasploitable 2 from [Vulnhub](https://vulnhub.com/entry/metasploitable-2,29/).

Extract the `.vmdk` file from the downloaded ZIP.

![Extract VMDK](https://github.com/user-attachments/assets/6b2f3222-b258-4853-9fbd-acf787fd9469)

Create a new VM in VirtualBox and attach the extracted disk.

![New VM](https://github.com/user-attachments/assets/94cf1927-a8a1-4975-bf93-9c85ba4ef9b5)

Configure the network settings and start the VM.

![Network Settings](https://github.com/user-attachments/assets/ce42f843-1bf5-4bd0-9603-6f11ff9c7a59)

Login credentials for Metasploitable 2

Username: msfadmin 

Password: msfadmin

---

### Verify Connectivity

Check the IP address of the VM with: **ip a**

![IP A](https://github.com/user-attachments/assets/956432cf-afbd-4853-a3c1-84abcc870bea)

Ping the Kali machine from Metasploitable:

![Ping Kali](https://github.com/user-attachments/assets/9468c8a9-9bd3-46c4-a2da-fc04dc64cee8)

Verify that external traffic to Google is blocked as expected.

![Google Ping Blocked](https://github.com/user-attachments/assets/3e2e770e-7db8-488b-bbb7-b4dac1e7d480)

---

### Final Steps

Ensure the Kali and Metasploitable VMs can communicate.

# 13. Building an Active Directory Lab

This guide explains how to set up a Windows Server 2019 and Windows 10 Enterprise virtual machines, configure an Active Directory environment, and create domain services.

## Prerequisites

- Download **Windows ISO files** from the [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter):
  - **Windows Server 2019**: Download ISO, fill out required info, select your language.
  - **Windows 10 Enterprise**: Download ISO-Enterprise, fill out required info, select your language.

---

## Steps Overview

1. [Create Virtual Machines](#create-virtual-machines)  
2. [Install and Configure Windows Server 2019](#install-and-configure-windows-server-2019)  
3. [Create Windows 10 Enterprise VM](#create-windows-10-enterprise-vm)  
4. [Configure AD Domain Services](#configure-ad-domain-services)  
5. [Set Up DNS and DHCP](#set-up-dns-and-dhcp)  
6. [Create a Domain Administrator Account](#create-a-domain-administrator-account)  

---

## Create Virtual Machines

### Windows Server VM
1. In VMware, click **New VM** and select the ISO image.
2. Allocate at least **2048 MB RAM** (preferably 4096 MB).
3. Adjust **Network Settings**: Switch to the `AD_LAB` network.

### Windows 10 VM
1. Create a new VM named `Win10EnterpriseTemplate`.
2. Use **2048-4096 MB RAM**.
3. Change the **network adapter** to the `AD_LAB` network.
4. Save settings but **do not start the VM**.

---

## Install and Configure Windows Server 2019

1. Start the VM and begin installation.
2. Choose **Windows Server 2019 Standard Evaluation (Desktop Experience)**.
3. Create a new drive, click **Next**, and complete installation.
4. Set a **local Administrator password** and log in.
5. Configure the **network adapter**:
   - IP: `10.25.25.2`
   - Subnet Mask: `255.255.255.0`
   - Gateway: `10.25.25.1`
   - DNS: `10.25.25.2`

6. Rename the server to `DeathStar` (or any name of your choice) and **restart**.

---

## Create Windows 10 Enterprise VM

1. Start the VM, install Windows 10, and configure basic settings.
2. Change the network adapter to use the `AD_LAB` network.

---

## Configure AD Domain Services

1. Open **Server Manager** > **Manage** > **Add Roles and Features**.
2. Install the following:
   - **Active Directory Domain Services**
   - **DNS Server**

3. After installation, click **Promote this server to a domain controller**.
4. Create a new forest, using a domain name like `galactic.empire`.
5. Set a restore password and complete the setup.  
6. The server will reboot automatically.

---

## Set Up DNS and DHCP

### Configure DNS Forwarders
1. Open the **DNS Manager**.
2. Expand **DNS** > **DC1** > **Forwarders**.
3. Add the IP of the **pfSense gateway** (`10.25.25.1`).

### Install and Configure DHCP
1. In **Server Manager**, go to **Manage** > **Add Roles and Features**.
2. Install **DHCP Server**.
3. Open **DHCP Manager** > Right-click **IPv4** > **New Scope**.
4. Configure:
   - Address Range: `10.25.25.100 - 10.25.25.200`
   - Gateway: `10.25.25.1`
   - DNS: `10.25.25.2`

---

## Create a Domain Administrator Account

1. Open **Active Directory Users and Computers**.
2. Right-click **Users** > **New** > **User**.
3. Fill in details and set a password.
4. Add the user to the **Domain Admins** group.

---

## Taking Snapshots

1. In VMware, click on the **VM menu** > **Snapshots** > **Take Snapshot**.
2. Label it (e.g., `Pre-Domain Setup`) and click **OK**.

---

## Conclusion

Your Active Directory lab is now set up and ready for use. You can roll back to the snapshot if needed, and the domain services, DHCP, and DNS settings are configured for optimal internal network testing.


