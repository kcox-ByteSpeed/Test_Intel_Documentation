# Pulling Logs Using SEL Viewer Utility on Windows
> This guide is intended for use with legacy systems where the Intel® System Event Log (SEL) Viewer Utility is required. For modern systems running Windows Server 2019 and Windows Server 2022, it is recommended to use Intel's SysInfo tool instead for enhanced compatibility and functionality.

> Here is a video featuring the steps outlined below. Click the image to watch the video on YouTube:
> <div align="left">
>  <a href="https://youtu.be/VT0fCEzwOH8" target="_blank">
>    <img src="https://img.youtube.com/vi/VT0fCEzwOH8/0.jpg" alt="Watch the video on YouTube">
>  </a>
> </div>

## Prerequisites
- **Administrative Rights:** You need administrative permissions to install and run the utility on Windows.

## Installation Instructions
1. Download the latest Java Runtime Environment (JRE)
    > **Note:** Do not install Java Development Kit (JDK)
2. Install JRE
    - Download and install the JRE X64 version compatible with your Windows OS.
        > If using Windows PE, install the JRE on a USB pen drive. Ensure it is the same version as your OS.
        > 1. While installing JRE on USB pen drive to support Windows PE OS, change the installation directory USB pen drive (for example, D:\)
        > 2. Set the JRE path:
        >       ```bash 
        >       PATH=%PATH%;\<USB-DIRECTORY\>:\bin
        >       ```
        >       - Replace <USB-DIRECTORY> with the path to the JRE installation directory. 

3. Prepare the SEL Viewer Utility
    - Download the [SEL Viewer utility][SEL_Download]
    - Extract/copy all files and subdirectories from the SEL Viewer release location to a folder on your hard drive (e.g., `C:\Selview`).

4. Install the Utility
    - Open a command prompt with administrative privileges.
    - Navigate to the installation directory:
        - For 32-bit Windows:
            ```bash
            cd C:\Selview\Windows\x86\imbdriver
            ```

        - For 64-bit Windows/Windows PE:
            ```bash
            cd C:\Selview\Windows\x64\imbdriver
            ```

    - Execute the installation script:
        ```bash
        install.cmd
        ```

        > The script installs the IPMI driver. If an existing IPMI driver from Microsoft is present, it will not be replaced.

5. Run the SEL Viewer Utility
    - Open a command prompt.
    - Navigate to the directory where selview.exe is located:
        ```bash
        cd C:\Selview\Windows\x64
        ```

    - Execute the SEL Viewer Utility:
        ```bash
        selview.exe
        ```

        > If selview.exe does not run a reboot may be required to finish installing dependencies.

6. Save the Logs
    
    Once the SEL Viewer Utility is open:
    - In the top-left corner of the screen, click on `File` > `Save As`.
    - Choose a location to save the log file.
    - Click `Save` to complete the process.

7. Generate and save logs using the SEL Viewer Utility from PowerShell
    - Open PowerShell as an **administrator**.
    - Navigate to the directory where `selview.exe` is located:
        ```bash
        cd C:\Selview\Windows\x64
        ```
    - Run the SEL Viewer Utility and save the log to a specific location:
        ```bash
        .\selview.exe -save <save location>.sel
        ```
        > For example: `.\selview.exe -save E:\ServerLog.sel`

        > **Note:** It is possible to save the log in `.txt` or `.log` format, but using the **`.sel`** format is recommended for compatibility with the SEL Viewer Utility.

## Important Notes
- Ensure you have the correct version of JRE installed for your OS.
- If you encounter issues with the IPMI driver, verify that no conflicting drivers are installed.

## Open a .sel file
1. Download and install the SEL Viewer Utility if it is not already installed [(refer to the above steps)](#installation-instructions)
2. Open a PowerShell window as an **administrator**.
3. Navigate to the SEL Viewer location, for example:
    ```bash
    cd C:\Selview\Windows\x64
    ```

4. Run the SEL Viewer by executing:
    ```bash
    .\selview.exe
    ```

5. In the SEL Viewer, go to the top-left corner and click on `File` > `Open`.
6. Browse and select the `.sel` file you want to open.

## Uninstall the SEL Viewer Utility
1. Navigate to the Installation Directory: Open File Explorer and go to the folder where the SEL Viewer Utility was installed.
    - For example, this might be `C:\Selview\Windows\x64\imbdriver`

2. Run the Uninstallation Script:
    - In the installation directory, locate the `uninstall.cmd` file.
    - Right-click on `uninstall.cmd` and select `Run as administrator` to execute the script. This will remove the IPMI driver and associated files.

3. Remove Remaining SEL Viewer Files:
    - After the script has completed, manually delete any remaining SEL Viewer files and folders from the installation directory.

4. Reboot the System (if necessary):
    - Some systems might require a reboot to fully remove all traces of the SEL Viewer Utility.

***

# Pulling Logs Using SEL Viewer Utility on UEFI Shell
> This guide is intended for use with legacy systems where the Intel® System Event Log (SEL) Viewer Utility is required. For modern systems running Windows Server 2019 and Windows Server 2022, it is recommended to use Intel's SysInfo tool instead for enhanced compatibility and functionality.

## Prerequisites
- UEFI Shell Access: Ensure you can boot to the EFI shell.

## Installation Instructions
1. Prepare Installation Media
    - Copy all the files from the SEL Viewer release directory for EFI to a USB flash drive or create an EFI-bootable CD.

2. Boot to EFI Shell
    - Insert the removable media into the server.
    - Boot the server and press <KBD>F2</KBD> when prompted to enter BIOS setup.
    - Go to the Boot Manager menu and select the option to boot to the EFI shell.

3. Run the SEL Viewer Utility
    - At the EFI shell prompt, type:
        ```bash
        fs<x>:
        ```
        Replace `<x>` with the file system number corresponding to the device containing the SEL Viewer utility files (e.g., fs0:).

4. Executing Commands
    - Once in the EFI shell, navigate to the directory containing the SEL Viewer files.
    - Run the utility using the command:
        ```bash
        selview
        ```

## Important Notes
- Ensure that the SEL Viewer files are correctly copied to the USB flash drive or EFI-bootable CD.
- The EFI shell should be properly configured to access the device where the SEL Viewer is stored.


## Sources
- [Installing the SEL Viewer][SEL_install]
- [Intel® System Event Log (SEL) Viewer Utility][SEL_Usage]
- [Download SEL Viewer][SEL_Download]


[SEL_install]:https://webdrivers.blob.core.windows.net/drivers/server/Intel/SELViewer_Windows_Install.pdf
[SEL_Usage]: https://www.intel.com/content/dam/support/us/en/documents/motherboards/server/s5400sf/sb/sel_viewer_user_guide.pdf
[SEL_Download]: https://webdrivers.blob.core.windows.net/drivers/server/Intel/selviewer_v14_1_build27_allos.zip

## Revision History
| Revision | Date       | Comments                                                                 | Author     |
|----------|------------|--------------------------------------------------------------------------|------------|
| 1.0      | 08/22/2024 | Initial release | Keegan Cox
| 1.0      | 08/23/2024 | Added media | Keegan Cox
| 1.0      | 08/23/2024 | Revised | Keegan Cox