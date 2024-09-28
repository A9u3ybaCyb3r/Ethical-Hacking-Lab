# Virtual-Network-Penetration-Testing-Lab

## Objective

The lab focuses on providing a safe and controlled space to practice various security skills, including network security, penetration testing, and defensive strategies. By building virtual machines and configuring a network with a firewall, you can simulate real-world scenarios and gain hands-on experience with security tools and techniques.

### Skills Learned

- Virtualization: Installing and configuring VirtualBox software, creating and managing virtual machines (VMs), allocating resources to VMs, and installing guest operating systems.
- Network Security: Understanding network concepts (VLANs, subnets, IP addressing), configuring virtual networks with pfSense firewall, setting up network segmentation, and implementing network security controls.
- Penetration Testing: Importing pre-configured vulnerable machines (VulnHub) and Kali Linux for practicing penetration testing techniques.
- Active Directory: Building a simulated Active Directory environment to understand directory services and practice potential attack vectors.
- Security Analysis: Utilizing tools like pfSense firewall for network traffic control.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used


- VirtualBox: A virtualization software platform used to create and manage virtual machines.
- pfSense: An open-source firewall software used to create a secure network gateway for the virtual lab environment.
- Kali Linux: A Linux distribution pre-loaded with various security and penetration testing tools.
- VulnHub: A repository of pre-configured vulnerable virtual machines for practicing penetration testing techniques.
- Windows Server 2019: Used as the Domain Controller (DC) to host Active Directory.
- Windows 10: Used as a client machine to join the domain and interact with the AD environment.
- Draw.io: Used to draw and document the network topology and lab setup.

## Steps to build the lab

### Planning Phase
1. First we will build a network diagram to represent our lab visually.
   
![Network Diagram](https://github.com/A9u3ybaCyb3r/Virtual-Network-Penetration-Testing-Lab/blob/main/StrikeZone%20Net%20Diagram.drawio.pdf)

 
### Downloading Virtualbox and installing Virtualbox
1. Go to this link https://www.virtualbox.org/wiki/Downloads and download depending on your operating system.

![image](https://github.com/user-attachments/assets/f291de59-ca36-44c4-93c0-dbb21030192f)

Do not forget to install the extension pack

![image](https://github.com/user-attachments/assets/40457f5e-4417-4b4b-b642-f0c4c704617e)

2. Click on the file that you downloaded and just go with the default settings.
3. Open the application, go to File, then Tools, then the Extention Pack Manager.

![image](https://github.com/user-attachments/assets/67c5e941-0cbf-4dc1-95e9-8ef9ffa4d88d)

4. Next hit the Install button and choose the Virtualbox extension pack that you downloaded.

![image](https://github.com/user-attachments/assets/2d202300-7d52-43c7-baa2-291f35362450)
![image](https://github.com/user-attachments/assets/230cf88a-54de-4522-858b-991670742f14)


## Building a pfSense VM

1. First we download the file that we need. 
 - Go to this link: https://www.google.com/search?q=site%3A*.netgate.com+download+-site%3Aforum.netgate.com+-site%3Adocs.netgate.com+-inurl%3Ablog+-site%3Awww.netgate.com+-site%3Ashop.netgate.com+-site%3Aforums.netgate.com+-site%3Ainfo.netgate.com&ref=benheater.com

Choose this one. 

![image](https://github.com/user-attachments/assets/b1c3be2d-a7dd-437d-af8d-3af6658d3056)


Then we choose the latest version.

![image](https://github.com/user-attachments/assets/4510c75a-d8b6-4821-ae6d-df8d84c0bf3a)


2. Extract the file, in this case I will be using 7-zip.

![image](https://github.com/user-attachments/assets/b395d9a3-6e1c-4d7d-a32f-352084f731eb)

3. Create a New Machine

![image](https://github.com/user-attachments/assets/a1bed139-45f7-4864-9d89-74ef542fc0cc)

Name your vm, choose the folder that you want to save the machine, choose the iso image that you want to use, and select the type and version of the VM.

![image](https://github.com/user-attachments/assets/fa7194ac-cf8c-44f5-882e-62213f7dc89d)

![image](https://github.com/user-attachments/assets/56b00275-2a31-4da9-8535-45e44f417f51)

![image](https://github.com/user-attachments/assets/bf359848-201f-438d-992a-66db8d18b070)

![image](https://github.com/user-attachments/assets/e73ca9a0-ee82-4aff-83a5-d966640e2c60)

!!Do not start the VM yet!!

4. Go to the settings of the machine

![image](https://github.com/user-attachments/assets/783117c5-c6c4-42d2-81c3-d70b5ce5d8fb)

Change the boot order and match it as in the image shown below. Also, uncheck the Floppy Disk 
This will ensure that the operating system boots upon installation from the disc.

![image](https://github.com/user-attachments/assets/f69d55aa-465c-4616-a2cb-ceac898494ef)

Go to the audio settings and disable the audio

![image](https://github.com/user-attachments/assets/0677dd7d-2d4d-4383-8697-01d8fe5b8c04)

Go to the USB settings and disable it.

![image](https://github.com/user-attachments/assets/96c4257b-b5aa-416e-a86a-2f23360f1d0c)

5. Configure the Network Interface

Still on the machine settings go to the Network settings.

![image](https://github.com/user-attachments/assets/f21163f3-85dc-4176-a402-9eb705f61631)

Adapter 1 WAN:

![image](https://github.com/user-attachments/assets/7ba13507-0c08-4ce8-a7a5-48591123ad08)

Adapter 2 LAN:

![image](https://github.com/user-attachments/assets/924e9715-78d5-45ba-8176-7dcb7d878862)

Adapter 3 ISOLATED:

![image](https://github.com/user-attachments/assets/7f6f4678-f46f-4344-8b99-9b39a45d55cf)

Adapter 4 AD-LAB:

![image](https://github.com/user-attachments/assets/7fe81f34-1f06-443e-bbaf-251de2fc6024)

After doing all of this we can start the machine.

## Intstalling pfSense

1. Start the machine.

![image](https://github.com/user-attachments/assets/e8207eaf-82db-4e52-a6e0-5efb4512622d)

![image](https://github.com/user-attachments/assets/16fb7088-5ea1-44f1-ac24-7f3a8b9eddea)

Press Enter 

![image](https://github.com/user-attachments/assets/178f335e-62cf-409e-91d4-9c175da0c808)

2. Choose Install pfSense

![image](https://github.com/user-attachments/assets/ebc7e2fa-5d63-4bcf-ad4a-7e31b10de690)

Choose Auto (ZFS)

![image](https://github.com/user-attachments/assets/fe0a64bc-c58a-4771-bacf-3412eccc69d3)

Then proceed with the installation using the default configuration.

![image](https://github.com/user-attachments/assets/3ef9e02b-aa6d-49f4-92c3-d64d3539a813)

Choose Stripe - No Redundancy

![image](https://github.com/user-attachments/assets/f109234a-7691-4aba-beb2-21ff7bb2fc25)

Use the Space Bar to choose the disk that you want. We should see an asterisk (*) on the option that we chose.

![image](https://github.com/user-attachments/assets/e26bf8a4-d30c-4f8b-bad7-b3c3c93121a4)

Choose YES to continue

![image](https://github.com/user-attachments/assets/4e52f142-af31-477e-bb39-06a898fe9910)

Now we wait for the installation to complete and then we choose Reboot

![image](https://github.com/user-attachments/assets/2296c60c-d355-4902-9789-5f394ef42f15)


## Configuring pfSense

When the VM finishes from booting We are going to be asked this question: Should VLANs be set up now [y|n]?, we will choose n

![image](https://github.com/user-attachments/assets/f9a0cf84-ee71-4439-a54a-731c478bcf64)

Then we will enter our interfaces. The first one is for WAN

![image](https://github.com/user-attachments/assets/4f3fe5fa-f812-4c77-a728-cb1f7fdd7b1d)

LAN Interface

![image](https://github.com/user-attachments/assets/ade25300-b7de-45d2-952d-2bf19da796fe)

ISOLATED Interface

![image](https://github.com/user-attachments/assets/dc1363e8-5b9f-43e6-9833-e7629f46e538)

Lastly our AD_LAB Interface

![image](https://github.com/user-attachments/assets/ea899840-4ee0-4bd5-9b48-8f6f6883aa5d)

We should finish with this configuration after we confirm that this is what we want to choose y

![image](https://github.com/user-attachments/assets/4e4f7eef-f07d-41f7-a125-1836168c733f)

### Setting up the Interfaces

- The WAN interface will pull an IP address from your home network. It will be different from mine.
- The LAN IP address is going to be in the default option which is going to be 192.168.1.1/24. We will change this later
- OPT1 is going to be our ISOLATED interface and is not yet configured. We will configure it later.
- OPT2 is going to be our AD_LAB interface and is not yet configured. We will configure it later.

![image](https://github.com/user-attachments/assets/32211990-aa57-4a3d-b86a-7dacca3b3e1d)

### Configure the LAN

Enter option 2

![image](https://github.com/user-attachments/assets/ded46fbe-ea36-48c8-89a1-ab5752bf9405)

We are going to change the LAN so enter option 2

![image](https://github.com/user-attachments/assets/2fd90833-1370-4f2f-a932-cf4a8a090c68)

We are going to configure the address statically we will enter 'n'

![image](https://github.com/user-attachments/assets/a33a78e9-4594-4597-b44a-4f61a55f324b)

Enter the IP address

![image](https://github.com/user-attachments/assets/d44ef8c7-3c84-4c2d-9a5e-95db20d74310)

Enter the subnet mask bits

![image](https://github.com/user-attachments/assets/b7dd1628-263f-4e7a-be09-dd3d69c55583)

Hit Enter this is for LAN.

![image](https://github.com/user-attachments/assets/3e8990ab-4066-4866-9196-0e9b157026e0)

Press n to configure the address statically

![image](https://github.com/user-attachments/assets/23ea1fb7-2727-459c-9187-f293acfeecfc)

Press Enter we are not going to be using IPv6

![image](https://github.com/user-attachments/assets/14099163-f473-42e9-a7de-86ab03eb58cc)

Enter y to enable the DHCP server

![image](https://github.com/user-attachments/assets/36f07dcd-46d5-41d1-9cf3-90c689094758)

Enter the start and end range

![image](https://github.com/user-attachments/assets/8701352d-1e83-4ce3-bfcd-a18683d29d21)

Enter n, we want to keep using TLS on the web portal

![image](https://github.com/user-attachments/assets/cee8c91a-3fea-497f-bcd4-c8eb6f794aa8)

Press Enter and you are done with the LAN

![image](https://github.com/user-attachments/assets/18fb87f1-88ba-4002-a764-e623e34fd87d)

### Configure the ISOLATED Interface

Enter 2

![image](https://github.com/user-attachments/assets/c8265961-0bed-425d-be7b-96efcad11aeb)

Enter option 3 to configure OPT3

![image](https://github.com/user-attachments/assets/0883dce2-053f-44fe-907b-3d96ae9ea5b5)

Enter n to configure the address statically

![image](https://github.com/user-attachments/assets/399d4ace-edf9-4359-a375-771a37bb71f3)

Enter the network address

![image](https://github.com/user-attachments/assets/d0f7ce08-b81e-4cd6-b3bf-b92a907264de)

Enter the subnet mask bit

![image](https://github.com/user-attachments/assets/5aa86244-f89a-4962-bfa1-466c09a68f29)

Press Enter this is for the LAN

![image](https://github.com/user-attachments/assets/c47dfcc5-e16b-47dc-9ae0-0d0f48a4bf63)

Press n to configure statically 

![image](https://github.com/user-attachments/assets/618cd159-3979-408c-bcfd-f9ea80c61d6a)

Press Enter we will not be using IPv6

![image](https://github.com/user-attachments/assets/232aafbb-ca03-43cb-9046-d4549ac6b424)

Enable the DHCP server "y" and then enter the start and end range

![image](https://github.com/user-attachments/assets/1c13e01c-9756-429b-8c42-448ae30ba4f3)

Enter n, we want to keep using TLS on the web portal.

![image](https://github.com/user-attachments/assets/c77ad20b-be1d-4135-8876-670b92f10a8a)

Now we are done with the ISOLATED Interface

![image](https://github.com/user-attachments/assets/93e0a0bd-f519-4ff1-9d6b-b945b2502173)

### Configure the AD_LAB

Enter option 2 

![image](https://github.com/user-attachments/assets/17caea15-b67f-49ba-8e12-6926a5124612)

Enter 4 to configure the OPT4

![image](https://github.com/user-attachments/assets/7119fee6-3375-4462-abd8-7d88f3423421)

Enter the n to configure the address statically

![image](https://github.com/user-attachments/assets/8b091b1f-4971-4ab4-8a8f-9690e7b12455)

Enter the network address

![image](https://github.com/user-attachments/assets/dc69c922-e5b7-45ca-a1f1-6f9a19df0f40)

Enter the subnet mask bits

![image](https://github.com/user-attachments/assets/06bd2dd6-0561-4389-9010-b2a70e671473)

Press Enter, this is for the LAN

![image](https://github.com/user-attachments/assets/ff489e11-bc9f-4929-bc91-9169e9ca5731)

Enter n to configure the address statically

![image](https://github.com/user-attachments/assets/b4fe77f0-fbd9-47e2-af03-133744f353e7)

Press Enter, we are not going to use IPv6

![image](https://github.com/user-attachments/assets/1597c9a7-a41f-4369-975e-30bfbfb0745f)

Enter n to disable the DHCP server, as the domain controller will be acting as the DHCP server

![image](https://github.com/user-attachments/assets/b691fdee-718b-4230-a0ba-c4915b2e1063)

Enter n, we want to keep using TLS on the web portal

![image](https://github.com/user-attachments/assets/ee252a48-5a29-4092-828f-81587093f117)

Now we are done with the AD_LAB Interface.

![image](https://github.com/user-attachments/assets/7d8c3f96-2db1-462f-a122-0c7ee1d66107)

### Final Check

This is how it should look like after we are done. Remember mine might be different than yours if you chose to use another IP address.

![image](https://github.com/user-attachments/assets/2a0f79b8-93a5-49ee-823b-f4970d67dd11)

### !!!Important!!!

We will not be making the pfSense web console accessible from the WAN to avoid exposing it to public networks, especially if using a laptop on public wireless. Instead, the configuration of the firewall rules will be done using a Kali VM later in the process.

## Importing Kali 

 Go to https://kali.org/get-kali/
   - Click on the image that says Virtual Machines and download the 64-bit version of Virtualbox.

      ![image](https://github.com/user-attachments/assets/ae2d558e-57a4-4d1a-8576-5ad25de659ec)
     
     ![image](https://github.com/user-attachments/assets/6430026d-9ca1-46db-9dd6-98e6d758617c)

 After downloading the file, extract it and hit the Add button on Virtualbox. 

![image](https://github.com/user-attachments/assets/37ef160d-c250-4151-80df-bdfb038f063c)

Then choose the .vbox extension file.

![image-38](https://github.com/user-attachments/assets/5cf67d2e-ebd6-4c6e-ab83-f49f87a27b82)

3. Right-click the machine and choose the Network settings.

![cd25168f5bf7404cb6e4d5a8b84ca441](https://github.com/user-attachments/assets/465b1135-d2b9-4e79-aa75-f6eb9f315ed1)

Change the network settings to the pfSense LAN network that you created.

![image](https://github.com/user-attachments/assets/82294fe3-d42c-44cb-8982-732ef4d9e3aa)

Then increase your RAM depending on how much you need. Mine is 8GB RAM because of the tools that I use. You can do it on the machine settings. 

![image](https://github.com/user-attachments/assets/9cf482b6-64c7-48be-8248-fe25ad5868eb)

4. Click OK and now you can start the machine. Use the default credentials of *kali:kali*

![image](https://github.com/user-attachments/assets/919a0fe4-12fe-4847-acad-0180f51a77b8)

5. Open the terminal to see if we are on the LAN network. Our IP Address should be 10.19.19.X/24. Later we can set up the IP Address that we want later.

![image](https://github.com/user-attachments/assets/3507057e-d6df-423e-9fbe-bde723849657)


## Configuring the pfSense firewall

1. Log into the web portal (firefox for me) in your Kali machine to: https://10.19.19.1

![image](https://github.com/user-attachments/assets/db0ecfcb-6a40-4817-8187-8cabda8db0bd)

2. If you encounter this, click Advanced

![image](https://github.com/user-attachments/assets/329900dc-3fec-47e3-8335-42b84cd7069a)

Then accept the risk

![image](https://github.com/user-attachments/assets/2fbd799e-db1d-447b-8616-538c8b91f774)

The default credentials are:

- Username: admin
- Password: pfsense

Click Next after loggin' in

![image](https://github.com/user-attachments/assets/4157974c-affb-43d9-aa12-f745ad488560)

Fill out the Hostname and Domain. Uncheck Override DNS. You can use whatever name you want. Click Next.

![image](https://github.com/user-attachments/assets/c3e8a9f6-c266-4412-a404-03931166ec10)

Double-check your timezone and click Next.

![image](https://github.com/user-attachments/assets/6a3875bf-c8be-4140-863b-3296c20aa10a)

Scroll down and uncheck this option. We’re double-NAT, meaning the WAN network is also private and we want to allow this. Click Next.

![image](https://github.com/user-attachments/assets/1fa7b998-b55c-4207-a454-831a331e4356)

Click the Next

![image](https://github.com/user-attachments/assets/d01ad2a6-3c77-446e-80a0-34b74245ba2c)

Change the admin password and remember it. 

![image](https://github.com/user-attachments/assets/73b60b4c-6325-479f-b7be-fe1ef1b8e934)

Click Next and Finish

## Configure the Interfaces

### Isolated Interface




## Importing Vulnhub VMs to the lab

## Building an Active Directory

## Building a Pivoting Lab
