# Updating the BIOS on Intel® Server Board M50CYP Family

> This tutorial provides step-by-step instructions to update the BIOS and firmware of the Intel® Server Board M50CYP Family using the uEFI System Update Package (SUP). Before proceeding, ensure you meet the prerequisites and follow the instructions carefully to avoid any issues during the update process.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/KmrpBfWQC9M" target="_blank">
>    <img src="https://img.youtube.com/vi/KmrpBfWQC9M/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

***

## Prerequisites
1. Hardware Requirements:
    - Intel® Server Board M50CYP Family
    - A USB flash drive (formatted to FAT32)

2. Current System Software Stack:
    - System BIOS: R01.01.0008
    - ME Firmware: 04.04.04.301
    - BMC Firmware: 2.91.8a19dcde
    - FRUSDR: 0.46
    - Pmem: 2.2.0.1553
    - CPLD: v4P9

> Ensure that your current system software stack matches these versions before proceeding. Failure to meet these requirements may result in an unsuccessful update

3. Software Downloads:
    - Download the BIOS and Firmware Update Package: [M50CYP_EFI_BIOSR01.01.0009_ME04.04.04.500_BMC2.92.19c01286_CPLD4.9_FRUSDR0.46_PMem2.2.0.1553.zip](https://www.intel.com/content/www/us/en/download/19810/intel-server-board-m50cyp-family-bios-and-firmware-update-package-for-uefi.html) from the Intel website
    - Verify the integrity of the downloaded file using the SHA256 checksum on the site

## Important Notes
- Update Order: It is recommended to first update to firmware version R01.01.0008 before proceeding to R01.01.0009
- Recovery Parameters: Use the -recovery parameter when updating certain firmware components, especially when dealing with specific System Volume Numbers (SVN)
- Downgrade Restrictions: Downgrading BIOS or BMC firmware is generally not recommended and may require special procedures, including setting the PCH or BMC SVN Bypass jumper

## Step-by-Step Instructions
1. Prepare the USB Flash Drive
    - Unzip the contents of the downloaded update package
    - Copy all files to the root directory of a USB flash drive formatted with the `FAT32` file system

2. Boot into uEFI Shell
    - Insert the USB flash drive into any available USB port on the server
    - Reboot the server and press <KBD>F2</KBD> during POST to access the BIOS Setup Utility
    - Navigate to Boot Manager and press <KBD>Enter</KBD>
    - Select uEFI Internal Shell

3. Execute the Update
    - The update process will typically start automatically by executing the Startup.nsh script located on your USB drive
    - If the Startup.nsh script does not start automatically:
        - Use the command `map -b` to list all of the drives connected to the system
        - Review the output list and locate the drive that matches the size and model of your USB disk
        - Use the command `fsx:` (replace the x with the number corresponding to your USB disk found in the `map -b` output) to access your USB drive
        - Run `ls` to display the files in the mounted drive. You should see the contents of the USB drive, including the Startup.nsh script
        - Run the command `Startup.nsh` to manually start the update process
    - The system will update the BIOS, CPLD, BMC, FRUSDR, and Pmem firmware components
    - Do not interrupt or power off the system once the update process begins. The screen will remain off, and the ID LED will turn solid blue during the update
    - The system will reboot automatically after the update is complete, which may take approximately 12 minutes
    - Remove the USB **after** the update is complete

4. Post-Update Verification
    - After the update and reboot, press <KBD>F2</KBD> during POST to access the BIOS Setup Utility
    - Verify the BIOS revision matches the updated version
    - Navigate to `SERVER MANAGEMENT > SYSTEM INFORMATION` to verify the BMC, ME, SDR, and CPLD firmware revisions
    - Alternatively, boot into the EFI shell and run `sysfwupdt.efi -i` to verify the active firmware versions

## Special Procedures
- Custom BIOS Update: If updating to a custom BIOS file (`R01010008_CAPSULE_ITK.cap`), first run the standard update procedure using Startup.nsh. After completion, flash the custom BIOS using the `UpdBIOS_CYP_CAP.nsh` script.
- Re-flashing Specific Components: After the initial update, individual components can be updated using specific scripts like `UpdBIOS_CYP.nsh`, `UpdCPLD_CYP.nsh`, etc. Ensure the system has been initially updated before using these standalone scripts.

## Warnings
- **Do Not Interrupt:** Interrupting the update process can render your system inoperable
- **Do Not Downgrade:** Avoid downgrading the system software as it may also cause system failure

## Conclusion
> Following these instructions will help ensure a successful BIOS and firmware update on the Intel® Server Board M50CYP Family. Always refer to the included release notes for detailed information on any known issues and additional guidance.

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/13/2024 | Initial release of BIOS and Firmware Update Tutorial for Intel® Server Board M50CYP Family. | Keegan Cox |


https://thetechylife.com/how-do-i-boot-from-usb-with-efi-shell/
https://www.intel.com/content/www/us/en/download/19810/intel-server-board-m50cyp-family-bios-and-firmware-update-package-for-uefi.html
https://downloadmirror.intel.com/793666/Readme%20and%20Update%20Instructions.txt
