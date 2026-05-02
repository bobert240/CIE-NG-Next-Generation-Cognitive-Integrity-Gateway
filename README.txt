CIE‑NG is a research prototype for runtime governance of multi‑LLM assistants. It sits in front of models like Sophia/Grok/DeepSeek, checking every request and response for security (canary tokens, jailbreak phrases), quality (falsifiability, gilding stripping), feasibility (pragmatic scoping), and auditability (three‑layer validation, uncertainty decomposition, falsification logging). Built from 83 governance patterns, it is non‑commercial (CC BY‑NC 4.0) and intended for alignment research, multi‑agent orchestration experiments, and policy education. Not production‑ready – known limitations include keyword‑based falsifiability and a stub dialectical resolver.

# CIE‑NG: Cognitive Integrity Gateway – Next Generation

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Research Prototype](https://img.shields.io/badge/status-research%20prototype-red)]()

> **⚠️ RESEARCH PROTOTYPE – NOT FOR PRODUCTION USE**  
> This software is a proof‑of‑concept for studying **runtime governance** of LLM assistants.  
> It is **non‑commercial only** (CC BY‑NC 4.0). Do not use in revenue‑generating systems or critical applications.  
> No warranties, no security audits, no support. Use at your own risk.

## Overview

**CIE‑NG** is a safety and quality filter that sits in front of multiple AI assistants (e.g., Sophia, Grok, DeepSeek). It checks every request before it reaches an assistant, and every answer before it returns to the user – to prevent mistakes, manipulation, and waste.

It implements **83 components** from a governance catalog, including:

- **Canary token detection** – stops prompt injection attacks.
- **Gilding stripping** – removes emotion‑charged language.
- **Pragmatic scoping** – routes tasks to the most suitable assistant.
- **Token budgeting** – prevents out‑of‑memory errors and cost overruns.
- **Falsifiability checks** – encourages testable objectives (heuristic).
- **Three‑layer validation** – schema + executable + eval (shallow examples).
- **Uncertainty decomposition** – distinguishes random from knowledge‑based uncertainty.
- **Veracity auditing** – flags likely factual errors.
- **Falsification logging** – persistent record of predictions for later analysis.

> **Dialectical resolution (C67)** is a stub; the current version raises `NotImplementedError` to encourage researchers to implement real contradiction handling.

## Who This Is For

- **Alignment researchers** studying falsifiable objectives, oversight, or audit logging.
- **Graduate students** needing a baseline for multi‑assistant orchestration experiments.
- **Policy / governance researchers** who want to see what “technical governance” looks like in executable code.
- **Educators** teaching LLM safety or multi‑agent systems.

This is **not** for building commercial products or production services.

## Quick Start

```bash
# Clone the repository
git clone https://github.com/yourusername/cie-ng.git
cd cie-ng

# (Optional) Create a virtual environment
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows

# Install dependencies (pytest for regression tests)
pip install -r requirements.txt

# Run the demo / regression tests
python cie_ng.py
You should see output showing the gateway processing a sample TPG packet and returning a structured response.

Using the CLI
bash
python cie_ng.py --input "Run a Monte Carlo simulation of oil prices" --assistant Grok
Using as a library
python
from cie_ng import CognitiveIntegrityGateway

gateway = CognitiveIntegrityGateway(falsification_db_file="my_log.json")
result = gateway.process("Your prompt here", assistant_role="Sophia")
print(result["status"])  # "success", "rejected", "blocked", or "error"
Note: The _route_to_assistant method is a stub that returns simulated answers. Replace it with real API calls to OpenAI, Anthropic, or local models.

Example (Simulated)
json
{
  "status": "success",
  "output": {
    "result": "[SIMULATED] Grok Monte Carlo: breach probability 85% (range 70-95%)",
    "citations": ["https://example.com/source1"],
    "hashes": {"content_hash": "e8b1c3a9f2d5..."},
    "uncertainty": {
      "aleatoric": "medium",
      "epistemic": "high",
      "dominant": "epistemic"
    }
  },
  "audit": {
    "issues": [],
    "severity": "low",
    "corrective_action": "Verify numbers against source data; add missing citations"
  },
  "integrity_score": 98
}
Known Limitations (Critical for Honesty)
Falsifiability check is keyword‑based (looks for falsifiable, indicator, >, <, etc.). It is easily fooled – use only for experimentation.

Dialectical resolver is a stub (raises NotImplementedError). Replace with actual debate/refinement logic if needed.

Token estimator uses 4 characters ≈ 1 token, which is imprecise. Use a real tokeniser for accurate budgeting.

Three‑layer validation is shallow: “executable” only checks JSON serialisability; “eval” is a placeholder.

No asynchronous execution – the pipeline is synchronous and single‑threaded.

No authentication, rate limiting, or load shedding – do not expose to the internet.

No PII redaction – the gateway logs raw inputs (except canary token). Use with care.

Contributing / Extending
You are welcome to fork and modify under the terms of the CC BY‑NC 4.0 license. Suggested research directions:

Replace the keyword‑based falsifiability check with a structured schema (metric, threshold, timeframe).

Implement a real dialectical resolver using debate or iterative refinement between multiple models.

Add OpenTelemetry metrics to measure component‑level latency and error rates.

Build a Docker container for reproducible experiments.

If you are a non‑profit research organisation and need a commercial exception, please contact the author.

License
This project is licensed under the Creative Commons Attribution‑NonCommercial 4.0 International (CC BY‑NC 4.0).

You are free to:

Share – copy and redistribute the material in any medium or format.

Adapt – remix, transform, and build upon the material.

Under the following terms:

Attribution – You must give appropriate credit, provide a link to the license, and indicate if changes were made.

NonCommercial – You may not use the material for commercial purposes.

See the full license text for details.

For commercial use (e.g., integrating into a product or service), please contact the repository owner.

Acknowledgments
This prototype synthesizes governance patterns from public research and the user’s original catalog of 83 components. No large language model was used to generate the final code without human review.

Built for intellectual exploration, not profit.
If you find this useful for your research, consider citing it as:

CIE‑NG: Next‑Generation Cognitive Integrity Gateway (2026). GitHub repository.
https://github.com/bobert240/CIE-NG-Next-Generation-Cognitive-Integrity-Gateway/upload/main