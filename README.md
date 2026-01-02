# HumanEval Benchmark Evaluation

This repository contains evaluation results for multiple code generation models on the **HumanEval benchmark**. The evaluation includes both **baseline (original prompt)** and **error-aware prompting** approaches to compare performance improvements.

##  Results Summary

| Model | Baseline Pass@1 | Error-Aware Pass@1 | Improvement |
|-------|-----------------|-------------------|-------------|
| **Qwen2.5-Coder-7B-Instruct** | 78.05% | 96.95% | +18.90% |
| **DeepSeek-Coder-6.7B-Instruct** | 61.59% | 84.76% | +23.17% |
| **Qwen2.5-Coder-1.5B-Instruct** | 48.78% | 53.05% | +4.27% |

##  Repository Structure

```
humaneval/
├── deepseek-coder-6.7b-instruct/
│   ├── final-humaneval-deepseek-6-7b-instruct.ipynb          # Baseline evaluation
│   ├── final-humaneval-deepseek-6-7b-instruct-erroraware.ipynb  # Error-aware evaluation
│   ├── output_original/                                       # Baseline results
│   │   ├── evaluation_results_original.json
│   │   ├── evaluation_summary_original.txt
│   │   └── output_log_original.txt
│   └── output_error_aware/                                    # Error-aware results
│       ├── evaluation_results_error_aware.json
│       ├── evaluation_summary_error_aware.txt
│       └── output_log_error_aware.txt
│
├── qwen-2.5-coder-7b-instruct/
│   ├── final-humaneval-qwen-7b.ipynb                         # Baseline evaluation
│   ├── final-humaneval-qwen-7b-erroraware.ipynb              # Error-aware evaluation
│   ├── output_original/                                       # Baseline results
│   │   ├── evaluation_results_qwen25_coder_7b.json
│   │   ├── evaluation_summary_qwen25_coder_7b.txt
│   │   └── output_log_qwen25_coder_7b.txt
│   └── output_error_aware/                                    # Error-aware results
│       ├── evaluation_results_qwen25_coder_7b_error_aware_all.json
│       ├── evaluation_summary_qwen25_coder_7b_error_aware_all.txt
│       └── output_log_qwen25_coder_7b_error_aware_all.txt
│
├── qwen2.5-coder-1.5b-instruct/
│   ├── final-humaneval-qwen-1-5b.ipynb                       # Baseline evaluation
│   ├── final-humaneval-qwen-1-5b-error-aware.ipynb           # Error-aware evaluation
│   ├── output_original/                                       # Baseline results
│   │   ├── evaluation_results_qwen25_coder_1.5b.json
│   │   ├── evaluation_summary_qwen25_coder_1.5b.txt
│   │   └── output_log_qwen25_coder_1.5b.txt
│   └── output_error_aware/                                    # Error-aware results
│       ├── evaluation_results_qwen25_coder_1.5b_error_aware_all.json
│       ├── evaluation_summary_qwen25_coder_1.5b_error_aware_all.txt
│       └── output_log_qwen25_coder_1.5b_error_aware_all.txt
│
└── README.md
```

##  Detailed Results

### DeepSeek-Coder-6.7B-Instruct
| Metric | Baseline | Error-Aware |
|--------|----------|-------------|
| **Pass@1** | 61.59% (101/164) | 84.76% (139/164) |
| Syntax Errors | 28.05% (46) | 12.80% (21) |
| Runtime Errors | 10.37% (17) | 2.44% (4) |
| Incomplete Code | 0.00% (0) | 0.00% (0) |
| Timeouts | 0.00% (0) | 0.00% (0) |

---

### Qwen2.5-Coder-7B-Instruct
| Metric | Baseline | Error-Aware |
|--------|----------|-------------|
| **Pass@1** | 78.05% (128/164) | 96.95% (159/164) |
| Syntax Errors | 21.95% (36) | 3.05% (5) |
| Runtime Errors | 0.00% (0) | 0.00% (0) |
| Incomplete Code | 0.00% (0) | 0.00% (0) |
| Timeouts | 0.00% (0) | 0.00% (0) |

---

### Qwen2.5-Coder-1.5B-Instruct
| Metric | Baseline | Error-Aware |
|--------|----------|-------------|
| **Pass@1** | 48.78% (80/164) | 53.05% (87/164) |
| Syntax Errors | 51.22% (84) | 46.95% (77) |
| Runtime Errors | 0.00% (0) | 0.00% (0) |
| Incomplete Code | 0.00% (0) | 0.00% (0) |
| Timeouts | 0.00% (0) | 0.00% (0) |

##  Models Evaluated

| Model | Parameters | Source |
|-------|------------|--------|
| `deepseek-ai/deepseek-coder-6.7b-instruct` | 6.7B | [HuggingFace](https://huggingface.co/deepseek-ai/deepseek-coder-6.7b-instruct) |
| `Qwen/Qwen2.5-Coder-7B-Instruct` | 7B | [HuggingFace](https://huggingface.co/Qwen/Qwen2.5-Coder-7B-Instruct) |
| `Qwen/Qwen2.5-Coder-1.5B-Instruct` | 1.5B | [HuggingFace](https://huggingface.co/Qwen/Qwen2.5-Coder-1.5B-Instruct) |

##  About HumanEval

HumanEval is a benchmark for evaluating code generation models. It consists of **164 hand-written programming problems** that test a model's ability to generate correct Python functions from docstrings.

- **Benchmark Source**: [OpenAI HumanEval](https://github.com/openai/human-eval)
- **Metric**: `pass@1` - Percentage of problems where the first generated solution passes all test cases

##  Error-Aware Prompting

Error-aware prompting is a technique that provides the model with explicit instructions to avoid common coding errors, such as:

- Proper code formatting (avoiding markdown code blocks)
- Correct indentation
- Avoiding re-defining function signatures
- Generating only the function body without explanatory text

This approach significantly reduces **syntax errors** and improves overall `pass@1` scores across all evaluated models.

##  Output Files

Each model's output directory contains:

| File | Description |
|------|-------------|
| `evaluation_results_*.json` | Detailed results for each problem (pass/fail, error type, generated code) |
| `evaluation_summary_*.txt` | Summary statistics (pass@1, error breakdown, successful/failed problem IDs) |
| `output_log_*.txt` | Full log of prompts and generated outputs for all 164 problems |
