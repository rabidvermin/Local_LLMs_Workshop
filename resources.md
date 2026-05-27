# Local LLM Resources for Security Professionals
## Tools, Models, Integrations, and References

**Last Updated: May 2026**

---

## 📑 Table of Contents

- [Local LLM Platforms](#local-llm-platforms)
- [Security-Focused Models](#security-focused-models)
- [Red Team Tools & Integrations](#red-team-tools--integrations)
- [Blue Team Tools & Integrations](#blue-team-tools--integrations)
- [MCP Ecosystem](#mcp-ecosystem)
- [Security Testing Tools](#security-testing-tools)
- [Hardware Recommendations](#hardware-recommendations)
- [Research & Papers](#research--papers)
- [Communities & Forums](#communities--forums)
- [Legal & Compliance](#legal--compliance)

---

## Local LLM Platforms

### Ollama (Recommended)

**Website:** [ollama.com](https://ollama.com)
**GitHub:** [github.com/ollama/ollama](https://github.com/ollama/ollama)

**Why Ollama:**
- CLI-first interface (perfect for automation)
- OpenAI-compatible API endpoint
- One command to download and run any model
- Excellent model library with security-focused variants
- Active community and frequent updates

**Installation:**
```bash
# Linux
curl -fsSL https://ollama.com/install.sh | sh

# macOS
brew install ollama

# Windows
winget install Ollama.Ollama
```

**Essential Commands:**
```bash
ollama list              # List installed models
ollama pull <model>      # Download a model
ollama run <model>       # Run interactive session
ollama serve             # Start API server
ollama rm <model>        # Remove model
```

---

### LM Studio

**Website:** [lmstudio.ai](https://lmstudio.ai)

**Why LM Studio:**
- Beautiful GUI for non-technical users
- Visual hardware monitoring
- Model discovery browser
- Easy model comparison
- Built-in chat interface

**Best For:**
- Analysts who prefer GUI over CLI
- Model testing and comparison
- Quick demonstrations
- Team members new to local LLMs

---

### GPT4All

**Website:** [gpt4all.io](https://gpt4all.io)
**GitHub:** [github.com/nomic-ai/gpt4all](https://github.com/nomic-ai/gpt4all)

**Why GPT4All:**
- Privacy-focused
- Runs on CPU (no GPU required)
- Local document search (RAG built-in)
- Cross-platform desktop app

**Best For:**
- Lower-end hardware
- Document analysis workflows
- Privacy-critical environments

---

### llama.cpp

**GitHub:** [github.com/ggerganov/llama.cpp](https://github.com/ggerganov/llama.cpp)

**Why llama.cpp:**
- Low-level control
- Maximum performance optimization
- Cross-platform (runs everywhere)
- Foundation for many other tools

**Best For:**
- Advanced users
- Custom integrations
- Embedded deployments
- Performance tuning

---

## Security-Focused Models

### Uncensored General Models

#### Dolphin (Mixtral-based)

**Ollama:** `ollama pull dolphin-mixtral`
**HuggingFace:** [huggingface.co/cognitivecomputations/dolphin-mixtral](https://huggingface.co/cognitivecomputations/dolphin-mixtral)

**Creator:** Eric Hartford (Cognitive Computations)
**Size:** ~26GB (Q4), 47GB (FP16)
**VRAM:** 24GB+ recommended

**Strengths:**
- Uncensored (alignment filtering removed)
- Excellent coding capability
- Strong reasoning
- Refuses nothing (use responsibly)

**Use Cases:**
- Exploit code generation
- Payload development
- Tool scripting
- Red team assistance

---

#### WizardLM-Uncensored

**Ollama:** `ollama pull wizard-vicuna-uncensored`
**HuggingFace:** [huggingface.co/TheBloke/WizardLM-Uncensored-GGUF](https://huggingface.co/TheBloke/WizardLM-Uncensored-GGUF)

**Size:** ~12GB (7B Q4)
**VRAM:** 8GB

**Strengths:**
- Coding without filters
- Smaller footprint than Dolphin
- Fast inference

**Use Cases:**
- Lower-VRAM systems
- Quick exploit prototyping
- Script generation

---

### Security-Specific Models

#### DeepSeek-R1 (Security Reasoning)

**Ollama:** `ollama pull deepseek-r1`
**Website:** [deepseek.com](https://deepseek.com)

**Size:** ~37GB (Q4)
**VRAM:** 32GB+ recommended

**Strengths:**
- #1 security reasoning benchmark (2026)
- Explainable reasoning traces
- Excellent malware analysis
- Strong threat modeling

**Use Cases:**
- Malware behavior analysis
- Threat hunting hypothesis generation
- Root cause analysis
- Complex security research

**Benchmark:**
- 94% recall on malware scenarios
- 89% on offensive security tasks (Cybench)

---

#### Cisco Foundation-Sec-8B

**Ollama:** `ollama pull cisco-foundation-sec-8b`
**HuggingFace:** [huggingface.co/cisco-ai/foundation-sec-8b](https://huggingface.co/cisco-ai/foundation-sec-8b)

**Size:** ~8GB (Q4)
**VRAM:** 8GB

**Strengths:**
- Built for SOC deployment
- Fine-tuned on security data
- Generates reasoning traces
- SIEM-friendly outputs

**Use Cases:**
- Threat hunting
- Log analysis
- Alert triage
- Detection rule generation

---

#### SIEM-LLAMA-3.1 (Wazuh-Specific)

**Ollama:** `ollama pull mranv/siem-llama-3.1`
**GitHub:** [github.com/mranv/siem-llama](https://github.com/mranv/siem-llama)

**Size:** ~5GB (8B Q4)
**VRAM:** 8GB

**Strengths:**
- Wazuh-specific fine-tune
- Understanding of Wazuh rule syntax
- Alert correlation
- Investigation playbooks

**Use Cases:**
- Wazuh SIEM analysis
- Automated alert enrichment
- Playbook generation

---

#### Xploiter/Pentester

**Ollama:** `ollama pull xploiter/pentester`
**HuggingFace:** [huggingface.co/xploiter/pentester](https://huggingface.co/xploiter/pentester)

**Size:** ~16GB (Q4)
**VRAM:** 16GB

**Strengths:**
- Purpose-built for penetration testing
- Pentest methodology knowledge
- Vulnerability analysis
- Tool guidance
- Report generation assistance

**Use Cases:**
- Penetration testing assistance
- Vulnerability assessment
- Security report writing
- Methodology guidance

---

### Model Selection Quick Reference

| Model | Size | VRAM | Best For |
|-------|------|------|----------|
| `wizard-vicuna-uncensored` | 12GB | 8GB | Quick coding, low VRAM |
| `cisco-foundation-sec-8b` | 8GB | 8GB | SOC/blue team, SIEM analysis |
| `xploiter/pentester` | 16GB | 16GB | Pentesting methodology |
| `dolphin-mixtral` | 26GB | 24GB | General security, coding |
| `deepseek-r1` | 37GB | 32GB | Advanced reasoning, malware analysis |
| `llama3.1:70b` | 48GB | 48GB | Best quality, complex tasks |

---

## Red Team Tools & Integrations

### Burp Suite Extensions

#### BurpGPT

**GitHub:** [github.com/aress31/burpgpt](https://github.com/aress31/burpgpt)

**Features:**
- Local Ollama endpoint support
- Real-time injection point analysis
- Payload suggestions
- Request/response analysis

**Setup:**
```
1. Download .jar from releases
2. Burp → Extensions → Add
3. Configure endpoint: http://localhost:11434/api/generate
4. Select model: dolphin-mixtral
```

---

#### Burpference (Black Hills InfoSec)

**Website:** [blackhillsinfosec.com](https://www.blackhillsinfosec.com/projects/burpference/)

**Features:**
- Forwards in-scope HTTP to local model
- Vulnerability hypothesis generation
- Works with RTX 3090-class hardware

---

#### Ollama-Pentesting-AI

**GitHub:** [github.com/steveschofield/ollama-pentesting-ai](https://github.com/steveschofield/ollama-pentesting-ai)

**Features:**
- Full Burp plugin
- Multi-vector payload suggestions
- Uncensored local models
- Customizable prompts

---

### Penetration Testing Frameworks

#### PentestGPT

**GitHub:** [github.com/hackerai-tech/PentestGPT](https://github.com/hackerai-tech/PentestGPT)

**Description:**
Reasoning layer over pentest tool output (Nmap, Nuclei, Burp, scanners)

**Features:**
- Routes to local models via Ollama or LM Studio
- Docker-first deployment
- Session persistence across engagements
- Tool orchestration

**Installation:**
```bash
git clone https://github.com/hackerai-tech/PentestGPT.git
cd PentestGPT
docker-compose up -d
# Configure to use http://ollama:11434
```

---

#### Pentest-AI

**GitHub:** [github.com/0xSteph/pentest-ai](https://github.com/0xSteph/pentest-ai)

**Features:**
- 197+ tool integrations (Burp, SQLMap, Nuclei, exploit frameworks)
- Fully offline via Ollama
- Exploit chaining
- PoC validation
- Zero cloud calls

**Installation:**
```bash
git clone https://github.com/0xSteph/pentest-ai.git
cd pentest-ai
pip install -r requirements.txt
# Configure Ollama endpoint in config.yaml
```

---

#### CAI - Cybersecurity AI

**GitHub:** [github.com/aliasrobotics/cai](https://github.com/aliasrobotics/cai)

**Features:**
- Multi-agent orchestration
- Full Ollama local support
- Bug-bounty-ready workflows
- Authorized testing compliance

---

### OSINT & Recon Tools

#### Penligent PentestAI

**Website:** [penligent.ai](https://penligent.ai)

**Features:**
- 200+ recon tools orchestrated by LLM
- Evidence-grade logging
- NIST 800-53 aligned
- Local LLM synthesis layer

---

#### RagIntel (MITRE ATT&CK RAG)

**GitHub:** [github.com/cxnturi0n/ragintel](https://github.com/cxnturi0n/ragintel)

**Features:**
- RAG over MITRE ATT&CK framework
- Plain English → technique + detection query
- Local LLM backend
- Threat hunting assistance

**Installation:**
```bash
git clone https://github.com/cxnturi0n/ragintel.git
cd ragintel
pip install -r requirements.txt
ollama pull llama3.1:8b
python main.py
```

---

## Blue Team Tools & Integrations

### SIEM Platforms

#### Wazuh 4.12.0+

**Website:** [wazuh.com](https://wazuh.com)
**Docs:** [documentation.wazuh.com](https://documentation.wazuh.com)

**LLM Features (Native):**
- LLM threat hunting via Ollama + LLaMA 3
- Plain-English queries: "Who tried to exfiltrate files last week?"
- Vectorized log RAG
- LOLBin detection via semantic analysis

**MCP Server:**
**GitHub:** [github.com/wazuh/wazuh-mcp-server](https://github.com/wazuh/wazuh-mcp-server)

**Setup:**
```bash
npm install -g @wazuh/mcp-server

# Configure in ~/.config/mcp/config.json
{
  "mcpServers": {
    "wazuh": {
      "command": "npx",
      "args": [
        "@wazuh/mcp-server",
        "--api-url", "http://localhost:55000",
        "--username", "wazuh",
        "--password", "wazuh"
      ]
    }
  }
}
```

---

#### Splunk DSDL 5.2

**Website:** [splunk.com](https://www.splunk.com/)
**Docs:** [Deep Learning Toolkit](https://splunkbase.splunk.com/app/4607/)

**LLM Features:**
- Local LLM inference INSIDE Splunk (data never traverses network)
- Tested: LLaMA3-8B, Gemma-7B, Mistral-7B
- Sub-2s average response time
- RAG over 1,800+ ESCU detection rules
- Generates Sigma/SPL rules aligned to MITRE ATT&CK

---

#### Elastic Security

**Website:** [elastic.co/security](https://www.elastic.co/security)
**Docs:** [Elastic AI Documentation](https://www.elastic.co/guide/en/security/current/ai-assistant.html)

**LLM Features:**
- Bring-your-own local LLM endpoint (vLLM or Ollama)
- Agentic triage-to-response workflows
- Data never leaves the network
- Security assistant for analysts

**Configuration:**
```yaml
# elasticsearch.yml
xpack.ml.enabled: true

# Configure Ollama endpoint
action.ai.ollama.url: "http://localhost:11434"
```

---

### Threat Hunting & Analysis

#### CABTA - Blue Team Assistant

**GitHub:** [github.com/ugurrates/Blue-Team-Assistant](https://github.com/ugurrates/Blue-Team-Assistant)

**Features:**
- Fully local-first SOC platform via Ollama
- 20+ threat intel sources
- Malware analysis
- Email forensics
- IOC enrichment

**Installation:**
```bash
git clone https://github.com/ugurrates/Blue-Team-Assistant.git
cd Blue-Team-Assistant
docker-compose up -d
```

---

## MCP Ecosystem

### Official MCP Servers

**Model Context Protocol:** [modelcontextprotocol.io](https://modelcontextprotocol.io)

#### Web Search (DuckDuckGo)

```bash
npm install -g @modelcontextprotocol/server-duckduckgo
```

**Use cases:** OSINT, CVE lookup, threat intel

---

#### Filesystem

```bash
npm install -g @modelcontextprotocol/server-filesystem
```

**Use cases:** Log analysis, evidence collection, report generation

---

#### GitHub

```bash
npm install -g @modelcontextprotocol/server-github
```

**Use cases:** Code review, vulnerability scanning, issue tracking

---

#### SQLite

```bash
npm install -g @modelcontextprotocol/server-sqlite
```

**Use cases:** Database queries, IOC tracking, case management

---

### Security-Specific MCP Servers

#### Custom Command Execution

See `solutions.md` for full implementation.

**Use cases:** Nmap, dig, whois, openssl, etc.

---

#### FastMCP (Build Your Own)

**GitHub:** [github.com/jlowin/fastmcp](https://github.com/jlowin/fastmcp)

**Description:** Wrap any Python function as an MCP tool in 5 minutes

**Example:**
```python
from fastmcp import FastMCP

mcp = FastMCP("threat-intel")

@mcp.tool()
def lookup_ip(ip: str) -> str:
    """Look up IP in threat intelligence databases"""
    # Your implementation here
    return f"Threat intel for {ip}"

if __name__ == "__main__":
    mcp.run()
```

---

### MCP Marketplace

**Website:** [mcpmarket.com](https://mcpmarket.com)

**Description:** Community marketplace for MCP servers

**Notable Security MCPs:**
- VirusTotal integration
- Shodan search
- MISP threat sharing
- OSINT framework tools

---

## Security Testing Tools

### AI Red Teaming Tools

#### Garak

**GitHub:** [github.com/leondz/garak](https://github.com/leondz/garak)

**Description:** LLM vulnerability scanner

**Features:**
- Prompt injection testing
- Jailbreak detection
- Data leakage probes
- Insecure output testing
- CLI-driven, extensible

**Installation:**
```bash
pip install garak

# Test your local model
garak --model-type ollama --model-name dolphin-mixtral
```

---

#### PyRIT (Microsoft)

**GitHub:** [github.com/Azure/PyRIT](https://github.com/Azure/PyRIT)

**Description:** Python Risk Identification Toolkit for LLMs

**Features:**
- Orchestrates LLM attack suites
- Targets local or cloud models
- Used by enterprise red teams
- Comprehensive attack library

**Installation:**
```bash
git clone https://github.com/Azure/PyRIT.git
cd PyRIT
pip install -r requirements.txt
```

---

#### Promptfoo

**GitHub:** [github.com/promptfoo/promptfoo](https://github.com/promptfoo/promptfoo)
**Website:** [promptfoo.dev](https://www.promptfoo.dev)

**Description:** CLI + CI/CD integration for prompt security testing

**Features:**
- Automated adversarial testing
- Used internally by OpenAI and Anthropic
- Test every model update
- Regression detection

**Installation:**
```bash
npm install -g promptfoo

# Create test config
promptfoo init

# Run tests
promptfoo eval
```

---

#### DeepTeam

**GitHub:** [github.com/confident-ai/deepteam](https://github.com/confident-ai/deepteam)

**Description:** Open-source AI red teaming platform

**Features:**
- Runs entirely locally
- Tests RAG pipelines, chatbots, agents, base models
- Covers indirect prompt injection via retrieved context
- Comprehensive reporting

---

## Hardware Recommendations

### Consumer Hardware

#### Entry Level (8B Models)

**GPU Options:**
- NVIDIA RTX 3060 (12GB) - $300
- NVIDIA RTX 3070 (8GB) - $400
- AMD RX 6800 (16GB) - $450

**Apple Silicon:**
- M1 Mac Mini (16GB) - $699
- M2 MacBook Air (24GB) - $1,699

**Use Cases:**
- Testing and learning
- Lightweight analysis tasks
- Cisco-foundation-sec-8b, wizard-vicuna-uncensored

---

#### Mid-Range (34B Models)

**GPU Options:**
- NVIDIA RTX 4090 (24GB) - $1,599
- NVIDIA RTX A5000 (24GB) - $2,500

**Apple Silicon:**
- M2 Pro Mac Studio (64GB) - $3,999
- M3 Max MacBook Pro (64GB) - $4,999

**Use Cases:**
- Most security tasks
- Dolphin-mixtral, xploiter/pentester
- Production SOC deployment

---

#### High-End (70B+ Models)

**GPU Options:**
- NVIDIA RTX A6000 (48GB) - $4,500
- NVIDIA A100 (80GB) - $10,000+
- Multi-GPU setups (2x RTX 4090) - $3,200

**Apple Silicon:**
- Mac Studio M2 Ultra (192GB) - $6,999

**Use Cases:**
- Complex reasoning tasks
- LLama3.1:70b, deepseek-r1
- High-volume production environments

---

### Server Deployments

**Recommended Platforms:**
- Dell PowerEdge with NVIDIA A100
- Supermicro GPU servers
- Lambda Labs GPU cloud (if air-gap not required)

**Considerations:**
- Power and cooling requirements
- Network bandwidth for distributed inference
- Redundancy for production SIEMs

---

## Research & Papers

### Foundational Papers

1. **"Language Models are Few-Shot Learners"** (GPT-3)
   - Brown et al., 2020
   - [arxiv.org/abs/2005.14165](https://arxiv.org/abs/2005.14165)

2. **"LLaMA: Open and Efficient Foundation Language Models"**
   - Touvron et al., 2023
   - [arxiv.org/abs/2302.13971](https://arxiv.org/abs/2302.13971)

3. **"Mixtral of Experts"**
   - Jiang et al., 2024
   - [arxiv.org/abs/2401.04088](https://arxiv.org/abs/2401.04088)

---

### Security-Specific Research

4. **"Cybersecurity AI Benchmarks (Cybench)"**
   - 2026 evaluation framework
   - [arxiv.org/abs/2602.xxxxx](https://arxiv.org) (placeholder)
   - Key finding: 93% task success rate in offensive security (Feb 2026)

5. **"Prompt Injection Attacks in Production LLM Deployments"**
   - 73% vulnerability rate documented
   - March 2026 research

6. **"Fine-Tuning Supply Chain Attacks on LLMs"**
   - Poisoned training data backdoors
   - Documented March 2026

7. **"Cognitive OPSEC: Prompt Logging as Intelligence Leakage"**
   - SEVN-X, 2026
   - Analysis of operational security risks in cloud AI usage

---

### Security Tool Papers

8. **"Garak: A Framework for Security Probing Large Language Models"**
   - Leon Derczynski et al.
   - [arxiv.org/abs/2406.11036](https://arxiv.org/abs/2406.11036)

9. **"PyRIT: Python Risk Identification Toolkit for Generative AI"**
   - Microsoft Security Research

---

## Communities & Forums

### Reddit

- [r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/) - Local LLM community
- [r/netsec](https://www.reddit.com/r/netsec/) - Network security
- [r/AskNetsec](https://www.reddit.com/r/AskNetsec/) - Security questions

---

### Discord Servers

- **Ollama Discord** - Official community
- **LM Studio Discord** - Model discussions
- **LocalLLaMA Discord** - Technical help
- **AI Security Discord** - Security-focused AI discussions

---

### GitHub Organizations

- [Cognitive Computations](https://github.com/cognitivecomputations) - Dolphin models
- [TheBloke](https://github.com/TheBloke) - Quantized models (legacy, now integrated into HF)
- [Ollama](https://github.com/ollama) - Official Ollama org

---

### Twitter/X Follows

- @eric_hartford - Dolphin creator
- @ollama_ai - Ollama updates
- @deepseek_ai - DeepSeek models
- @wazuh - Wazuh SIEM updates

---

## Legal & Compliance

### Regulations to Know

**United States:**
- **CFAA** (Computer Fraud and Abuse Act) - Unauthorized access laws
- **DMCA** - Digital Millennium Copyright Act (reverse engineering)
- **ITAR** - International Traffic in Arms Regulations (data sovereignty)

**European Union:**
- **GDPR** - General Data Protection Regulation (data privacy)
- **NIS2 Directive** - Network and Information Security
- **AI Act** (2024+) - Regulation of high-risk AI systems

**International:**
- **Budapest Convention** - Cybercrime treaty (48 countries)

---

### Compliance Frameworks

**SOC 2** - Service Organization Control 2
- Relevant for vendors providing security services
- Controls around data security and privacy

**ISO 27001** - Information Security Management
- International standard for ISMS
- Covers AI system security

**NIST Cybersecurity Framework**
- Identify, Protect, Detect, Respond, Recover
- AI security controls guidance (2025+)

**NIST AI Risk Management Framework**
- [nist.gov/itl/ai-risk-management-framework](https://www.nist.gov/itl/ai-risk-management-framework)
- Managing risks of AI systems

---

### Penetration Testing Standards

**PTES** - Penetration Testing Execution Standard
- [pentest-standard.org](http://www.pentest-standard.org)
- Industry framework for pentest methodology

**OWASP Testing Guide**
- [owasp.org/www-project-web-security-testing-guide/](https://owasp.org/www-project-web-security-testing-guide/)
- Web application security testing

**OSSTMM** - Open Source Security Testing Methodology Manual
- Comprehensive security testing methodology

---

## Quick Reference Cards

### Model Download Cheat Sheet

```bash
# Uncensored general models
ollama pull dolphin-mixtral           # 26GB - Best all-around uncensored
ollama pull wizard-vicuna-uncensored  # 12GB - Lightweight uncensored

# Security-specific
ollama pull deepseek-r1               # 37GB - Security reasoning #1
ollama pull cisco-foundation-sec-8b   # 8GB - SOC/SIEM optimized
ollama pull xploiter/pentester        # 16GB - Pentesting methodology
ollama pull mranv/siem-llama-3.1      # 5GB - Wazuh-specific

# General purpose
ollama pull llama3.1:70b              # 48GB - Highest quality
ollama pull llama3.1:8b               # 5GB - Lightweight
```

---

### Hardware Quick Reference

| Model Size | VRAM Needed | Hardware Examples | Use Case |
|------------|-------------|-------------------|----------|
| 8B | 8GB | RTX 3070, M1 16GB | Testing, light tasks |
| 34B | 24GB | RTX 4090, M2 64GB | Most security work |
| 70B | 48GB | A6000, M2 Ultra 192GB | Complex reasoning |
| 70B+ | 80GB+ | A100, multi-GPU | Production, high-volume |

---

### Tool Integration Matrix

| Tool | Integration | Model Recommendation | Difficulty |
|------|-------------|----------------------|------------|
| Burp Suite | BurpGPT | dolphin-mixtral | Easy |
| Wazuh | Native + MCP | cisco-foundation-sec-8b | Medium |
| Splunk | DSDL | llama3.1:8b | Medium |
| Nmap | MCP command exec | Any | Easy |
| Metasploit | Custom scripts | dolphin-mixtral | Medium |
| Nuclei | PentestGPT | deepseek-r1 | Medium |

---

## Staying Updated

### Newsletters

- **Ollama Newsletter** - Model releases and updates
- **HuggingFace Newsletter** - New model announcements
- **TLDR AI** - Daily AI news (includes security)

### Blogs

- [Ollama Blog](https://ollama.com/blog)
- [Wazuh Blog](https://wazuh.com/blog/)
- [Cisco AI Research Blog](https://research.cisco.com)

### Conferences

- **DEF CON AI Village** - Annual hacker con AI track
- **RSA Conference** - AI security sessions
- **Black Hat** - AI/ML security talks
- **BSides Events** - Local AI security discussions

---

## Contributing

### How to Contribute to This Resource

1. Found a new security-focused model? Add it!
2. Built a custom MCP server? Share it!
3. Discovered better configurations? Document them!
4. Found errors or outdated info? Fix it!

**Submit via:**
- GitHub pull requests
- Community forums
- Workshop feedback forms

---

## Emergency Contacts

### Security Issues with Tools

- **Ollama Security:** security@ollama.com
- **Wazuh Security:** security@wazuh.com
- **Report AI Vulnerabilities:** [CERT/CC](https://www.kb.cert.org/vuls/)

### Responsible Disclosure

If you discover vulnerabilities in any tools listed here:
1. Do NOT publicize before vendor notification
2. Contact vendor security team directly
3. Allow 90 days for patch development
4. Coordinate disclosure date
5. Publish responsibly after patch

---

## 📝 Final Notes

**This is a living document.** The AI security landscape changes rapidly.

**Last major update:** May 2026
**Next scheduled review:** August 2026

**Feedback:** Share improvements with the workshop community!

---

**"The model doesn't need to phone home. Neither does your tradecraft." 🔒**

Use these resources wisely, securely, and ethically.
