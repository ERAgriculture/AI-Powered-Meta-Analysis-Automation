# AI-Powered Meta-Analysis Automation: Part of the ERA data ecosystem

Welcome to the ERA AI Meta-Analysis Repository. This project advances evidence synthesis and meta-analysis by automating the repetitive while keeping the complex scientific questions squarely in the hands of domain experts.

At a high level, the workflow systematizes literature discovery and triage using OpenAlex (with optional benchmarking against Web of Science), then applies AI-assisted screening, tagging, and keyword extraction to rapidly structure information for downstream analysis. The goal is not to replace scientific judgment, but to amplify it, freeing scientists to interrogate mechanisms, uncertainty, and context, while the pipeline handles query engineering, data wrangling, and transparent reporting.

The repository ships with ready-to-knit reports and configurable YAML policies so methods are reproducible, auditable, and adaptable across agricultural and climate research topics.

---

## Purpose

This repository aims to:

* Provide a **reproducible, R-based pipeline** for literature discovery and triage with OpenAlex.
* Enable **AI-assisted screening and tagging** for rapid evidence mapping.
* Offer **benchmarking** against WoS exports and simple evaluation metrics.
* Produce **shareable HTML reports** (GitHub Pages) for transparency and collaboration.

---

## Contents

### Repository Structure

* **`AI.Rproj`** (optional): R Project file to organize and manage the repository.
* **`scripts/`**: R scripts for querying, screening, tagging, comparison, and evaluation.

  * `openalex_query.R`, `screen.R`, `tag.R`, `compare_wos.R`, `evaluate.R`
* **`configs/`**: YAML configs (criteria, schemas, prompt templates).
* **`queries/`**: Search term lists (YAML/TXT).
* **`data/`**

  * `raw/`: OpenAlex exports (`.ndjson`/`.jsonl`)
  * `processed/`: screened/tagged tables (e.g., Parquet)
  * `external/`: optional WoS or other exports (not versioned)
* **`docs/`**: HTML reports published via GitHub Pages (links below).
* **`renv.lock`**: Pinned R package versions (created by `renv`).
* **`README.md`**: This file.

---

## Features

1. **OpenAlex Querying**

   * Generate and run search strategies; export results to NDJSON/JSONL.
   * Rate-limit friendly + simple resumption.

2. **AI Screening & Tagging**

   * Apply inclusion/exclusion criteria from YAML.
   * Extract keywords/tags; harmonize fields for downstream analysis.

3. **Benchmarking & Evaluation**

   * Compare OpenAlex pulls with WoS exports.
   * Evaluate tagging quality against manual or gold labels.

4. **Reports & Transparency**

   * Render shareable HTML reports with figures and tables.
   * Continuous improvement via versioned configs and logs.

---

## Getting Started

### 1) Setup (R)

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

### 2) Minimal Pipeline

```bash
# Query OpenAlex using a YAML of search terms
Rscript scripts/openalex_query.R \
  --query-file queries/search_terms.yaml \
  --since 2010-01-01 \
  --out data/raw/openalex.ndjson \
  --limit 50000

# Screen results with AI criteria
Rscript scripts/screen.R \
  --in data/raw/openalex.ndjson \
  --out data/processed/screened.parquet \
  --model gpt-4o-mini \
  --policy configs/screening_criteria.yaml

# Tag / keyword extraction
Rscript scripts/tag.R \
  --in data/processed/screened.parquet \
  --out data/processed/tagged.parquet \
  --model gpt-4o-mini \
  --schema configs/tag_schema.yaml

# (Optional) Benchmark against WoS
Rscript scripts/compare_wos.R \
  --openalex data/raw/openalex.ndjson \
  --wos data/external/wos_export.csv \
  --out reports/wos_comparison.csv
```

> Prefer columnar formats like **Parquet** via `{arrow}` for speed and memory.

---

## View Reports

* **🔗 GPT Tagging Report**: [View Report](https://eragriculture.github.io/AI/docs/GPT_tagging.html)
* **🔗 Use of AI for Data Extraction**: [View Report](https://eragriculture.github.io/AI/docs/Use_of_AI_for_Extraction.html)
* **🔗 AI Screening Report**: [View Report](https://eragriculture.github.io/AI/docs/Screening_GPT.html)
* **🔗 OpenAlex vignette**: [View Report](https://eragriculture.github.io/AI/docs/OA-vignette.html)
* **🔗 Web Scraping for data extraction with make.com**: [View Report](https://eragriculture.github.io/AI/docs/GCA-web-scraping.html)

---

## Configuration

Create or edit `~/.Renviron` (user-level) or a project `.Renviron`:

```ini
# LLM providers (examples)
OPENAI_API_KEY=...
ANTHROPIC_API_KEY=...
AZURE_OPENAI_ENDPOINT=...
AZURE_OPENAI_API_KEY=...

# runtime
REQUESTS_TIMEOUT=60
CACHE_DIR=.cache
```

Reload with `readRenviron("~/.Renviron")` inside R as needed.

* **OpenAlex**: no key required; be polite with rate limits.
* **Privacy**: keep proprietary exports (e.g., WoS CSVs) in `data/external/` and **do not commit** unless licensed.
* **SPDX**: optional headers in R files, e.g., `# SPDX-License-Identifier: MIT`.

---

## Data Sources

* **OpenAlex** — modern, open scholarly metadata and abstracts for discovery and analysis.
* **Web of Science (optional)** — used for comparisons where access permits.
* **Generated screening/tagging data** — produced by scripts and stored under `data/processed/`.

---

## How to Use the Reports

Open the HTML files in `docs/` (or visit GitHub Pages links above). Each report includes:

* Query summaries and counts
* Screening and tagging summaries
* Keyword trends and topic overviews
* (Optional) Comparisons with WoS exports

---

## FAQ

**I get zero results.**
• Loosen date filters; verify `--since`.
• Validate YAML (spaces, not tabs).

**Rate limits or timeouts.**
• Add pauses/backoff in your fetcher; split large queries.

**LLM costs.**
• Run a small sample first (e.g., `--limit 500`) and cache responses.

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
* Excel Template (evidence extraction): [https://github.com/CIAT/ERA_dev/blob/main/data_entry/industrious_elephant_2023/excel_data_extraction_template/V2.0.28%20-%20Industrious%20Elephant.xlsm](https://github.com/CIAT/ERA_dev/blob/main/data_entry/industrious_elephant_2023/excel_data_extraction_template/V2.0.28%20-%20Industrious%20Elephant.xlsm)

---

## Team

This project is led and implemented by the **Climate Action Lever** of the **Alliance of Bioversity International and CIAT**.

* **Lolita Muller** — *Senior Research Associate & Lead Developer*
  Email: [m.lolita@cgiar.org](mailto:m.lolita@cgiar.org)

(Contributions welcome via PR.)

---

## License

* **Code**: MIT License (recommended for software).
* **Docs & Reports**: CC-BY 4.0 (unless otherwise specified).
  See [`LICENSE`](./LICENSE) for details.

---

## Acknowledgments

This work is supported under the **Climate** area within the **CGIAR Excellence in Agronomy Initiative (EiA)**. Thanks to **OpenAlex** and to any data providers used (e.g., WoS) for enabling open research.

---

![Logos](https://github.com/user-attachments/assets/d3112c9d-6392-46a2-9fc6-8d0b72e6aec1)
