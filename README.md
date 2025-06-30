# Make2023BootableMedia.ps1

Modified Microsoft script to create bootable USB or CD/DVD from Windows Insider ISOs. ⚠️ For systems supporting PCA 2023 signed boot (updated Secure Boot keys). Otherwise, use official Microsoft tools to create installation media.



\# Make2023BootableMedia – PCA 2023-Compatible Version



\## 📌 Description

This is a modified version of Microsoft's `Make2023BootableMedia.ps1` script.  

It allows you to create a \*\*bootable USB or CD/DVD\*\* from \*\*Windows Insider ISOs\*\*, even when Secure Boot requires \*\*PCA 2023-signed EFI binaries\*\*.



\## ❗ Why this script is needed

Recent Windows Insider ISO files still include bootloaders (`bootx64.efi`, `bootmgr.efi`) signed with the \*\*2011 Windows Production PCA\*\* certificate.  

However, Microsoft now enforces Secure Boot updates that \*\*revoke PCA 2011 certificates\*\*, via the `DBX` (revocation list), especially due to CVE-2020-0689.



This results in:

\- Boot failure on systems requiring PCA 2023 signatures

\- Blank screen or fallback to BIOS when using official Insider ISOs



\## ✅ What this script does

\- Replaces the bootloader with `bootmgfw\_EX.efi` (PCA 2023-signed)

\- Adds support for \*\*NTFS-formatted USB drives\*\*, allowing large `install.wim` files

\- Removes the Authenticode signature block to avoid execution errors



\## 🛠 Requirements

\- A system with Secure Boot \*\*updated to PCA 2023\*\*

\- A Windows Insider ISO (from UUP Dump, Microsoft, etc.)



\## 📦 Dependencies

To run the script properly, the following components must be available:



\- \*\*Windows PowerShell 5.1\*\* (or higher)

\- \*\*Administrator privileges\*\*

\- Access to:

&nbsp; - `bootmgfw\_EX.efi` file signed with PCA 2023

&nbsp; - A Windows Insider ISO (`.iso`)

&nbsp; - A USB drive or CD/DVD



Additional requirements:

\- The \*\*Windows Assessment and Deployment Kit (ADK)\*\* must be installed  

\- The \*\*Windows PE Add-on for ADK\*\* must also be installed  

&nbsp; These provide tools like `oscdimg.exe`, `copype.cmd`, and required boot environment components.



👉 Download the ADK and PE Add-on here:  

https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install



\## 📅 Usage

```powershell

.\\Make2023BootableMedia.ps1 -MediaPath D:\\ -ISOSourcePath C:\\ISO\\Win11\_Insider.iso

```

> For full usage and options, run:  

> `Get-Help .\\Make2023BootableMedia.ps1 -Detailed`



\## 📟 License

This project is licensed under the \[BSD-2-Clause-Patent](./LICENSE), as used by Microsoft.  

It includes a patent grant for the covered contributions.  

See \[LICENSE](./LICENSE) for full legal terms.



\## ✏️ Author \& Modifications

Modified and maintained by \*\*Yoann Deferi\*\* (a.k.a. \*\*koubinovski\*\*) – June 2025  

Original script by Microsoft, available in the \[`secureboot\_objects`](https://github.com/microsoft/secureboot\_objects) repository.



👉 \[Lire en français](./README.fr.md)



