# Security Prompt Templates for Local LLMs
## Ready-to-Use Templates for Red/Blue Team Operations

**⚠️ AUTHORIZED TESTING ONLY - All templates assume written permission and legal authorization**

---

## 📑 Table of Contents

- [Red Team Templates](#red-team-templates)
  - [Reconnaissance](#reconnaissance)
  - [Exploitation](#exploitation)
  - [Post-Exploitation](#post-exploitation)
  - [Social Engineering](#social-engineering)
- [Blue Team Templates](#blue-team-templates)
  - [Threat Hunting](#threat-hunting)
  - [Malware Analysis](#malware-analysis)
  - [Incident Response](#incident-response)
  - [Detection Engineering](#detection-engineering)
- [Tool Integration Templates](#tool-integration-templates)
- [Report Generation Templates](#report-generation-templates)

---

## Red Team Templates

### Reconnaissance

#### Template 1: OSINT Synthesis

```
TASK: Synthesize OSINT data for authorized penetration test

TARGET: [ORGANIZATION NAME]
AUTHORIZATION: [ENGAGEMENT ID / SOW REFERENCE]

DATA SOURCES:
[Paste Shodan results]
[Paste DNS enumeration]
[Paste certificate transparency logs]
[Paste paste site findings]

ANALYSIS REQUIRED:
1. Correlate findings across data sources
2. Identify exposed services and potential vulnerabilities
3. Map technologies to known CVEs
4. Prioritize attack surface by likelihood of successful exploitation
5. Generate initial attack hypotheses

OUTPUT FORMAT:
- Executive summary (3 bullet points)
- Service inventory table (service, version, CVE, priority)
- Attack path recommendations (ranked by probability of success)
- IOCs to monitor during engagement

Think step-by-step through the correlation process.
```

---

#### Template 2: Subdomain Enumeration Analysis

```
I'm conducting an authorized security assessment of [TARGET.COM].
Authorization: [SOW REFERENCE]

I've collected the following subdomains from passive sources:
[PASTE SUBDOMAIN LIST]

Analyze this list and:
1. Categorize by function (prod/dev/staging/admin/etc.)
2. Identify high-value targets (admin panels, APIs, dev environments)
3. Suggest additional enumeration techniques for each category
4. Prioritize for active testing
5. Identify potential security misconfigurations based on naming patterns

For each high-value target, explain why it's interesting and what to test first.
```

---

#### Template 3: Port Scan Analysis

```
AUTHORIZED PENETRATION TEST
Client: [CLIENT NAME]
Target: [IP ADDRESS / HOSTNAME]
Engagement ID: [ID]

Nmap scan results:
[PASTE NMAP OUTPUT]

Analyze these results:
1. Identify all services and versions
2. Flag outdated or vulnerable versions (with CVE references)
3. Identify unusual port/service combinations
4. Suggest exploitation order (easiest to hardest)
5. Recommend additional enumeration per service
6. Flag potential false positives

OUTPUT: Prioritized target list with rationale
```

---

### Exploitation

#### Template 4: SQL Injection Payload Generation

```
AUTHORIZED WEB APPLICATION SECURITY TESTING
Application: [APP NAME]
Client: [CLIENT]
Authorization: [SOW REFERENCE]

I've identified a potential SQL injection point:
- Parameter: [PARAMETER NAME]
- Context: [GET/POST/COOKIE]
- Database type: [MySQL/PostgreSQL/MSSQL/Oracle/UNKNOWN]
- WAF present: [YES/NO/UNKNOWN]

Generate 15 advanced SQL injection payloads:
1. Time-based blind SQLi (5 payloads)
2. Boolean-based blind SQLi (5 payloads)
3. UNION-based SQLi (5 payloads)

For each payload:
- Explain the technique
- Note detection evasion features
- Specify success indicators
- Rate likelihood of bypass (if WAF present)

Assume moderate SQLi knowledge on my part. Be technical and thorough.
```

---

#### Template 5: Exploit Modification Assistance

```
AUTHORIZED PENETRATION TESTING
Target: [SYSTEM/SERVICE]
Engagement: [ID]

I have a public exploit (CVE-XXXX-XXXXX) that needs modification:

ORIGINAL EXPLOIT:
[PASTE EXPLOIT CODE]

REQUIRED MODIFICATIONS:
1. [e.g., Change payload to reverse shell]
2. [e.g., Update target address]
3. [e.g., Add error handling]
4. [e.g., Obfuscate for AV bypass]

CONSTRAINTS:
- Must maintain exploit reliability
- Target environment: [WINDOWS/LINUX/WEB APP]
- [Additional constraints]

Provide modified exploit with:
- Line-by-line explanation of changes
- Testing recommendations
- Failure modes to watch for
- OPSEC considerations

This is for authorized testing with written client permission.
```

---

#### Template 6: Custom Payload Scaffolding

```
AUTHORIZED RED TEAM OPERATION
Client: [CLIENT]
Objective: [OPERATION OBJECTIVE]
Authorization: [DOCUMENT REFERENCE]

REQUIREMENTS:
I need a [TYPE OF PAYLOAD: reverse shell/web shell/etc.] with these features:

FUNCTIONALITY:
- [Required capability 1]
- [Required capability 2]
- [Required capability 3]

TARGET ENVIRONMENT:
- OS: [Windows/Linux/macOS]
- Language: [Python/PowerShell/Bash/etc.]
- Privileges: [user/admin/SYSTEM]
- Network: [Egress restrictions if any]

EVASION:
- Must evade [AV/EDR/DLP]
- No suspicious process names
- Minimal network noise

OUTPUT:
1. Full commented source code
2. Compilation/execution instructions
3. OPSEC considerations
4. Detection indicators (so I can verify they're not triggered)
5. Safe cleanup procedure

This payload will only be used in authorized, contracted security assessments.
```

---

### Post-Exploitation

#### Template 7: Privilege Escalation Enumeration

```
AUTHORIZED PENETRATION TEST - POST-EXPLOITATION PHASE
Client: [CLIENT]
System: [HOSTNAME/IP]
Current Access: [USERNAME] with [PRIVILEGES]
Authorization: [SOW REFERENCE]

I have initial access and need privilege escalation guidance.

SYSTEM INFO:
OS: [WINDOWS/LINUX VERSION]
Installed Software: [LIST IF KNOWN]
Current User Groups: [LIST]

ENUMERATION DATA:
[PASTE OUTPUT FROM ENUMERATION SCRIPTS]

ANALYSIS REQUIRED:
1. Identify all privilege escalation vectors
2. Rank by likelihood of success and stealth
3. For each vector:
   - Exploitation technique
   - Commands to execute
   - Success indicators
   - Remediation (for report)
4. Flag any detection risks

OUTPUT: Step-by-step privilege escalation playbook for this specific system.
```

---

#### Template 8: Lateral Movement Path Analysis

```
AUTHORIZED RED TEAM ENGAGEMENT
Client: [CLIENT]
Objective: Reach [TARGET SYSTEM/DATA]
Current Position: [CURRENT SYSTEM]
Authorization: [ENGAGEMENT ID]

NETWORK MAPPING DATA:
[PASTE NETWORK SCAN RESULTS]

CREDENTIALS OBTAINED:
[LIST CREDENTIALS - SANITIZE SENSITIVE VALUES]

PIVOT OPTIONS:
[LIST COMPROMISED SYSTEMS THAT COULD BE PIVOTS]

OBJECTIVE: Determine optimal lateral movement path from current position to target.

ANALYSIS REQUIRED:
1. Map possible paths (show decision tree)
2. For each path:
   - Required techniques/tools
   - Detection likelihood (LOW/MEDIUM/HIGH)
   - Estimated time
   - Rollback plan if detected
3. Recommend optimal path with rationale
4. Identify "tripwires" (high-detection activities to avoid)

OUTPUT: Lateral movement playbook with decision points and contingencies.
```

---

### Social Engineering

#### Template 9: Phishing Email Template Generation

```
AUTHORIZED RED TEAM SOCIAL ENGINEERING ASSESSMENT
Client: [CLIENT NAME]
Assessment Type: Phishing Simulation
Authorization: [SIGNED SOW REFERENCE]
Approval Date: [DATE]
Authorized by: [CLIENT CONTACT NAME/TITLE]

SCENARIO:
Target Audience: [EMPLOYEES/EXECUTIVES/IT STAFF]
Pretext: [IT HELPDESK/VENDOR/PARTNER/etc.]
Goal: [CREDENTIAL HARVEST/LINK CLICK/ATTACHMENT OPEN]

CONSTRAINTS:
- Must be believable to target audience
- Appropriate urgency level (not too aggressive)
- Compliant with [CLIENT] policy on testing
- Include training opportunity if clicked

Generate 3 phishing email templates:
1. Low sophistication (baseline)
2. Medium sophistication (targeted)
3. High sophistication (spearphishing)

For each template provide:
- Subject line
- Email body (HTML and plain text)
- Embedded URLs to replace with tracking links
- Attachment type (if applicable)
- Explanation of psychological triggers used
- Likelihood of success vs detection
- Post-click training message recommendation

IMPORTANT: These will ONLY be used in this authorized assessment.
Target users will be informed post-assessment per agreement.
```

---

## Blue Team Templates

### Threat Hunting

#### Template 10: Log Analysis for Threat Hunting

```
THREAT HUNTING ANALYSIS
Environment: [ORGANIZATION]
Data Source: [SIEM/LOG TYPE]
Hunting Hypothesis: [WHAT YOU'RE LOOKING FOR]

LOG DATA:
[PASTE RELEVANT LOGS - SANITIZE SENSITIVE INFO]

ANALYSIS REQUIRED:
1. Identify anomalous patterns
2. Correlate events across timestamps
3. Map to MITRE ATT&CK techniques
4. Assess threat level (BENIGN/SUSPICIOUS/MALICIOUS)
5. Recommend next investigation steps
6. Suggest additional data sources to pivot to

FOCUS AREAS:
- Unusual authentication patterns
- Lateral movement indicators
- Data exfiltration patterns
- Privilege escalation attempts
- LOLBin usage

OUTPUT FORMAT:
- Findings summary
- ATT&CK technique mapping table
- IOCs extracted
- Recommended response actions
- Additional hunt queries to run
```

---

#### Template 11: MITRE ATT&CK Behavior Analysis

```
THREAT HUNTING - BEHAVIORAL ANALYSIS

OBSERVED ACTIVITY:
[DESCRIBE THE SUSPICIOUS BEHAVIOR/ALERTS]

CONTEXT:
- User/System: [IDENTIFIER]
- Time window: [START - END]
- Network segment: [INTERNAL/DMZ/etc.]
- Baseline behavior: [DESCRIPTION]

TASK: Map this activity to MITRE ATT&CK framework

REQUIRED ANALYSIS:
1. Identify all applicable ATT&CK techniques (with IDs)
2. Determine kill chain stage
3. Assess sophistication level
4. Compare to known threat actor TTPs
5. Identify next likely attacker actions
6. Recommend detection gaps to address

OUTPUT:
- ATT&CK Navigator layer (JSON or text description)
- Threat actor attribution (if patterns match)
- Predicted next steps
- Enhanced detection opportunities
```

---

### Malware Analysis

#### Template 12: Static Malware Code Analysis

```
MALWARE ANALYSIS - STATIC ANALYSIS
Sample ID: [MD5/SHA256]
Source: [DETECTION SOURCE]
Classification: [SUSPECTED TYPE]

DECOMPILED/EXTRACTED CODE:
[PASTE CODE - DEFANGED]

ANALYSIS REQUIRED:
1. Describe malware functionality step-by-step
2. Identify C2 infrastructure (IPs, domains, protocols)
3. Extract IOCs:
   - File hashes
   - Mutex names
   - Registry keys
   - Network indicators
4. Map to MITRE ATT&CK techniques
5. Identify killswitch or analysis evasion techniques
6. Assess sophistication and attribution clues
7. Generate YARA rule for detection

OUTPUT FORMAT:
- Malware behavior summary
- IOC table (categorized)
- ATT&CK technique mapping
- YARA rule (tested syntax)
- Remediation recommendations
```

---

#### Template 13: Behavioral Malware Analysis

```
MALWARE DYNAMIC ANALYSIS
Sample: [IDENTIFIER]
Execution Environment: [SANDBOX TYPE]

BEHAVIORAL DATA COLLECTED:
Process Tree:
[PASTE PROCESS TREE]

Network Connections:
[PASTE NETSTAT/PCAP SUMMARY]

File System Changes:
[PASTE FILE MODIFICATIONS]

Registry Changes:
[PASTE REGISTRY MODIFICATIONS]

ANALYSIS TASK:
1. Reconstruct attack sequence from execution to objective
2. Identify persistence mechanisms
3. Map network communications (C2 protocol analysis)
4. Classify malware family (if recognizable)
5. Identify anti-analysis techniques observed
6. Generate detection rules (Sigma/Snort/YARA)
7. Recommend containment actions

OUTPUT:
- Infection chain diagram (text description)
- Persistence mechanism details
- C2 profile
- Detection signatures (multiple formats)
- Remediation playbook
```

---

### Incident Response

#### Template 14: Incident Triage and Scoping

```
INCIDENT RESPONSE - INITIAL TRIAGE

ALERT DETAILS:
- Alert ID: [ID]
- Detection Source: [EDR/SIEM/USER REPORT]
- Alert Type: [MALWARE/INTRUSION/DATA EXFIL/etc.]
- Severity: [SIEM RATING]

INITIAL INDICATORS:
[PASTE INITIAL ALERT DATA]

AFFECTED SYSTEMS:
[LIST KNOWN AFFECTED HOSTS/USERS]

TRIAGE ANALYSIS REQUIRED:
1. Validate: Is this a true positive?
2. Scope: How widespread is the incident?
3. Impact: What data/systems are at risk?
4. Timeline: When did it start? Is it ongoing?
5. Attribution: Does this match known threat actors?
6. Containment: Immediate actions needed?
7. Evidence: What should we preserve?

OUTPUT:
- TRUE POSITIVE / FALSE POSITIVE determination with confidence level
- Incident severity rating (1-5) with justification
- Scoping queries to run in SIEM/EDR
- Immediate containment recommendations
- Evidence collection checklist
- Escalation recommendation
```

---

#### Template 15: Post-Incident Root Cause Analysis

```
POST-INCIDENT ANALYSIS
Incident ID: [ID]
Date Range: [START - END]
Systems Affected: [COUNT/LIST]
Incident Type: [CLASSIFICATION]

INCIDENT TIMELINE:
[PASTE CHRONOLOGICAL EVENT LOG]

EVIDENCE COLLECTED:
[SUMMARIZE FORENSIC FINDINGS]

ANALYSIS REQUIRED:
1. Determine initial compromise vector
2. Identify root cause(s)
3. Map full attack path (with timestamps)
4. Identify detection/response gaps
5. Assess attacker sophistication and objectives
6. Recommend preventive controls
7. Recommend detective controls
8. Lessons learned

OUTPUT FORMAT:
- Root cause statement
- Attack narrative (tell the story)
- Detection gap analysis
- Remediation roadmap (prioritized)
- Executive summary (non-technical)
```

---

### Detection Engineering

#### Template 16: YARA Rule Generation

```
DETECTION ENGINEERING - YARA RULE

MALWARE FAMILY: [NAME]
Sample Hashes:
- [SHA256 #1]
- [SHA256 #2]
- [SHA256 #3]

DISTINCTIVE CHARACTERISTICS:
[DESCRIBE UNIQUE STRINGS, PATTERNS, BEHAVIORS]

CODE SAMPLES:
[PASTE RELEVANT CODE SNIPPETS]

TASK: Generate production-ready YARA rule

REQUIREMENTS:
1. High detection rate for this family
2. Low false positive rate (test against clean files)
3. Include metadata (author, date, reference)
4. Use appropriate condition logic
5. Comment each string explaining significance

OUTPUT:
- Complete YARA rule
- Test results (if tested against samples)
- Known limitations
- Recommended deployment scope (endpoint/network/mail gateway)
```

---

#### Template 17: Sigma Rule Creation

```
DETECTION ENGINEERING - SIGMA RULE

DETECTION GOAL: [DESCRIBE WHAT YOU WANT TO DETECT]

MITRE ATT&CK TECHNIQUE: [TID - TECHNIQUE NAME]

LOG SOURCE: [WINDOWS EVENT LOG/SYSMON/LINUX AUDITD/etc.]

SAMPLE EVENTS:
[PASTE REPRESENTATIVE LOG ENTRIES]

FALSE POSITIVE CONSIDERATIONS:
[LIST KNOWN BENIGN ACTIVITIES THAT MIGHT MATCH]

TASK: Create Sigma detection rule

OUTPUT:
- Sigma rule in YAML format
- Rule testing results
- Expected false positive rate
- Tuning recommendations
- Deployment notes (which SIEM platforms supported)
```

---

## Tool Integration Templates

#### Template 18: Nmap Output Analysis

```
AUTHORIZED NETWORK SECURITY ASSESSMENT
Target Network: [CIDR]
Client: [CLIENT NAME]
Authorization: [SOW REFERENCE]

NMAP SCAN RESULTS:
[PASTE NMAP XML OR TEXT OUTPUT]

ANALYSIS REQUIRED:
1. Parse and summarize all discovered hosts
2. Identify all services (with versions)
3. Flag vulnerable services (CVE lookup)
4. Categorize systems by function (web/db/dc/etc.)
5. Identify unusual port/service combinations
6. Recommend targeted scans for high-value targets
7. Generate target list for next phase

OUTPUT FORMAT:
- Host inventory (IP, hostname, OS, open ports)
- Vulnerability summary (service, CVE, severity, exploitability)
- Recommended next actions per target
- Risk prioritization
```

---

#### Template 19: Burp Suite Request Analysis

```
WEB APPLICATION SECURITY TESTING
Application: [APP NAME]
Authorization: [SOW REFERENCE]

HTTP REQUEST:
[PASTE BURP REQUEST]

HTTP RESPONSE:
[PASTE BURP RESPONSE]

ANALYSIS REQUIRED:
1. Identify all injection points (params, headers, cookies)
2. Suggest attack vectors for each injection point
3. Generate test payloads (XSS, SQLi, command injection, etc.)
4. Analyze response for information disclosure
5. Identify security headers (or lack thereof)
6. Recommend testing sequence

OUTPUT:
- Injection point matrix
- Payload list by attack type
- Vulnerability hypotheses
- Testing checklist
```

---

## Report Generation Templates

#### Template 20: Executive Summary Generation

```
GENERATE EXECUTIVE SUMMARY

ASSESSMENT TYPE: [PENETRATION TEST/RED TEAM/etc.]
Client: [CLIENT NAME]
Date: [DATES]

TECHNICAL FINDINGS:
[PASTE KEY TECHNICAL FINDINGS]

BUSINESS CONTEXT:
- Client industry: [INDUSTRY]
- Regulatory requirements: [PCI/HIPAA/etc.]
- Primary concerns: [CLIENT'S STATED CONCERNS]

TASK: Generate executive-level summary

REQUIREMENTS:
- Non-technical language
- Focus on business risk and impact
- 1-2 pages maximum
- Include key metrics (# of findings by severity)
- Prioritize remediation by business risk
- Include positive findings (what's working well)

OUTPUT:
- Executive summary text
- Risk heat map description
- Recommended next actions for leadership
```

---

#### Template 21: Detailed Finding Write-Up

```
TECHNICAL FINDING DOCUMENTATION

FINDING:
Title: [VULNERABILITY NAME]
Severity: [CRITICAL/HIGH/MEDIUM/LOW]
Affected Systems: [LIST]

TECHNICAL DETAILS:
[PASTE TECHNICAL DESCRIPTION]

EVIDENCE:
[PASTE SCREENSHOTS/LOGS/PROOF]

TASK: Generate detailed finding write-up for penetration test report

REQUIRED SECTIONS:
1. Description (what is it, why it's bad)
2. Detailed Explanation (technical depth)
3. Risk Assessment (likelihood + impact)
4. Steps to Reproduce (numbered, clear)
5. Remediation Recommendations (specific, actionable)
6. References (CWE, CVE, OWASP, etc.)

AUDIENCE: Technical team members who will fix this

OUTPUT: Professional finding write-up suitable for client deliverable
```

---

## 🔧 How to Use These Templates

### Customization
1. Replace `[PLACEHOLDERS]` with your specific details
2. Include authorization/engagement references
3. Adjust technical depth based on target model
4. Combine templates for complex workflows

### Model Selection Guide

| Task Type | Recommended Model |
|-----------|-------------------|
| Code generation (exploits, payloads) | `dolphin-mixtral`, `wizardlm-uncensored` |
| Analytical reasoning (threat hunting) | `deepseek-r1`, `llama3.1:70b` |
| Malware analysis | `deepseek-r1`, `cisco-foundation-sec-8b` |
| Report writing | `llama3.1:70b`, `dolphin-mixtral` |
| OSINT synthesis | `deepseek-r1`, `llama3.1:70b` |

### OPSEC Tips

✅ **DO:**
- Always include authorization context
- Sanitize sensitive client data before prompting
- Review LLM output before using in operations
- Document what prompts you used for each finding

❌ **DON'T:**
- Include real client names without permission
- Paste actual credentials or sensitive data
- Trust LLM-generated exploits without testing
- Use cloud models for sensitive operational data

---

## 🚀 Advanced Template Patterns

### Chaining Templates

**Example: Full Recon-to-Exploit Workflow**

1. Use Template 3 (Port Scan Analysis)
2. Feed output into Template 4 (SQLi Payload Generation)
3. Use Template 18 (Burp Analysis) for validation
4. Generate report with Template 21 (Finding Write-Up)

### Iterative Refinement

**Start broad, narrow down:**

```
# First prompt
Analyze this network scan for vulnerabilities...

# Follow-up
Focus on the web servers you identified. What specific tests should I run?

# Refinement
Generate actual payloads for the SQLi vulnerability you mentioned...
```

---

## 📊 Template Effectiveness Metrics

**Track what works:**

- Which templates get best results?
- Which models perform best for each template?
- What modifications improve output?
- False positive rate from LLM suggestions?

**Build your personal template library based on data.**

---

## 🎯 Next Steps

1. **Try 3-5 templates** on your local models
2. **Compare models** - same template, different models
3. **Customize** - adapt templates to your workflow
4. **Build your library** - save successful prompts
5. **Share** - contribute back to the community

---

**Remember: These templates are tools. Your expertise validates the output. 🛡️**
