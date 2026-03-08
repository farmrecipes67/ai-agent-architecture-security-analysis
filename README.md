<!-- Open Graph Meta Tags -->
<!-- <meta property="og:title" content="On the Exploitability of Autonomous Email-Triggered Code Execution Pipelines: A Security Analysis of the Papersaurus Architecture"> -->
<!-- <meta property="og:description" content="A Nature-style academic paper analyzing security vulnerabilities in autonomous AI agent architectures with email-triggered code execution and tool access."> -->
<!-- <meta property="og:type" content="article"> -->
<!-- <meta property="og:image" content="./assets/papersaurus-threat-model.png"> -->
<!-- <meta property="og:url" content="https://github.com/security-analysis/papersaurus-exploitability"> -->
<!-- <meta property="og:site_name" content="Papersaurus Security Analysis"> -->
<!-- <meta property="article:published_time" content="2025-07-13"> -->
<!-- <meta property="article:author" content="Independent Security Research Collective"> -->
<!-- <meta property="article:section" content="AI Security"> -->
<!-- <meta name="twitter:card" content="summary_large_image"> -->
<!-- <meta name="twitter:title" content="Exploitability of Autonomous Email-Triggered Code Execution Pipelines"> -->
<!-- <meta name="twitter:description" content="Security analysis of the Papersaurus AI agent architecture — abuse vectors, data exfiltration, and prompt injection risks."> -->

---

# 🦕🔓 On the Exploitability of Autonomous Email-Triggered Code Execution Pipelines

### *A Security Analysis of the Papersaurus Architecture*

**A Nature-style academic paper on adversarial risks in agentic AI systems**

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Paper Status](https://img.shields.io/badge/Status-Preprint-orange)]()
[![arXiv](https://img.shields.io/badge/arXiv-2507.XXXXX-b31b1b.svg)]()
[![Responsible Disclosure](https://img.shields.io/badge/Disclosure-Responsible-green)]()

---

## 📌 Project Description

This repository contains the full manuscript, supplementary materials, threat models, and supporting analysis for our paper examining the security implications of **autonomous AI agent architectures that couple email ingestion with code execution and tool access**.

We use the **Papersaurus** system — an AI-powered pipeline that receives email requests, autonomously generates academic-style papers, and executes code with access to external tools — as a concrete case study. While Papersaurus itself is a creative and technically interesting project, its architecture exemplifies a broader class of emerging AI systems that introduce **novel and underexamined attack surfaces**.

This work is intended to be constructive. We do not provide working exploits. Our goal is to formalize the threat landscape, propose mitigations, and contribute to the responsible development of agentic AI systems. We follow responsible disclosure norms and have communicated with relevant parties prior to publication.

---

## 📄 Abstract

The rapid proliferation of autonomous AI agent architectures — systems capable of receiving external input, reasoning over tasks, generating and executing code, and invoking external tools — represents a fundamental shift in the security threat landscape. Unlike traditional software systems where attack surfaces are bounded by well-defined input interfaces, agentic AI systems introduce a class of vulnerabilities in which **natural language itself becomes an attack vector**, and where the boundary between data and instruction is inherently blurred. In this paper, we present a systematic security analysis of one such architecture, **Papersaurus**, an autonomous pipeline that monitors an email inbox, interprets incoming messages as requests to produce academic-style papers, and fulfills those requests through a chain of large language model (LLM) calls, code generation, code execution, and tool invocations. We argue that this architecture — while novel and technically compelling — instantiates a particularly high-risk pattern: **unsolicited external input triggering autonomous code execution with tool access and no human-in-the-loop verification**.

Through structured threat modeling, we identify and taxonomize **seven primary abuse vectors**, including indirect prompt injection via email body and attachments, social engineering of the LLM reasoning process, data exfiltration through tool-mediated side channels, resource exhaustion attacks, supply chain poisoning of downstream dependencies invoked during code execution, and reputation hijacking through the generation of fabricated academic content. For each vector, we characterize the attacker capabilities required, the potential impact severity, and the architectural features that enable exploitation. We demonstrate through analytical argument — without providing working proof-of-concept exploits, consistent with responsible disclosure norms — that **a motivated attacker with no more access than the ability to send an email** could, under plausible conditions, achieve outcomes ranging from unauthorized information disclosure to arbitrary code execution on the host system.

We further contextualize our findings within the broader landscape of agentic AI security, drawing connections to concurrent work on prompt injection, tool-use safety, and the alignment problem as it manifests in deployed systems. We propose a layered mitigation framework encompassing input sanitization, execution sandboxing, output verification, behavioral anomaly detection, and human-in-the-loop checkpoints. Our analysis suggests that the Papersaurus pattern — email-to-code-execution with tool access — is not an isolated curiosity but rather a **harbinger of a common architectural motif** that will recur with increasing frequency as AI agents are deployed in production environments. The security community must develop principled frameworks for reasoning about these systems before their adoption outpaces our ability to secure them.

---

## 🔬 Key Topics Covered

### Threat Taxonomy

| # | Abuse Vector | Severity | Attacker Requirement |
|---|---|---|---|
| 1 | **Indirect Prompt Injection via Email** | 🔴 Critical | Send an email |
| 2 | **Social Engineering of LLM Reasoning** | 🟠 High | Craft persuasive natural language |
| 3 | **Data Exfiltration via Tool Side Channels** | 🔴 Critical | Knowledge of available tools |
| 4 | **Resource Exhaustion & Denial of Service** | 🟡 Medium | Send many emails |
| 5 | **Supply Chain Poisoning of Executed Code** | 🔴 Critical | Poison upstream packages |
| 6 | **Reputation Hijacking via Fabricated Content** | 🟠 High | Send a targeted email |
| 7 | **Chained Multi-Stage Exploitation** | 🔴 Critical | Combine vectors 1–6 |

### In-Depth Analysis Sections

- **§2 — Architecture Decomposition**: Formal specification of the Papersaurus pipeline, including dataflow diagrams, trust boundaries, and privilege analysis at each processing stage.

- **§3 — Prompt Injection as a First-Class Threat**: Analysis of how email content (subject lines, body text, attachments, headers, and even sender display names) can serve as injection vectors when processed by an LLM that conflates data with instruction.

- **§4 — The Tool Access Problem**: Examination of how LLM access to tools (file system operations, web requests, code interpreters, API calls) transforms prompt injection from a *confusion* attack into a *capability* attack.

- **§5 — Social Engineering at Machine Speed**: How attackers can craft emails that manipulate the LLM's reasoning process — exploiting instruction-following tendencies, authority bias, and the absence of adversarial training against email-borne social engineering.

- **§6 — Data Exfiltration Pathways**: Systematic enumeration of how an attacker could extract sensitive information (environment variables, API keys, file system contents, other emails) through legitimate-seeming tool use embedded in generated papers.

- **§7 — The Fabrication Weaponization Problem**: How the ability to generate authoritative-looking academic papers on demand could be exploited for disinformation, credential fraud, or reputational harm to named researchers or institutions.

- **§8 — Mitigation Framework**: A layered defense-in-depth proposal including input sanitization, execution sandboxing (gVisor, Firecracker), output content verification, behavioral anomaly detection, rate limiting, and human-in-the-loop approval gates.

- **§9 — Broader Implications for Agentic AI**: Situating the findings within the larger context of AI safety, the principal-agent problem in LLM systems, and the need for security-by-design in autonomous AI architectures.

---

## 📂 Repository Structure

```
.
├── README.md                          # This file
├── paper/
│   ├── main.tex                       # Full manuscript (LaTeX)
│   ├── main.pdf                       # Compiled PDF
│   ├── figures/
│   │   ├── architecture-diagram.pdf   # Papersaurus pipeline decomposition
│   │   ├── threat-model.pdf           # Attack tree visualization
│   │   ├── kill-chain.pdf             # Multi-stage exploitation kill chain
│   │   └── mitigation-layers.pdf      # Defense-in-depth framework
│   ├── supplementary/
│   │   ├── threat-taxonomy-full.pdf   # Extended threat enumeration
│   │   ├── mitigation-matrix.pdf      # Control mapping to threats
│   │   └── related-work-table.pdf     # Comparative analysis
│   └── bibliography.bib              # References
├── analysis/
│   ├── architecture-notes.md          # Detailed architecture observations
│   ├── dataflow-analysis.md           # Trust boundary analysis
│   └── risk-scoring.md               # CVSS-style risk assessments
├── CITATION.cff                       # Machine-readable citation
├── LICENSE                            # CC BY-NC 4.0
└── RESPONSIBLE-DISCLOSURE.md          # Disclosure policy and timeline
```

---

## 🦖 Dedication

> *For Bruce.*
>
> *Who understood, long before the rest of us, that the most interesting questions live at the boundaries — between systems and their environments, between trust and verification, between what a machine is told to do and what it can be made to do.*
>
> *This one's for you.*

---

## 🤖 AI Disclosure & Acknowledgment

In the interest of full transparency and in accordance with emerging norms for responsible AI-assisted research, we disclose the following:

**This manuscript was produced with substantial assistance from large language model systems.** Specifically:

- **Anthropic Claude Opus 4** — Primary drafting, structural reasoning, threat analysis, and iterative refinement of the manuscript. Claude Opus 4 was used extensively throughout the research and writing process, serving as the principal analytical and compositional engine.

- **OpenAI GPT-5** — Secondary consultation for cross-validation of threat models, alternative framing of mitigation strategies, and adversarial review of draft sections to identify gaps in reasoning.

- **Google Gemini** — Supplementary research assistance, literature survey verification, and comparative analysis with concurrent work in agentic AI security.

All AI-generated content was reviewed, validated, edited, and approved by the human authors. The threat models, risk assessments, and mitigation recommendations reflect the judgment of the research team, informed by but not uncritically dependent upon AI-generated analysis. We affirm that the intellectual direction, ethical framing, responsible disclosure decisions, and final editorial authority rested entirely with human researchers.

We believe that transparent disclosure of AI involvement in research is essential to maintaining scientific integrity and invite the community to adopt similar practices.

---

## 📖 Citation

If you reference this work, please cite:

```bibtex
@article{papersaurus-security-2025,
  title     = {On the Exploitability of Autonomous Email-Triggered Code Execution
               Pipelines: A Security Analysis of the {Papersaurus} Architecture},
  author    = {{Independent Security Research Collective}},
  journal   = {Preprint},
  year      = {2025},
  month     = {July},
  doi       = {10.xxxx/xxxxx},
  url       = {https://github.com/security-analysis/papersaurus-exploitability},
  note      = {Dedicated to Bruce. Preprint under review.}
}
```

**APA Format:**

> Independent Security Research Collective. (2025). On the exploitability of autonomous email-triggered code execution pipelines: A security analysis of the Papersaurus architecture. *Preprint*. https://doi.org/10.xxxx/xxxxx

**Nature Style:**

> Independent Security Research Collective. On the exploitability of autonomous email-triggered code execution pipelines: a security analysis of the Papersaurus architecture. *Preprint* (2025). https://doi.org/10.xxxx/xxxxx

A machine-readable citation file is also available at [`CITATION.cff`](./CITATION.cff).

---

## 📜 License

This work is licensed under the **Creative Commons Attribution-NonCommercial 4.0 International License** ([CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)).

You are free to:
- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material

Under the following terms:
- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made.
- **NonCommercial** — You may not use the material for commercial purposes.

**No working exploit code is included in this repository.** This is a deliberate choice consistent with responsible security research practices. The analysis is intended to inform defensive measures, not to enable attacks.

---

## ⚠️ Responsible Disclosure

This research was conducted under responsible disclosure principles. We did not test attacks against live systems without authorization. Our analysis is based on architectural reasoning, published documentation, and general principles of computer security. Relevant parties were notified prior to public release.

For security concerns, please see [`RESPONSIBLE-DISCLOSURE.md`](./RESPONSIBLE-DISCLOSURE.md).

---

<p align="center">
  <i>The email you send to an AI agent is not just a message. It's code that hasn't been compiled yet.</i>
</p>

<p align="center">
  🦕
</p>