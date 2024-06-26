# Active Directory Lab Project

![Active Directory lab](https://github.com/TCHAPTCHET-Florian/files/blob/main/Arch_AD.gif)
<br><br>
<!-- ![Active Directory lab2](https://imgur.com/q23hpCu.gif) -->

## Introduction

Welcome to my dynamic lab project, where I'll be crafting a virtual environment to simulate a mini corporate setup. Through VirtualBox, I've orchestrated two key players: a Windows Server 2019 Domain Controller and a Windows 10 Client. The Domain Controller stands as the authority figure, managing the digital domain, while the Windows 10 Client plays the role of an employee navigating within this intricate network. As I dive into configuring network interfaces, my aim is to create a functional small-scale representation that reflects the complexities of a real-world corporate IT environment. Join me as I navigate the details of this lab journey, aiming to create a rich learning experience in network management and system administration.


The Active Directory Homelab architecture includes:


- **VirtualBox:** The foundation for creating and managing virtual machines, facilitating real-world scenario simulation

- **Windows Server 2019:** As the Domain Controller, it manages users, devices, and policies, forming the core of Active Directory Domain Services

- **Windows 10:** Representing an employee workstation, it provides insights into the corporate end-user experience

- **Network Interfaces:** Enabling communication, with one for internet access and another for internal network interaction

- **Active Directory Domain Services:** Crucial for user and network organization, structuring users, computers, and resources coherently

- **DHCP:** Automates IP address assignment, streamlining network configuration

- **RAS/NAT:** Facilitates seamless internal-external network connectivity

- **User List Text File:** Stores user info, aiding efficient user setup and management

- **Python Script:** Adds automation and customization, enhancing user creation

- **Group Policy Object:** Enforces network-wide policies, maintaining settings, security, and access controls


Collectively, these tools and architectural elements culminate in an environment where virtual machines interact harmoniously, mirroring the intricacies of a corporate ecosystem. Through exploration and manipulation, this lab offers an immersive platform to experiment, learn, and finesse the art of network management and system administration.

<details>
  <summary><h2><b>Section 1: NETWORK INTERFACE CARD (NIC) CONFIGURATIONS</b></h2></summary>
  <br> <br>
  In this section, We'll be configuring the 2 NICs on the Windows Server 2019.<br><br>
  
  ![Image 1](https://imgur.com/q23hpCu.gif)
  <br><br>
  
  **Step 1: Access Network Settings:**
  - Open "Network Connections" from the Control Panel
  
  **Step 2: Identify NICs:**
  - Identify the two NICs and renaming them to "Internet" and "Internal"
  
  **Step 3: Assign IP Addresses and Configure DNS:**
  - For NIC 1 (Internal):
    - IP Address: 10.2.22.1
    - Subnet Mask: 255.255.255.0
    - Default Gateway: (empty)
    - Preferred DNS Server: 127.0.0.1
  - For NIC 2 (Internet):
    - Obtain IP settings automatically (DHCP) for internet access
    - Obtain DNS server address automatically 
  
  **Reasons for the Configuration:**
  - NIC 1: Provides a gateway for the internal network.
    - **Explanation:** NIC 1 with IP "10.2.22.1" connects devices inside our network. We don't set a gateway to keep this network separate from the internet.
  - NIC 2: Enables connection to the internet.
    - **Explanation:** NIC 2 gets settings from the network, letting us connect online easily.
   
</details>

<details>
  <summary><h2><b>Section 2: INSTALL ACTIVE DIRECTORY DOMAIN SERVICES</b></h2></summary>
  <br><br>
  
  In this section, we'll be installing Active Directory Domain Services (AD DS) on Windows Server 2019.<br><br>
  
  
  **Step 1: Install AD DS:**
  - Open Server Manager.
  - Click "Manage" > "Add Roles and Features."
  - Choose "Role-based or feature-based installation" and click "Next."
  - Select the local server and click "Next."
  - Check "Active Directory Domain Services" and proceed.
  - Click through until you reach the installation summary, then click "Install."<br><br>

  ![Image 2](https://imgur.com/q23hpCu.gif)
<br><br>
  
  **Step 2: Promote Server to Domain Controller:**
  - After installation, click "Promote this server to a domain controller."
  - Choose "Add a new forest" and set domain details.
    - Server: DC
    - Operation System: Windows Server 2019
    - Domain Name: Streetrack.com
  - Set a Directory Services Restore Mode (DSRM) password.
  - DNS can be left alone for automatic configuration.
  - Complete the wizard and let the server restart.<br><br>
  
  ![Image 3](https://imgur.com/q23hpCu.gif)
<br><br>
  
  Awesome! We've successfully installed and configured Active Directory Domain Services on our Windows Server 2019.
</details>

<details>
  <summary><h2><b>Section 3: CREATING USERS AND ORGANIZATIONAL UNITS (OUs)</b></h2></summary>
  <br><br>
  
  Here, we'll be exploring how to efficiently manage users by creating Organizational Units (OUs), adding users, and assigning administrative privileges.<br><br>
  
  ![Image 4](https://imgur.com/q23hpCu.gif)
<br><br>
  
  **Step 1: Create Organizational Units (OUs):**
  - Open "Active Directory Users and Computers"
  - Right-click on the domain name and choose "New" > "Organizational Unit"
  - Create 2 OUs and name them: "_ADMINS" and "_USERS" respectively<br><br>

  ![Image 5](https://imgur.com/q23hpCu.gif)
<br><br>
  
  **Step 2: Create User Account:**
  - Right-click on the "_ADMINS" OU and choose "New" > "User"
  - Enter user details:
    - First Name: Thong
    - Last Name: Huynh
    - User Logon Name: thuynh<br><br>
      
  ![Image 6](https://imgur.com/q23hpCu.gif)
<br><br>

  **Step 3: Add User to Domain Admins Group:**
  - Locate the user we just created and right-click
  - Select "Properties"
  - In the "Member Of" tab, click "Add"
  - Enter "Domain Admins" and click "Check Names"
  - Click "OK" to add the user to the "Domain Admins" group<br><br>
  
  ![Image 7](https://imgur.com/q23hpCu.gif)<br><br>
  
  ![Image 8](https://imgur.com/q23hpCu.gif)<br><br>
  
  **Step 4: Verify User and OU Creation:**
  - Refresh Active Directory by restarting and log in with new Admin User credentials to confirm User and OU Creation<br><br>
  
  ![Image 9](https://imgur.com/q23hpCu.gif)
<br><br>
  
  Yay! we've successfully created Organizational Units (OUs), added a user to the "_ADMINS" OU, and granted administrative privileges by adding our user to the "Domain Admins" group.
</details>

<details>
  <summary><h2><b>Section 4: INSTALL & CONFIGURE DHCP</b></h2></summary>
  <br><br>
  
  In this section, we'll explore the process of installing and configuring the Dynamic Host Configuration Protocol (DHCP) to automate IP address assignment within our network.
  
  **Step 1: Open Server Manager:**
  - Launch "Server Manager" on the Windows Server 2019.<br><br>
  
  ![Image 10](https://imgur.com/q23hpCu.gif)<br><br>
  
  **Step 2: Add DHCP Role:**
  - Click "Manage" > "Add Roles and Features"
  - Select "Role-based or feature-based installation" and click "Next"
  - Choose the local server(DC) and proceed
  - Check "DHCP Server" and complete the installation wizard<br><br>
  
  ![Image 11](https://imgur.com/q23hpCu.gif)<br><br>

  **Step 3: Configure DHCP:**
  - After installation, open "DHCP Manager" from "Administrative Tools"
  - Right-click on our server name and choose "Configure DHCP"
  - Follow the wizard, selecting the appropriate network connection<br><br>
  
  ![Image 12](https://imgur.com/q23hpCu.gif)<br><br>
  
  **Step 4: Create DHCP Scope:**
  - In "DHCP Manager," right-click on "IPv4" and choose "New Scope"
  - Set the scope name, IP range, subnet mask, default gateway, DNS servers, and lease duration:
    - Scope Name: 10.2.22.100-200
    - Start IP Address: 10.2.22.100
    - End IP Address: 10.2.22.200
    - Length: 24
    - Subnet Mask: 255.255.255.0
    - Default Gateway: 10.2.22.1
    - DNS: 127.0.0.1
    - Lease Duration: 8 days<br><br>
  
  ![Image 13](https://imgur.com/q23hpCu.gif)<br><br>

  **Step 5: Authorize DHCP Server:**
  - If needed, we'll right-click on the server name in "DHCP Manager" and choose "Authorize."<br><br>
  
  Great! We've successfully installed and configured DHCP, automating IP address assignment to devices within our network.
</details>

<details>
  <summary><h2><b>Section 5: INSTALL & CONFIGURE NAT</b></h2></summary>
  <br><br>
  
  In this section, we'll focus on installing and configuring Network Address Translation (NAT), a technique that enables devices within our internal network to access the external internet while using a single public IP address.<br><br>
  
  ![Image 14](https://imgur.com/q23hpCu.gif)<br><br>

  **Step 1: Open Server Manager:**
  - Launch "Server Manager" on the Windows Server 2019
  - Click "Manage" > "Add Roles and Features"
  - Select "Role-based or feature-based installation" and click "Next"
  - Choose the local server (DC) and proceed
  - Check "Remote Access" and continue
  - Check "Routing" and finish the installation wizard<br><br>

  ![Image 15](https://imgur.com/q23hpCu.gif)<br><br>

  ![Image 16](https://imgur.com/q23hpCu.gif)<br><br>
  
  **Step 2: Configure NAT:**
  - After installation, open "Routing and Remote Access" from "Administrative Tools"
  - Right-click on our server name and choose "Configure and Enable Routing and Remote Access"<br><br>

  ![Image 17](https://imgur.com/q23hpCu.gif)<br><br>
  
  - Follow the wizard, selecting "Network address translation (NAT)"
  - Select the external network interface (Internet) for public connection<br><br>
  
  ![Image 18](https://imgur.com/q23hpCu.gif)<br><br>

  - In the "NAT" section, right-click on the server name and choose "NAT" > "Enable"<br><br>
</details>

<details>
  <summary><h2><b>Section 6: JOIN DOMAIN </b></h2></summary>
  <br><br>
  
  **Step 3: Join Domain With Windows 10 VM:**<br><br>

  Here, we will run the Windows 10 VM, join the domain (Streetrack.com),  and test connectivity <br><br>
  
  ![Image 19](https://imgur.com/q23hpCu.gif)<br><br>
  
  - On the client VM (Windows 10), log in using the Domain Admin "thuynh"
  - Right-click the "Start Menu" and choose "System"<br><br>

  ![Image 20](https://imgur.com/q23hpCu.gif)<br><br>
  
  - Click on "Advanced system settings"<br><br>

  ![Image 21](https://imgur.com/q23hpCu.gif)<br><br>
    
  - Go to the "Computer Name" tab and click "Change"<br><br>
  
  ![Image 22](https://imgur.com/q23hpCu.gif)<br><br>
  
  - Change "Computer name" to "Client-1"
  - Choose "Domain" and enter our domain name "Streetrack.com"<br><br>
  
  ![Image 23](https://imgur.com/q23hpCu.gif)<br><br>
  
  - Provide the "thuynh" credentials to join the domain<br><br>
  
  ![Image 24](https://imgur.com/q23hpCu.gif)<br><br>

  - Let's go! We've joined the Domain!<br><br>
</details>

<details>
  <summary><h2><b>Section 7: TEST CONNECTIVITY </b></h2></summary>
  <br><br>

  Now, we will test and confirm the confgurations that we set, ensuring the proper DHCP assignments and being able to connect to the internet.
  
  **Step 4: Test Connectivity:**<br><br>

  - On the Windows 10 VM, open a Command Prompt
  - Use the following commands to verify network settings and connectivity:
    - Run `ipconfig` to check the assigned IP configuration
    - Run `ping www.google.com` to test internet connectivity<br><br>
  
  ![Image 25](https://imgur.com/q23hpCu.gif)<br><br>
  
  There we go! We've successfully configured Network Address Translation (NAT), joined the domain using "thuynh" credentials, and verified internet and internal network connectivity on the client VM.
</details>

<details>
  <summary><h2><b>Section 8: CREATING USERS WITH PYTHON SCRIPT</b></h2></summary>
  <br><br>
  
  In this section, we will be going through the process of creating and running a Python script that takes a text file with a list of usernames to make user creation smoother and more dynamic. This will add a layer of automation and customization to our homelab environment.<br><br>

  I've created the following files that we'll be using for this section:

  My_users_list.txt 
   - A list of over 100 names(first and last)<br><br>
  
  ![Image 26](https://imgur.com/q23hpCu.gif)<br><br>

  <details>
  <summary>Create_AD_Users.py <b>(CLICK HERE TO VIEW)</b></summary>
  
  ```python
# This will import everything from the pyad module
from pyad import *

# Here, we'llset the default connection parameters for the Active Directory server
pyad.set_defaults(ldap_server="10.2.22.1", username="thuynh@streetrack.com", password="Cyberlab123!")

# This line will create a container object for the "_USERS" Organizational Unit (OU)
ou = pyad.adcontainer.ADContainer.from_dn("OU=_USERS,DC=Streetrack,DC=com")

# This will open the my_users_list text file and read its lines into the 'lines' variable
with open('my_users_list.txt', 'r') as file:
    lines = file.readlines()

# Iterate through each line in the 'lines' list
for line in lines:
    # Here, we split the line into 'first_name' and 'last_name'
    first_name, last_name = line.strip().split()
    
    # Create a username by capitalizing the first letter of 'first_name' and making 'last_name' lowercase
    username = first_name[0].upper() + last_name.lower()
    
    try:
        # This line will create the Active Directory user with the 'username' and 'ou' specified
        user = pyad.aduser.ADUser.create(username, ou)
        
        # These updates will give the various attributes of the user
        user.update_attribute('displayName', f"{first_name} {last_name}")
        user.update_attribute('sAMAccountName', username)
        user.update_attribute('givenName', first_name)
        user.update_attribute('sn', last_name)
        
        # And now, the user's password
        password = "Cyberlab123!"
        user.set_password(password)
        
        # This line will print a success message
        print(f"User {username} created successfully.")
        
    except Exception as e:
        # This will print an error message if an exception occurs and will help with error handling. 
        print(f"Error creating user {username}: {str(e)}")
```
  </details>
  
   - A Python script to create Users from the My_users_list.txt file
   - Users will be placed in the "_USERS" OU in "Streetrack.com" Domain
   - Default password will be set to "Cyberlab123!"<br><br>
  
  ![Image 27](https://imgur.com/q23hpCu.gifNSCjdXp.png)<br><br>
  
  **Step 1: Download and Install Python:**
  - Download Python from website, right-click install file and choose "Run as Administrator"<br><br>
  
  ![Image 28](https://imgur.com/q23hpCu.gifLfjqV1i.png)<br><br>
  
  **Step 2: Install Required Dependencies:**
  - Open a Command Prompt as administrators<br><br>
  
  - Run the each of the following commands to install the necessary libraries and components:
    ```
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    python get-pip.py
    pip install pyad
    pip install pywin32
    ```

  ![Image 33](https://imgur.com/q23hpCu.gifL0A0n1e.png)<br><br>
  
  ![Image 34](https://imgur.com/q23hpCu.gif1GwzbDo.png)<br><br>
  
  ![Image 35](https://imgur.com/q23hpCu.gif9EreQX8.png)<br><br>
  
  **Step 3: Navigate to Script Directory:**
  - Navigate to the directory where the Python script and user list text file resides<br><br>

  ![Image 36](https://imgur.com/q23hpCu.gifW0aHdyI.png)<br><br>
  
  ![Image 37](https://imgur.com/q23hpCu.gifAKnhjst.png)<br><br>
  
  **Step 4: Run the Python Script:**
  - In the Command Prompt, run the script using the command:
    ```
    python create_ad_users.py
    ```
  <br><br>
  
  ![Image 38](https://imgur.com/q23hpCu.gifH8cpUUg.png)<br><br>
  
  **Step 5: Verify User Creations:**
  - In Active Directory Users and Computers, navigate to the "_USERS" OU to verify that the users created by the scripts are listed<br><br>
  
  ![Image 39](https://imgur.com/q23hpCu.gifCP0Lcax.png)<br><br>
  
  **Step 6: Test User Accounts:**
  - Log into one of the created user accounts to confirm its functionality and attributes<br><br>
  
  ![Image 40](https://imgur.com/q23hpCu.gifAaz86PX.png)<br><br>
  
  Let's go!! We now have created and ran the Python script to automate user creations in Active Directory, streamlining the process and enhancing efficiency!
</details>

<details>
  <summary><h2><b>Section 9: GROUP POLICY CONFIGURATIONS</b></h2></summary>
  <br><br>
  
  In this section, we're diving into Group Policy configurations, a powerful tool that allows us to manage various settings, security policies, and access controls across our Active Directory environment.<br><br>

  **Step 1: Access Group Policy Management:**
  - Open "Server Manager" on the Windows Server 2019.
  - Click "Tools" > "Group Policy Management."<br><br>
  
  ![Image 82](https://imgur.com/q23hpCu.gifhPri6r2.png)<br><br>
  
  **Step 2: Create a New Group Policy Object (GPO):**
  - Right-click on the "Group Policy Objects" container and select "New."
  - We're going to name the GPO "Homelab Users GPO"<br><br>
  
  ![Image 83](https://imgur.com/q23hpCu.gifgA7abT1.png)<br><br>
  
  ![Image 84](https://imgur.com/q23hpCu.gifZtkDWFo.png)<br><br>
  
  **Step 3: Edit GPO Settings:**
  - Right-click on the newly created GPO and select "Edit."<br><br>
  
  ![Image 85](https://imgur.com/q23hpCu.gifwRANEkt.png)<br><br>
  
  - After selecting "Edit," navigate to the following path within the editor:
    
    - Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy
      - Password Policy:
        - Set password complexity requirements.
        - Enable "Password must meet complexity requirements."
        - Set minimum password length to 14 characters.<br><br>
        
  ![Image 86](https://imgur.com/q23hpCu.gifo70pjTw.png)<br><br>
  
  ![Image 87](https://imgur.com/q23hpCu.gifCXQg0dV.png)<br><br>
  
   - Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy
     - Account Lockout Policy:
      - Set account lockout threshold to 3 attempts
      - Other Account Lockout Policies will be changed to suggested values <br><br>
  
  ![Image 88](https://imgur.com/q23hpCu.gifpOqc2nW.png)<br><br>

  - Computer Configuration > Administrative Templates > System 
    - Turn off forced restart. (Good Practice: Avoids unwanted restarts, preventing interruptions and data loss)<br><br>

  ![Image 89](https://imgur.com/q23hpCu.gifnnhopXN.png)<br><br>
      
  - Computer Configuration > Administrative Templates > All Settings:
    - Prohibit user installs. (Good Practice: Limits unauthorized software installation to maintain control over applications running on the network)<br><br>

  ![Image 90](https://imgur.com/q23hpCu.gifnIo4EHC.png)<br><br>
  
  - Computer Configuration > Administrative Templates > Windows Components > Store
    - Turn off the Store application. (Good Practice: Controls software sources by disabling the Microsoft Store application)<br><br>
        
  ![Image 91](https://imgur.com/q23hpCu.gifH4SJGTe.png)<br><br>

  - Computer Configuration > Administrative Templates > Windows Components > OneDrive 
    - Prevent the usage of OneDrive for file storage. (Good Practice: Enhances data control by preventing accidental or unauthorized data exposure)<br><br>
  
  ![Image 92](https://imgur.com/q23hpCu.gifoBgG0nj.png)<br><br>
    
  - User Configuration > Administrative Templates > Control Panel:
    - Prohibit access to the Control Panel (Good Practice: Prevents unauthorized system changes and helps maintain a consistent and secure enviroment)<br><br>
        
  ![Image 93](https://imgur.com/q23hpCu.gifS4bzHwt.png)<br><br>
  
  - User Configuration > Administrative Templates > System:
    - Prevent access to the command prompt (Good Practice: Reduces misuse risks by preventing users from running commmands that might cause unintended damage or securtiy breach)<br><br>
        
  ![Image 94](https://imgur.com/q23hpCu.gifBVA8llG.png)<br><br>
  
  - User Configuration > Administrative Templates > System > Removable Storage Access:
    - All Removable Storage classes: Deny all access (Good Practice: Prevents data leakage by preventing unauthorized copying or transfering sensitive data onto external devices)<br><br>
        
  ![Image 95](https://imgur.com/q23hpCu.gifQj7QsSw.png)<br><br>
        
  **Step 4: Apply GPO to "_USERS" OU:**
  - Go back to Group Policy Management
  - Right-click on the "_USERS" OU and select "Link an Existing GPO."
  - Choose the GPO we've created (Homelab Users GPO) and link it to the "_USERS" OU.<br><br>
  
  ![Image 96](https://imgur.com/q23hpCu.gifBYugf90.png)<br><br>

  ![Image 97](https://imgur.com/q23hpCu.gifSERQGPT.png)<br><br>
  
  **Step 5: Force Group Policy Update:**
  - On the client machine, open a Command Prompt as an administrator.
  - Run the command: `gpupdate /force`<br><br>
  
  ![Image 98](https://imgur.com/q23hpCu.gif8MN86eY.png)<br><br>
  
  **Step 6: Test GPO Effects:**
  - Verify that the applied GPO settings are in effect on the client machine.<br><br>
  
  ![Image 99](https://imgur.com/q23hpCu.gifJ6eEOLm.png)<br><br>

  ![Image 100](https://imgur.com/q23hpCu.gif5TfBer6.png)<br><br>
  
  Group Policy configurations offer a structured way to manage and enforce consistent settings, security policies, and access controls. By effectively using GPOs, we can enhance the security and organization of the network, creating a more efficient system.
</details>

<br><br>


## Conclusion

In this dynamic lab project, we embarked on a journey to create a virtual environment that simulates a mini corporate setup. Through the orchestration of a Windows Server 2019 Domain Controller and a Windows 10 Client using VirtualBox, we ventured into the complexities of network management and system administration.

This project allowed us to explore various aspects of network administration and system management:

- **NIC Configurations:** We configured network interfaces, establishing distinct connections for internal and external communication.
- **Installing AD DS:** Active Directory Domain Services were installed and configured, forming the backbone of our domain management.
- **Creating Users and OUs:** We learned to create organizational units, add users, and grant administrative privileges for effective user management.
- **DHCP Setup:** Dynamic Host Configuration Protocol simplified IP assignment, enabling smoother network integration.
- **RAS/NAT Configuration:** Network Address Translation empowered internal devices to access the internet using a single public IP.
- **Joining the Domain:** The Windows 10 Client was successfully joined to the domain, ensuring seamless interaction with our network.
- **User Automation:** With a Python script, we automated user creation, enhancing efficiency and customization.
- **Group Policy Configuration:** We explored Group Policy configurations, implementing security practices and access controls network-wide.

Throughout this endeavor, we've crafted a comprehensive environment that mirrors the complexities of a corporate network. By mastering these tools and techniques, we've honed our skills in network management and system administration. This lab project offers a rich platform for experimentation, learning, and refinement, providing a valuable experience for anyone aspiring to excel in the realm of IT infrastructure.





