# Setting Up the BMC
> This guide will walk you through setting up the Baseboard Management Controller (BMC) on your server.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/o4y_G4bLZgs" target="_blank">
>    <img src="https://img.youtube.com/vi/o4y_G4bLZgs/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

***

## Prerequisites
> Before you begin, ensure you have the following:

- **Physical Access to the Server:** You will need to connect peripherals (mouse, keyboard, monitor) to the server and access the physical ports.
- **Network Information:** Have the **IP address**, **subnet mask**, and **gateway** information ready if you plan to use static IP configuration.
- **Admin Privileges:** You should have administrative privileges to make changes to the server’s UEFI settings.
- **Ethernet Cable:** Ensure you have an Ethernet cable to connect the server to your network via the management port.
- **Web Browser:** Access to a web browser on a device connected to the **same network as the server** for final BMC access.

## 1. Initial Setup
1. Connect Hardware:
    - Plug in a mouse, keyboard, and monitor to your server.
2. Restart the Server:
    - Power on or restart the server.
    - During boot, rapidly press <KBD>F2</KBD> to enter the System Setup.

## 2. Entering UEFI and Navigating
1. Access UEFI:
    - Once in UEFI, use the arrow keys to navigate
2. Navigate to Server Management and press <KBD>Enter</KBD>

3. Configure BMC LAN:
    - Navigate to the bottom of the page to `BMC LAN Configuration` and press <KBD>Enter</KBD>


## 3. Configuring BMC Network Settings
1. Dedicated Management LAN Configuration:
    - Enter your network information under `Dedicated Management LAN Configuration`:
        - Set a static or dynamic IPv4 address (Static is recommended for most applications)
        - Enter the subnet mask
        - Enter the gateway
        > Record network information for later use
    - Plug an Ethernet cable into the management port of the server
        - There is a mgmt label next to the port

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/BMC_Management_Port.png)

2. (Optional) Baseboard LAN Configuration:
    - If desired, navigate to Baseboard LAN Configuration to set up another network address
    - This will enable remote management over the onboard Ethernet NIC


## 4. User Configuration
1. At the top of the page, navigate to User Configuration and press <KBD>Enter</KBD>:

2. Set Privileges for User2:
    - Under User2, set the privilege to the desired level (`User`, `Operator`, `Administrator`, `No Access`).
    - Change the user status to `Enabled`
    - Set a username and a secure password
    > **Note:** You can `enable` complex passwords under `User Configuration > Enable Complex Password`. Once enabled, the password complexity criteria will be displayed on the right-hand side of the screen.

3. (Optional) Set Up Additional Users:
    - If needed, set up additional users with desired privileges


## 5. Finalizing and Accessing BMC
1. Save and Exit:
    - Press <KBD>F10</KBD> to save changes and exit the setup

2. Access the BMC:
    - Ensure the management port is connected to your network via Ethernet
    - Open a web browser from a machine connected to the same network as the `Dedicated Management LAN Configuration IP` address you set in step [3.1](#3-configuring-bmc-network-settings)
    - Navigate to the IP address you set during configuration  (Eg. `https://192.168.15.5` )
    - Enter the username and password you created to access the BMC and manage your system remotely