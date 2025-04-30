# Audit-Nginx-Web-Server-Misconfiguration-Scanner-
Task: Check for outdated nginx/PHP (from your report).
#!/bin/bash
curl -I http://testphp.vulnweb.com | grep -E "nginx|PHP"
if [[ $? -eq 0 ]]; then
    echo "[!] Vulnerable Server Detected: $(curl -I http://testphp.vulnweb.com | grep 'Server')"
fi
