# Pulling Server Logs on Intel Servers Using SysInfo

## Overview
> The Intel® Server Information Retrieval Utility (SysInfo) is a tool designed to collect system information from Intel® Server Boards and Intel® Server Systems. This utility is compatible with `UEFI`, `Windows`, and `Linux` environments and supports a wide range of Intel® server products. The information collected by SysInfo is recorded in various log files, which can be used for diagnostics, troubleshooting, and system management.
a
> Here is a video from Intel featuring the steps outlined below. [Click here][sysinfo_video]


***

## Prerequisites
> Before installing and using the SysInfo utility, ensure the following prerequisites are met:

1. Supported Intel® Server Products: Verify that the server is listed among the supported products (e.g., Intel® Server Board `S2600WT` Family, Intel® Server System `M50CYP` Family, etc.).

2. Operating System Compatibility: Ensure the server is running a supported operating system:
    - UEFI shell
    - Windows Server 2019/2022 or Windows 10
    - Red Hat Enterprise Linux (RHEL) 8.x/9.x (64-bit)
    - SUSE Linux Enterprise Server (SLES) 12 SP3/15 (64-bit)
    - Ubuntu 20.04/22.04

3. Administrative or Root Permissions: Administrative rights are required on Windows systems, and root permissions are required on Linux systems.
4. Required Drivers: For RAID information collection, ensure all necessary RAID drivers are installed on the server.

## Installation Instructions
1. **UEFI Environment**
    - Download the SysInfo Utility:
    - Prepare the Environment:
        - Boot the server into the UEFI shell. **Note: press <kbd>f6</kbd> for the `boot manager`**
        - Create a directory (e.g., `fs0:\sysinfo`).
        - Copy the [downloaded .zip][sysinfo_download] file to the directory and unzip it.

    - Run the Utility:
        - Navigate to the UEFI folder within the unzipped directory.
        - Execute the command `sysinfo.efi` to start the utility.
        - The collected data is saved in three log files (`sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `PCI_Log.txt`) in the LogFiles directory.

2. **Windows Environment**
    - [Download the Utility][sysinfo_download]
    - Prepare the Environment:
        - Boot the server into Windows with Windows Management Instrumentation (WMI) enabled.
        - Create a local directory (e.g., `C:\sysinfo`) and unzip the downloaded `.zip` file into this directory.

    - Install the Driver
        - Navigate to `Win_x64\Drivers` and run install.bat to install the SMI driver.

    - Run the Utility:
        - Navigate to `Win_x64\Binaries` and run `sysinfo.exe` as an administrator.
        - The collected data is saved in five log files (`sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `OS_Eventlog.txt`, `SATA_log.txt`, `PCI_log.txt`) in the LogFiles folder.

3. **Linux Environment**
    - [Download the Utility][sysinfo_download]
    - Prepare the Environment:
        - Boot the server into a supported Linux distribution (`RHEL`, `SLES`, `Ubuntu`).
        - Create a directory (e.g., `/root/sysinfo`) and unzip the downloaded `.zip` file into this directory.

    - Install the Utility:
        - Navigate to the `Linux_X64` folder.
        - Run `chmod 755 *` to change the permissions of the executables.
        - Run `./install.sh` to install the utility.

    - Run the Utility:
        - Close the current terminal and open a new one.
        - Run the utility using `./sysinfo`.
        - The collected data is saved in four log files (`sysinfo_log.txt`, `RAID_NVRAMlog.txt`, `PCI_Log.txt`, `OS_Eventlog.txt`) in the LogFiles folder.

## Command Usage
1. **UEFI Command Usage**
    - Basic Command: `sysinfo.efi`
    - Non-Interactive Mode: `sysinfo.efi -ni`
    - Include RAID Information: `sysinfo.efi -raid`

2. **Windows Command Usage**
    - Basic Command: `sysinfo.exe`
    - Non-Interactive Mode: `sysinfo.exe -ni`
    - SATA and PCI Information: `sysinfo.exe -sata -pci`

3. **Linux Command Usage**
    - Basic Command: `./sysinfo`
    - Non-Interactive Mode: `./sysinfo -ni`
    - Include RAID Information: `./sysinfo -raid`
    - Specify Output Directory: `./sysinfo [Directory name]`

## Removal Instructions
1. **UEFI Environment**
    - Boot the server into the UEFI shell.
    - Navigate to the directory where SysInfo was installed.
    - Delete all files and directories related to SysInfo.

2. **Windows Environment**
    - Navigate to the directory where SysInfo was installed.
    - Run `uninstall.bat` in the `Win_x64\Drivers` directory to uninstall the utility.

3. **Linux Environment**
    - Navigate to the directory where SysInfo was installed.
    - Run `./uninstall.sh` to remove the utility.
    - Delete the `Linux_x64` directory.

## Log File Descriptions
- **BMC SEL (System Event Log):** Captures critical hardware events, error codes, and system status messages from the Baseboard Management Controller (BMC). Presented as Hexadecimal or human-readable text. 
- **BIOS_Settings.txt:** Contains a snapshot of the current BIOS settings, which can be useful for diagnosing configuration-related issues.
- **Memory_Dump.log:** Provides details on memory usage, errors, and configuration.
- **Device_Manager_Log.txt:** Logs all detected hardware devices and their driver statuses, helping to identify any hardware compatibility issues.
- **Network_Configuration.txt:** Documents the server's network settings, including IP addresses, MAC addresses, and VLAN configurations.
- **FRU_Data.txt:** Stores Field Replaceable Unit (FRU) data, including serial numbers and part numbers, essential for hardware inventory management.

## Important Notes
- **Backplane Drives:** SysInfo may not retrieve hard drive information if the drives are installed onto a backplane. Ensure drives are connected directly to the system board for accurate log collection.
- **Driver Certification:** The `memrwd.sys` driver used by SysInfo to collect PCI/SATA information is not WHQL certified, which may lead to warnings during installation on Windows systems.


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



