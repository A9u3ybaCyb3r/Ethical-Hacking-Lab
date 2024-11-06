# Steps to Build the Lab

## Table of Contents
- [1. Planning Phase](#1-planning-phase)
- [2. Downloading and Installing VirtualBox](#2-downloading-and-installing-virtualbox)
- [3. Building a pfSense VM](#3-building-a-pfsense-vm)
- [4. Installing pfSense](#4-installing-pfsense)
- [5. Configuring pfSense](#5-configuring-pfsense)
- [6. Importing Kali](#6-importing-kali)
- [7.Configuring the pfSense firewall](#7-configuring-the-pfSense-firewall)
- [8.Importing Vulnhub VMs to the lab ](#8-importing-vulnhub-vms-to-the-lab)
- [9. Building an Active Directory](#9-building-an-active-directory)
- [10. Make your AD Lab vulnerable](#10-make-your-ad-lab-vulnerable)
- [11.Building a Pivoting Lab To Practice External Pentest](#11-building-a-pivoting-lab-to-practice-external-pentest)

---

# 1. Planning Phase

 We will build a network diagram to represent our lab visually.
   
[Network Diagram](https://github.com/A9u3ybaCyb3r/Virtual-Network-Penetration-Testing-Lab/blob/main/Building%20The%20Lab/Empire%20Net%20Diagram.drawio.pdf)

---
 
# 2. Downloading VirtualBox and Installing VirtualBox

1. Go to the [VirtualBox download page](https://www.virtualbox.org/wiki/Downloads) and download the installer suitable for your operating system.

   ![VirtualBox download page](https://github.com/user-attachments/assets/f291de59-ca36-44c4-93c0-dbb21030192f)

2. **Don't forget to download the Extension Pack**, which adds extra features to VirtualBox.

   ![Extension pack download](https://github.com/user-attachments/assets/40457f5e-4417-4b4b-b642-f0c4c704617e)

3. After downloading the file, open the installer and proceed with the default settings to complete the installation.

4. After installation, open VirtualBox, then go to:
   - **File** > **Tools** > **Extension Pack Manager**

   ![Accessing Extension Pack Manager](https://github.com/user-attachments/assets/67c5e941-0cbf-4dc1-95e9-8ef9ffa4d88d)

5. In the Extension Pack Manager, click the **Install** button, then locate and select the downloaded VirtualBox Extension Pack file.

   ![Installing Extension Pack](https://github.com/user-attachments/assets/2d202300-7d52-43c7-baa2-291f35362450)
   
   ![Final installation step](https://github.com/user-attachments/assets/230cf88a-54de-4522-858b-991670742f14)


---

# 3. Building a pfSense VM

### Step 1: Download the pfSense Installation File

1. Open [this link](https://www.google.com/search?q=site%3A*.netgate.com+download+-site%3Aforum.netgate.com+-site%3Adocs.netgate.com+-inurl%3Ablog+-site%3Awww.netgate.com+-site%3Ashop.netgate.com+-site%3Aforums.netgate.com+-site%3Ainfo.netgate.com&ref=benheater.com) to locate the latest pfSense ISO.
2. Select the latest version of pfSense available.

   ![Download pfSense](https://github.com/user-attachments/assets/b1c3be2d-a7dd-437d-af8d-3af6658d3056)

### Step 2: Extract the Downloaded File

1. Use 7-Zip (or any file extraction tool) to extract the downloaded pfSense ISO file.

   ![Extract with 7-Zip](https://github.com/user-attachments/assets/b395d9a3-6e1c-4d7d-a32f-352084f731eb)

### Step 3: Create a New Virtual Machine

1. Open your virtualization software and create a new virtual machine.
2. Name your VM, choose the folder to save it, select the extracted ISO as the installation image, and set the VM type and version (Linux/BSD, 64-bit).

   ![New Machine Settings](https://github.com/user-attachments/assets/a1bed139-45f7-4864-9d89-74ef542fc0cc)

    ![image](https://github.com/user-attachments/assets/fa7194ac-cf8c-44f5-882e-62213f7dc89d)
   
   ![image](https://github.com/user-attachments/assets/56b00275-2a31-4da9-8535-45e44f417f51)

   ![image](https://github.com/user-attachments/assets/bf359848-201f-438d-992a-66db8d18b070)

   ![image](https://github.com/user-attachments/assets/e73ca9a0-ee82-4aff-83a5-d966640e2c60)


**Important**: **Do not start the VM yet!**

### Step 4: Adjust VM Settings

1. **Boot Order**: Go to the VM's settings, adjust the boot order as shown below, and uncheck the floppy disk option. This ensures that pfSense boots from the ISO.

   ![Boot Order](https://github.com/user-attachments/assets/f69d55aa-465c-4616-a2cb-ceac898494ef)

2. **Audio**: Go to Audio settings and disable it.

   ![Disable Audio](https://github.com/user-attachments/assets/0677dd7d-2d4d-4383-8697-01d8fe5b8c04)

3. **USB**: Go to USB settings and disable it.

   ![Disable USB](https://github.com/user-attachments/assets/96c4257b-b5aa-416e-a86a-2f23360f1d0c)

### Step 5: Configure Network Interfaces

In Network settings, configure the following adapters:

- **Adapter 1 (WAN)**: Set up as shown below.

   ![WAN Adapter](https://github.com/user-attachments/assets/7ba13507-0c08-4ce8-a7a5-48591123ad08)

- **Adapter 2 (LAN)**: Configure as shown below.

   ![LAN Adapter](https://github.com/user-attachments/assets/924e9715-78d5-45ba-8176-7dcb7d878862)

- **Adapter 3 (Isolated)**: Set up as shown below.

   ![Isolated Adapter](https://github.com/user-attachments/assets/7f6f4678-f46f-4344-8b99-9b39a45d55cf)

- **Adapter 4 (AD-Lab)**: Configure as shown below.

   ![AD-Lab Adapter](https://github.com/user-attachments/assets/7fe81f34-1f06-443e-bbaf-251de2fc6024)

### Step 6: Start the VM

After completing the settings above, start the VM to begin the pfSense installation.

---

# 4. Installing pfSense

1. **Start the VM**  
   Start your pfSense virtual machine.

   ![Start VM](https://github.com/user-attachments/assets/e8207eaf-82db-4e52-a6e0-5efb4512622d)

2. **Boot pfSense**  
   When prompted, press **Enter** to boot.

   ![Press Enter](https://github.com/user-attachments/assets/16fb7088-5ea1-44f1-ac24-7f3a8b9eddea)

3. **Select Installation**  
   Choose **Install pfSense** and press **Enter**.

   ![Install pfSense](https://github.com/user-attachments/assets/ebc7e2fa-5d63-4bcf-ad4a-7e31b10de690)

4. **Choose Partitioning Scheme**  
   - Select **Auto (ZFS)** as the partitioning scheme.

     ![Auto ZFS](https://github.com/user-attachments/assets/fe0a64bc-c58a-4771-bacf-3412eccc69d3)

5. **Default Configuration**  
   - Proceed with the installation by selecting the **default configuration**.

     ![Default Configuration](https://github.com/user-attachments/assets/3ef9e02b-aa6d-49f4-92c3-d64d3539a813)

6. **Select Disk Mode**  
   - Choose **Stripe - No Redundancy** for the disk mode.

     ![Stripe No Redundancy](https://github.com/user-attachments/assets/f109234a-7691-4aba-beb2-21ff7bb2fc25)

7. **Select Disk**  
   - Use the **Space Bar** to select the disk where you want to install pfSense. The selected disk will show an asterisk (*).

     ![Select Disk](https://github.com/user-attachments/assets/e26bf8a4-d30c-4f8b-bad7-b3c3c93121a4)

8. **Confirm Installation**  
   - Choose **YES** to confirm and continue with the installation.

     ![image](https://github.com/user-attachments/assets/4e52f142-af31-477e-bb39-06a898fe9910)

9. **Wait for Installation**  
   - Wait for the installation to complete. Once done, choose **Reboot** to restart the system.

     ![Reboot](https://github.com/user-attachments/assets/2296c60c-d355-4902-9789-5f394ef42f15)

---

# 5. Configuring pfSense

### Initial Setup

1. **VLAN Configuration Prompt**  
   When the VM finishes booting, you'll be prompted with:  
   *"Should VLANs be set up now [y|n]?"*  
   - Choose **n**.

   ![VLAN Prompt](https://github.com/user-attachments/assets/f9a0cf84-ee71-4439-a54a-731c478bcf64)

2. **Set Interfaces**  
   Enter the interfaces as follows:

   - **WAN Interface**: Assign as shown.

     ![WAN Interface](https://github.com/user-attachments/assets/4f3fe5fa-f812-4c77-a728-cb1f7fdd7b1d)

   - **LAN Interface**: Assign as shown.

     ![LAN Interface](https://github.com/user-attachments/assets/ade25300-b7de-45d2-952d-2bf19da796fe)

   - **ISOLATED Interface**: Assign as shown.

     ![ISOLATED Interface](https://github.com/user-attachments/assets/dc1363e8-5b9f-43e6-9833-e7629f46e538)

   - **AD_LAB Interface**: Assign as shown.

     ![AD_LAB Interface](https://github.com/user-attachments/assets/ea899840-4ee0-4bd5-9b48-8f6f6883aa5d)

3. **Confirm Configuration**  
   Review your setup and confirm by entering **y**.

   ![Confirm](https://github.com/user-attachments/assets/4e4f7eef-f07d-41f7-a125-1836168c733f)

### Setting Up the Interfaces

- **WAN Interface**: Automatically pulls an IP address from your network.
- **LAN Interface**: Default IP is **192.168.1.1/24** (we’ll change this later).
- **OPT1** (ISOLATED Interface): Unconfigured; we'll configure it later.
- **OPT2** (AD_LAB Interface): Unconfigured; we'll configure it later.

   ![Interface Overview](https://github.com/user-attachments/assets/32211990-aa57-4a3d-b86a-7dacca3b3e1d)

---

### Configure the LAN

1. **Enter LAN Configuration Mode**  
   - Select option **2**.

   ![Option 2](https://github.com/user-attachments/assets/ded46fbe-ea36-48c8-89a1-ab5752bf9405)

2. **Set LAN IP Address**  
   - Choose **2** again to modify the LAN IP.

   ![Choose 2](https://github.com/user-attachments/assets/2fd90833-1370-4f2f-a932-cf4a8a090c68)

3. **Static IP Configuration**  
   - Enter **n** for static IP setup.

   ![Static IP](https://github.com/user-attachments/assets/a33a78e9-4594-4597-b44a-4f61a55f324b)

4. **Enter IP Address and Subnet Mask**  
   - Provide the IP and subnet mask.

     ![Enter IP](https://github.com/user-attachments/assets/d44ef8c7-3c84-4c2d-9a5e-95db20d74310)  
     ![Subnet Mask](https://github.com/user-attachments/assets/b7dd1628-263f-4e7a-be09-dd3d69c55583)

5. **DHCP and TLS Configuration**  
   - Enable **DHCP** (enter **y**).
   - Enter the DHCP range (start and end).
   - Confirm to keep using **TLS** on the web portal (enter **n**).
   - For the rest of the options that appear hit **Enter**

     ![DHCP Range](https://github.com/user-attachments/assets/8701352d-1e83-4ce3-bfcd-a18683d29d21)  
     ![TLS Confirmation](https://github.com/user-attachments/assets/cee8c91a-3fea-497f-bcd4-c8eb6f794aa8)

6. **Finish LAN Setup**  
   - Complete the configuration and press **Enter**.

     ![Finish LAN](https://github.com/user-attachments/assets/18fb87f1-88ba-4002-a764-e623e34fd87d)

---

### Configure the ISOLATED Interface

1. **Enter ISOLATED Interface Mode**  
   - Select option **2** then choose **3** to configure **OPT3**.

   ![Option 3](https://github.com/user-attachments/assets/0883dce2-053f-44fe-907b-3d96ae9ea5b5)

2. **Set Static IP**  
   - Choose **n** for static IP configuration.

   ![Static IP](https://github.com/user-attachments/assets/399d4ace-edf9-4359-a375-771a37bb71f3)

3. **Enter IP Address, Subnet Mask, and DHCP Range**  
   - Provide the IP, subnet mask, and DHCP range. Enable DHCP (enter **y**).

     ![IP and Subnet](https://github.com/user-attachments/assets/d0f7ce08-b81e-4cd6-b3bf-b92a907264de)

4. **Finish ISOLATED Setup**  
   - Confirm TLS usage for web portal (enter **n**).

     ![TLS](https://github.com/user-attachments/assets/c77ad20b-be1d-4135-8876-670b92f10a8a)  
     ![Finish ISOLATED](https://github.com/user-attachments/assets/93e0a0bd-f519-4ff1-9d6b-b945b2502173)

---

### Configure the AD_LAB Interface

1. **Enter AD_LAB Interface Mode**  
   - Select option **2** then choose **4** to configure **OPT4**.

   ![Option 4](https://github.com/user-attachments/assets/7119fee6-3375-4462-abd8-7d88f3423421)

2. **Set Static IP**  
   - Enter **n** for static IP setup.

   ![Static IP](https://github.com/user-attachments/assets/8b091b1f-4971-4ab4-8a8f-9690e7b12455)

3. **Enter IP Address, Subnet Mask, and Disable DHCP**  
   - Provide the IP, subnet mask, and disable DHCP (enter **n**).

     ![IP and Subnet](https://github.com/user-attachments/assets/dc69c922-e5b7-45ca-a1f1-6f9a19df0f40)  
     ![Disable DHCP](https://github.com/user-attachments/assets/b691fdee-718b-4230-a0ba-c4915b2e1063)

4. **Finish AD_LAB Setup**  
   - Confirm TLS usage (enter **n**).

     ![Finish AD_LAB](https://github.com/user-attachments/assets/7d8c3f96-2db1-462f-a122-0c7ee1d66107)

---

### Final Check

Review the completed configuration. Note that IP addresses may vary based on your setup.

![Final Configuration](https://github.com/user-attachments/assets/2a0f79b8-93a5-49ee-823b-f4970d67dd11)

### Important Security Note

To avoid exposing the pfSense web console to public networks, we will **not make it accessible from the WAN**. Configuration of firewall rules will be completed using a Kali VM later in the setup.


---

# 6. Importing Kali Linux

1. **Download Kali Linux**  
   - Go to [https://kali.org/get-kali/](https://kali.org/get-kali/).
   - Click on **Virtual Machines** and download the 64-bit **VirtualBox** version.

   ![Download Page](https://github.com/user-attachments/assets/ae2d558e-57a4-4d1a-8576-5ad25de659ec)

   ![Select Version](https://github.com/user-attachments/assets/6430026d-9ca1-46db-9dd6-98e6d758617c)

2. **Extract and Add to VirtualBox**  
   - After downloading, extract the file.
   - In VirtualBox, click **Add** and select the `.vbox` file.

   ![Add to VirtualBox](https://github.com/user-attachments/assets/37ef160d-c250-4151-80df-bdfb038f063c)

   ![Select .vbox File](https://github.com/user-attachments/assets/5cf67d2e-ebd6-4c6e-ab83-f49f87a27b82)

3. **Configure Network Settings**  
   - Right-click the Kali machine, go to **Network** settings.

   ![Network Settings](https://github.com/user-attachments/assets/465b1135-d2b9-4e79-aa75-f6eb9f315ed1)

   - Change the network adapter to the **pfSense LAN** network you created.

   ![Select pfSense LAN Network](https://github.com/user-attachments/assets/82294fe3-d42c-44cb-8982-732ef4d9e3aa)

4. **Adjust RAM**  
   - Increase the RAM based on your requirements (e.g., 8GB for heavy usage). You can do this in **Machine Settings**.

   ![Adjust RAM](https://github.com/user-attachments/assets/9cf482b6-64c7-48be-8248-fe25ad5868eb)

5. **Start the Machine**  
   - Click **OK** to save the settings, then start the Kali machine.
   - Login with the default credentials: **Username**: `kali`, **Password**: `kali`.

   ![Login Screen](https://github.com/user-attachments/assets/919a0fe4-12fe-4847-acad-0180f51a77b8)

6. **Verify Network Connection**  
   - Open a terminal and check the IP address to ensure you're on the LAN network. It should show an IP in the `10.19.19.X/24` range.
   - You can later configure a specific IP address if needed.

   ![Check Network Connection](https://github.com/user-attachments/assets/3507057e-d6df-423e-9fbe-bde723849657)

---

# 7. Configuring the pfSense firewall

## Log into the Web Portal

1. Open Firefox on your Kali machine and go to:  
   **`https://10.19.19.1`**  
   ![Login Portal](https://github.com/user-attachments/assets/db0ecfcb-6a40-4817-8187-8cabda8db0bd)

2. If you encounter a security warning, click **Advanced**.  
   ![Advanced Security Warning](https://github.com/user-attachments/assets/329900dc-3fec-47e3-8335-42b84cd7069a)

3. Accept the risk by clicking on **Accept the Risk and Continue**.  
   ![Accept Risk](https://github.com/user-attachments/assets/2fbd799e-db1d-447b-8616-538c8b91f774)

4. Enter Default Credentials:  
   - Username: `admin`  
   - Password: `pfsense`  
   Click **Next** after logging in.  
   ![Default Credentials](https://github.com/user-attachments/assets/4157974c-affb-43d9-aa12-f745ad488560)

5. Fill out Hostname and Domain:  
   Uncheck **Override DNS**. You can use any name you prefer. Click **Next**.  
   ![Hostname and Domain](https://github.com/user-attachments/assets/c3e8a9f6-c266-4412-a404-03931166ec10)

6. Double-check your timezone and click **Next**.  
   ![Timezone Setting](https://github.com/user-attachments/assets/6a3875bf-c8be-4140-863b-3296c20aa10a)

7. Scroll down and uncheck the option to allow double-NAT, as the WAN network is also private. Click **Next**.  
   ![Double-NAT Option](https://github.com/user-attachments/assets/1fa7b998-b55c-4207-a454-831a331e4356)

8. Click **Next** again.  
   ![Next Confirmation](https://github.com/user-attachments/assets/d01ad2a6-3c77-446e-80a0-34b74245ba2c)

9. Change the Admin Password: Remember to note the new password.  
   ![Change Admin Password](https://github.com/user-attachments/assets/73b60b4c-6325-479f-b7be-fe1ef1b8e934)

10. Click **Next** and then **Finish** to complete the setup.

---

## Configure the Interfaces

### Isolated Interface

11. Go to `Interfaces` and choose **OPT1**.  
   ![OPT1 Interface](https://github.com/user-attachments/assets/1d51f12c-c551-4c49-9543-464d5f1f9302)

12. Set the **Description** to **ISOLATED**. Then scroll down and click **Save** and **Apply Changes**.  
   ![Isolated Interface Save](https://github.com/user-attachments/assets/90a7eff1-1423-4d85-921b-a4c649c6f7aa)  
   ![Isolated Interface Apply Changes](https://github.com/user-attachments/assets/5e86a71c-cb18-452a-b6f8-687eebaf96c8)

### AD_LAB Interface

13. Go to `Interface` and choose **OPT2**.  
   ![OPT2 Interface](https://github.com/user-attachments/assets/f6b7f5cc-1410-4316-a3ba-df06c50e7cb6)

14. Change the **Description** to **AD_LAB**. Then scroll down and click **Save** and **Apply Changes**.  
   ![AD_LAB Interface Save](https://github.com/user-attachments/assets/4a1b57ba-2a69-43d3-a743-fde6276d0868)  
   ![AD_LAB Interface Apply Changes](https://github.com/user-attachments/assets/44d8157c-8736-484a-8def-c67444700015)

### Optimize the DNS Resolver Service

15. Go to `Services > DNS Resolver`.  
   ![DNS Resolver](https://github.com/user-attachments/assets/b0dd2a59-96fb-4496-8c93-423fd49f4bfe)

16. Check both options, then click **Save** and **Apply Changes**.  
   ![DNS Resolver Options](https://github.com/user-attachments/assets/7b7612c2-1fde-463d-aa03-ebf2125d3aab)

17. Go to Advanced Settings in DNS Resolver and check both options. Don’t forget to **Save and Apply Changes**.  
   ![DNS Resolver Advanced Settings](https://github.com/user-attachments/assets/e7f537a4-9c21-4fe7-889b-68b01c09afa2)

### Give Kali a Static DHCP Lease

18. Go to `Status > DHCP Leases`.  
   ![DHCP Leases](https://github.com/user-attachments/assets/1129d9f4-f090-470c-8a27-3202972cff1e)

19. Click on the button to **add a static mapping**. (Note: The hostname may differ; my Kali machine is named Vulnhunter).  
   ![Add Static Mapping](https://github.com/user-attachments/assets/8e402467-88ac-4272-8336-7f0f00ad6c80)

20. Set the IP address for your Kali machine. Click **Save** and **Apply Changes**.  
   ![Set Kali IP Address](https://github.com/user-attachments/assets/a85398a6-99fe-4090-9bb2-7f5540b39e88)

### Configure the Firewall Rules

21. Create an Alias for RFC1918. Go to `Firewall > Aliases`.  
   ![Firewall Aliases](https://github.com/user-attachments/assets/d1132f04-0a9e-48d1-b6c2-102723e3c00b)

22. Click **Add**, fill out the necessary details, then click **Save**.  
   ![Add RFC1918 Alias](https://github.com/user-attachments/assets/b4e2dcdc-e912-4bf3-be1d-097eddbdee25)

23. Create an Alias for Kali: Click **Add**, then **Save** and **Apply Changes**.  
   ![Add Kali Alias](https://github.com/user-attachments/assets/b9e15e1a-9c14-42e1-8096-26c560fe7891)

### Configure LAN Rules

24. Go to `Firewall > Rules`.  
   ![Firewall Rules](https://github.com/user-attachments/assets/00e87e94-4a92-49cb-84ea-bdbb97dbbe80)

25. Select LAN and click **Add Rule**.  
   ![Add LAN Rule](https://github.com/user-attachments/assets/eb5af460-2933-4136-9018-fda3bd73f433)

26. Copy the following rules:  
   ![LAN Rules](https://github.com/user-attachments/assets/5c1b56a4-808a-45e8-9669-cf0f18cc6b54)

27. This is how it should look when you are done:  
   ![Finished LAN Rules](https://github.com/user-attachments/assets/388db847-7bf8-4421-8563-0153d522d6aa)

### Configure ISOLATED Rules

28. Click on ISOLATED and then click **Add Rule**.  

![ISOLATED Add Rule](https://github.com/user-attachments/assets/c5e09e3a-6633-4157-8d2f-fffcee1e5938)  

![ISOLATED Add Rule Screenshot 1](https://github.com/user-attachments/assets/fd4acef1-4374-4758-ac44-cbe094730803)

![ISOLATED Add Rule Screenshot 2](https://github.com/user-attachments/assets/f30108a8-dd32-43fb-893f-51d6fb4d3707)

  - Add another rule:

    ![ISOLATED Add Rule](https://github.com/user-attachments/assets/9df9fcf5-e0a0-4d03-8aaa-ae7f844d5856)

    ![ISOLATED Add Rule Screenshot 3](https://github.com/user-attachments/assets/56e4d325-79c9-401a-93dc-8d9c5ef1b505)

  - Lastly, we add an isolated rule:
    ![ISOLATED Add Rule](https://github.com/user-attachments/assets/8c67283a-c782-4803-aad0-d1f509d66e08)

    ![ISOLATED Add Rule Screenshot 4](https://github.com/user-attachments/assets/a5fa3d8b-e313-4b79-84dc-98f83b19f941)

    ![ISOLATED Add Rule Screenshot 5](https://github.com/user-attachments/assets/dc5850a1-70a8-4548-b69e-bc1dc935007e)

### Configure AD_LAB Rules

29. Go to `Firewall > Rules > AD_LAB`.  
   ![AD_LAB Rules](https://github.com/user-attachments/assets/354dc273-5e98-41d7-bd3d-1b39e246359d)

30. Add rules:

    ![AD_LAB Rules Screenshot 1](https://github.com/user-attachments/assets/a92c06e5-bc3d-4368-a396-8159cd84619a)  
   
   ![AD_LAB Rules Screenshot 2](https://github.com/user-attachments/assets/21947bc9-1f65-4e6d-b362-3fd67ccc3039)

31. Ensure the rule to block traffic to private IPs is below any allow rules.  

  - Add another rule:

    ![image](https://github.com/user-attachments/assets/cd42f591-7f97-4725-9baa-48bcc7b4d413)

    ![image](https://github.com/user-attachments/assets/7c7f7019-a65c-4ed8-bb69-b814c6fd6166)
   
  - Add another rule:

    ![image](https://github.com/user-attachments/assets/5c0cb759-aded-4b16-85ab-5286e6bf6e58)

    ![image](https://github.com/user-attachments/assets/13aa5108-fdfe-44b4-9577-d0e8caf224fa)

  - Final rule:

    ![image](https://github.com/user-attachments/assets/6db4663a-9c11-4cff-9f53-a0739ae4156e)

    ![image](https://github.com/user-attachments/assets/7b9235e4-b712-42b4-b076-1889f7358bc3)

    ![image](https://github.com/user-attachments/assets/35cf63a4-ff61-4fcb-b5a1-bea349450758)


### Configure Floating Rules

32. Create Port Alias: Go to `Firewall > Aliases > Ports` and add the required rule.

    ![image](https://github.com/user-attachments/assets/619133f6-b021-44a0-9ac4-8d2b1b7748c1)

    ![Port Alias](https://github.com/user-attachments/assets/08a31367-b3a1-463d-9873-23ca20873fc9)

34. Add Separators: Go to `Firewall > Rules > Floating` and add two separators.

    ![image](https://github.com/user-attachments/assets/e0a96622-c717-4600-bfed-ccc811c7bbd9)

![Add Floating Separator](https://github.com/user-attachments/assets/1bc1957f-3550-4f6a-a8c4-2c7b6d8778c5)

- You should have two separators:

  ![image](https://github.com/user-attachments/assets/aa9127bd-e1c4-47ff-b04b-fd5d4f644dc9)

34. Block Login Access: Create a floating rule to prevent ISOLATED and AD_LAB subnets from accessing firewall login ports.

     ![image](https://github.com/user-attachments/assets/b34e2ea1-ab27-4dcd-a6ec-0aba4839348e)

    ![image](https://github.com/user-attachments/assets/ddde4107-32c5-4d1f-8691-c952f0eed999)

    ![image](https://github.com/user-attachments/assets/5240f215-a47b-4479-8a25-295e3a340417)

    ![image](https://github.com/user-attachments/assets/2936151e-28c2-4105-b561-dc94fc86df5d)

![Block Login Access Rule](https://github.com/user-attachments/assets/efdb2193-6a39-4d8e-81be-d76b396d1223)

---

## System Tweaks

35. Go to `System > Advanced > Networking`. Scroll to find the specific network option, check it, then click **Save** and **Apply Changes**.  
   ![Specific Network Option](https://github.com/user-attachments/assets/313f82d4-2e26-4f65-ad4f-f641c3c142bc)

36. Reboot pfSense: Go to `Diagnostics > Reboot`.  

---

## Final Steps

37. Update Kali's Network: Open a terminal and run:  

   `sudo ip link set eth0 down && sudo ip link set eth0 up`

---

# 8. Importing Vulnhub VMs to the lab

## Step 1: Download Metasploitable 2

- **VM Info on Vulnhub**: [Metasploitable 2 Entry](https://vulnhub.com/entry/metasploitable-2,29/)
- **Vulnhub Download Link**: [Download Metasploitable 2](https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip)

After downloading, you will get a zip file. Extract it to access the `.vmdk` file.

![Extracted File](https://github.com/user-attachments/assets/852efc57-8754-4618-ada7-5e8d4533cf57)

## Step 2: Set Up the VM in VirtualBox

1. Open **VirtualBox** and click on **New** to create a new virtual machine.

   ![New VM](https://github.com/user-attachments/assets/94cf1927-a8a1-4975-bf93-9c85ba4ef9b5)

2. Follow the prompts to configure your VM settings as needed.

   ![VM Configuration](https://github.com/user-attachments/assets/23473cf4-7b97-401e-b5e4-78b4c37a23c5)

3. When prompted, select **Add a disk**.

   ![Add Disk](https://github.com/user-attachments/assets/d53613eb-96ac-47c7-b7d7-1225d52424a6)

4. Click on the disk icon to choose your disk file.

   ![Disk Icon](https://github.com/user-attachments/assets/ce21926b-c715-476c-899a-a5e430dda9aa)

5. Navigate to where you downloaded and unzipped Metasploitable 2. Select the `.vmdk` file.

   ![Select VMDK](https://github.com/user-attachments/assets/c26467eb-5e9b-4423-8447-8cffc81f6623)

6. Confirm that it looks correct and click **Finish**.

   ![Finish VM Setup](https://github.com/user-attachments/assets/b083e8e6-1b8e-4e3f-a18e-d087a9eadd4a)

## Step 3: Configure Network Settings

1. **Do not start the VM yet**. Right-click the Metasploitable 2 VM and choose **Settings**.

   ![Settings](https://github.com/user-attachments/assets/ce42f843-1bf5-4bd0-9603-6f11ff9c7a59)

2. Go to **Network** settings and configure as needed.

   ![Network Settings](https://github.com/user-attachments/assets/61ba46aa-5273-462a-a242-9aaa1d5c6e2a)

## Step 4: Start the VM and Log In

1. Now, you can start the VM.
2. Log in with the following credentials:
   - **Username**: `msfadmin`
   - **Password**: `msfadmin`

   ![Login Screen](https://github.com/user-attachments/assets/1856ad49-3f18-46ed-aea6-a9714d7528d6)

## Step 5: Check the IP Address

1. Use the command below to check the IP address of the Metasploitable VM:

`ip a`

![image](https://github.com/user-attachments/assets/956432cf-afbd-4853-a3c1-84abcc870bea)

## Step 6: Ping the Kali Machine

1. Start by pinging your Kali machine from Metasploitable 2 using the IP address.

![image](https://github.com/user-attachments/assets/9468c8a9-9bd3-46c4-a2da-fc04dc64cee8)

2. Next, use the local DNS suffix to ping.

![image](https://github.com/user-attachments/assets/69a58057-7d8e-4dbf-85eb-5673d19234bf)

3. Finally, try to ping Google. This should fail because we’ve blocked all outside traffic.

![image](https://github.com/user-attachments/assets/3e2e770e-7db8-488b-bbb7-b4dac1e7d480)

## Step 7: Ping Metasploitable from Kali

Lastly, check connectivity by pinging the Metasploitable VM from your Kali machine.

![image](https://github.com/user-attachments/assets/4e73696b-f0d9-40fb-92ab-27ce6058ded5)

---

# 9. Building an Active Directory

## Setting Up Windows Server and Domain Controller

### Downloading the ISOs

### Step 1: Visit Microsoft Evaluation Center
1. Go to Google and search for "Microsoft Evaluation Center."
   - Official link: [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter)
2. Open the official Microsoft Evaluation Center page from the search results.

### Step 2: Browse Available Software
- The Evaluation Center offers trial versions of Windows, Windows Server, SQL Server, and more.
- For this lab, download **Windows 10 Enterprise** and **Windows Server 2022**.

### Step 3: Download Windows 10 Enterprise
1. Select **Windows 10 Enterprise** from the list.
2. Choose the **64-bit ISO** version for your region (e.g., United States).
3. Fill out the registration form (generic information is acceptable).
4. Click **Download Now** to start the download.

### Step 4: Download Windows Server 2022
1. Select **Windows Server 2022** and open the download page.
2. Choose the **64-bit ISO** version.
3. Complete the registration form, then click **Download Now** to begin.

### Step 5: Notes
- Note that these downloads are large (Windows 10 Enterprise is ~5.2 GB, Windows Server 2022 is ~4.7 GB).
- After 90 days, the OS may prompt for activation or start shutting down if inactive. Reboot as needed for testing.

---

## Setting Up the Domain Controller

### Step 1: Create a New Virtual Machine
1. In VMware or VirtualBox, select **Create a New Virtual Machine**.
2. Choose the **Typical** setup option.
3. Browse for the **Windows Server 2022 ISO** file you downloaded and select it.

### Step 2: Operating System Selection
- Choose **Windows Server 2016** if Windows Server 2022 isn’t listed. This won’t affect the setup.

### Step 3: Configure Disk Space
- Allocate **at least 60 GB** of disk space.
- Select the option to **Split virtual disk into multiple files** for efficient disk space use.

### Step 4: Adjust Virtual Machine Settings
1. Open **Edit Virtual Machine Settings**.
2. Set memory to **4–8 GB** (8 GB recommended if available).
3. Remove any **floppy disk device** if it appears.

### Step 5: Power On and Install Windows Server
1. Power on the virtual machine.
2. Press any key to boot from the ISO when prompted.
3. Follow installation prompts, choosing:
   - **Language and region** (defaults are typically fine).
   - **Standard Evaluation Desktop Experience** as the installation type.
   - Accept **license terms**.
   - **Custom installation** on Drive 0 (unallocated space).

### Step 6: Complete Initial Setup
- After installation, Windows will reboot.
- Set an **administrator password** (e.g., `P@$$w0rd!`).

### Step 7: Install VMware Tools (Optional but Recommended)
1. In VMware, go to **VM > Install VMware Tools**.
2. Run the `setup64` file from the **D drive** to install the tools.
3. Choose the **Complete** installation option, then finish and reboot if needed.

### Step 8: Rename the Computer
1. Open the Start menu and search for **View your PC name**.
2. Click **Rename this PC**.
3. Name your domain controller (e.g., **Hydra-PC**).
4. Restart the virtual machine after renaming.

### Step 9: Reboot and Continue
- Allow the machine to restart.
- Once logged back in, continue with additional domain controller configurations as needed.

---

## Making the Machine a Domain Controller

### Step 1: Open Server Manager
- Open Server Manager, then select **Manage > Add Roles and Features**.

### Step 2: Roles and Features Wizard
1. Click **Next** on the introduction screen.
2. Choose **Role-based or feature-based installation** and click **Next**.
3. Select the server (e.g., "Hydra DC") and click **Next**.

### Step 3: Select AD DS
1. Select **Active Directory Domain Services** and add any required features when prompted.
2. Click **Next** until you reach the **Install** button, then start the installation.
3. Wait for the installation to complete.

### Step 4: Promote to Domain Controller
1. After installation, click **Promote this server to a domain controller**.
2. Choose **Add a new forest** and enter a root domain name (e.g., `Marvel.local`).
3. Click **Next** and set the Forest and Domain functional levels (e.g., 2016).
4. Set the **Directory Services Restore Mode (DSRM) password**.

### Step 5: Configure NetBIOS and Paths
1. Accept the automatically generated NetBIOS domain name.
2. Proceed with default paths for **NTDS, SYSVOL**, etc.
3. Click **Install** and let the server reboot after installation.

### Step 6: Log into the Domain
- After reboot, log in using the new domain (e.g., `Marvel\administrator`) and the administrator password.

---

## Setting Up Active Directory Certificate Services (AD CS)

### Step 1: Add Roles and Features for AD CS
1. In Server Manager, select **Manage > Add Roles and Features**.
2. Choose **Role-based or feature-based installation** and proceed by clicking **Next**.
3. Select **Active Directory Certificate Services** and add required features.

### Step 2: Install Certificate Authority
1. Continue through the wizard and select **Certification Authority**.
2. Enable **Restart if required**, then click **Install**.



### Step 3: Configure AD CS
1. After installation, select **Configure Active Directory Certificate Services**.
2. Choose **Certification Authority** and set it up as an **Enterprise CA** and **Root CA**.
3. Create a **New Private Key** and use default cryptographic settings (e.g., SHA-256).
4. Set the **Validity Period** to 99 years for long-term lab setup.
5. Click **Next**, review settings, then **Configure**.

### Step 4: Reboot
- After configuration, restart the server to finalize setup.

## Setting Up User Virtual Machines for Lab

## Step 1: Shut Down the Domain Controller
- Shut down the domain controller to free up resources, especially if working with limited RAM or storage.

## Step 2: Create New Virtual Machines
1. Open **VMware Workstation** and select **Create a New Virtual Machine**.
2. Select the **ISO file for Windows 10** (instead of the Windows Server ISO used for the domain controller).
3. Click **Next** to proceed through setup steps.
4. When prompted, skip entering the **Windows product key**.
5. Select **Windows 10 Enterprise** as the version.

## Step 3: Name the Machines
- Assign unique names to each VM. Examples:
  - **Punisher** (e.g., for one user)
  - **Spider-Man** (for another user)

## Step 4: Configure Virtual Machine Hardware
1. Allocate **60 GB** of disk space and select **Split virtual disk**.
2. Customize hardware settings:
   - Remove the **floppy disk drive**.
   - Set **memory allocation** based on system resources:
     - Use **8 GB** if available, or adjust to **4 GB** or **2 GB** if limited.
   - Use **NAT** for the network adapter, similar to previous lab configurations.

## Step 5: Power On and Start Installation
1. Power on each VM, and when prompted, press a key to start the boot sequence.
2. Go through the Windows setup:
   - Set language to **English** (or your region’s language).
   - Choose **Custom Install**.
   - Partition the drive by clicking **New** and applying settings, then proceed with **Next** to start the installation.

## Step 6: Complete Windows Installation Steps
1. After installation, reboot each machine as prompted.
2. Select region (e.g., **U.S.**) and keyboard layout.
3. Choose to **skip the second keyboard layout**.

## Step 7: Configure User Accounts
1. When prompted to sign in with Microsoft, select **Domain Join Instead**.
   - For Punisher:
     - **Username**: Frank Castle
     - **Password**: Password1
   - For Spider-Man:
     - **Username**: Peter Parker
     - **Password**: Password1
2. Set security questions with generic answers (e.g., answer each with "Bob").

## Step 8: Disable Optional Settings
- Skip optional settings like **advertising**, **location services**, and **Cortana setup**.

## Step 9: Install VMware Tools
1. In each VM, install **VMware Tools** to enable full-screen mode and improved performance.
2. Perform a **Complete Install** and restart if prompted.
3. Adjust display settings if needed (e.g., **150%** for better visibility).

## Step 10: Rename Each VM for Identification
1. Rename **Frank Castle’s** machine as **Punisher**.
2. Rename **Peter Parker’s** machine as **Spider-Man**.

## Step 11: Final Reboot
- Restart each machine after renaming to complete the setup process for both VMs.

Once these steps are complete, both user machines should be ready. The next step is to join them to the domain when you power on the domain controller again.

## Setting Up Users, Groups, Policies, and Configurations on a Windows Server Domain Controller

## Step 1: Boot up the Domain Controller
1. Power down any non-essential virtual machines (e.g., workstations named Punisher and Spider-Man).
2. Start the Domain Controller (Windows Server 2022, named as Windows Server 2016 in this example) and log in.

## Step 2: Access Active Directory Users and Computers
1. Open **Server Manager** on the domain controller.
2. Navigate to **Tools > Active Directory Users and Computers**.
3. Observe the existing **Organizational Units (OUs)**, users, and groups.

## Step 3: Create Organizational Units (OUs) for Users and Groups
1. Right-click on the root of your domain (e.g., Marvel.local), select **New > Organizational Unit**, and name it **Groups**.
2. Move default system groups (e.g., Domain Admins, Enterprise Admins) into the **Groups OU** for organizational clarity.

## Step 4: Create New User Accounts
1. **Tony Stark (Domain Admin)**:
   - Right-click the existing **Administrator** account, select **Copy**, and create a new user with the following:
     - Full Name: **Tony Stark**
     - Username: **TStark**
     - Password: **Password12345!**
     - **Password Never Expires**: Enabled
2. **SQL Service Account (for demonstration)**:
   - Copy the **Administrator** account and create a new service account with the following:
     - Full Name: **SQL Service**
     - Username: **SQLService**
     - Password: **MyPassword123#**
     - Add a description for demonstration purposes: "Password is MyPassword123#".
3. **Standard Users (Frank Castle and Peter Parker)**:
   - Create individual user accounts as follows:
     - **Frank Castle**:
       - Username: **FCastle**
       - Password: **Password1**
       - **Password Never Expires**: Enabled
     - **Peter Parker**:
       - Username: **PParker**
       - Password: **Password2**
       - **Password Never Expires**: Enabled

## Step 5: Configure an SMB File Share
1. In **Server Manager**, go to **File and Storage Services > Shares**.
2. Click **Tasks > New Share**, and select **SMB Share - Quick**.
3. Choose a share location on the **C:** drive, name the share **HackMe**, and complete the configuration.
4. The network path should look like `\\Hydra-DC\HackMe`.

## Step 6: Set up a Service Principal Name (SPN) for the SQL Service Account
1. Open **Command Prompt** as Administrator.
2. Use the following command to set up an SPN for the SQL service account:
   ```shell
   setspn -a Hydra-DC/SQLService.Marvel.local:60111 Marvel\SQLService
3. Verify the SPN by querying with:
   ```shell
   setspn -T Marvel.local -Q */*

## Step 7: Create a Group Policy to Disable Microsoft Defender
1. In Server Manager, open Group Policy Management.
2. Expand **Forest: Marvel.local > Domains > Marvel.local.**
3. Right-click Marvel.local and select **Create a GPO** in this domain. Name it Disable Windows Defender.
4. Right-click the new GPO and select **Edit**. Navigate to:
    ```shell
    Computer Configuration > Policies > Administrative Templates > Windows Components > Microsoft Defender Antivirus
5. Double-click **Turn off Microsoft Defender Antivirus**, set it to **Enabled**, then click **Apply** and **OK**.
6. Enforce the policy by right-clicking the GPO and selecting Enforce.

## Step 8: Set a Static IP Address
1. Go to **Network & Internet Settings > Change adapter options**.
2. Open **Properties** for the network adapter, and configure IPv4 settings:
   - **IP Address**: 192.168.138.136 (IP Address of pfSense network interface)
   - **Subnet Mask**: 255.255.255.0
   - **Default Gateway**: 192.168.138.2 (IP Address of pfSense Gateway)
3. Apply the settings.

## Final Notes
- Confirm all configurations are as expected.
- Ensure the domain controller is correctly configured for user authentication, file sharing, and group policies before running further security tests.

## Joining Machines to the Domain (Marvel.local)

This guide outlines the steps to join client machines to the Marvel.local domain, configure network settings, set up user roles, and verify shared drive access.

## Step 1: Adjust RAM Allocation (If Necessary)

- **Windows Server**: 2 GB (unless more RAM is available).
- **Punisher Machine**: 4 GB.
- **Spider-Man Machine**: 2 GB (optional, you can allocate 4 GB for better performance).

## Step 2: Power On All Machines

- Start the domain controller (DC) and both client machines (Punisher and Spider-Man).
- Log in with the default local admin password (`Password1` with a capital "P" as per your setup).

## Step 3: Configure Network Settings on Each Machine

1. Open **Network and Sharing Center**:
   - Go to **Change Adapter Settings**.
   - Right-click on **Ethernet0** and choose **Properties**.
   - Select **Internet Protocol Version 4 (TCP/IPv4)**, then **Properties**.

2. **Set Static IP and DNS**:
   - Use the domain controller’s IP as the DNS server (e.g., `192.168.138.136`).
   - Save the settings.

## Step 4: Join Each Machine to the Domain (Marvel.local)

1. On each machine:
   - Go to **Settings > Accounts > Access work or school**.
   - Select **Connect** and choose **Join this device to a local Active Directory domain**.

2. **Enter the Domain Information**:
   - **Domain Name**: `Marvel.local`
   - **Username**: `administrator`
   - **Password**: (use the administrator password for the DC).

3. **Restart Each Machine** once they’re successfully joined.

## Step 5: Verify Domain Join on Domain Controller

- On the DC, open **Active Directory Users and Computers**:
   - Navigate to **Computers** in the **Marvel.local** domain.
   - Ensure **Punisher** and **Spider-Man** appear in the list.

## Step 6: Configure Local Users and Groups on Each Client Machine

1. **Enable and Set Password for the Local Administrator Account**:
   - Go to **Computer Management > Local Users and Groups > Users**.
   - Double-click on **Administrator**, set the password (`Password1!`), and enable the account.

2. **Add Domain Users as Local Administrators**:
   - Go to **Computer Management > Local Users and Groups > Groups > Administrators**.
   - Add `Fcastle` (Frank Castle) as a local administrator on **Punisher**.
   - Add both `Fcastle` and `Pparker` (Peter Parker) as local administrators on **Spider-Man**.

## Step 7: Enable Network Discovery

- On each client, go to **Network & Sharing Center > Change advanced sharing settings**:
   - Turn on **Network discovery** and **File and printer sharing**.

## Step 8: Map the Shared Drive (HackMe) on Spider-Man

1. Open **File Explorer**:
   - Go to **This PC > Map Network Drive**.

2. **Set Drive Mapping**:
   - Choose a drive letter (e.g., `Z:`).
   - Enter the path `\\Hydra-DC\HackMe`.
   - Select **Connect using different credentials**.
   - Use the **Administrator** account and password for authentication.

## Step 9: Verify Access to Shared Drive

- Ensure the **HackMe** shared drive is accessible on **Spider-Man**.

---

By following these steps, your machines should now be correctly joined to the **Marvel.local** domain with all necessary configurations for domain access, shared drive mapping, and user roles.


---

# 10. Make your AD Lab vulnerable

## Using a Vulnerable AD Script

We will use this script to create a vulnerable active directory: [Vulnerable AD Plus Script](**https://github.com/WaterExecution/vulnerable-AD-plus?)**

Following along with the installation guidance, you should do the following:

- Log into your Domain Controller VM
- Run the script on the Domain Controller

## Open Powershell as Administrator

Right-click the Start Menu and Choose **Windows PowerShell (Admin)**.

![image](https://github.com/user-attachments/assets/f4b0a229-ad3a-448a-a788-dcf203db5fc1)

### Run the script in Memory 

Run the following command: 

1. **Set the Execution Policy to allow unsigned scripts**

`Set-ExecutionPolicy -ExecutionPolicy Bypass -Force`

2. **Download and Run the Script in Memory:**

We will download the script as a string using a .NET class. The script includes a placeholder domain name `change.me`, so it must be modified to match your domain name.

Use the `-replace` operator in PowerShell to change `change.me` to your domain (e.g., `ad.lab`). The script will then run in memory using `Invoke-Expression`.

```powershell
[System.Net.WebClient]::new().DownloadString('https://raw.githubusercontent.com/WaterExecution/vulnerable-AD-plus/master/vulnadplus.ps1') -replace 'change\.me', 'ad.lab' | Invoke-Expression
```
Note: Replace `ad.lab` with the actual name of your domain.

3. **Monitor the Output:**

As the script executes, you should see output with green status messages indicating successful operations. At the end of the script, the server will reboot automatically after 30 seconds.

![image](https://github.com/user-attachments/assets/1958d78e-329e-401c-8c33-4783b14c2f5c)


# 11. Building a Pivoting Lab To Practice External Pentest

### Network Diagram

![image](https://github.com/user-attachments/assets/2890a7eb-2f5a-470d-9962-91c1ae89af25)

### Setting up the Firewall

The point is to make the lab as realistic as possible. To do so, we will add a rule to the LAN subnet that blocks all packets to the AD_LAB subnets.

### Block Packets to AD Subnet

1. Go to **Firewall > Rules** on pfSense.

    ![image](https://github.com/user-attachments/assets/271ad827-b60f-4539-82f2-1d45ff5ca8cc)

2. Choose **LAN**.

    ![image](https://github.com/user-attachments/assets/1fb49432-f36e-48db-a96e-c7d187fa9cdb)

3. Click **Add**.

    ![image](https://github.com/user-attachments/assets/bfd20b19-b5a9-475e-873a-06b788b5a1e2)
    
    ![image](https://github.com/user-attachments/assets/db76748b-500c-4252-a03e-8c9b9405c0be)

    ![image](https://github.com/user-attachments/assets/f9fd88b8-41e3-46bd-9cae-c78399647ed1)

4. Save and Apply Changes.

### Toggling the New Rule

In pfSense, you can toggle a rule on and off without deleting it by pressing the little ✅ or ❌ to the left side of the rule.

![image](https://github.com/user-attachments/assets/ea350f85-01ca-45ed-bbf3-7d49bf810c5a)

Once you've toggled the rule on or off, click **Apply Changes** for it to take effect. You can turn it off if you do not want it. But for the sake of this lab, we need it enabled.

### Setting up the Vulnerable Target

To keep things simple, we'll use an existing target that should already be in our lab. We are going to use Metasploitable 2 but you can use whatever machine you want.

### Tweaking Metasploitable 2

1. Right-click **Metasploitable 2 > Snapshots**.

    ![image](https://github.com/user-attachments/assets/2439f8bc-9637-47d4-af11-65ecdf8494c4)

    ![image](https://github.com/user-attachments/assets/b20c688d-11d3-4b5e-b170-3125d386c7fe)

    ![image](https://github.com/user-attachments/assets/16f89731-de26-4cd4-be85-09959238a98d)

2. Right-click **Metasploitable 2 > Settings**.

    ![image](https://github.com/user-attachments/assets/6be6cc5b-68b2-4a15-9226-18fe1c043415)

    ![image](https://github.com/user-attachments/assets/1cc0a036-a77c-42a1-b01e-7eb0de48766d)

3. Configure network adapters:

   - **Adapter 1**: ISOLATED

        ![image](https://github.com/user-attachments/assets/f8c6b4f9-921e-4c4a-abfb-4bff0448dbbd)

   - **Adapter 2**: AD LAB

        ![image](https://github.com/user-attachments/assets/8146f32d-0e74-4638-8914-799ceeb9b8fd)

### Start Up and Configure the Interfaces

1. Log into the Metasploitable 2 VM with **msfadmin:msfadmin** credentials.

    ![image](https://github.com/user-attachments/assets/98f7738b-ea50-412f-8468-e93192ac54d2)

2. Edit the network interfaces configuration file.

    ```bash
    sudo nano /etc/network/interfaces
    ```

    **Before:**

    ![image](https://github.com/user-attachments/assets/e2fc5ab0-b1c4-41a6-be76-b9b649bc7301)

    **The post-up IP route commands shown below are used to prefer the 10.25.25.1 gateway as the default route so that the Metasploitable 2 host can retain internet access.**

    **After:**

    ![image](https://github.com/user-attachments/assets/04470746-0cb9-46a9-a509-3acf38cdbb48)

3. Press `CTRL + X`, then `Y` to save the changes to the file. Press **Enter** to confirm.

4. Refresh the networking stack to get a new DHCP address on the AD_LAB subnet.

Command: **sudo /etc/init.d/networking restart**

![image](https://github.com/user-attachments/assets/8f55beb3-450a-4686-9c0e-837ff839cb5f)

**Now we are done with the lab! Happy Hacking!**
