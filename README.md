# Evaluating Bias, Trustworthiness and Fairness in Open-Source LLMs
ARTI 6000 — Advanced Topics in AI and ML | Adelaide University | April 2026  
Joel Jorly | a1959854


## What this is

This project tests whether open-source LLMs assign phishing vulnerability labels based on demographic stereotypes rather than actual risk factors. I collected 840 persona-level responses from 15 models across 5 providers and ran statistical tests to measure gender, age, domain, and experience bias.

The clearest result: non-binary personas were flagged 61.3% of the time versus 18.6% for male personas. Chi2 = 66.542, p < 0.0001.


## Files

- `assignment2_v2_a1959854_jorly.ipynb` — main notebook
- `dataset_a1959854_jorly.xlsx` — 840-row dataset
- `results_a1959854_jorly.json` — statistical outputs
- `fig1_dataset_overview.png` — provider, gender, age charts
- `fig2_analysis.png` — education, domain, consistency charts
- `fig3_consistency_qualitative.png` — per-model consistency and heatmap


## How to replicate

Open the notebook in Google Colab and add these to Colab Secrets before running:
GROQ_API_KEY
HF_TOKEN
OPENROUTER_API_KEY
CEREBRAS_API_KEY
NVIDIA_API_KEY

Install dependencies:
pip install groq openai huggingface_hub scipy pandas matplotlib seaborn numpy openpyxl

Run all cells in order to replicate data collection from scratch. If you just want to reproduce the analysis, start from the cell beginning with `persona_df = pd.read_excel(EXCEL_FILE)` — the dataset is already included.


## Providers and models

5 providers, 3 models each, 840 rows total:

- Groq — Llama 3.1 8B, Llama 3.3 70B, GPT-OSS-120B (120 rows)
- HuggingFace — Llama 3.1 8B, Qwen2.5 32B, Gemma 3 27B (210 rows)
- OpenRouter — Llama 3.1 8B, Qwen2.5 7B, GPT-OSS-120B (180 rows)
- Cerebras — Llama 3.1 8B, Qwen 235B, GPT-OSS-120B (120 rows)
- NVIDIA — Llama 3.1 70B, Llama 3.3 70B, Nemotron Super (210 rows)

2 models excluded due to API errors during collection.


## Key numbers

- Gender Chi-Square: Chi2 = 66.542, p < 0.0001
- Age t-test: t = -3.693, p = 0.0002
- IT domain odds ratio: 0.611 overall, 10.636 for Cerebras
- 3 models hit 100% consistency across 10 runs at temperature 0.8
- Majority of valid models scored above 70% consistency


## References

Wang et al. (2024) — DecodingTrust. NeurIPS 2023.  
Sarker et al. (2023) — Personalized anti-phishing guidelines. arXiv:2311.12827.  
Navigli et al. (2023) — Biases in large language models. ACM JDIQ.  
Ouyang et al. (2022) — Training language models with human feedback. NeurIPS.  
Bender et al. (2021) — On the dangers of stochastic parrots. FAccT.  
ACSC (2023) — Phishing. Australian Government.  
Trepa, C. (2026) — Topic 5 lecture slides. Adelaide University.
