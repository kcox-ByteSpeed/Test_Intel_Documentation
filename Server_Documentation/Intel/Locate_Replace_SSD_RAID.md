#Locating and Replacing an SSD in an Intel RAID Array Using RAID Web Console 3

## Prerequisites 
- Ensure you have administrative access to the RAID Web Console 3. 
    - Download Link: [RWC3 Download](https://webdrivers.blob.core.windows.net/drivers/server/Intel/RWC3_Win_v007.017.011.000.zip) 
- Backup all important data before proceeding. 
- Have a compatible replacement SSD ready. 
    - Always ensure that the replacement SSD has the same or higher capacity as the one being replaced. 

***

## Steps 

### Install RAID Web Console 3 (RWC3)
1. Unzip the folder
2. Run the installer
    - For connecting to a local RAID card, install the standalone version
    - For connecting to a remote RAID card, install the gateway version

### Accessing the RAID Web Console 3 
1. Open the RAID Web Console 3 (RWC3) application.
2. Log in with your administrative credentials.

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/1.png)

### Disabling The Alarm
1. On the home page in the controller information section, uncheck the `Alarm checkbox`.
    - Unchecked means the alarm is disabled
    - Checked means the alarm is enabled

**Note: Ensure the alarm is enabled when the issue is resolved**

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/RAID_Alarm.png)

### Identifying the Degraded Virtual Drive 
1. Click on the + icon to view critical issues. 
2. Identify the virtual drive in a degraded state, indicated by a red warning banner.

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/2.png)

### Navigating to the Drive Group 
1. Click on the RAID button. 

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/3_1.png)

2. Select Go Back to Drive Group, Drives, and Other Hardware List

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/3_2.png)

3. Click on the Drive Groups tab. 
4. Expand the degraded drive group indicated by the red X

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/3_3.png)

### Locating The Faulty SSD
1. Click on Physical Drives to see a list of physical drives. 
2. Select the degraded drive. 
3. On the left, click Start Locating

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/4.png)

4. Look for the orange LED indicator on the physical server chassis to locate the faulty SSD.

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/4_4.png)

### Replacing the Faulty SSD
1. Remove the faulty SSD from its slot. It is critical you remove the correct drive. 
2. Insert the new SSD into the same slot.
    - Wait for the RWC3 page to reload (this may take several minutes)

### Configuring the New SSD
1. Click on the Drives tab. 
2. Expand the Unconfigured Drive section.
3. Select the unconfigured drive and click Make Unconfigured Good.
    - Confirm if necessary.
    - Wait for the page to reload.

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/6_1.png)

4. Expand the Foreign Drives section. 
5. Select the new drive (clear the drive if necessary). 
6. Click Replace Missing Drive

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/6_4.png)

7. Ensure the drive is assigned to the correct drive group 
8. Confirm

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/6_7.png)

### Rebuilding the RAID Array
1. Go to the Drive Groups tab and expand the drive group. 
2. Click on Physical Devices and select the new drive (it should be marked). 
3. Click Start Rebuild

**Note: The Symbol by the drive will change from red to yellow after you start the rebuild process.**

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/7_1.png)

4. Check The Drive's Status
    1. Select the new drive in the drive group (See steps 1-3 above)
    2. Click on the ellipses on the left-hand side of the page ...
    3. In the pop-up window, ensure the `Status` says `Rebuilding`

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/7_4.png)

5. Monitor the rebuild process, which may take some time depending on the size of the disk and type of RAID.
    1. On the home page, expand the `Background Processes in Progress` section.
    2. A progress bar will appear with an estimate of the rebuild time. 

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/Monitor_Raid_Rebuild.png)

### Verifying the Rebuild

**Note: The yellow symbol next to the new drive should disappear when the rebuild finishes.**

1. Go back to the drive group and select the new drive as you did in the previous section
2. Click on the ellipsis (…) to display more information. 
3. Ensure the `Status` is `Online`. 
4. Verify there are no other `Critical Issues` with the RAID card by returning to the home page and looking for red error indicators

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/8_1.png)

### Enabling The Alarm

**Do not forget to do this!**

1. On the home page in the controller information section, check the `Alarm checkbox`.
    - Unchecked means the alarm is disabled
    - Checked means the alarm is enabled

![](https://github.com/kcox-ByteSpeed/Test_Intel_Documentation/blob/main/Images/RAID_Alarm.png)

***