# Local LLMs Workshop
## Uncensored and Offline: Models That Do What You Ask Without Asking Why

**Workshop for Hacker Conventions | 60 Minutes**

---

## 🎯 Workshop Overview

This hands-on workshop teaches security professionals how to deploy, configure, and operationalize local LLMs for offensive and defensive security work. Learn why "cognitive OPSEC" matters, how to run uncensored models locally, and build agentic workflows that never phone home.

**Key Outcomes:**
- Understand OPSEC risks of cloud AI for security work
- Deploy and configure local LLMs (Ollama, LM Studio)
- Select and run uncensored models for red/blue team tasks
- Build MCP-based agents with web search and command execution
- Secure your local AI stack against emerging threats

---

## ⚠️ LEGAL & ETHICAL DISCLAIMER

**READ THIS BEFORE PROCEEDING:**

This workshop covers techniques and tools for authorized security testing only. All exercises assume:

- ✅ **Authorized penetration testing** with written permission
- ✅ **Red team operations** within scope of engagement
- ✅ **CTF competitions** and sanctioned hacking challenges
- ✅ **Security research** on systems you own or have explicit permission to test
- ✅ **Defensive security** and threat hunting on authorized networks

**PROHIBITED USE:**
- ❌ Unauthorized access to computer systems
- ❌ Malicious exploitation of vulnerabilities
- ❌ Development of malware for distribution
- ❌ Any activity violating CFAA or applicable laws

By participating in this workshop, you agree to use these skills ethically and legally. The instructor and workshop organizers are not responsible for misuse of these techniques.

**"With great power comes great responsibility. Use your skills to make security better, not worse."**

---

## 🔒 The OPSEC Problem Nobody Talks About

Every cloud AI prompt is **LOGGED**:
- Full prompt text, timestamps, API key identity
- Query volume, timing patterns, metadata
- Even "zero-retention" providers retain metadata

**Think about what's in your security prompts:**
- Target hostnames, internal IP schemas
- Vulnerability findings, client names, exploit chains
- Malware samples you're analyzing

**"Cognitive OPSEC" (SEVN-X, 2026):**
> A single well-structured prompt can reveal an entire campaign's methodology to whoever holds the log.

Cloud models also **REFUSE** at the worst possible moment:
- Exploit code, shellcode, phishing templates, payloads

**The Solution:** Local models that never phone home.

---

## 📋 Prerequisites

**Before the Workshop:**

### Required Software (Install Before Arriving)
- **Ollama** - [ollama.com](https://ollama.com) - CLI model management
- **LM Studio** - [lmstudio.ai](https://lmstudio.ai) - GUI for model management
- **Git** - For cloning repositories
- **Python 3.10+** - For MCP setup

### Recommended Models to Pre-Download (Multi-GB!)
```bash
# Download these BEFORE the workshop (saves bandwidth)
ollama pull llama3.1:70b           # ~40GB - General purpose
ollama pull dolphin-mixtral        # ~26GB - Uncensored
ollama pull deepseek-r1            # ~37GB - Security reasoning
```

### Hardware Requirements
- **Minimum:** 16GB RAM, 8GB VRAM (for 8B models)
- **Recommended:** 32GB RAM, 24GB VRAM (for 34B models)
- **Optimal:** 64GB+ unified RAM (Apple Silicon) or 48GB+ VRAM (for 70B models)

**Don't have hardware?** You can still follow along conceptually and run exercises later.

---

## 📚 Workshop Materials

| File | Description |
|------|-------------|
| `exercises.md` | Hands-on labs: model setup, MCP agents, security tasks |
| `model-templates.md` | Prompt templates for red/blue team operations |
| `local-framework.md` | L.O.C.A.L. methodology for secure local AI deployment |
| `solutions.md` | Example solutions and configuration files |
| `resources.md` | Tools, models, integrations, and further reading |

---

## ⏱️ Workshop Schedule (60 Minutes)

### Introduction & OPSEC Case (5 min)
- Why cloud AI is an OPSEC risk for security professionals
- Real-world examples of prompt logging exposing operations
- The case for local, uncensored models

### Setup Verification (5 min)
- Verify Ollama and LM Studio installations
- Check downloaded models
- Test basic inference

### Core Concepts (10 min)
- **Hardware & quantization:** VRAM requirements, Q4_K_M sweet spot
- **Local vs Cloud decision framework:** When to use each
- **Uncensored models:** Dolphin, WizardLM, Pentester variants
- **Model selection:** 8B vs 34B vs 70B for security tasks

### Hands-On Lab 1: Uncensored Models for Security Tasks (15 min)
- Load and test uncensored models
- Compare cloud refusal vs local compliance
- Red team prompts: exploit scaffolding, payload generation
- Blue team prompts: malware analysis, YARA rules

### Hands-On Lab 2: MCP Agent Setup (15 min)
- Install Model Context Protocol (MCP)
- Configure web search MCP server
- Configure system command execution MCP server
- Build agentic workflow for OSINT + recon

### Security & Best Practices (5 min)
- Defending your local stack
- Model weight security
- Prompt injection via log pipelines
- Testing your AI deployment (Garak, PyRIT)

### Wrap-Up & Resources (5 min)
- L.O.C.A.L. framework review
- Next steps and advanced integrations
- Community resources

---

## 🚀 Quick Start

1. **Verify Prerequisites**
   ```bash
   ollama --version
   # Should return version info

   ollama list
   # Should show downloaded models
   ```

2. **Test Basic Inference**
   ```bash
   ollama run dolphin-mixtral "Write a Python function to parse Nmap XML output"
   ```

3. **Open Workshop Materials**
   - Start with `exercises.md` for hands-on labs
   - Reference `model-templates.md` for security-focused prompts
   - Follow `local-framework.md` for L.O.C.A.L. methodology

---

## 🎓 The L.O.C.A.L. Framework

A systematic methodology for secure local AI deployment:

- **L** - **Locality:** Keep sensitive data on-premises
- **O** - **Operational Security:** Protect your AI infrastructure
- **C** - **Capability Selection:** Choose the right model for each task
- **A** - **Agent Integration:** Build MCP-based autonomous workflows
- **L** - **Legal/Ethical:** Ensure authorized testing only

*See `local-framework.md` for detailed methodology*

---

## 🛡️ Security-First Approach

This workshop emphasizes:
- **Privacy:** No data leaves your machine
- **OPSEC:** No logging, no telemetry, no cloud calls
- **Control:** You own the model weights and infrastructure
- **Compliance:** ITAR, sovereignty, air-gap requirements met

---

## 🏆 Post-Workshop Challenge

**The 30-Day Local AI Security Sprint:**

1. **Week 1:** Set up local stack (Ollama + LM Studio + MCP)
2. **Week 2:** Integrate with security tools (Burp, Wazuh, etc.)
3. **Week 3:** Build custom MCP servers for your workflow
4. **Week 4:** Red team your own deployment, document findings

Share your results with the community!

---

## 🤝 Contributing

Found a better model? Built a cool MCP server? Share it!

1. Fork this repository
2. Add your configurations or improvements
3. Submit a pull request
4. Help the community level up

---

## 📖 Additional Resources

- [Ollama Documentation](https://ollama.com)
- [LM Studio Guide](https://lmstudio.ai)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [Uncensored Models List](https://ollama.com/search?q=uncensored)

See `resources.md` for comprehensive list of tools, integrations, and research.

---

## 💬 Feedback & Questions

- Open an issue for questions or suggestions
- Share your local AI security workflows
- Connect with the offensive/defensive AI community

---

## 🔗 Quick Links

- **Ollama Library:** [ollama.com/library](https://ollama.com/library)
- **Dolphin Models:** [ollama.com/library/dolphin-mixtral](https://ollama.com/library/dolphin-mixtral)
- **Pentester Model:** [ollama.com/xploiter/pentester](https://ollama.com/xploiter/pentester)
- **MCP Marketplace:** [mcpmarket.com](https://mcpmarket.com)
- **Wazuh MCP:** [github.com/wazuh/wazuh-mcp-server](https://github.com/wazuh/wazuh-mcp-server)

---

## ⚡ Key Takeaways

> **"The model doesn't need to phone home. Neither does your tradecraft."**

- Local models are **production-ready** (Wazuh, Splunk, Elastic ship integrations)
- Capability gap is **closing** (70B Q4 handles most security tasks adequately)
- **Hybrid posture wins:** Local for sensitive work, frontier for complex reasoning on sanitized data

---

**Ready to take control of your AI-assisted security work? Let's dive in! 🚀**

Start with `exercises.md` and begin the hands-on challenges.

---

**Workshop Version:** 1.0
**Last Updated:** May 2026
**Presented at:** CYBR HAK CON 2026 - AI Village
