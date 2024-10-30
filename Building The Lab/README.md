# Steps to Build the Lab

## Table of Contents
- [1. Planning Phase](#1-planning-phase)
- [2. Downloading and Installing VirtualBox](#2-downloading-and-installing-virtualbox)
- [3. Building a pfSense VM](#3-building-a-pfsense-vm)
- [4. Installing pfSense](#4-installing-pfsense)
- [5. Configuring pfSense](#5-configuring-pfsense)

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
