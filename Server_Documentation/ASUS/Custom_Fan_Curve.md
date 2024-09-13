# Creating a Custom Fan Profile for ASUS Server Chassis via ASMB11-iKVM
> This document will guide you through the process of creating a custom fan profile using the `ASMB11-iKVM` interface on your ASUS server chassis. A custom fan profile allows you to adjust the fan curve to achieve the optimal balance between noise levels and thermal management.

## ⚠️ Important Notes:
- **Profile Application:** The custom fan profile does not apply when the server is in the Power-On Self-Test (POST) phase during boot-up. Once the system is fully operational, the fan control will switch to the custom profile.

## ‼️ Heat Warnings:
- Running your server with a fan curve that is too conservative can lead to high temperatures, **potentially causing thermal throttling or hardware damage**.
- Ensure your cooling is sufficient to avoid overheating, which could impact system performance or even lead to failure.

## Step-by-Step Instructions:
1. Set Up the ASMB11-iKVM
    - Ensure that the ASMB11-iKVM interface is connected to your server and configured correctly for remote access.

2. Log Into the Remote Management console
    - Access the ASMB11-iKVM interface through your web browser using the BMC's IP address. 
    - Enter your login credentials to access the dashboard.
![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Fan_Profile_Adjustment/Final/Login.png)

3. Navigate to Fan Control Settings
    - Once logged in, locate the navigation pane on the left-hand side of the screen.
    - Click on `Settings`.
![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Fan_Profile_Adjustment/Final/ClickOnSettings.png)
    - From the options, select the `Fan Control` tile.
![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Fan_Profile_Adjustment/Final/ClickOnFanControl.png)

4. Create a Customized Fan Profile
    - In the Fan Control section, click on the `Customized` tile to create your custom fan profile.
![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Fan_Profile_Adjustment/Final/ClickOnCustomized.png)

    - You'll now be able to adjust the fan speed based on specific temperature points.
    - Adjust the Fan Curve
    - Customize each point of the fan curve based on your server’s hardware and cooling needs. 
> Below is a recommended fan curve setup provided by Bytespeed to balance noise levels and thermal efficiency:

> Use these values as a starting point. Adjust them if necessary based on your specific server hardware and environmental conditions.
> | **Point** | **Temperature (°C)** | **Fan Duty (%)** |
> |-----------|----------------------|------------------|
> | A         | 50                   | 15               |
> | B         | 70                   | 20               |
> | C         | 75                   | 70               |
> | D         | 85                   | 100              |

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/ASUS/Fan_Profile_Adjustment/Final/SetCurveAndSave.png)

5. Save Your Changes
    - Click the save button below the custom curve. 

6. Repeat steps 4 and 5 for all curves.

> By following these steps and adjusting the fan curve appropriately, you can optimize the cooling and noise levels for your server environment. Always monitor system temperatures after making changes to ensure optimal performance.


## More Information
- [ASMB11-iKVM Server Management Board User Guide][ASMB-iKVM_reference]

[ASMB-iKVM_reference]: https://dlcdnets.asus.com/pub/ASUS/server/accessory/ASMB11/Manual/E20952_ASMB11-iKVM_UM_WEB.pdf?model=ASMB11-iKVM


## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 09/13/2024 | Initial release | Keegan Cox |
