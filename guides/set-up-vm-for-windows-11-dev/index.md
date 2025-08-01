# 🛠️ Setting Up a Windows 11 Development VM with Revit

This comprehensive guide walks you through setting up a Windows 11 VM, configuring it for development, installing Revit, and managing add-ins.

---

## 1. Enable Hyper-V

Ensure your system supports virtualization and enable Hyper-V:

1. Open **Control Panel** > **Programs** > **Turn Windows features on or off**.
2. Check the following options:
   - Hyper-V
   - Virtual Machine Platform
   - Windows Hypervisor Platform
3. Click **OK** and restart your computer.

*Reference: [Microsoft Learn - Install Hyper-V](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/Install-Hyper-V)*

---

## 2. Connect VM to the Internet

Configure the VM's network settings to ensure internet connectivity:

1. Open **Hyper-V Manager**.
2. Right-click your VM and select **Settings**.
3. Under **Network Adapter**, choose a virtual switch that provides internet access (e.g., Default Switch).

*Reference: [Robots.net - How To Connect Virtual Machine To Internet VMware](https://robots.net/tech/how-to-connect-virtual-machine-to-internet-vmware/)*

---

## 3. Create and Connect a Local Network Drive

To share files between the host and VM:

1. On the host machine, share the desired folder.
2. In the VM, open **File Explorer**.
3. Click on **This PC** > **Map network drive**.
4. Choose a drive letter and enter the folder path (e.g., `\\HostMachineName\SharedFolder`).
5. Check **Reconnect at sign-in** and click **Finish**.

*Reference: [SolveYourTech - Map a Network Drive](https://www.solveyourtech.com/windows-11-how-to-map-a-network-drive-a-step-by-step-guide/)*

---

## 4. Expand Disk Storage

If you need more storage in your VM:

1. Open **Disk Management** in the VM.
2. Right-click on the volume you wish to expand and select **Extend Volume**.
3. Follow the wizard to allocate additional space.

*Reference: [Microsoft Learn - Extend a Basic Volume](https://learn.microsoft.com/en-us/windows-server/storage/disk-management/extend-a-basic-volume)*

---

## 5. Install Revit

To install Autodesk Revit:

1. Download the installer from the [Autodesk website](https://www.autodesk.com/products/revit/overview).
2. Run the installer and follow the on-screen instructions.
3. Activate the product using your Autodesk account credentials.

*Reference: [Autodesk Help - Revit Installation](https://help.autodesk.com/cloudhelp/2024/ENU/Revit-Installation/files/GUID-DA49AED9-764F-41CC-B516-570EAF9FE565.htm)*

---

## 6. Build Revit Add-ins into the Dev VM

Set up your development environment:

1. Install **Visual Studio** with the **.NET Desktop Development** workload.
2. Install the **Revit API SDK** from Autodesk.
3. Create a new Class Library project in Visual Studio.
4. Reference the necessary Revit API DLLs.
5. Implement your add-in logic.
6. Build the project to generate the `.dll` file.

*Reference: [ArchSmarter - Create Your Own Revit Add-in](https://www.archsmarter.com/revit-add-in-5-steps)*

---

## 7. Check Add-in Works

To test your add-in:

1. Place the compiled `.dll` and its corresponding `.addin` manifest file into Revit's Add-ins folder (e.g., `C:\ProgramData\Autodesk\Revit\Addins\2024`).
2. Launch Revit.
3. Navigate to the **Add-Ins** tab and verify your add-in appears and functions as expected.

---

## 8. Bundle the Add-in for Deployment

Prepare your add-in for distribution:

1. Create an installer package that places the `.dll` and `.addin` files into the appropriate directory.
2. Ensure the installer sets any necessary registry keys or environment variables.
3. Test the installer on a clean environment to verify proper installation.

*Reference: [Microsoft Learn - Deploy and Publish Office Add-ins](https://learn.microsoft.com/en-us/office/dev/add-ins/publish/publish)*

---

**Note:** For detailed instructions and visuals, refer to the respective links provided in each section.

