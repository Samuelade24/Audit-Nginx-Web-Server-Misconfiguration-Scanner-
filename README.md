Project Description

PortScan Pro is a PowerShell-based network scanning tool that simplifies port scanning and service enumeration using Nmap. The tool provides an intuitive interface for security professionals to quickly identify open ports, detect services, and assess security risks on target systems.

Languages and Utilities Used
PowerShell (Primary scripting language)
Nmap (Network scanning engine)
Windows Task Scheduler (For scheduled scans)
HTML/CSV (Report generation)

Environments Used
Windows 10
Linux (With PowerShell Core and Nmap installed)

Features
Intuitive target selection interface
Multiple scan profiles (Quick, Comprehensive, Stealth)
Service version detection
Security risk assessment
HTML and CSV report generation
Scheduled scanning capabilities


Program Walk-through
<p align="center"> Launch the utility: <br/> <img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Tool Launch"/> <br /> <br /> Enter target IP/hostname: <br/> <img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Target Input"/> <br /> <br /> Select scan type: <br/> <img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Scan Selection"/> <br /> <br /> Review scan parameters: <br/> <img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Parameter Review"/> <br /> <br /> Scan in progress: <br/> <img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Scan Progress"/> <br /> <br /> Scan results summary: <br/> <img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Results Summary"/> <br /> <br /> Vulnerability assessment: <br/> <img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Vulnerability Report"/> </p>

Installation

Install prerequisites:

Clone the repository:
git clone https://github.com/yourusername/portscan-pro.git
cd portscan-pro

Run the tool:
.\PortScanPro.ps1

Usage Examples
Basic scan:
.\PortScanPro.ps1 -Target 192.168.1.1

Comprehensive scan with OS detection:
.\PortScanPro.ps1 -Target example.com -ScanType Full -OSDetection

Stealth scan with HTML report:
.\PortScanPro.ps1 -Target 10.0.0.1 -ScanType Stealth -ReportFormat HTML

Sample Code Structure
# PortScanPro.ps1

param(
    [string]$Target,
    [ValidateSet('Quick','Full','Stealth')]
    [string]$ScanType = 'Quick',
    [switch]$OSDetection,
    [ValidateSet('HTML','CSV','Text')]
    [string]$ReportFormat = 'Text'
)

# Import modules
. .\modules\nmap-wrapper.ps1
. .\modules\risk-assessor.ps1
. .\modules\report-generator.ps1

function Show-Banner {
    Write-Host "=== PortScan Pro - Network Scanning Tool ===" -ForegroundColor Cyan
    Write-Host "Version 1.0 | Secure your network infrastructure`n"
}

function Main {
    Show-Banner
    
    # Validate target input
    if (-not $Target) {
        $Target = Read-Host "Enter target IP/hostname"
    }
    
    # Build Nmap command based on parameters
    $scanCommand = Build-NmapCommand -Target $Target -ScanType $ScanType -OSDetection:$OSDetection
    
    # Execute scan
    $scanResults = Invoke-NmapScan -Command $scanCommand
    
    # Analyze results
    $riskAssessment = Get-RiskAssessment -ScanResults $scanResults
    
    # Generate report
    New-ScanReport -Results $scanResults -Risk $riskAssessment -Format $ReportFormat
}

Main

Security Considerations
Always obtain proper authorization before scanning

Stealth mode uses slower scan techniques to avoid detection

Includes automatic rate limiting to prevent network congestion

Clearly marks potentially risky findings in reports



Risk Assessment Matrix

Finding	Risk Level	Recommended Action
Open HTTP port (80)	Medium	Implement HTTPS
Outdated service version	High	Update service
Unencrypted services	Critical	Enable encryption
Unexpected open ports	Medium	Review firewall rules
