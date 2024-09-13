# Setting Up the Baseboard Management Controller (BMC) on ASUS 1U and 2U servers
> This article provides a step-by-step guide to set up the Baseboard Management Controller (BMC) on ASUS server motherboards and configure the iKVM (Keyboard, Video, Mouse) to be accessible over the network. It includes prerequisites, configuration steps, and important security notes for a secure setup.

## Prerequisites
> Before configuring the BMC and accessing the iKVM, ensure the following:
1. Hardware Requirements:
    - ASUS server with the BMC pre-installed.
    - A network cable for connecting the BMC.

2. Software Requirements:
    - Compatible web browser: Firefox, Chrome, Edge, or Safari.

3. NOTE TO CHECK IF THE SERVER SUPPORTS THE BMC THERE IS A LINK SOMEWHERE IN THE MANUAL WITH MORE INFO :bangbang:


## Step-by-Step Guide
### Step 1: Connect the Network Cable
1. Attach the Network Cable
    - Connect the network cable to the Dedicated Management Port or the Shared Ethernet Port on the server.
    - Ensure the other end of the cable is connected to your network, either directly or through a network switch/router.

![](image of back of 1U and 2U ASUS servers)

### Step 2: Configure BIOS Settings
1. Enter BIOS Setup:
    - Restart the server and press <Del> during POST to enter the BIOS setup.
2. Access the BMC Network Configuration:
    - Navigate to Server Mgmt > BMC network configuration.
3. Set IP Configuration:
    - Choose IPv4 or IPv6 based on your network:
        - For IPv4:
            - Set Configuration Address source to [Static].
            - Enter the Station IP Address and Subnet Mask.
        - For IPv6:
            - Enable IPv6 Support, then configure the Station IP Address and Prefix Length.
4. Save and Exit:
    - Press <KBD>F10</KBD> to save changes and exit the BIOS.

### Step 3: Access ASMB11-iKVM via Web Browser
1. Open the Web Browser:
    - On a device connected to the same network, open a web browser and enter the IP address you configured in the BIOS settings.

2. Login to the BMC Interface:
    - Use one of the following default credentials:
        | **Username**  | **Password** |
        |---------------|-------------|
        | admin         | admin       |
        | Administrator | superuser   |

    - After the first login, you will be prompted to change the password for security purposes.

### Step 4: Create User Accounts
1. Navigate to User Management:
    - After logging in, on the left had pane navigate to Settings
    - Click on the `User Management` tile

2. Create New User Accounts:
    - Add new user accounts as needed.
    - Usernames are case sensitive 
    - Assign appropriate roles and permissions for each user.


## Important Notes
- **Security:** After the initial login, it is critical to change the default passwords for the admin and Administrator accounts.
- **IP Configuration:** For ease of management, consider assigning a static IP address to the BMC.
- **Network Ports:** Ensure your network firewall allows the following ports to enable BMC functionality:
    - Port 623 (IPMI)
    - Port 443 (HTTPS)
    - Port 161 (SNMP) (Optional)




















Initial Setup:

Ensure the server system is powered off before handling any components to prevent damage.
Verify that the latest firmware and BIOS versions are installed on the server.
Step-by-Step Guide
Step 1: Install the BMC and Network Setup
Power Down:

Unplug the server from the power source.
BMC Hardware Installation:

Insert the LAN cable into the server’s LAN port designated for server management (DM_LAN1 or Shared LAN).
Connect the other end of the cable to a router or network hub for internet access.
Power On:

Once connected, power on the system. It may take up to 120 seconds for the system to fully initialize.
Step 2: Firmware Update and BIOS Configuration
Firmware Update:

To update the BMC firmware on Linux or Windows, use the provided update script (FWUpdate_Linux.sh or FWUpdate_Win.bat) from the tools folder on the installation media:
Remote firmware update: ./FWUpdate_Linux.sh [IP address] [username] [password].
For local updates: ./FWUpdate_Linux.sh -local [username] [password].
BIOS Configuration:

Restart the server and press <Del> during POST to enter the BIOS setup.
Navigate to Server Mgmt > BMC network configuration.
Set the configuration for IPv4 or IPv6 based on your network setup:
For IPv4:
Set Configuration Address source to [Static].
Configure the Station IP address and Subnet mask.
For IPv6:
Enable IPv6 support and configure the station IP address and prefix length.
Save and Exit:

Press <F10> to save changes and exit the BIOS.
Step 3: Web-based iKVM Setup and Access
Accessing the iKVM:

Ensure your remote console (PC) is connected to the same network as the server.
Open a web browser and enter the IP address assigned to the BMC during the BIOS configuration.
Login:

Use either of the following credentials:
Username: admin | Password: admin
Username: Administrator | Password: superuser
After the first login, you will be prompted to change the password for security purposes.
Launching iKVM:

Navigate to the Remote Control section in the web interface.
Click on Launch H5Viewer to access the iKVM console.
Disable any pop-up blockers in your browser, and ensure that Java Runtime Environment (JRE) is installed for full functionality.
Step 4: BMC Network and Security Settings
Network Configuration:

For security, it is advised to use a static IP address for the BMC.
Configure firewall settings to allow necessary ports for remote access:
Ports to allow:
623 (IPMI)
443 (HTTPS, iKVM, Virtual Media)
161 (SNMP)
SSL and Firewall Configuration:

Enable SSL for secure connections by navigating to Settings > SSL Settings.
Optionally, configure the system firewall to restrict access based on IP or port under System Firewall.
Important Notes
Security: Ensure that both the default admin and Administrator accounts are changed to secure passwords upon initial login.
Java Runtime Environment (JRE): Make sure JRE is installed on the remote console to enable features like JViewer.
Pop-up Blockers: Disable pop-up blockers to allow the iKVM session to launch successfully.
Firmware Compatibility: Always ensure the firmware on the BMC is up to date to avoid compatibility issues.
Conclusion
Setting up the BMC and configuring remote access to the iKVM is essential for effective server management over the internet. Follow the steps carefully and ensure that security measures are implemented to protect the system from unauthorized access.

For more details or troubleshooting, refer to the official ASUS ASMB11-iKVM user guide.