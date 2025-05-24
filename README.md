*Flight analysis notebooks*

The relevance checker can be found [here](https://github.com/aacudad/flight_analysis/blob/main/relevance.ipynb)

The sentiment analyser can be found [here](https://github.com/aacudad/flight_analysis/blob/main/sentiment.ipynb)
# README

## Overview

This repository contains two Jupyter notebooks that demonstrate how to classify airline passenger feedback using an **Ollama**‑hosted large‑language model (LLM):

| Notebook | Task |
|----------|------|
| `transfer_relevance_classification.ipynb` | Detects whether a feedback sentence is **Relevant** or **Not Relevant** to the airline **transfer page**. |
| `sentiment_classification.ipynb`          | Classifies general feedback as **Positive** or **Negative**. |

Both notebooks use the open‑weights **Gemma 3‑4B Instruct** model (`gemma3:4b-it-qat`) running locally through the Ollama runtime and accessed from Python via the `ollama` pip package.

---

## 1. Prerequisites

| Requirement | Version | Installation |
|-------------|---------|--------------|
| **Python**  | 3.8 or newer | Download & install from the official website: <https://www.python.org/downloads/> |
| **Ollama runtime** | Latest | Follow the instructions for your platform: <https://ollama.ai/download> |
| **pip** | Comes with Python ≥ 3.4 | Upgrade if necessary: `python -m pip install --upgrade pip` |

> **Tip:** We strongly recommend working inside a virtual environment (`venv` or `conda`) to keep dependencies isolated.

---

## 2. Setup

1. **Clone** or download this project:

   ```bash
   git clone <YOUR-REPO-URL>
   cd <YOUR-REPO>
   ```

2. **Create & activate** a virtual environment (optional but recommended):

   ```bash
   # Linux / macOS
   python -m venv .venv && source .venv/bin/activate
   # Windows (PowerShell)
   python -m venv .venv; .\.venv\Scripts\Activate
   ```

3. **Install Python dependencies**:

   ```bash
   pip install ollama jupyter
   ```

4. **Start the Ollama daemon** (if it isn’t already running):

   ```bash
   ollama serve
   ```

5. **Download the Gemma model** (this happens automatically on first use, but you can pull it explicitly):

   ```bash
   ollama pull gemma3:4b-it-qat
   ```

---

## 3. Running the notebooks

1. Launch Jupyter Lab or Notebook:

   ```bash
   jupyter lab         # or: jupyter notebook
   ```

2. Open `transfer_relevance_classification.ipynb` or `sentiment_classification.ipynb`.

3. Run **`Kernel ▶ Restart & Run All`** (or execute the cells individually).  
   The notebook will:
   - Build a concise prompt.  
   - Send each feedback sentence plus the prompt to the Gemma model via `ollama.chat(...)`.  
   - Print the classification results to stdout.

> ⚠️ The first model invocation may take a minute while the weights load into memory.

---

## 4. Running the code as plain Python scripts

If you prefer not to use Jupyter, you can export each notebook to a `.py` file and run it directly:

```bash
jupyter nbconvert --to python transfer_relevance_classification.ipynb
python transfer_relevance_classification.py
```

Do the same for `sentiment_classification.ipynb`.

---

## 5. Troubleshooting

| Symptom | Possible fix |
|---------|--------------|
| `ModuleNotFoundError: No module named 'ollama'` | Verify the virtual environment is active and run `pip install ollama`. |
| `ollama: command not found` | Ensure the Ollama runtime is installed and its binary folder is on your PATH. |
| Model download extremely slow or fails | Check your internet connection or set the `OLLAMA_HOST` environment variable if you’re pointing to a remote Ollama server. |
| GPU out‑of‑memory errors | Run with CPU (`OLLAMA_NO_GPU=1`) or use a smaller quantisation (e.g. `:q4_K_M`). |

---

## 6. Extending the notebooks

- **Change the model**: simply replace `"gemma3:4b-it-qat"` with any other model you have pulled (`ollama pull llama3:8b...`).
- **Adapt the prompt**: edit the `prompt` string to reflect a different classification rubric.
- **Batch processing**: replace the sample `feedback_data` list with your own CSV or database queries.

---

## 7. License

The code in this repository is released under the MIT License (see `LICENSE`).  
The Gemma model weights are subject to [Google’s Gemma Community License](https://ai.google.dev/gemma) and the Ollama [terms of service](https://ollama.ai/tos).

---

Enjoy classifying your airline feedback! ✈️
