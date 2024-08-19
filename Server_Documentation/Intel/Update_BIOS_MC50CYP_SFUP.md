# Intel® Server Board M50CYP Family BIOS and Firmware Update Package (SFUP) for Windows* and Linux*

**ID:** 19813  
**Date:** 11/03/2023  
**Version:** R01.01.0009 (Latest)

## Introduction

Provides Intel® Server Board M50CYP Family BIOS and System Firmware Update Package (SFUP) for Windows* and Linux*. (R01.01.0009)

## Available Downloads

- **File:** M50CYP_SFUP_BIOSR01.01.0009_ME04.04.04.500_BMC2.92.19c01286_CPLD4.9_FRUSDR0.46_PMem2.2.0.1553.zip  
  **Size:** 46.3 MB  
  **SHA1:** E93F255ABE079A717895316B3DE6C44C66CE0A9D

## Detailed Description

This update package includes the following production level system software updates and update utilities:

- **System BIOS:** R01.01.0009
- **ME Firmware:** 04.04.04.500
- **BMC Firmware:** 2.92.19c01286
- **FRUSDR:** 0.46
- **Pmem:** 2.2.0.1553
- **CPLD:** v4P9
- **sysfwupdt:** Version 16.0.9

### Important Notes

- **Firmware check is not applicable:** Updates will be triggered even when the versions in the system and in the SFUP package are the same.
- **Do NOT interrupt or reboot** or remove power from your system during the update process. Doing so may render your system inoperable.
- **Do NOT attempt to down rev** the system software once loaded onto the system. Doing so may render your system inoperable.
- All updates provided in this package are installed using the Windows and Linux operating environment only.
- **Do not modify any of the script files.** The scripts as written will provide the most reliable update experience.
- Refer to the user guide available in the `sysfwupdt` folder for any update scenarios or `sysfwupdt` commands.
- ITK `.cap` file needs to be customized, else `.cap` file update will fail.

## Supported Products

- Intel® Server Board M50CYP2SBSTD
- Intel® Server Board M50CYP2SB1U
- Intel® Server System M50CYP2UR208
- Intel® Server System M50CYP2UR312
- Intel® Server System M50CYP1UR212
- Intel® Server System M50CYP1UR204

## SFUP Contents

- **Windows:**  
  - `startup.bat`
  - `sysfwupdt_win` directory containing the `sysfwupdt` executable for Windows x64 bit OS.

- **Linux:**  
  - `startup.sh`
  - `sysfwupdt_linux` directory containing installable `.rpm` for RHEL, SLES, and UBUNTU.

- **Update Files:**
  - `bios_cap_update.bat`, `bios_cap_update.sh`, `bios_update.bat`, `bios_update.sh`
  - `bmc_update.bat`, `bmc_update.sh`, `cpld_update.bat`, `cpld_update.sh`
  - `dimms_update.bat`, `dimms_update.sh`, `driver_install.bat`, `driver_uninstall.bat`
  - `frusdr_update.bat`, `frusdr_update.sh`, `startup.bat`, `startup.sh`
  - `sysfwupdt_install.sh`, `sysfwupdt_uninstall.sh`

- **BIOS:** `R01010008_TennesseePass_LBG_ICX_UpdateCapsule_prd.bin`
- **BMC:** `TennesseePass-bmc_prod_signed_cap_2.91.cb510bad.bin`
- **CPLD:** `pfr_tnp_627p4_v4p7_cfm1_auto_prd.bin`
- **DIMM:** `fw_bwva1_2.2.0.1553_rel.bin`
- **FRU:** `D50TNP1SBCR.fru`, `D50TNP1SB.fru`
- **SDR:** `D50TNP.sdr`
- **CFG:** `master.cfg`, `sdr_update_noprompt.cfg`
- **PDF:** `CR_FW_CRFW_2.2.0.1553_Intel_Optane_persistent_memory_200_series_FW_Release_Notes_1553.pdf`

## System Software Requirements

To update the system software stack to the versions included in this update package, the system software stack currently installed on the target server system MUST meet the following requirements:

- **System BIOS:** R01.01.0008
- **ME Firmware:** 04.04.04.301
- **BMC Firmware:** 2.91.8a19dcde
- **FRUSDR:** 0.46
- **Pmem:** 2.2.0.1553
- **CPLD:** v4P7

## Prerequisites Before Running Windows and Linux Update Scripts

- **Install "ipmctl" tool** in both Windows and Linux.

### Windows

- Download `ipmctl_windows_install_xx.xx.xx.xxxx.exe` from [Intel GitHub](https://github.com/intel/ipmctl/) (use the latest version).

### Linux

#### RHEL8

1. Set proxy in your RHEL OS (if required).
2. `ipmctl` is available in `epel-release`. Add the latest `epel-release` to your repolist.
3. Install `ipmctl` using the following commands:
    - `yum install epel-release` or
    - `dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`
    - `yum install ipmctl`

#### SLES15 SPx

1. Set proxy in your SLES15 OS (if required).
2. `ipmctl` is available on the [Intel GitHub](https://github.com/intel/ipmctl/) (use the latest version).
    - Dependencies may include the following:
        - `libipmctl` (available on the above GitHub)
3. `ipmctl` may have dependencies; find dependencies in the following openSUSE repositories:
    - http://ftp.opensuse.org/update/leap/15.2/oss/x86_64/
    - Dependencies may include:
        - `libndctl`
        - `ndctl`
4. For SLES15 SP2:
    - `wget http://ftp.opensuse.org/update/leap/15.2/oss/x86_64/ndctl-70.1-lp152.7.12.1.x86_64.rpm --no-check-certificate`
    - `wget http://ftp.opensuse.org/update/leap/15.2/oss/x86_64/libndctl6-70.1-lp152.7.12.1.x86_64.rpm --no-check-certificate`
    - `zypper install ndctl-70.1-lp152.7.12.1.x86_64.rpm`
    - `zypper install libndctl6-70.1-lp152.7.12.1.x86_64.rpm`
    - `zypper install libipmctl-02.00.00.3878-1.el8.x86_64.rpm`
    - `zypper install ipmctl-02.00.00.3878-1.el8.x86_64.rpm`

## Important Information for the Update Procedure

- **Windows:** When `startup.bat` is executed from SFUP, the update order is CPLD, PMEM, BMC, FRUSDR, and BIOS, followed by a system reset.
- **Linux:** When `./startup.sh` is executed from SFUP, it uninstalls existing `sysfwupdt` (if any) and installs the latest `sysfwupdt` from SFUP. The update order is CPLD, PMEM, BMC, FRUSDR, and BIOS, followed by a system reset.

## General Installation Procedure

1. Unzip the contents of the SFUP package to any directory.
2. **Windows:** Unzip the package, open a command prompt or PowerShell from the SFUP directory, and execute `startup.bat`.
3. **Linux:** Unzip the package, open a terminal from the SFUP directory, and execute `./startup.sh`.

## Known Issues

1. On Windows OS, if the "system PMEM FW" and "PMEM FW in the SFUP" package are the same versions, `ipmctl` tool may error out with the following message:
   - "Error 308 - FW Update authentication failure"
2. If the "system PMEM FW" has a production stack and the "PMEM FW in the SFUP" is in debug stack (or vice versa), `ipmctl` tool will error out with the following message:
   - "Error 308 - FW Update authentication failure"

**Warning:**  
Do NOT interrupt or reboot or remove power from your system during the update process. Doing so may render your system inoperable.  
Do NOT attempt to downgrade the system software once loaded onto the system. Doing so may render your system inoperable.


## Sources
- [Intel® Server BIOS Support Central][Intel® Server BIOS Support Central]
- [Intel® Server Board M50CYP Intel® SFUP Download][Intel® Server Board M50CYP Intel® SFUP Download]
- [Release Notes and Update Instructions][Release Notes and Update Instructions]

[Intel® Server BIOS Support Central]: https://www.intel.com/content/www/us/en/support/articles/000088822/server-products.html
[Intel® Server Board M50CYP Intel® SFUP Download]: https://www.intel.com/content/www/us/en/download/19813/intel-server-board-m50cyp-family-bios-and-firmware-update-package-sfup-for-windows-and-linux.htmlintel-server-board-s2600wf-family-bios-and-firmware-update-for-intel-one-boot-flash-update-intel-ofu-utility.html
[Release Notes and Update Instructions]: https://downloadmirror.intel.com/794048/Readme%20and%20Update%20Instructions.txt

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/13/2024 | Initial release | Keegan Cox |