# Instructions for Updating BIOS Firmware on Intel® Server Board S2600WF Family
## Introduction
> This tutorial provides step-by-step instructions to update the BIOS and firmware of the `Intel® Server Board S2600WF Family` using the UEFI System Update Package (SUP). The procedure described here applies to version `R02.01.0017` and will generally work for later versions. Read documentation on [Intel's site][intel] to ensure you meet the prerequisites and follow the instructions carefully to avoid any issues during the update process.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/NiNJuqm8suQ" target="_blank">
>    <img src="https://img.youtube.com/vi/NiNJuqm8suQ/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

***

## Prerequisites
1. Hardware Requirements:
    - Intel® Server Board S2600WF Family
    - A USB flash drive (formatted to FAT32)

2. Current System Software Stack:
    - System BIOS: `R02.01.0016`
    - ME Firmware: `04.01.04.804`
    - BMC Firmware: `2.88.71773d70`
    - FRUSDR: `2.04`

> Ensure that your current system software stack matches these versions before proceeding. Failure to meet these requirements may result in an unsuccessful update. Refer to Intel's site for recommended software versions for updates beyond R02.01.0017.

3. Software Downloads:
    - Download the BIOS and Firmware Update Package: [S2600WF_EFI_BIOSR02.01.0017.zip][Intel® Server Board S2600WF Intel® Download] from the Intel website.

> Verify the integrity of the downloaded file using the SHA256 checksum provided on the site.


## Important Notes:
- Do not interrupt the update process (e.g., reboot or remove power), as it may render the system inoperable.
- Do not downgrade the firmware once it has been updated.
- Ensure you have the correct SSL certificate (2048-bit or longer) starting from BMC v2.88.
- Review any warnings related to BMC firmware updates, especially those that may affect Active Directory, security settings, and SSL certificates.


## General Installation Procedure
1. Prepare the Update Package:
    - Unzip the contents of the downloaded update package.
    - Copy all files to the root directory of a USB flash drive formatted with the `FAT32` file system.
    - Insert the USB flash drive into any available USB port on the server.

> [Download BIOS and Firmware Update Package][Intel® Server Board S2600WF Intel® Download]

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

## Troubleshooting and Additional Resources
- Security and Compatibility Issues: Refer to the PDFs on Intel's site (e.g., TA-1143) for more information on ipmitool and BMC security settings.
- Firmware Downgrades: Downgrading BMC below version 1.43.660a4315 is not supported due to security changes.
- Operating System Compatibility: Refer to the respective installation guides (e.g., RHEL73_InstallationGuide_Rev1.00.pdf) for operating systems that might encounter boot issues due - to the BMC PCIe bridge being disabled.

## **Important Warnings**
- Do NOT interrupt the update process.
- Do NOT attempt to downgrade the firmware once updated.
- Always ensure that you are using compatible firmware and hardware to avoid issues.
- By following these instructions carefully, you can ensure a successful BIOS and firmware update on your Intel® Server Board S2600WF Family.

## Sources
- [Intel® Server BIOS Support Central][Intel® Server BIOS Support Central]
- [Intel® Server Board S2600WF Intel® Download][Intel® Server Board S2600WF Intel® Download]
- [Release Notes and Update Instructions][Release Notes and Update Instructions]

[Intel® Server BIOS Support Central]: https://www.intel.com/content/www/us/en/support/articles/000088822/server-products.html
[Intel® Server Board S2600WF Intel® Download]: https://www.intel.com/content/www/us/en/download/18911/intel-server-board-s2600wf-family-bios-and-firmware-update-package-for-uefi.htmlhtmlhtmlintel-server-board-s2600wf-family-bios-and-firmware-update-for-intel-one-boot-flash-update-intel-ofu-utility.html
[Release Notes and Update Instructions]: https://downloadmirror.intel.com/812650/Readme%20and%20Update%20Instructions.txt

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/13/2024 | Initial release | Keegan Cox |
| 1.1      | 08/19/2024 | Added media | Keegan Cox |
| 1.2      | 08/19/2024 | published | Keegan Cox |