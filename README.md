# Audit-Nginx-Web-Server-Misconfiguration-Scanner-
Task: Check for outdated nginx/PHP (from your report).
#!/bin/bash
curl -I http://testphp.vulnweb.com | grep -E "nginx|PHP"
if [[ $? -eq 0 ]]; then
    echo "[!] Vulnerable Server Detected: $(curl -I http://testphp.vulnweb.com | grep 'Server')"
fi

Risk Rating:

CVSS: 8.1 (High) – CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:L

Impact: Exploitable server flaws (e.g., nginx 1.19.0 EOL).

Likelihood: High (scanners detect versions).

Compliance:

CIS Benchmark: Section 3.1 (patch management).

PCI-DSS: Requirement 6.2 (vendor-supplied patches).
