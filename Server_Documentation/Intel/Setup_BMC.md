# Setting Up the BMC
> This guide will walk you through setting up the Baseboard Management Controller (BMC) on your server.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/o4y_G4bLZgs" target="_blank">
>    <img src="https://img.youtube.com/vi/o4y_G4bLZgs/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

***


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
    - Plug an Ethernet cable into the management port of the server

2. (Optional) Baseboard LAN Configuration:
    - If desired, navigate to Baseboard LAN Configuration to set up another network address
    - This will enable remote management over the onboard Ethernet NIC


## 4. User Configuration
1. At the top of the page, navigate to `User Configuration` and press <KBD>Enter</KBD>:

2. Set Privileges for User2:
    - Under User2, set the privilege to the desired level (`User`, `Operator`, `Administrator`, `No Access`)
    - Change the user status to `Enabled`
    - Set a `username` and a secure `password`

3. (Optional) Set Up Additional Users:
    - If needed, set up additional users with desired privileges


## 5. Finalizing and Accessing BMC
1. Save and Exit:
    - Press <KBD>F10</KBD> to save changes and exit the setup.

2. Access the BMC:
    - Ensure the management port is connected to your network via Ethernet.
    - Open a web browser and navigate to the IP address you set during configuration.
    - Enter the username and password you created to access the BMC and manage your system remotely.