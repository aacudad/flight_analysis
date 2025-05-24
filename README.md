# README

## Overview

This repository contains two Jupyter notebooks that demonstrate how to classify airline passenger feedback using an **Ollama**‑hosted large‑language model (LLM):

| Notebook | Task |
|----------|------|
| [`relevance.ipynb`](https://github.com/aacudad/flight_analysis/blob/main/relevance.ipynb) | Detects whether a feedback sentence is **Relevant** or **Not Relevant** to the airline **transfer page**. |
| [`sentiment.ipynb`](https://github.com/aacudad/flight_analysis/blob/main/sentiment.ipynb) | Classifies general feedback as **Positive** or **Negative**. |

Both notebooks use the open‑weights **Gemma 3‑4B Instruct** model (`gemma3:4b-it-qat`) running locally through the Ollama runtime and accessed from Python via the `ollama` pip package.

---

## 1. Prerequisites

| Requirement | Version | Installation |
|-------------|---------|--------------|
| **Python**  | 3.8 or newer | Download & install from the official website: <https://www.python.org/downloads/> |
| **Ollama runtime** | Latest | Follow the instructions for your platform: <https://ollama.ai/download> |
| **pip** | Comes with Python ≥ 3.4 | Upgrade if necessary: `python -m pip install --upgrade pip` |

---

## 2. Setup

1. **Clone** or download this project:

   ```bash
   git clone <YOUR-REPO-URL>
   cd <YOUR-REPO>
   ```

2. **Install Python dependencies**:

   ```bash
   pip install ollama jupyter
   ```

3. **Start the Ollama daemon** (if it isn’t already running):

   ```bash
   ollama serve
   ```

---

## 3. Running the notebooks

1. Launch Jupyter Lab or Notebook:

   ```bash
   jupyter lab         # or: jupyter notebook
   ```

2. Open **`relevance.ipynb`** or **`sentiment.ipynb`**.

3. Run **`Kernel ▶ Restart & Run All`** (or execute the cells individually).  
   The notebook will:
   - Build a concise prompt.  
   - Send each feedback sentence plus the prompt to the Gemma model via `ollama.chat(...)`.  
   - Print the classification results to stdout.

> ⚠️ The first model invocation may take a minute while the weights load into memory.

---

## 4. Troubleshooting

| Symptom | Possible fix |
|---------|--------------|
| `ModuleNotFoundError: No module named 'ollama'` | Verify that you installed the package with `pip install ollama`. |
| `ollama: command not found` | Ensure the Ollama runtime is installed and its binary folder is on your PATH. |
| Model download extremely slow or fails | Check your internet connection or set the `OLLAMA_HOST` environment variable if you’re pointing to a remote Ollama server. |
| GPU out‑of‑memory errors | Run with CPU (`OLLAMA_NO_GPU=1`) or use a smaller quantisation (e.g. `:q4_K_M`). |

---

## 5. Extending the notebooks

- **Change the model**: simply replace `"gemma3:4b-it-qat"` with any other model you have pulled (`ollama pull llama3:8b...`).
- **Adapt the prompt**: edit the `prompt` string to reflect a different classification rubric.
- **Batch processing**: replace the sample feedback list with your own CSV or database queries.

---

## 6. License

The code in this repository is released under the MIT License.  
The Gemma model weights are subject to [Google’s Gemma Community License](https://ai.google.dev/gemma) and the Ollama [terms of service](https://ollama.ai/tos).

---

Enjoy classifying your airline feedback! ✈️
