# Instructions for Updating BIOS Firmware on Intel® Server Board S2600WF Family
## Introduction
This guide will walk you through updating the BIOS and firmware for Intel® Server Board S2600WF Family using the UEFI System Update Package (SUP). Please ensure that you meet all prerequisites before proceeding.

## Prerequisites
1. Current Firmware Versions:
    - System BIOS: R02.01.0016 or later
    - ME Firmware: 04.01.04.804 or later
    - BMC Firmware: 2.88.71773d70 or later
    - FRUSDR: 2.04 or later


2. Supported Products:
    - Intel® Server Board S2600WF Family
    - Intel® Server System R1000WF Family
    - Intel® Server System R2000WF Family


3. Important Notes:
    - Do not interrupt the update process (e.g., reboot or remove power), as it may render the system inoperable.
    - Do not downgrade the firmware once it has been updated.
    - Ensure you have the correct SSL certificate (2048-bit or longer) starting from BMC v2.88.
    - Review any warnings related to BMC firmware updates, especially those that may affect Active Directory, security settings, and SSL certificates.


## General Installation Procedure
1. Prepare the Update Package:
    - Download the UEFI System Update Package (SUP).
    - Unzip the contents of the package.
    - Copy all files to the root directory of a USB flash drive.


2. Update the Firmware:
    - Insert the USB flash drive into any available USB port on the server.
    - Power on the server and access the UEFI shell.
    - Navigate to the USB flash drive in the UEFI shell.
    - Run `Startup.nsh` to begin the update process.
    - The system will reboot automatically after the update is completed.


3. Additional Steps for Intel® Optane™ DC Persistent Memory (PMEM):
    - If PMEM is installed, run `Startup.nsh` a second time after the first reboot to update the PMEM firmware.
    - Power cycle the system to load the new PMEM firmware.


4. Verify the Update:
    - Reboot the system after the update.
    - During POST, press <KBD>F2</KBD> to access the BIOS Setup Utility.
    - Press <KBD>F9</KBD> to load BIOS defaults and <KBD>F10</KBD> to save changes.
    - Verify the BIOS, BMC, FRUSDR, and ME firmware revisions are correct.
    - Configure desired BIOS settings and save changes by pressing <KBD>F10</KBD>.


5. Final Notes:
    - The system may reboot multiple times during the update process. This is normal.
    - After the initial BIOS update, a backup BIOS image will be installed. Do not power off the system during this process.
    - If the system doesn't boot after a downgrade using the recovery jumper, reset the BIOS settings by temporarily moving the BIOS default jumper to the "clear" position.


## Troubleshooting and Additional Resources
- Security and Compatibility Issues: Refer to the included PDFs (e.g., TA-1143) for more information on ipmitool and BMC security settings.
- Firmware Downgrades: Downgrading BMC below version 1.43.660a4315 is not supported due to security changes.
- Operating System Compatibility: Refer to the respective installation guides (e.g., RHEL73_InstallationGuide_Rev1.00.pdf) for operating systems that might encounter boot issues due - to the BMC PCIe bridge being disabled.

## **Important Warnings**
- Do NOT interrupt the update process.
- Do NOT attempt to downgrade the firmware once updated.
- Always ensure that you are using compatible firmware and hardware to avoid issues.
- By following these instructions carefully, you can ensure a successful BIOS and firmware update on your Intel® Server Board S2600WF Family.

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/13/2024 | Initial release of BIOS and Firmware Update Tutorial for Intel® Server Board S2600WF Family. | Keegan Cox |