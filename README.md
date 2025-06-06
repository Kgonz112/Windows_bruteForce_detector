# Windows Brute Force Detector

This project detects and analyzes failed login attempts on a Windows system by parsing Event ID 4625 from the Windows Security logs. The goal is to simulate a brute-force attack scenario, extract meaningful patterns from the logs, and provide remediation steps to improve system security.

## Project Objectives
- Detect failed login attempts (Event ID 4625)
- Extract and analyze usernames, timestamps, and IP addresses
- Identify suspicious login behavior (brute-force patterns)
- Visualize attack trends using Excel dashboards
- Provide a short security report with actionable recommendations

## Tools & Technologies
- 💻 Windows 10/11 (Home Edition)
- 🔍 Event Viewer & PowerShell
- 📊 Microsoft Excel

## Steps Performed
1. **Enabled audit logging** (already active on most Windows systems)
2. **Simulated failed login attempts** by entering incorrect passwords
3. **Used PowerShell** to extract Event ID 4625 from Windows Security Logs:
   ```powershell
   Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625} |
   Select-Object TimeCreated, @{Name="User";Expression={$_.Properties[5].Value}}, @{Name="IP";Expression={$_.Properties[18].Value}}, Message |
   Export-Csv "$env:USERPROFILE\Desktop\failed_logins.csv" -NoTypeInformation