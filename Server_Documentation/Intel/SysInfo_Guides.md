# Guide 1: Pulling Server Logs on Intel Servers Using SysInfo – UEFI Environment
## Overview
> The Intel® Server Information Retrieval Utility (SysInfo) is a tool designed to collect system information from Intel® Server Boards and Intel® Server Systems. It is compatible with the UEFI environment and supports a wide range of Intel® server products. The information collected is recorded in various log files, useful for diagnostics, troubleshooting, and system management.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/mkhUDWr5HF8" target="_blank">
>    <img src="https://img.youtube.com/vi/mkhUDWr5HF8/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

Prerequisites
- Supported Intel® Server Products: Confirm that your server is supported (e.g., Intel® Server Board S2600WT Family).
- UEFI Shell Access: Ensure the server can boot into the UEFI shell.
- Administrative Permissions: Ensure you have the necessary permissions to perform these actions.

## Installation Instructions
1. Download and Prepare:
    - [Download the SysInfo Utility:][sysinfo_download].
    - Unzip the downloaded .zip file into a folder named `sysinfo` on your USB drive (e.g., `D:\sysinfo`).

2. Prepare the Environment:
    - Restart the server and enter the Boot Manager by pressing <kbd>F6</kbd> during startup.
    - Boot into the `UEFI shell` from the Boot Manager.

3. Navigate and Run the Utility:
    - In the UEFI shell, navigate to the USB drive where you unzipped the utility. This is typically mounted as `fs0:`.
        - Use `cd` to change directories (e.g., `cd fs0:\sysinfo\UEFI_x64`).
        - Use `ls` to list files and directories.
    > **Note:** If fs0: is not the correct USB drive, run `map -b` to list connected devices.
    - Execute the utility by running the command: `sysinfo.efi`
        - You can add flags to the command as needed (refer to the command usage below).
    - The utility will collect data and save it in three log files (`sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `PCI_Log.txt`) within the `LogFiles` directory.

## Command Usage
| Name                      | Command                     | Log Files Generated                                |
|---------------------------|-----------------------------|----------------------------------------------------|
| Basic Command             | `sysinfo.efi`               | `sysinfo_log.txt`, `PCI_Log.txt`                   |
| Non-Interactive Mode      | `sysinfo.efi -ni`           | `sysinfo_log.txt`, `PCI_Log.txt`                   |
| Include RAID Information  | `sysinfo.efi -raid`         | `sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `PCI_Log.txt` |


## Removal Instructions
1. Boot the server into the UEFI shell.
2. Navigate to the directory where SysInfo was installed.
3. Delete all files and directories related to SysInfo.

## Log File Descriptions
- BMC SEL (System Event Log): Captures critical hardware events and error codes from the BMC.
- BIOS_Settings.txt: A snapshot of the current BIOS settings.
- Memory_Dump.log: Details memory usage, errors, and configuration.

## Important Notes
- Backplane Drives: SysInfo may not retrieve hard drive information if the drives are installed onto a backplane. Ensure drives are connected directly to the system board for accurate log collection.

***

# Guide 2: Pulling Server Logs on Intel Servers Using SysInfo – Windows Environment
## Overview
> The Intel® Server Information Retrieval Utility (SysInfo) is a tool designed to collect system information from Intel® Server Boards and Intel® Server Systems. It is compatible with Windows environments and supports a wide range of Intel® server products. The information collected is recorded in various log files, useful for diagnostics, troubleshooting, and system management.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/C_oZMsJncYE" target="_blank">
>    <img src="https://img.youtube.com/vi/C_oZMsJncYE/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

## Prerequisites
- **Supported Intel® Server Products:** Confirm that your server is supported (e.g., Intel® Server System M50CYP Family and S2600WT Family).
- **Operating System Compatibility:** Ensure the server is running Windows Server 2019/2022 or Windows 10/11.
- **Administrative Permissions:** Ensure you have administrative rights on the Windows system.
- **Required Drivers:** Ensure all necessary RAID drivers are installed (only if RAID logs are needed). 

## Installation Instructions
1. [Download the SysInfo Utility:][sysinfo_video]
2. Prepare the Environment:
    - Boot the server into Windows with Windows Management Instrumentation (WMI) enabled (typically enabled by default).
    - Create a local directory (e.g., `C:\sysinfo`) and unzip the downloaded .zip file into this directory.

3. Install the Driver:
    - Navigate to `C:\sysinfo\Win_x64\Drivers` and run `install.bat` to install the SMI driver.

4. Run the Utility:
- Navigate to `C:\sysinfo\Win_x64\Binaries` and run `sysinfo.exe` as an **administrator.**
    > See [Command Usage](##command-usage) below for more information on flags and which logs are generated.
- The collected data is saved in five log files (`sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `OS_Eventlog.txt`, `SATA_log.txt`, `PCI_log.txt`) in the `LogFiles` folder.

## Command Usage
| Name                       | Command                     | Log Files Generated                                                                            |
|----------------------------|-----------------------------|------------------------------------------------------------------------------------------------|
| Basic Command              | `sysinfo.exe`               | `sysinfo_log.txt`, `OS_Eventlog.txt`, `RAID_NVRAMlog.txt`                                      |
| Non-Interactive Mode       | `sysinfo.exe -ni`           | `sysinfo_log.txt`, `OS_Eventlog.txt`, `RAID_NVRAMlog.txt`                                      |
| SATA and PCI Information   | `sysinfo.exe -sata -pci`    | `sysinfo_log.txt`, `SATA_log.txt`, `PCI_log.txt`, `OS_Eventlog.txt`                            |
> **Note:** `RAID_NVRAMlog.txt` will only generate with the proper RAID drivers installed... On intel systems, it is easier to get RAID information through RAID web console 3 (RWC3).

## Log File Descriptions
- **sysinfo_log.txt:** Captures comprehensive platform and system information, including platform firmware inventory, sensor data records, BMC settings (e.g., SEL, user, LAN, SOL, power restore, and channel settings), SMBIOS types (1, 2, and 3), memory, processor, SATA, IDE/SCI, hard drive, operating system information, device manager information, BIOS settings, and the list of installed software.
- **RAID_NVRAMlog.txt:** Contains RAID settings and related RAID log data.
- **OS_Eventlog.txt:** Logs entries from the operating system's event log.
- **SATA_log.txt:** Records detailed SATA device information.
- **PCI_log.txt:** Logs information related to the PCI Bus, including details about connected PCI devices.

## Important Notes
- Driver Certification: The `memrwd.sys` driver used by SysInfo to collect PCI/SATA information is not WHQL certified, which may lead to warnings during installation.

## Removal Instructions
1. Navigate to the directory where SysInfo was installed.
2. Run `uninstall.bat` in the `Win_x64\Drivers` directory to uninstall the utility.


***

# Guide 3: Pulling Server Logs on Intel Servers Using SysInfo – Linux Environment
## Overview
> The Intel® Server Information Retrieval Utility (SysInfo) is a tool designed to collect system information from Intel® Server Boards and Intel® Server Systems. It is compatible with Linux environments and supports a wide range of Intel® server products. The information collected is recorded in various log files, useful for diagnostics, troubleshooting, and system management.

> Watch the instructional video for steps on using SysInfo in a Linux environment.

## Prerequisites
- **Supported Intel® Server Products:** Confirm that your server is supported (e.g., Intel® Server System M50CYP Family).
- **Operating System Compatibility:** Ensure the server is running a supported Linux distribution (`RHEL 8.x/9.x`, `SLES 12 SP3/15`, `Ubuntu 20.04/22.04`).
- **Root Permissions:** Ensure you have root permissions on the Linux system.
- **Required Drivers:** Ensure all necessary RAID drivers are installed.

## Installation Instructions
1. [Download the SysInfo Utility:][sysinfo_download]
2. Prepare the Environment:
- Boot the server into a supported Linux distribution (`RHEL`, `SLES`, `Ubuntu`).
- Create a directory (e.g., `/root/sysinfo`) and unzip the downloaded .zip file into this directory.

3. Install the Utility:
- Navigate to the `Linux_X64` folder.
- Run `chmod 755 *` to change the permissions of the executables.
- Run `./install.sh` to install the utility.

4. Run the Utility:
- Close the current terminal and open a new one.
- Run the utility using `./sysinfo`.
- The collected data is saved in four log files (`sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `PCI_Log.txt`, `OS_Eventlog.txt`) in the LogFiles folder.

## Command Usage
- **Basic Command:** `./sysinfo`
- **Non-Interactive Mode:** `./sysinfo -ni`
- **Include RAID Information:** `./sysinfo -raid`
- **Specify Output Directory:** `./sysinfo [Directory name]`

## Removal Instructions
- Navigate to the directory where SysInfo was installed.
- Run ./uninstall.sh to remove the utility.
- Delete the Linux_x64 directory.

## Log File Descriptions
- BMC SEL (System Event Log): Captures critical hardware events and error codes from the BMC.
- Memory_Dump.log: Details memory usage, errors, and configuration.
- PCI_Log.txt: Logs PCI device information, useful for identifying hardware issues.


## Sources
- [Intel® Server BIOS Support Central][support_central]
- [Sysinfo Video – Intel System Information Retrieval Utility][sysinfo_video]
- [User Guide for Intel System Information Retrieval Utility (Sysinfo)][sysinfo_home]
- [Server Information Retrieval Utility (SysInfo) for Intel® Server Boards and Intel® Server Systems Download][sysinfo_download]


[support_central]:https://www.intel.com/content/www/us/en/support/articles/000088822/server-products.html
[sysinfo_video]: https://www.intel.com/content/www/us/en/support/articles/000032842/server-products.html
[sysinfo_home]: https://www.intel.com/content/www/us/en/support/articles/000023940/server-products/server-boards.html
[sysinfo_download]: https://www.intel.com/content/www/us/en/download/765096/server-information-retrieval-utility-sysinfo-for-intel-server-boards-and-intel-server-systems.html?wapkw=%20Intel%20System%20Information%20Retrieval%20Utility%20(Sysinfo)

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/19/2024 | Initial release | Keegan Cox |
| 1.1      | 08/19/2024 | Revisions | Keegan Cox |
