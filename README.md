<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# Project: Creating and Configuring an osTicket System on Microsoft Azure

## Objective
To set up and configure a comprehensive ticketing system using osTicket hosted on a Windows 10 virtual machine within Microsoft Azure.

---

## Environments and Technologies Used
- **Microsoft Azure:** Virtual Machine
- **Remote Desktop**
- **IIS (Internet Information Services)**

## Operating System Used
- Windows 10 (21H2)

## List of Prerequisites
1. Azure Subscription
2. Remote Desktop Application
3. osTicket Installation Files
4. Basic understanding of IIS and MySQL
5. Virtual Machine configuration knowledge

---

## Steps and Configurations

### **Step 1: Create an Azure Virtual Machine**
- **Name:** `osticket-vm`
- **Specifications:** Windows 10, 4 vCPUs
- **Credentials:** 
  - Username: `labuser`
  - Password: `osTicketPassword1!`

### **Step 2: Log into the VM**
- Connect to the Azure VM using Remote Desktop.

### **Step 3: Download osTicket Installation Files**
- Download and unzip the `osTicket-Installation-Files.zip` onto your desktop within the VM.
- This folder contains all necessary dependencies for osTicket installation.

### **Step 4: Install and Enable IIS with CGI**
1. Open IIS Manager and enable the following:
   - `World Wide Web Services`
   - `Application Development Features`
   - `[X] CGI`
     ![image](https://github.com/user-attachments/assets/b3907ffd-4902-48d3-968b-caab8251bd0a)

   
### **Step 5: Install Required Dependencies**
From the `osTicket-Installation-Files` folder, install the following:
1. **PHP Manager for IIS**: `PHPManagerForIIS_V1.5.0.msi`
   ![image](https://github.com/user-attachments/assets/c47e2fb5-f23f-4b1f-90fa-cd46c26bf02c)

3. **Rewrite Module**: `rewrite_amd64_en-US.msi`
   ![image](https://github.com/user-attachments/assets/f8ffe256-f568-4206-8072-c7d48fad0b6d)


### **Step 6: Setup PHP**
1. Create the directory `C:\PHP`.
2. Unzip `PHP 7.3.8` into `C:\PHP` using the file `php-7.3.8-nts-Win32-VC15-x86.zip`.
   ![image](https://github.com/user-attachments/assets/a65d0464-3bef-4cc5-88e7-2f2c1fecbd78)

4. Install `VC_redist.x86.exe`.
   ![image](https://github.com/user-attachments/assets/48c39a8a-21cb-4ce1-a27e-d2b6f4dd05d3)


### **Step 7: Install MySQL**
1. Install **MySQL 5.5.62**:
   ![image](https://github.com/user-attachments/assets/f2008d98-6c2e-4bdd-bee2-e8b0d0bd429b)

   - **Username:** root
   - **Password:** root
3. Launch the MySQL Configuration Wizard and select:
   - `Standard Configuration`
     ![image](https://github.com/user-attachments/assets/714edff1-accc-412c-ac39-8c6f7524b319)

   
### **Step 8: Configure IIS for PHP**
1. Open IIS Manager.
2. Use PHP Manager to register PHP:
   - Path: `C:\PHP\php-cgi.exe`
     ![image](https://github.com/user-attachments/assets/7bd1a105-37f7-478c-a63f-45fbe0acf900)

3. Restart IIS (Stop and Start the Server).

### **Step 9: Install osTicket**
1. Unzip `osTicket-v1.15.8.zip` from the `osTicket-Installation-Files` folder.
2. Copy the `upload` folder into `C:\inetpub\wwwroot` and rename it to `osTicket`.
   ![image](https://github.com/user-attachments/assets/1e480773-f9f8-46c8-9ba1-0426b1301c57)

4. Restart IIS.

### **Step 10: Verify osTicket Setup**
1. Browse to `http://localhost/osTicket`.
   ![image](https://github.com/user-attachments/assets/3a3bbba7-2124-4599-b92d-23b5dbd66d47)

3. Enable necessary PHP extensions:
   - `php_imap.dll`
   - `php_intl.dll`
   - `php_opcache.dll`
     ![image](https://github.com/user-attachments/assets/42522f42-6084-4302-ac75-80c6a310a916)
     ![image](https://github.com/user-attachments/assets/7b8c9d35-606d-4d30-b1d0-8f8c820c4392)


4. Rename `ost-config.php`:
   - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
   - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`
     ![image](https://github.com/user-attachments/assets/191c8145-1a81-4f2f-a531-3a51e8b19855)

5. Assign permissions to `ost-config.php`:
   - Disable inheritance and remove all permissions.
     ![image](https://github.com/user-attachments/assets/6d65ca7a-c94a-4f00-a924-819604d33a7f)

   - Add permissions: `Everyone` with `Full Control`.
     ![image](https://github.com/user-attachments/assets/57f8607d-a861-43b7-8e77-f60170b58ab4)


### **Step 11: Finalize osTicket Setup in the Browser**
1. Provide the following details:
   - **Helpdesk Name**
   - **Default Email**
     ![image](https://github.com/user-attachments/assets/31a16c7e-7dec-487d-b7f9-61f2c8c6aefe)

2. Install **HeidiSQL** and use it to create a database:
   ![image](https://github.com/user-attachments/assets/071357be-ae47-42ce-bff3-dcd9cf81f1cf)

   - **Database Name:** `osTicket`
     ![image](https://github.com/user-attachments/assets/06b02ccc-6da2-40b5-9b1e-a492ddfff399)

   - **Username:** root
   - **Password:** root
4. Complete the browser setup:
   - **MySQL Database Name:** `osTicket`
   - Click `Install Now`.
     ![image](https://github.com/user-attachments/assets/2c037161-8bb7-48ed-9433-c58a6b09bfac)
     ![image](https://github.com/user-attachments/assets/1a8c9231-8835-409d-bcad-3b537cf51c16)

## URLs
- **Help Desk Admin Login:** `http://localhost/osTicket/scp/login.php`
  ![image](https://github.com/user-attachments/assets/8d6e9db5-6da4-46fc-b195-ba00a82b02e6)

- **End Users Access:** `http://localhost/osTicket/`
  ![image](https://github.com/user-attachments/assets/25092ecb-31ca-4870-896c-f39ef382f179)


### **Step 12: Clean Up**
1. Delete the `setup` folder:
   - Path: `C:\inetpub\wwwroot\osTicket\setup`
2. Set `Read-Only` permissions for:
   - Path: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

---


This project showcases a robust osTicket setup and configuration for an Azure-hosted environment.
