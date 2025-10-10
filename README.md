# AI-Powered Meta-Analysis Automation: Part of the ERA data ecosystem

Welcome to the ERA AI Meta-Analysis Repository. This project advances evidence synthesis and meta-analysis by automating the repetitive while keeping the complex scientific questions squarely in the hands of domain experts.

At a high level, the workflow systematizes literature discovery and triage using OpenAlex (with optional benchmarking against Web of Science), then applies AI-assisted screening, tagging, and keyword extraction to rapidly structure information for downstream analysis. The goal is not to replace scientific judgment, but to amplify it, freeing scientists to interrogate mechanisms, uncertainty, and context, while the pipeline handles query engineering, data wrangling, and transparent reporting.

The repository ships with ready-to-knit reports and configurable YAML policies so methods are reproducible, auditable, and adaptable across agricultural and climate research topics.

---

## Purpose

This repository aims to:

- Provide a reproducible, R-based pipeline for literature discovery and triage across multiple scholarly sources (e.g., OpenAlex, and optionally Web of Science/Scopus/others).
- Enable AI‑assisted screening, tagging, and structured data extraction to accelerate evidence mapping and meta‑analysis.
- Support benchmarking and quality assessment (e.g., inter‑annotator checks, hold‑out labels, and cross‑source comparisons) with simple, transparent metrics.
- Produce shareable, versioned HTML reports and machine‑readable outputs (e.g., Parquet/JSONL) for transparency and collaboration.

---

## Contents

---

### View Reports

* **🔗 GPT Tagging Report**: [View Report](https://eragriculture.github.io/AI/docs/GPT_tagging.html)
* **🔗 Use of AI for Data Extraction**: [View Report](https://eragriculture.github.io/AI/docs/Use_of_AI_for_Extraction.html)
* **🔗 AI Screening Report**: [View Report](https://eragriculture.github.io/AI/docs/Screening_GPT.html)
* **🔗 OpenAlex vignette**: [View Report](https://eragriculture.github.io/AI/docs/OA-vignette.html)
* **🔗 Web Scraping for data extraction with make.com**: [View Report](https://eragriculture.github.io/AI/docs/GCA-web-scraping.html)

---


### Repository Structure

* **`AI.Rproj`** (optional): R Project file to organize and manage the repository.
* **`scripts/`**: R scripts for querying, screening, tagging, comparison, and evaluation.
* **`data/`** : Datasets used for analsys
* **`docs/`**: HTML reports published via GitHub Pages (links above).
* **`README.md`**: This file.

---



## Getting Started

### Setup (R)

```bash
# clone
git clone https://github.com/eragriculture/AI.git
cd AI

# restore dependencies (recommended)
R -q -e "install.packages('renv', repos='https://cloud.r-project.org'); renv::restore()"
# if renv.lock does not exist yet:
# R -q -e "install.packages('renv'); renv::init(); renv::snapshot()"
```

> **Note:** OpenAlex is public—no API key needed. If you use an LLM for screening/tagging, add keys to **~/.Renviron** (see **Configuration**).


## Configuration

Create or edit `~/.Renviron` (user-level) or a project `.Renviron`:

```ini
# LLM providers (examples)
OPENAI_API_KEY=...
```

Reload with `readRenviron("~/.Renviron")` inside R as needed.

---

## Data Sources

* **ERA Dataset**: A compilation of scientific papers focused on agricultural practices and their outcomes across various geographies.
* **OpenAlex** — modern, open scholarly metadata and abstracts for discovery and analysis.

---


## Citing

If you use this repository, please cite the software and, when available, the archived release:

**Software (concept DOI)**

> *AI-Powered Meta-Analysis Automation.* Versioned software. DOI: `10.5281/zenodo.XXXXXXX` (concept).

**This release**

> *AI-Powered Meta-Analysis Automation vX.Y.Z*, DOI: `10.5281/zenodo.YYYYYYY` (version).

**BibTeX**

```bibtex
@software{meta_ai_automation,
  title = {AI-Powered Meta-Analysis Automation},
  author = {Muller, Lolita and collaborators},
  year = {2025},
  version = {vX.Y.Z},
  doi = {10.5281/zenodo.YYYYYYY},
  url = {https://github.com/eragriculture/AI}
}
```

---

## Links

* ERA GitHub: [https://github.com/CIAT/ERA_dev](https://github.com/CIAT/ERA_dev)

---

## Team

This project is led and implemented by the **Climate Action Lever** of the **Alliance of Bioversity International and CIAT**.

* **Lolita Muller** — *Senior Research Associate & Lead Developer*
  Email: [m.lolita@cgiar.org](mailto:m.lolita@cgiar.org)


---

## License

* **Code**: MIT License (recommended for software).
* **Docs & Reports**: CC-BY 4.0 (unless otherwise specified).
  See [`LICENSE`](./LICENSE) for details.

---

## Acknowledgments

This work is supported under the **Climate** area within the **CGIAR Excellence in Agronomy Initiative (EiA)**.

---

![Logos](https://github.com/user-attachments/assets/d3112c9d-6392-46a2-9fc6-8d0b72e6aec1)
