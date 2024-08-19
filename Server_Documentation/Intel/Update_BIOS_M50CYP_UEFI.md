# Updating the BIOS on Intel® Server Board M50CYP Family

> This tutorial provides step-by-step instructions to update the BIOS and firmware of the `Intel® Server Board M50CYP Family` using the uEFI System Update Package (SUP). The procedure described here applies to version `R01.01.0009` and will generally work for later versions. Read documentation on [Intel's site][intel] to ensure you meet the prerequisites and follow the instructions carefully to avoid any issues during the update process.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/NiNJuqm8suQ" target="_blank">
>    <img src="https://img.youtube.com/vi/NiNJuqm8suQ/0.jpg" alt="Watch the video on YouTube">
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

> Ensure that your current system software stack matches these versions before proceeding. Failure to meet these requirements may result in an unsuccessful update. Refer to [Intel's site][intel] for recommended software versions for updates beyond `R01.01.0009`

3. Software Downloads:
    - Download the BIOS and Firmware Update Package: [M50CYP_EFI_BIOSR01.01.0009_X.zip][intel] from the Intel website
> Verify the integrity of the downloaded file using the SHA256 checksum on the site

## Important Notes
- Update Order: It is recommended to first update to firmware version `R01.01.0008` before proceeding to `R01.01.0009`
- Recovery Parameters: Use the `-recovery` parameter when updating certain firmware components, especially when dealing with specific System Volume Numbers (SVN)
- Downgrade Restrictions: Downgrading BIOS or BMC firmware is generally not recommended and may require special procedures, including setting the PCH or BMC SVN Bypass jumper

## Step-by-Step Instructions
1. Prepare the USB Flash Drive
    - Unzip the contents of the downloaded update package
    - Copy all files to the root directory of a USB flash drive formatted with the `FAT32` file system
    - Insert the USB flash drive into any available USB port on the server

> [Download BIOS and Firmware Update Package][intel]

2. Boot into UEFI Shell
    - Reboot the server and rapidly pressing <KBD>F6</KBD> during POST to access the Boot Menu
    - Select UEFI Internal Shell
> Alternatively, enter the Boot Menu through the BIOS by rapidly pressing <KBD>F6</KBD> during POST. Then select Boot Manager.

3. Execute the Update
    - The update process will typically start automatically by executing the Startup.nsh script located on your USB drive
    > - If the Startup.nsh script does not start automatically: [Source][efi-shell]
    >    - Use the command `map -b` to list all of the drives connected to the system
    >    - Review the output list and locate the drive that matches the size and model of your USB disk
    >    - For servers running Windows, type `fs0:` at the prompt. For VMWare/ESXi servers, select the removable media device (e.g., `blk1:`)
    >    - Run `ls` to display the files in the mounted drive. You should see the contents of the USB drive, including the `Startup.nsh` script
    >    - Run the command `Startup.nsh` to manually start the update process
    - The update process will begin automatically. 
    - Partway through, you will be prompted to select an option (1-5). Choose <KBD>3</KBD>, then press <KBD>N</KBD> for the following questions
    - **Do not interrupt or power off the system once the update process begins.** The screen will remain off, and the ID LED will turn solid blue during the update
    - The system will reboot automatically after the update is complete, which may take approximately 12 minutes
    - Remove the USB **after** the update is complete

4. Post-Update Verification
    - After the update and reboot, press <KBD>F2</KBD> during POST to access the BIOS Setup Utility
    - Verify the BIOS revision matches the updated version
    - Navigate to `SERVER MANAGEMENT > SYSTEM INFORMATION` to verify the BMC, ME, SDR, and CPLD firmware revisions

> Alternatively:
> - View version numbers through the `Integrated BMC Web Console` if you set up the BMC
> - Boot into the EFI shell and run `sysfwupdt.efi -i` to verify the active firmware versions

## Special Procedures
- Custom BIOS Update: If updating to a custom BIOS file (`R01010008_CAPSULE_ITK.cap`), first run the standard update procedure using Startup.nsh. After completion, flash the custom BIOS using the `UpdBIOS_CYP_CAP.nsh` script.
- Re-flashing Specific Components: After the initial update, individual components can be updated using specific scripts like `UpdBIOS_CYP.nsh`, `UpdCPLD_CYP.nsh`, etc. Ensure the system has been initially updated before using these standalone scripts.

## Warnings
- **Do Not Interrupt:** Interrupting the update process can render your system inoperable
- **Do Not Downgrade:** Avoid downgrading the system software as it may also cause system failure

> Following these instructions will help ensure a successful BIOS and firmware update on the Intel® Server Board M50CYP Family. Always refer to the included release notes for detailed information on any known issues and additional guidance.

## Sources
- [Intel Download Center][intel]
- [BIOS and Firmware Update Instructions][intel-instructions]
- [EFI Shell USB Boot Guide][efi-shell]

[intel]: https://www.intel.com/content/www/us/en/download/19810/intel-server-board-m50cyp-family-bios-and-firmware-update-package-for-uefi.html
[intel-instructions]: https://downloadmirror.intel.com/793666/Readme%20and%20Update%20Instructions.txt
[efi-shell]: https://thetechylife.com/how-do-i-boot-from-usb-with-efi-shell/



## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/13/2024 | Initial release | Keegan Cox |
| 1.1      | 08/14/2024 | Added media and proofed process | Keegan Cox |
| 1.2      | 08/14/2024 | Revised process accounting for SDR and FRU update | Keegan Cox |
| 1.3      | 08/16/2024 | Updated instructions for specific OS and added details | Keegan Cox |
