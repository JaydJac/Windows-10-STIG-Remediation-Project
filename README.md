# 🔐 Windows 10 STIG Remediation 

## Overview

This project demonstrates the remediation process of a Windows 10 Security Technical Implementation Guide (STIG) vulnerability using both manual and automated (PowerShell) methods. The selected STIG is WN10-CC-000110, which prevents the client computer from printing over HTTP. Some features may communicate with the vendor, sending system information or downloading data or components for the feature. Turning off this capability will prevent potentially sensitive information from being sent outside the enterprise and uncontrolled updates to the system.
---

## 🛠️ STIG Creation & Remediation Methodology

## 1. Initial Scan
- Scanned a virtual machine (VM) with a Windows 10 STIG Audit Policy.
- Collected and reviewed the scan results.

**📸 Initial scan results:** 

![image](https://github.com/user-attachments/assets/54290f4d-4e47-41bd-b1f3-0d6e02942385)



## 2. STIG Selection
- Selected WN10-CC-000110 based on scan results.
- Reviewed DISA STIG documentation for context and remediation steps.

**📸 STIG details in scan report :** 

![image](https://github.com/user-attachments/assets/14531351-a0ad-4388-a6b1-417022c75773)


## 3. Manual Remediation
- Implemented manual fix using Registry Editor.

**📸 Manual configuration steps:**

![image](https://github.com/user-attachments/assets/496ebdeb-a496-4501-82c1-e2f739667bc7)


## 4. Verification of Manual Fix
- Rescanned to confirm the STIG was remediated.

**📸 Post-manual remediation scan:** 

![image](https://github.com/user-attachments/assets/ceb0a3f7-d99e-4f66-9940-adfb9359fb4b)


## 5. Reversion for Validation
- Undid the manual fix to confirm vulnerability reappears.
- Exported registry entry before reverting as documentation.

**📸 Reversion proof :**   

![image](https://github.com/user-attachments/assets/fd7b773c-f88f-469a-8f67-a8d83a2f3c4d)


## 6. PowerShell Automation
- Used PowerShell to automate the remediation.
 ### 🛠️ Script Used

Run this script with **Administrator privileges** to manually remediate the WN10-CC-000110 STIG finding:

```powershell
# Run this script with Administrator privileges 

# Define the registry path
$regPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Printers"

# Create the registry key if it doesn't exist
if (-not (Test-Path $regPath)) {
    New-Item -Path $regPath -Force | Out-Null
}

# Set the DisableHTTPPrinting DWORD value to 1
Set-ItemProperty -Path $regPath -Name "DisableHTTPPrinting" -Value 1 -Type DWord

# Confirm the setting
Write-Output "'DisableHTTPPrinting' successfully set to 1 under $regPath"
```


## 7. Verification of Scripted Fix
- Ran another scan to confirm the STIG was remediated via script.

**📸 Final scan results after PowerShell fix t:** Final scan results after PowerShell fix  

![image](https://github.com/user-attachments/assets/35dae240-1384-42b1-9fbf-65c67c5e3956)

## 8. Published My Fix to GitHub
- Documented the process and uploaded the PowerShell script and scan evidence.

👉 **[Click here to view the PowerShell fix on GitHub](https://github.com/JaydJac/JaydJac/blob/main/STIGS/WN10-CC-000110.ps1)**

---


