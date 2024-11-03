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

## 1. Planning Phase

 We will build a network diagram to represent our lab visually.
   
[Network Diagram](https://github.com/A9u3ybaCyb3r/Virtual-Network-Penetration-Testing-Lab/blob/main/Building%20The%20Lab/Empire%20Net%20Diagram.drawio.pdf)

---
 
## 2. Downloading VirtualBox and Installing VirtualBox

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

## 3. Building a pfSense VM

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

## 4. Installing pfSense

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

9. **Wait for Installation**  
   - Wait for the installation to complete. Once done, choose **Reboot** to restart the system.

     ![Reboot](https://github.com/user-attachments/assets/2296c60c-d355-4902-9789-5f394ef42f15)

---

## 5. Configuring pfSense

When the VM finishes booting We are going to be asked this question: Should VLANs be set up now [y|n]? we will choose n.

![image](https://github.com/user-attachments/assets/f9a0cf84-ee71-4439-a54a-731c478bcf64)

Then we will enter our interfaces. The first one is for WAN.

![image](https://github.com/user-attachments/assets/4f3fe5fa-f812-4c77-a728-cb1f7fdd7b1d)

LAN Interface.

![image](https://github.com/user-attachments/assets/ade25300-b7de-45d2-952d-2bf19da796fe)

ISOLATED Interface.

![image](https://github.com/user-attachments/assets/dc1363e8-5b9f-43e6-9833-e7629f46e538)

Lastly our AD_LAB Interface.

![image](https://github.com/user-attachments/assets/ea899840-4ee0-4bd5-9b48-8f6f6883aa5d)

We should finish with this configuration after we confirm that this is what we want to choose 'y'

![image](https://github.com/user-attachments/assets/4e4f7eef-f07d-41f7-a125-1836168c733f)

### Setting up the Interfaces

- The WAN interface will pull an IP address from your home network. It will be different from mine.
- The LAN IP address is going to be in the default option which is going to be 192.168.1.1/24. We will change this later
- OPT1 is going to be our ISOLATED interface and is not yet configured. We will configure it later.
- OPT2 is going to be our AD_LAB interface and is not yet configured. We will configure it later.

![image](https://github.com/user-attachments/assets/32211990-aa57-4a3d-b86a-7dacca3b3e1d)

### Configure the LAN

Enter option 2.

![image](https://github.com/user-attachments/assets/ded46fbe-ea36-48c8-89a1-ab5752bf9405)

We are going to change the LAN so enter option 2.

![image](https://github.com/user-attachments/assets/2fd90833-1370-4f2f-a932-cf4a8a090c68)

We are going to configure the address statically we will enter 'n'

![image](https://github.com/user-attachments/assets/a33a78e9-4594-4597-b44a-4f61a55f324b)

Enter the IP address.

![image](https://github.com/user-attachments/assets/d44ef8c7-3c84-4c2d-9a5e-95db20d74310)

Enter the subnet mask bits.

![image](https://github.com/user-attachments/assets/b7dd1628-263f-4e7a-be09-dd3d69c55583)

Hit Enter this is for LAN.

![image](https://github.com/user-attachments/assets/3e8990ab-4066-4866-9196-0e9b157026e0)

Press 'n' to configure the address statically.

![image](https://github.com/user-attachments/assets/23ea1fb7-2727-459c-9187-f293acfeecfc)

Press Enter we are not going to be using IPv6.

![image](https://github.com/user-attachments/assets/14099163-f473-42e9-a7de-86ab03eb58cc)

Enter 'y' to enable the DHCP server.

![image](https://github.com/user-attachments/assets/36f07dcd-46d5-41d1-9cf3-90c689094758)

Enter the start and end range.

![image](https://github.com/user-attachments/assets/8701352d-1e83-4ce3-bfcd-a18683d29d21)

Enter 'n', we want to keep using TLS on the web portal.

![image](https://github.com/user-attachments/assets/cee8c91a-3fea-497f-bcd4-c8eb6f794aa8)

Press Enter and you are done with the LAN.

![image](https://github.com/user-attachments/assets/18fb87f1-88ba-4002-a764-e623e34fd87d)

### Configure the ISOLATED Interface

Enter 2.

![image](https://github.com/user-attachments/assets/c8265961-0bed-425d-be7b-96efcad11aeb)

Enter option 3 to configure OPT3.

![image](https://github.com/user-attachments/assets/0883dce2-053f-44fe-907b-3d96ae9ea5b5)

Enter 'n' to configure the address statically.

![image](https://github.com/user-attachments/assets/399d4ace-edf9-4359-a375-771a37bb71f3)

Enter the network address.

![image](https://github.com/user-attachments/assets/d0f7ce08-b81e-4cd6-b3bf-b92a907264de)

Enter the subnet mask bit.

![image](https://github.com/user-attachments/assets/5aa86244-f89a-4962-bfa1-466c09a68f29)

Press Enter this is for the LAN.

![image](https://github.com/user-attachments/assets/c47dfcc5-e16b-47dc-9ae0-0d0f48a4bf63)

Press 'n' to configure statically.

![image](https://github.com/user-attachments/assets/618cd159-3979-408c-bcfd-f9ea80c61d6a)

Press Enter we will not be using IPv6.

![image](https://github.com/user-attachments/assets/232aafbb-ca03-43cb-9046-d4549ac6b424)

Enable the DHCP server y' and then enter the start and end range.

![image](https://github.com/user-attachments/assets/1c13e01c-9756-429b-8c42-448ae30ba4f3)

Enter 'n', we want to keep using TLS on the web portal.

![image](https://github.com/user-attachments/assets/c77ad20b-be1d-4135-8876-670b92f10a8a)

Now we are done with the ISOLATED Interface.

![image](https://github.com/user-attachments/assets/93e0a0bd-f519-4ff1-9d6b-b945b2502173)

### Configure the AD_LAB

Enter option 2.

![image](https://github.com/user-attachments/assets/17caea15-b67f-49ba-8e12-6926a5124612)

Enter 4 to configure the OPT4.

![image](https://github.com/user-attachments/assets/7119fee6-3375-4462-abd8-7d88f3423421)

Enter the 'n' to configure the address statically.

![image](https://github.com/user-attachments/assets/8b091b1f-4971-4ab4-8a8f-9690e7b12455)

Enter the network address.

![image](https://github.com/user-attachments/assets/dc69c922-e5b7-45ca-a1f1-6f9a19df0f40)

Enter the subnet mask bits.

![image](https://github.com/user-attachments/assets/06bd2dd6-0561-4389-9010-b2a70e671473)

Press Enter, this is for the LAN.

![image](https://github.com/user-attachments/assets/ff489e11-bc9f-4929-bc91-9169e9ca5731)

Enter 'n' to configure the address statically.

![image](https://github.com/user-attachments/assets/b4fe77f0-fbd9-47e2-af03-133744f353e7)

Press Enter, we are not going to use IPv6.

![image](https://github.com/user-attachments/assets/1597c9a7-a41f-4369-975e-30bfbfb0745f)

Enter 'n' to disable the DHCP server, as the domain controller will be acting as the DHCP server.

![image](https://github.com/user-attachments/assets/b691fdee-718b-4230-a0ba-c4915b2e1063)

Enter 'n', we want to keep using TLS on the web portal.

![image](https://github.com/user-attachments/assets/ee252a48-5a29-4092-828f-81587093f117)

Now we are done with the AD_LAB Interface.

![image](https://github.com/user-attachments/assets/7d8c3f96-2db1-462f-a122-0c7ee1d66107)

### Final Check

This is how it should look like after we are done. Remember mine might be different than yours if you chose to use another IP address.

![image](https://github.com/user-attachments/assets/2a0f79b8-93a5-49ee-823b-f4970d67dd11)

### !!!Important!!!

We will not be making the pfSense web console accessible from the WAN to avoid exposing it to public networks, especially if using a laptop on public wireless. Instead, the firewall rules will be configured using a Kali VM later in the process.

---

## 6. Importing Kali 

 Go to https://kali.org/get-kali/

   - Click on the image that says Virtual Machines and download the 64-bit version of Virtualbox.

      ![image](https://github.com/user-attachments/assets/ae2d558e-57a4-4d1a-8576-5ad25de659ec)
     
     ![image](https://github.com/user-attachments/assets/6430026d-9ca1-46db-9dd6-98e6d758617c)

 After downloading the file, extract it and hit the Add button on Virtualbox. 

![image](https://github.com/user-attachments/assets/37ef160d-c250-4151-80df-bdfb038f063c)

Then choose the .vbox extension file.

![image-38](https://github.com/user-attachments/assets/5cf67d2e-ebd6-4c6e-ab83-f49f87a27b82)

 Right-click the machine and choose the Network settings.

![cd25168f5bf7404cb6e4d5a8b84ca441](https://github.com/user-attachments/assets/465b1135-d2b9-4e79-aa75-f6eb9f315ed1)

Change the network settings to the pfSense LAN network that you created.

![image](https://github.com/user-attachments/assets/82294fe3-d42c-44cb-8982-732ef4d9e3aa)

Then increase your RAM depending on how much you need. Mine is 8GB RAM because of the tools that I use. You can do it on the machine settings. 

![image](https://github.com/user-attachments/assets/9cf482b6-64c7-48be-8248-fe25ad5868eb)

 Click OK and now you can start the machine. Use the default credentials of *kali:kali*.

![image](https://github.com/user-attachments/assets/919a0fe4-12fe-4847-acad-0180f51a77b8)

 Open the terminal to see if we are on the LAN network. Our IP Address should be 10.19.19.X/24. Later, we can set up the IP Address that we want.

![image](https://github.com/user-attachments/assets/3507057e-d6df-423e-9fbe-bde723849657)

---

## 7. Configuring the pfSense firewall

 Log into the web portal (firefox for me) in your Kali machine to: **https://10.19.19.1**.

![image](https://github.com/user-attachments/assets/db0ecfcb-6a40-4817-8187-8cabda8db0bd)

 If you encounter this, click Advanced.

![image](https://github.com/user-attachments/assets/329900dc-3fec-47e3-8335-42b84cd7069a)

Then accept the risk.

![image](https://github.com/user-attachments/assets/2fbd799e-db1d-447b-8616-538c8b91f774)

The default credentials are:

- Username: admin
- Password: pfsense

Click Next after logging in.

![image](https://github.com/user-attachments/assets/4157974c-affb-43d9-aa12-f745ad488560)

Fill out the Hostname and Domain. Uncheck Override DNS. You can use whatever name you want. Click Next.

![image](https://github.com/user-attachments/assets/c3e8a9f6-c266-4412-a404-03931166ec10)

Double-check your timezone and click Next.

![image](https://github.com/user-attachments/assets/6a3875bf-c8be-4140-863b-3296c20aa10a)

Scroll down and uncheck this option. We’re double-NAT, meaning the WAN network is also private and we want to allow this. Click Next.

![image](https://github.com/user-attachments/assets/1fa7b998-b55c-4207-a454-831a331e4356)

Click Next.

![image](https://github.com/user-attachments/assets/d01ad2a6-3c77-446e-80a0-34b74245ba2c)

Change the admin password and remember it. 

![image](https://github.com/user-attachments/assets/73b60b4c-6325-479f-b7be-fe1ef1b8e934)

Click Next and Finish.

## Configure the Interfaces

### Isolated Interface

Go to Interfaces and choose OPT1.

![image](https://github.com/user-attachments/assets/1d51f12c-c551-4c49-9543-464d5f1f9302)

Set the Description to ISOLATED. Then scroll down to click Save and Apply Changes.

![image](https://github.com/user-attachments/assets/90a7eff1-1423-4d85-921b-a4c649c6f7aa)

![image](https://github.com/user-attachments/assets/5e86a71c-cb18-452a-b6f8-687eebaf96c8)


### AD_LAB Interface

Go to Interface and choose OPT2.

![image](https://github.com/user-attachments/assets/f6b7f5cc-1410-4316-a3ba-df06c50e7cb6)

Change the Description to AD_LAB. Then scroll down to click Save and Apply Changes.

![image](https://github.com/user-attachments/assets/4a1b57ba-2a69-43d3-a743-fde6276d0868)

![image](https://github.com/user-attachments/assets/44d8157c-8736-484a-8def-c67444700015)

### Optimize the DNS Resolver Service

Go to Services > DNS Resolver.

![image](https://github.com/user-attachments/assets/b0dd2a59-96fb-4496-8c93-423fd49f4bfe)

Check both of these options, then click save and apply changes just like before.

![image](https://github.com/user-attachments/assets/7b7612c2-1fde-463d-aa03-ebf2125d3aab)

If you are still in the DNS Resolver, go to Advance Settings and check both of these options. Do not forget to Save and Apply Changes.

![image](https://github.com/user-attachments/assets/e7f537a4-9c21-4fe7-889b-68b01c09afa2)

### Give Kali a Static DHCP Lease

Go to Status > DHCP Leases.

![image](https://github.com/user-attachments/assets/1129d9f4-f090-470c-8a27-3202972cff1e)

Click on this button to add a static mapping (the hostname is different because my Kali machine is named Vulnhunter).

![image](https://github.com/user-attachments/assets/8e402467-88ac-4272-8336-7f0f00ad6c80)

Now we set up the IP address of our Kali machine. Click Save and Apply changes.

![image](https://github.com/user-attachments/assets/a85398a6-99fe-4090-9bb2-7f5540b39e88)

### Configure the Firewall Rules

Create an Alias for RFC1918. This will be used to reference all private IPv4 spaces. Go to Firewall > Alianses.

![image](https://github.com/user-attachments/assets/d1132f04-0a9e-48d1-b6c2-102723e3c00b)

Click Add and fill this and then click Save.

![image](https://github.com/user-attachments/assets/b4e2dcdc-e912-4bf3-be1d-097eddbdee25)

### Create an Alias for Kali

Click Add, Save, and Apply Changes.

![image](https://github.com/user-attachments/assets/b9e15e1a-9c14-42e1-8096-26c560fe7891)

### LAN

Click on Firewall > Rules.

![image](https://github.com/user-attachments/assets/00e87e94-4a92-49cb-84ea-bdbb97dbbe80)

Click on LAN and then add a rule.

![image](https://github.com/user-attachments/assets/eb5af460-2933-4136-9018-fda3bd73f433)

 Copy these rules.

 ![image](https://github.com/user-attachments/assets/5c1b56a4-808a-45e8-9669-cf0f18cc6b54)

This is how it should look like when you are done.

![image](https://github.com/user-attachments/assets/388db847-7bf8-4421-8563-0153d522d6aa)


### ISOLATED

Click on ISOLATED and then we add a rule.

![image](https://github.com/user-attachments/assets/c5e09e3a-6633-4157-8d2f-fffcee1e5938)

![image](https://github.com/user-attachments/assets/fd4acef1-4374-4758-ac44-cbe094730803)

![image](https://github.com/user-attachments/assets/f30108a8-dd32-43fb-893f-51d6fb4d3707)

Then we add another rule.

![image](https://github.com/user-attachments/assets/9df9fcf5-e0a0-4d03-8aaa-ae7f844d5856)

![image](https://github.com/user-attachments/assets/56e4d325-79c9-401a-93dc-8d9c5ef1b505)

Lastly, we add an Isolated rule.

![image](https://github.com/user-attachments/assets/8c67283a-c782-4803-aad0-d1f509d66e08)

![image](https://github.com/user-attachments/assets/a5fa3d8b-e313-4b79-84dc-98f83b19f941)

This is how it should look like when you are done.

![image](https://github.com/user-attachments/assets/dc5850a1-70a8-4548-b69e-bc1dc935007e)

### AD_LAB

Click on the AD_LAB and then we add a rule.

![image](https://github.com/user-attachments/assets/354dc273-5e98-41d7-bd3d-1b39e246359d)

![image](https://github.com/user-attachments/assets/a92c06e5-bc3d-4368-a396-8159cd84619a)

![image](https://github.com/user-attachments/assets/21947bc9-1f65-4e6d-b362-3fd67ccc3039)

**This rule effectively blocks traffic to any private IP address. Then we'll add another rule above this one to allow traffic to Kali, which is aliased to 10.19.19.2. If there are additional private IPv4 addresses you want your AD_LAB hosts to be able to talk to, you'll need to place the firewall rules above this one, as rules are evaluated from top to bottom.**

Then we will add another rule.

![image](https://github.com/user-attachments/assets/cd42f591-7f97-4725-9baa-48bcc7b4d413)

![image](https://github.com/user-attachments/assets/7c7f7019-a65c-4ed8-bb69-b814c6fd6166)

 Add another rule.

 ![image](https://github.com/user-attachments/assets/5c0cb759-aded-4b16-85ab-5286e6bf6e58)

![image](https://github.com/user-attachments/assets/13aa5108-fdfe-44b4-9577-d0e8caf224fa)

Final AD_LAB rule.

![image](https://github.com/user-attachments/assets/6db4663a-9c11-4cff-9f53-a0739ae4156e)

![image](https://github.com/user-attachments/assets/7b9235e4-b712-42b4-b076-1889f7358bc3)

This is how it should look like when you are done.

![image](https://github.com/user-attachments/assets/35cf63a4-ff61-4fcb-b5a1-bea349450758)

### Floating Rules

Floating rules are a flexible way to create firewall rules that can be applied to multiple interfaces. Unlike rules attached directly to specific interfaces, floating rules can be applied to any interface. This is helpful for rules that need to be consistent across multiple network locations.

Add the port Alias.

Go to Firewall > Aliases.

![image](https://github.com/user-attachments/assets/afd67561-4332-48a6-b4c0-eb89886cb4c3)

Then click on ports and we add a rule.

![image](https://github.com/user-attachments/assets/1aee82ef-8ea6-4bdc-8ae1-7e8f506c447e)

![image](https://github.com/user-attachments/assets/619133f6-b021-44a0-9ac4-8d2b1b7748c1)

Fill it out and then click on Save.

![image](https://github.com/user-attachments/assets/08a31367-b3a1-463d-9873-23ca20873fc9)

### Add the Separators

Go to Firewall > Rules.

![image](https://github.com/user-attachments/assets/c0a61275-99c3-4a50-9ed6-835921920d3a)

Choose Floating.

![image](https://github.com/user-attachments/assets/5ef5ef01-0caa-4954-a8f9-4917bf8ac593)

Click this button to add a separator.

![image](https://github.com/user-attachments/assets/e0a96622-c717-4600-bfed-ccc811c7bbd9)

Write this and do it again.

![image](https://github.com/user-attachments/assets/1bc1957f-3550-4f6a-a8c4-2c7b6d8778c5)

You should have two separators when you are done, we will use them to sandwich the other rules that we create.

![image](https://github.com/user-attachments/assets/aa9127bd-e1c4-47ff-b04b-fd5d4f644dc9)

Don't forget to save what you created.

### Block Logins to the Firewall

Add a rule.

![image](https://github.com/user-attachments/assets/b34e2ea1-ab27-4dcd-a6ec-0aba4839348e)

![image](https://github.com/user-attachments/assets/ddde4107-32c5-4d1f-8691-c952f0eed999)

The subnets ISOLATED and AD_LAB are isolated from the firewall's login ports to enhance security. The "in" direction is chosen because traffic is flowing from external hosts into the firewall interface.

![image](https://github.com/user-attachments/assets/5240f215-a47b-4479-8a25-295e3a340417)

Click Save and Apply changes.

![image](https://github.com/user-attachments/assets/2936151e-28c2-4105-b561-dc94fc86df5d)

### FLOATING Rules Desired End State

Drag and drop items to re-order, then click Save and Apply Changes.

![image](https://github.com/user-attachments/assets/efdb2193-6a39-4d8e-81be-d76b396d1223)

**To prevent hosts from accessing the firewall login ports, additional interfaces will be created as you progress through the VirtualBox lab. Subnets that are allowed to access the internet but not private IP addresses need to reach the gateway address. To achieve this without allowing access to the firewall login ports, specific rules are created.**

### Make Some System Tweaks to pfSense

Go to System > Advanced.

![image](https://github.com/user-attachments/assets/a2199be8-544f-4688-9109-3fd44c28d47f)

Then Networking.

![image](https://github.com/user-attachments/assets/a3ae6783-b1d0-4961-9e87-db9835445ecf)

Scroll down until you find this option and check it.

![image](https://github.com/user-attachments/assets/313f82d4-2e26-4f65-ad4f-f641c3c142bc)

Click Save and Apply Changes. Click Reboot and reboot now.

Lastly, you will grab Kali's new DHCP reservation(IP we set up earlier). Open a terminal on your and type this command **"sudo ip link set eth0 down && ip link set eth0 up"**.

---

## 8. Importing Vulnhub VMs to the lab

We are going to Import Machines from Vulnhub. We are going to download Metasploitable 2 these are the links:

VM Info on Vulnhub: https://vulnhub.com/entry/metasploitable-2,29/

Vulnhub Download Link: https://download.vulnhub.com/metasploitable/metasploitable-linux-2.0.0.zip

You will get a zip file so we need to extract it.

![image](https://github.com/user-attachments/assets/852efc57-8754-4618-ada7-5e8d4533cf57)

The .vmdk file is what we want.

![image](https://github.com/user-attachments/assets/6b2f3222-b258-4853-9fbd-acf787fd9469)

On Virtualbox Click New so we can build a new machine.

![image](https://github.com/user-attachments/assets/94cf1927-a8a1-4975-bf93-9c85ba4ef9b5)

![image](https://github.com/user-attachments/assets/23473cf4-7b97-401e-b5e4-78b4c37a23c5)

![image](https://github.com/user-attachments/assets/3a6874c8-8a31-4972-aa27-2a7d97e008b7)

Then we go here so we can add a disk.

![image](https://github.com/user-attachments/assets/d53613eb-96ac-47c7-b7d7-1225d52424a6)

Click this icon.

![image](https://github.com/user-attachments/assets/ce21926b-c715-476c-899a-a5e430dda9aa)

Then you go where you downloaded and unzipped Metasploitable 2 and get this file.

![image](https://github.com/user-attachments/assets/c26467eb-5e9b-4423-8447-8cffc81f6623)

It should look like this.

![image](https://github.com/user-attachments/assets/8a730189-dbda-4797-8299-3d4cddf79c91)

Then we click Finish.

![image](https://github.com/user-attachments/assets/b083e8e6-1b8e-4e3f-a18e-d087a9eadd4a)

We don't start the VM, we right-click the Metasploitable2 VM, choose Settings, and go to network settings.

![image](https://github.com/user-attachments/assets/ce42f843-1bf5-4bd0-9603-6f11ff9c7a59)

![image](https://github.com/user-attachments/assets/61ba46aa-5273-462a-a242-9aaa1d5c6e2a)

Now you can start the VM.

Login to the machine with the credentials msfadmin:msfadmin 

![image](https://github.com/user-attachments/assets/1856ad49-3f18-46ed-aea6-a9714d7528d6)

You can check the IP of the machine, by command: **ip a**.

![image](https://github.com/user-attachments/assets/956432cf-afbd-4853-a3c1-84abcc870bea)

Next, we ping our Kali machine from Metasploitable 2, we will do it with the IP address first.

![image](https://github.com/user-attachments/assets/9468c8a9-9bd3-46c4-a2da-fc04dc64cee8)

Then we will use the local DNS suffix.

![image](https://github.com/user-attachments/assets/69a58057-7d8e-4dbf-85eb-5673d19234bf)

Lastly, we will ping Google and it should fail because we blocked everything outside.

![image](https://github.com/user-attachments/assets/3e2e770e-7db8-488b-bbb7-b4dac1e7d480)

Now we should ping the Metasploitable VM from Kali.

![image](https://github.com/user-attachments/assets/4e73696b-f0d9-40fb-92ab-27ce6058ded5)

---

## 9. Building an Active Directory

For an Internal Penetration test, you only need to change the network adapter settings of the Kali machine and put it into the AD_LAB network. 

### Windows Iso files 

We will get the iso files from this link [Mircrosoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter) and get these two machines:

Windows Server 2019

 - Download the ISO
 - Fill out the information
 - Then select your language and download

Windows 10 Enterprise

- Download the ISO-Enterprise
- Fill out the information
- Select your language and click download

### Creating the Windows Server

Click the New VM button, choose the ISO image, and then click Next.

![image](https://github.com/user-attachments/assets/9236f1e2-8434-4fac-ad75-75abdef2523a)

You can use 2048 MB RAM which is the minimum. 4096 MB RAM is preferred.

![image](https://github.com/user-attachments/assets/bc72a1f8-930d-4735-b485-5b06d5dec688)

![image](https://github.com/user-attachments/assets/9207ef6d-7170-45b8-a9f2-f97def9bc35a)

![image](https://github.com/user-attachments/assets/ea745f88-9a49-43e9-9660-72eaf56c5ffb)

Right-click, choose Settings and go to Network.

![image](https://github.com/user-attachments/assets/2dfca7fd-ac04-4ce6-977d-2f015f04abd2)

![image](https://github.com/user-attachments/assets/f3210e6a-7c63-4d53-b284-27cbe2b1cf94)

### Create a Windows 10 Enterprise Template 

Create a new VM and name it: Win10EnterpriseTemplate. Then choose the ISO file and click Next.

![image](https://github.com/user-attachments/assets/95cd722a-afb5-428e-affe-d68f151856a5)

You can use 2048 MB RAM which is the minimum. 4096 MB RAM is preferred.

![image](https://github.com/user-attachments/assets/73e05703-3c5d-4ef2-a3a5-6be3027d15c2)

![image](https://github.com/user-attachments/assets/478a1849-f01a-44d8-a093-738e021c9507)

Then go to network settings and change the network adapter.

![image](https://github.com/user-attachments/assets/b3c12b35-1707-4cc9-8733-a3ed0db29fda)

![image](https://github.com/user-attachments/assets/0d653eb3-2c29-4908-bc6d-f8a1642c530d)

Save the settings but do not start the VM.

### Install Windows Server 2019

Start the VM, it will start the installation. Choose your language and then click Install Now.

![image](https://github.com/user-attachments/assets/911f2ead-4caf-4ba6-8d80-d754ccb9b25f)

Choose Windows Server 2019 Standard Evaluation (Desktop Experience).

![image](https://github.com/user-attachments/assets/8bd4d678-196f-43e4-a3d7-279d82e32817)

Click Next and accept the terms and conditions. Choose New and then Apply, to create a new drive.

![image](https://github.com/user-attachments/assets/1eb2e5a6-2b07-449a-bc7a-d308e35a5baf)

![image](https://github.com/user-attachments/assets/6d06fc60-5b8f-4c75-a03b-23d57e8a8657)

![image](https://github.com/user-attachments/assets/617f1db9-2305-480f-8790-4092d03f254b)

Then we Click Next and wait for the installation to finish.

![image](https://github.com/user-attachments/assets/c0cc35a8-20f8-43e5-ab74-8a7695df6d90)

Create a local Administrator password (do not forget it). Press CTRL + ALT + DEL and log in with your local Administrator password.

![image](https://github.com/user-attachments/assets/f7c5d4cb-9ab8-4b44-9959-061a8b988700)

**The DHCP service was disabled on pfSense for the AD Lab LAN. This was done to allow the domain controller to serve as the DHCP server. As a result, the domain controller will need to be configured manually.**

Right-click the network interface icon.

![image](https://github.com/user-attachments/assets/e230d92c-111e-4be1-bb10-bbfbbcad97c7)

Choose Open Network & Internet Settings.

![image](https://github.com/user-attachments/assets/ee7a3cbd-6019-4f04-9b6f-ba1dbf32b660)

Scroll down and choose Change adapter options.

![image](https://github.com/user-attachments/assets/11162fbb-b875-45f9-8fcd-8acc5a972b9b)

Right-click the adapter and choose Properties.

![image](https://github.com/user-attachments/assets/03dfa97f-a2a2-43b4-b1df-91d19fdf5ce4)

Double-click Internet Protocol Version 4 (TCP/IPv4).

![image](https://github.com/user-attachments/assets/7bc35dcf-8793-4079-88d0-bd2585525b20)


Configure your adapter as such:

![image](https://github.com/user-attachments/assets/30fa54b8-3246-4106-8047-cc99165c912a)

DNS queries will be initially handled by the domain controller's DNS server. If the domain controller's DNS server cannot resolve a query, it will forward the query to the default gateway, which will then be resolved by pfSense.

### Rename the Server 

Click the Start Menu and click Settings.

![image](https://github.com/user-attachments/assets/0c78f167-eb1d-4394-8b05-97f366105bdf)

![image](https://github.com/user-attachments/assets/70b9ed00-a739-4b5a-83be-de105f59e9ec)

![image](https://github.com/user-attachments/assets/df0e88ab-3af5-428a-ac4f-5f7449625652)

![image](https://github.com/user-attachments/assets/907643dd-9906-4fa3-bdbf-8ed47b98fb0a)

Enter the name of the domain controller. Mine is DeathStar.

![image](https://github.com/user-attachments/assets/883e5a8c-8734-43aa-ac16-deec9f877cc6)

Choose Restart Now. If a reason is required, choose Other (planned).

### Take a Snapshot of the VM

We are going to create a snapshot of the VM before we create a domain. Next to the VM click the menu icon and choose Snapshots. 

![image](https://github.com/user-attachments/assets/f97eac30-6dd0-400d-bbae-6ff295c88fbf)

Click the Take button.

![image](https://github.com/user-attachments/assets/1824a038-9ffb-4ece-a5ae-3182de360c99)

You can fill it out with something like this.

![image](https://github.com/user-attachments/assets/2cbb7a5c-5428-46a8-844b-0e26d31e7ab1)

Click OK. Now, we can restore this snapshot at any time if we want to roll back to a pre-domain install.

### Configure Domain Services

On the Windows Server, Open Server Manager, and click Manage > Add Roles and Features.

![image](https://github.com/user-attachments/assets/3c5d8e8d-e79d-4511-827c-2d68e3f58e30)

Click Next > Next > Next until you reach Server Roles. Check the following boxes:

- Active Directory Domain Services: This will enable the server to act as a domain controller for an Active Directory domain.
- DNS Server: This will enable the server to act as a DNS server, allowing other devices to resolve domain names within the network.

Then Click Add Features

![image](https://github.com/user-attachments/assets/e5f34826-48f5-4d72-87f9-c3816f0018ba)

![image](https://github.com/user-attachments/assets/169182bd-7d30-4487-940a-2ae63c43e46a)

Click Next > Install. Wait for the installation to finish and click Close.

![image](https://github.com/user-attachments/assets/2b817f0c-18de-490b-a6ae-6c69b270d291)

### Configure Active Directory Domain Services

Log back into the domain controller as the local administrator and wait for the Server Manager app to load.

![image](https://github.com/user-attachments/assets/4ff65c32-6db1-4bac-b5cb-8d8411c9acca)

Click Promote this server to a domain controller.

![image](https://github.com/user-attachments/assets/3ec9b97a-e43b-49fb-9f07-bbfaa4a91fa6)

When creating a new Active Directory forest, you need to specify a root domain name. This domain name will be used to identify the forest and its domain controllers. Examples of suitable domain names include .lab, .local, .com, .org, and .net. However, it is recommended to avoid using .local, as it can interfere with multicast traffic.

![image](https://github.com/user-attachments/assets/e589f244-ea9b-4302-8889-3c06899d41a9)

Click Next. The default options are fine. Specify a restore password. You can use the same password as the local admin or something different. It doesn’t matter. Click Next.

![image](https://github.com/user-attachments/assets/5a052621-8569-4a81-976e-5c60adad81be)

Ignore this message.

![image](https://github.com/user-attachments/assets/932f6756-b3a2-423c-aeed-21cb0782d26a)

Click Next and continue with the defaults.

![image](https://github.com/user-attachments/assets/874cc392-1625-440a-8f9e-a2fa209a4cd2)

Click Install and wait for it to complete.

![image](https://github.com/user-attachments/assets/9b9ee9a5-e763-4fc5-93b7-1817789c841a)

The server will automatically reboot.

### Configure Active Directory Certificate Services

To enable LDAPS (Lightweight Directory Access Protocol Secure), Active Directory Certificate Services will be installed. After installation, log back into the domain controller using the local administrator account and wait for the Server Manager application to load.

Open Server Manager and go to Manage > Add Roles and Features.

![image](https://github.com/user-attachments/assets/830e519e-bb03-48f2-950e-8979a75caf36)

Click Next > Next > Next > Choose Active Directory Certificate Services.

![image](https://github.com/user-attachments/assets/664c7489-1afe-4dc9-907b-286d2cd14c48)

Click Next > Next > Next > Next. For AD CS, choose the Certificate Authority role service.

![image](https://github.com/user-attachments/assets/04aa0450-a9ee-4c85-8949-c60c6639dc6e)

Click on the alert icon and click on the text to Configure Active Directory Certificate Services.

![image](https://github.com/user-attachments/assets/4b12e359-f9d3-4cf7-bc18-172983dfe37a)

Click Next, then select the service role to configure. Click Next.

![image](https://github.com/user-attachments/assets/b53723e5-1e5f-42e4-ba34-d54d2768f4fb)

Choose Enterprise CA and click Next.

![image](https://github.com/user-attachments/assets/6c009654-c758-41f8-917c-5e6eee5c44e6)

We're just going to use the default settings. Click Next > Next > Next > Next > Next > Next > Configure.

### Configure DNS Forwarders

The domain controller's DNS server will be used to resolve DNS queries within the [name of domain].lab domain. However, for queries that it cannot resolve, it will need to forward them to a downstream DNS server. The pfSense default gateway can be used as this downstream DNS server. To configure the DNS settings on the domain controller, open the Start Menu and search for "DNS."

![image](https://github.com/user-attachments/assets/4cc97fa9-e96a-4b5f-b974-a55d0629cc12)

Expand DNS > DC1 and double-click Forwarders.

![image](https://github.com/user-attachments/assets/a52fec83-9dbd-4cf6-97b3-b1a60215d89c)

Click Edit and add the IP address of the default gateway. Click OK.

![image](https://github.com/user-attachments/assets/04c9aa9a-83fd-4707-aae9-10f136085fec)

![image](https://github.com/user-attachments/assets/b2472dbe-ba9f-4774-90bf-4273ac20b596)

### Add and Configure a DHCP Server

Open Server Manager and go to Manage > Add Roles and Features.

![image](https://github.com/user-attachments/assets/c2346bc9-350a-449d-a468-5ee45b39106f)

Click Next > Next > Next. Click DHCP Server.

![image](https://github.com/user-attachments/assets/7276d0ec-a13b-4350-969c-34fa33f0a4e2)

![image](https://github.com/user-attachments/assets/924de763-5c47-4907-a92d-c867354eb5de)

Click Add Features and click Next > Next > Next > Install.

Once the installation is complete, click on Complete DHCP Configuration.

![image](https://github.com/user-attachments/assets/f0869208-1c18-482a-ade0-731d2fdc830b)

![image](https://github.com/user-attachments/assets/c093e03e-261c-4458-a281-6443eb01fb4c)

Click Next > Commit > Close > Close.

Go to the Start Menu and search DHCP.

![image](https://github.com/user-attachments/assets/f528ad4e-c78a-4b4c-bb00-6436031119f3)

Expand the DHCP server tree right-click IPv4 and choose New Scope.

![image](https://github.com/user-attachments/assets/3183010a-c384-4e5a-80e5-dd1745ea1527)

Click Next and give your DHCP configuration a name and description. Then, click Next.

![image](https://github.com/user-attachments/assets/18d77c1e-ae7b-47a0-a96a-6f0630ba36ba)

Configure the DHCP address space and subnet mask. Then, click Next.

![image](https://github.com/user-attachments/assets/9f8f218b-407c-4007-b5b4-15b8d91a71f1)

We're not configuring any DHCP exclusions (reservations), so click Next.

![image](https://github.com/user-attachments/assets/49ba30e1-d159-4d6b-8790-419bf4a974b2)

We'll make it so clients' leases are good for one year. Click Next.

![image](https://github.com/user-attachments/assets/51bcf912-2265-429b-a0f8-79d894d610ab)

Click Next to configure it now.

![image](https://github.com/user-attachments/assets/a0f43082-23ee-44a3-80a2-6276d28b425e)

Enter the address of the default gateway and click Add. Mine is **10.25.25.1**.

![image](https://github.com/user-attachments/assets/ed6d9661-2e60-4df6-b38f-c32ebe335900)


The default DNS configuration for DHCP clients is good here. Click Next. My domain is **galactic.empire** and the IP of **10.25.25.2**.

![image](https://github.com/user-attachments/assets/a7962a82-72c5-4406-be46-a44f9e3a6be8)

We don't have a WINS server in our lab environment. Click Next.

![image](https://github.com/user-attachments/assets/386e6e33-a831-456a-b828-b807ed0939e0)

Click Next to activate the DHCP scope and click Finish.

![image](https://github.com/user-attachments/assets/676e4eba-e20b-4174-b10d-d700469cd0b1)

### Adding a Domain Administrator Account

Go to the Start Menu. Search for Active Directory Users and Computers and open the app.

![image](https://github.com/user-attachments/assets/fa6d2c7b-00bd-4728-9974-743258b6d177)

![image](https://github.com/user-attachments/assets/caef1670-d782-4050-80e3-6f6f2474b14f)

[name of domain].lab > Right-click Users > New > User.

![image](https://github.com/user-attachments/assets/3f84b18e-2fc8-40a2-9b15-8cb32ea00c72)


Fill out the fields according to what you want.

![image](https://github.com/user-attachments/assets/ebefe8fd-c25d-4cc9-a5e8-8aa81632394b)


Set the password and password options.

![image](https://github.com/user-attachments/assets/8c9f6279-7983-454f-af94-d5061bacaa84)

Click Users.

![image](https://github.com/user-attachments/assets/cbb2467c-bfca-4b28-889a-1294b1b87440)

Click Domain Admins.

![image](https://github.com/user-attachments/assets/13ff5758-fb2b-4246-b599-dcb5d634c1d6)

Enter the domain administrator username and click Check Names. Click Ok > Ok.

![image](https://github.com/user-attachments/assets/d18499c1-033f-4030-8c81-fef8f7f63127)

Sign out of the local administrator account.

![image](https://github.com/user-attachments/assets/c084c198-55af-429e-a4ab-6d05a474ca81)

### Add Some Users to the Lab

Log in as the new domain administrator.

![image](https://github.com/user-attachments/assets/724633b2-c68f-4400-b30d-14f192210444)

Go to the Start Menu. Search for Active Directory Users and Computers and open the app.

![image](https://github.com/user-attachments/assets/3f5076ef-a893-408c-a3a4-3a0c437ff776)

[name of domain].lab > Right-click Users > New > User.

![image](https://github.com/user-attachments/assets/bf078b27-be93-4c88-87ca-f594728f46c9)

Create two users, in my case, I created two users related to the environment (Darth Vader and Emperor Palpatine).

![image](https://github.com/user-attachments/assets/0446adca-377b-45c4-8d55-92735aa733f8)

![image](https://github.com/user-attachments/assets/3b6acc7d-b8b5-4002-9c1d-ce4fbc326e72)

![image](https://github.com/user-attachments/assets/66f26d75-4759-49fa-93bd-aa8380796704)

![image](https://github.com/user-attachments/assets/d3f08088-f2cf-4c80-8a29-7588bb38908c)

### Windows 10 Enterprise Template

Power on the VM, choose your language and click Next.

![image](https://github.com/user-attachments/assets/333b62a3-6414-4e11-8724-93206d39fd5c)

Choose Install Now and accept the terms and conditions. Choose Custom: Install Windows Only.

![image](https://github.com/user-attachments/assets/87e00b4a-70ff-48e7-97bf-217e3c62136e)

Click New and then Apply.

![image](https://github.com/user-attachments/assets/c1ee4c41-6cbc-44bc-b42a-f9e922a9bc61)

Click Next. Wait for the installation to finish.

![image](https://github.com/user-attachments/assets/7a0fb988-d9cf-486d-bd69-feb1a903209c)

Select your regional and language settings. Choose Domain Join instead.

![image](https://github.com/user-attachments/assets/60534f60-499b-4085-8ae0-2fc7484ae487)

Enter the username Template, as this is going to be our template VM.

![image](https://github.com/user-attachments/assets/0bb612e2-2554-4085-9265-31036839f8c0)

Enter a password and set security questions. Save the information in a password vault. Turn off all the services here.

![image](https://github.com/user-attachments/assets/37c2c135-c985-4820-86a6-a83dc3fc2283)

Choose Not Now for Cortana.

![image](https://github.com/user-attachments/assets/bf39d3cf-1bb6-410b-85cd-0fea40c20ec2)

### Sysprep the Template

Sysprep will be used to create a template VM. This will ensure that when the VM is cloned, the resulting Windows systems will have unique Security Identifier (SID) values. This is important for joining these cloned systems to a domain, as each system needs a unique SID to be identified within the domain.

Log into the system using the template credentials and open a PowerShell terminal as administrator.

Run the command: C:\Windows\System32\Sysprep\sysprep.exe

![image](https://github.com/user-attachments/assets/65c870df-fa35-4671-9f2e-81c8d032209a)

Click OK. Let the sysprep process run to completion. The VM should shut down.

### Windows 10 Enterprise VM 1

Right-click the Windows 10 Enterprise Template and choose Clone. Give the cloned VM a name such as Win10Ent1.

![image](https://github.com/user-attachments/assets/6723c25d-b9f1-4ba9-b307-19f0304e222b)

![image](https://github.com/user-attachments/assets/a10acb89-8808-4fbb-a2cc-8dbca685599d)

Click Clone and move on to clone the next one.

### Windows 10 Enterprise VM 2

Right-click the Windows 10 Enterprise Template and choose Clone. Give the cloned VM a name such as Win10Ent2.

![image](https://github.com/user-attachments/assets/09b73fac-e1c6-4251-914c-4d2849b697c5)

![image](https://github.com/user-attachments/assets/d4b43e8a-40c5-4d5b-9714-8971b77ea6eb)

Click Clone and wait for the process to complete.

### Joining the Computers to the Domain

This process you need to repeat it with the other machine. 

**Since we chose the Out-of-Box-Experience (OOBE) option when running sysprep on the template VM, we need to go through the Windows setup process again. This is similar to receiving a newly imaged Windows computer from your employer and joining it to the local domain.**

Choose Domain Join instead.

![image](https://github.com/user-attachments/assets/074384a8-19fe-4542-bca7-ff67349ca848)

Set up a password and security questions. Save them in a password manager.

![image](https://github.com/user-attachments/assets/b8e4d853-e39c-40b6-a04f-e29bc1282e4f)

Disable this.

![image](https://github.com/user-attachments/assets/1bf022d3-d557-492a-8a8b-f92c4c15326c)

Choose Not Now for Cortana.

![image](https://github.com/user-attachments/assets/c7c7f72b-37bc-4a77-9441-6142ba7afe7e)

If prompted, choose Yes.

![image](https://github.com/user-attachments/assets/7ec27bd4-2659-4677-b037-041865b37a1d)

Go to the Start Menu > Search for This PC > Right-click > choose Properties.

![image](https://github.com/user-attachments/assets/daad5140-747f-4ea1-9859-891a8a2c7f60)

Go to Advance Settings.

![image](https://github.com/user-attachments/assets/caeb1675-30c6-4011-add8-bbdff7825617)

Click Computer Name and then Change.

![image](https://github.com/user-attachments/assets/de846123-1802-4a3e-8fd5-d687c10c6276)

![image](https://github.com/user-attachments/assets/2e04a1ed-d6d5-4cee-836e-3614f6076d1b)

Click More.

![image](https://github.com/user-attachments/assets/a58eda6b-4f90-4220-81d6-ddd184e76198)

Then enter your local DNS suffix for your AD domain (name of the domain that you created).

![image](https://github.com/user-attachments/assets/a51856bd-07fc-485a-b043-fbb5997bbc78)

Name your computer, whatever you like.

![image](https://github.com/user-attachments/assets/b7c87756-337a-46b4-a1cf-dbe2eaf12335)

Enter your AD local admin.

![image](https://github.com/user-attachments/assets/6eb156ac-29ec-47cc-80a8-6641bd74ace8)

Enter the domain administrator credentials.

![image](https://github.com/user-attachments/assets/2724e77f-f041-41e4-a5a2-9c45e3216124)

![image](https://github.com/user-attachments/assets/b618ce62-4486-465e-9cab-93c65973a173)

Choose Other User > Log in as a domain user.

![image](https://github.com/user-attachments/assets/375905eb-0653-4ff5-9d32-063ffd411f6a)

---

## 10. Make your AD Lab vulnerable

### Using a Vulnerable AD Script

We will use this script to create a vulnerable active directory: **https://github.com/WaterExecution/vulnerable-AD-plus?ref=benheater.com**

Following along with the installation guidance, you should do the following:

- Log into your Domain Controller VM
- Run the script on the Domain Controller

### Open Powershell as Administrator

Right-click the Start Menu and Choose Windows PowerShell (Admin).

![image](https://github.com/user-attachments/assets/f4b0a229-ad3a-448a-a788-dcf203db5fc1)

### Run the script in Memory 

Run the following command: 

*# Set the Execution Policy to allow unsigned scripts*

*Set-ExecutionPolicy -ExecutionPolicy Bypass -Force*

We're going to download the script as a string using a .NET class. The script has a placeholder domain name of change.me, so we must change that before running it.

I'll use the PowerShell -replace operator to change change.me to [name of domain].lab. Be sure to substitute it with whatever your domain is. The script will then run in memory using Invoke-Expression.

*[System.Net.WebClient]::new().DownloadString('https://raw.githubusercontent.com/WaterExecution/vulnerable-AD-plus/master/vulnadplus.ps1') -replace 'change\.me', 'ad.lab' | Invoke-Expression*

As the script executes, you should see lots of output and green status indicating successful operations. In the screenshot below, we're at the end of the script and the server is going to reboot in 30 seconds.

![image](https://github.com/user-attachments/assets/1958d78e-329e-401c-8c33-4783b14c2f5c)

## Enable Some Extra Configurations

### Disable Windows Defender Antivirus and Firewall

Open the Start Menu and search for Group Policy.

![image](https://github.com/user-attachments/assets/9044e22f-c381-49a4-9f43-005a777d0d86)

Expand your forest until you see your domain.

![image](https://github.com/user-attachments/assets/b4ce6ea5-38fe-4f2e-be98-acffe6a1097c)

Right-click your domain name and choose Create a GPO.

![image](https://github.com/user-attachments/assets/816d5a99-cb60-4644-a378-b7c806a97d5e)

![image](https://github.com/user-attachments/assets/03ed6d43-a76a-498f-88dc-84ab0462f27a)

Click OK. Right-click on your new group policy object and click Edit.

![image](https://github.com/user-attachments/assets/e23c24ee-5fdd-4a5e-8ffc-d3017d819c1f)

Expand down into Computer Configuration > Policies > Administrative Templates > Windows Components.

![image](https://github.com/user-attachments/assets/dfaf703c-e6e2-4e8d-a58a-945df3d74dc1)

Click on Windows Defender Antivirus, set it to enabled, and click OK.

![image](https://github.com/user-attachments/assets/24bacaef-a79c-411f-8f44-2e3c416029b4)

Click on Real-time Protection.

![image](https://github.com/user-attachments/assets/57a37453-830d-4b0e-979e-c42bac1608a8)

Double-click Turn off real-time protection, set it to enabled, and click OK.

![image](https://github.com/user-attachments/assets/493169c3-b5fe-45f6-a90c-5ad84c2b5c85)

Now, go to Network > Network Connections > Windows Defender Firewall > Domain Profile.

![image](https://github.com/user-attachments/assets/cd016b5d-4e89-418a-bd8e-7bc212495d5c)

Double-click Windows Defender Firewall: Protect all network connections. Set to Disabled and click OK.

![image](https://github.com/user-attachments/assets/3b266d98-e79c-4c15-9e6a-51155a22162a)

Right-click the group policy object. Turn on the Enforced option.

![image](https://github.com/user-attachments/assets/c92383d2-475e-402f-b4e6-1955e1e524e7)

### Enabling Any Local Admin Remote Login

Log into your Domain Controller and run the Group Policy Management app.

![image](https://github.com/user-attachments/assets/3493e5c9-d87f-447f-8071-ba3771ebfe28)

Expand into and right-click the domain name. Choose Create a GPO in this domain, and Link it here.

![image](https://github.com/user-attachments/assets/36f6d10c-d3b5-45a7-9423-1aa5fb60458d)

![image](https://github.com/user-attachments/assets/80a67dea-edc3-47d8-95d8-5ea4f9075dcc)

Right-click the new GPO and click Edit.

![image](https://github.com/user-attachments/assets/d41f4424-6a7a-487a-913b-09745ed79009)

Descend into Computer Configuration > Preferences > Windows Settings > Registry. Then, right-click Registry and choose New > Registry Item.

![image](https://github.com/user-attachments/assets/d373f471-1521-48e1-aba8-b9f95014d671)

- The Hive is **HKEY_LOCAL_MACHINE**
- The Key Path is **SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\**
- The ValueName is **LocalAccountTokenFilterPolicy**
- The ValueType is **REG_DWORD**
- The ValueData is **1**

![image](https://github.com/user-attachments/assets/07ed763a-d3cd-4d2c-bdbe-4c08af57f651)

### Enable WinRM Server on All Domain Hosts

Log into your Domain Controller and run the Group Policy Management app.

![image](https://github.com/user-attachments/assets/bc783e8c-2654-4c1b-afc2-09326bee650d)

Expand into and right-click the domain name. Choose Create a GPO in this domain, and Link it here.

![image](https://github.com/user-attachments/assets/219893af-923a-4454-bdbd-008617320bd6)

Give the GPO a name of something descriptive like Enable WinRM Service. Then, right-click the new GPO and choose Edit.

Start from Step 5 on the IBM knowledge base article below. You don't need to run gpupdate /force just yet, as we have other GPOs to create.

Also, skip the last step to create a firewall rule because we have it disabled earlier.

Link: https://www.ibm.com/docs/en/tarm/8.13.0?topic=management-enabling-winrm-via-global-policy-objects

This will open TCP/5985 on your Windows 10 hosts. You can verify the service is running by checking if that port is open.

### Enable Remote Desktop Service on All Domain Hosts

Log into your Domain Controller and run the Group Policy Management app.

![image](https://github.com/user-attachments/assets/0c867525-3c88-4df3-8c89-c9cde7d59b36)

Expand into and right-click the domain name. Choose Create a GPO in this domain, and Link it here.

![image](https://github.com/user-attachments/assets/b92e96be-0f1e-4290-ae3c-e807bbdc0889)

Give the GPO a name of something descriptive like Enable Remote Desktop Service. Then, right-click the new GPO and choose Edit.

Descend into Computer Configuration > Policies > Administrative Templates > Windows Components > Remote Desktop Services > Remote Desktop Session Host > Connections. Then, configure the policy as shown below and click OK.

![image](https://github.com/user-attachments/assets/7a310ec5-2cc3-49a2-b5e5-70548973dddf)

This will open TCP/3389 on your Windows 10 hosts.


**If you want to allow any non-admin user to RDP into your domain hosts, follow the guidance here: https://technet2.github.io/Wiki/articles/17671.how-to-add-domain-usersgroup-to-remote-desktop-users-group-on-servers-using-group-policy.html?ref=benheater.com**

**Use the GPO you've created here in this step and follow along with the article. The article uses the Remote Server Users security group, which doesn't exist in this lab. Instead, you can use the Domain Users group.**

### Enable RPC Access on All Hosts

Log into your Domain Controller and run the Group Policy Management app.

![image](https://github.com/user-attachments/assets/d4cf396e-d6d3-4771-aa13-ba8f0a92cf56)

Expand into and right-click the domain name. Choose Create a GPO in this domain, and Link it here.

![image](https://github.com/user-attachments/assets/ebf6bc16-f9ce-41e1-8322-0cdafce13903)

Give the GPO a name of something descriptive like Enable RPC Access on All Hosts. Then, right-click the new GPO and choose Edit.

Descend into Computer Configuration > Administrative Templates > System > Remote Procedure Call and set Enable RPC Endpoint Mapper Client Authentication to Enabled.

![image](https://github.com/user-attachments/assets/32b29036-a153-49d8-bc07-4a9c1298d51f)

### Update the Domain Policies

Now, open a PowerShell console as administrator on the Domain Controller and run this command: gpupdate /force

![image](https://github.com/user-attachments/assets/4cff3f44-644c-482e-aac3-d03dd6a80b31)

Finally, reboot your Windows 10 VMs, so that they pull the new policies when they come up. Alternatively, you can log into each VM and run the gpupdate /force command.

**Now we can start attacking our Active Directory**

**You can add this if you want, to cover another attack. Link: https://www.blumira.com/integration/how-to-disable-null-session-in-windows/
A reboot is required to apply the changes.**

---

## 11. Building a Pivoting Lab To Practice External Pentest

### Network Diagram

![image](https://github.com/user-attachments/assets/2890a7eb-2f5a-470d-9962-91c1ae89af25)

### Setting up the Firewall

The point is to make the lab as realistic as possible. To do so, we will add a rule to the LAN subnet that blocks all packets to the AD_LAB subnets.

### Block Packets to AD Subnet

Go to Firewall > Rules on pfSense.

![image](https://github.com/user-attachments/assets/271ad827-b60f-4539-82f2-1d45ff5ca8cc)

Choose LAN.

![image](https://github.com/user-attachments/assets/1fb49432-f36e-48db-a96e-c7d187fa9cdb)

Click Add.

![image](https://github.com/user-attachments/assets/bfd20b19-b5a9-475e-873a-06b788b5a1e2)

![image](https://github.com/user-attachments/assets/db76748b-500c-4252-a03e-8c9b9405c0be)

![image](https://github.com/user-attachments/assets/f9fd88b8-41e3-46bd-9cae-c78399647ed1)

Save and Apply Changes.

### Toggling the New Rule

In pfSense you can toggle a rule on and off without deleting it by pressing the little ✅ or ❌ to the left side of the rule.

![image](https://github.com/user-attachments/assets/ea350f85-01ca-45ed-bbf3-7d49bf810c5a)

Once you've toggled the rule on or off, click Apply Changes for it to take effect. You can turn it off if you do not want it. But for the sake of this lab, we need it enabled.

### Setting up the Vulnerable Target

To keep things simple, we'll use an existing target that should already be in our lab. We are going to use Metasploitable 2 but you can use whatever machine you want. 

### Tweaking Metasploitable 2

Right-click Metasploitable 2 > Snapshots.

![image](https://github.com/user-attachments/assets/2439f8bc-9637-47d4-af11-65ecdf8494c4)

![image](https://github.com/user-attachments/assets/b20c688d-11d3-4b5e-b170-3125d386c7fe)

![image](https://github.com/user-attachments/assets/16f89731-de26-4cd4-be85-09959238a98d)

Right-click Metasploitable 2 > Settings.

![image](https://github.com/user-attachments/assets/6be6cc5b-68b2-4a15-9226-18fe1c043415)

![image](https://github.com/user-attachments/assets/1cc0a036-a77c-42a1-b01e-7eb0de48766d)

Adapter 1 (ISOLATED).

![image](https://github.com/user-attachments/assets/f8c6b4f9-921e-4c4a-abfb-4bff0448dbbd)

Adapter 2 (AD LAB).

![image](https://github.com/user-attachments/assets/8146f32d-0e74-4638-8914-799ceeb9b8fd)

### Start Up and Configure the Interfaces

For this step, we will need to log into the Metasploitable 2 VM with some credentials and configure the /etc/network/interfaces file, so that we get a DHCP lease on the AD_LAB subnet. Use msfadmin:msfadmin credentials.

![image](https://github.com/user-attachments/assets/98f7738b-ea50-412f-8468-e93192ac54d2)

Command: **sudo nano /etc/network/interfaces**

Before.

![image](https://github.com/user-attachments/assets/e2fc5ab0-b1c4-41a6-be76-b9b649bc7301)

**The post-up IP route commands shown below are used to prefer the 10.25.25.1 gateway as the default route so that the Metasploitable 2 host can retain internet access.**

After.

![image](https://github.com/user-attachments/assets/04470746-0cb9-46a9-a509-3acf38cdbb48)

Press CTRL + X then Y to save the changes to the file. Then, press Enter. Finally, we need to refresh the networking stack so that we get a new DHCP address on the AD_LAB subnet.

Command: **sudo /etc/init.d/networking restart**

![image](https://github.com/user-attachments/assets/8f55beb3-450a-4686-9c0e-837ff839cb5f)

**Now we are done with the lab! Happy Hacking!**
