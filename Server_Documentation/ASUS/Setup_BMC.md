# Setting Up the Baseboard Management Controller (BMC) on ASUS 1U and 2U servers
> This article provides a step-by-step guide to set up the Baseboard Management Controller (BMC) on ASUS server motherboards and configure the iKVM (Keyboard, Video, Mouse) to be accessible over the network. It includes prerequisites, configuration steps, and important security notes for a secure setup.

***

## Prerequisites
> Before configuring the BMC and accessing the iKVM, ensure the following:
1. Hardware Requirements:
    - ASUS server with the BMC pre-installed.
    - A network cable for connecting the BMC.

2. Software Requirements:
    - Compatible web browser: Firefox, Chrome, Edge, or Safari.

***

## Important Notes ⚠️
- ‼️ **Security:** After the initial login, it is critical to change the default passwords for the admin and Administrator accounts.
- **IP Configuration:** For ease of management, consider assigning a static IP address to the BMC.
- **Network Ports:** Ensure your network firewall allows the following ports to enable BMC functionality:
    - Port 623 (IPMI)
    - Port 443 (HTTPS)
    - Port 161 (SNMP) (Optional)
- **Firmware Update:** Ensure the BMC firmware is up to date by checking the BMC web interface for updates. 

***

## Step-by-Step Guide
### Step 1: Connect the Network Cable
1. Attach the Network Cable
    - Connect the network cable to the Dedicated Management Port or the Shared Ethernet Port on the server.
    - Ensure the other end of the cable is connected to your network, either directly or through a network switch/router.
    

    *ASUS 2U Server:*

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/2U_Ports.png)

### Step 2: Configure BMC Network Settings in the BIOS
1. Enter the BIOS
    - Connect a monitor and keyboard to the server
    - Power cycle the server
    - During post rappidly press <KBD>Delete<KBD> to enter BIOS

2. Enter BMC network Configuratoin Settings
    - Navigate to the `Server MGMT` tab 
    - Press <KBD>Enter</KBD> on `BMC Network Configuration`

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/1-ServerMGMT_BMC_Network_Config.png)

3. (Option 1) Dedicated Management LAN Configuration (DM_LAN):
    > This configuration enables remote management over the `dedicated management port (DM_LAN)`.
    > It provides dedicated lights out management but does not offer a redundant failover path.

    Steps:
    - Set `Configuratoin Address Source` to `Static` 
    - Enter your network information under `DM_LAN` configuration:
        - Set a static or dynamic IPv4 address (Static is recommended for most applications).
        - Enter the subnet mask.
        - Enter the gateway.
    - If not already done, plug an Ethernet cable into the `DM_LAN (Direct Management) port` of the server (see image above).
        - The management port is labeled "MGMT" next to the port.

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/2-1-DM_LAN.png)

4. (Option 2) Shared LAN Configuration:
    > Enables remote management over the onboard Ethernet NICs that shares the port with other host traffic.
    > This configuration offers greater redundancy because the host can fail over between the onboard Ethernet NICs; however, host traffic can bottleneck remote management traffic, potentially causing a denial of service to the remote management console.

    Steps:
    - Set `Configuratoin Address Source` to `Static` 
    - Enter your network information under `Shared LAN` configuration:
        - Set a static or dynamic IPv4 address (Static is recommended for most applications).
        - Enter the subnet mask.
        - Enter the gateway.
        - This will enable remote management over the Shared LAN Ethernet NICs, which handle both host and management traffic.
    - If not already done, plug an Ethernet cable into the `Shared LAN port` of the server (see image above).
        - The Shared LAN is one of the onboard Ethernet NICs that are not labled MGMT or Console

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/2-2-Shared_LAN.png)

5. (Option 3) Shared LAN or DM_LAN over IPv6
    > Disable IPv6 if it is not needed
    
    Steps:
    - Below the IPv4 settings, navigate to the respective port (DM_LAN or Shared LAN) and `Enable IPv6 Support`
    - Set `Configuration Address Source` to `Static` 
    - Enter your network information for the respective interface

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/3-Enable_IPV6.png)

6. Save and Exit BIOS
    - Press <KBD>f10</KBD> to save changes and exit. 
    - Confirm if necessary

### Step 3: Access ASMB11-iKVM via Web Browser
1. Open the Web Browser:
    - On a device connected to the same network, open a web browser and enter the IP address you configured in the BIOS settings.

2. Login to the BMC Interface:
    - Use one of the following default credentials:
        > Usernames are case sensitive

        | **Username**  | **Password** |
        |---------------|-------------|
        | admin         | admin       |
        | Administrator | superuser   |

    - After the first login, you will be prompted to change the password for security purposes.
        > ‼️ Remember to change the default password for both default users...

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/4-Login.png)

### Step 4: Create User Accounts
1. Navigate to User Management:
    - After logging in, on the left hand pane, navigate to Settings

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/5-ClickOnSettings.png)

    - Click on the `User Management` tile

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/6-ClickOnUserManagement.png)

2. Create New User Accounts:
    - Click on the User tile you want to edit.

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/6-ClickOnUserManagement.png)

    - Add new user accounts as needed.
    - Usernames are case sensitive 
    - Assign appropriate roles and permissions for each user.

    ![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Setup_BMC/8-SetAndSaveSettingsForTheUSer.png)


## ‼️ Change the default password of all default accounts.

## More Information
- [ASMB11-iKVM Server Management Board User Guide][ASMB-iKVM_reference]

[ASMB-iKVM_reference]: https://dlcdnets.asus.com/pub/ASUS/server/accessory/ASMB11/Manual/E20952_ASMB11-iKVM_UM_WEB.pdf?model=ASMB11-iKVM

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 09/13/2024 | Initial release | Keegan Cox |