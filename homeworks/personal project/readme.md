```markdown
# FTEC5660 Reproducibility Project: AI-Trader (Agentic System)

## Project Overview
This repository contains a reproducibility study of the **AI-Trader** benchmark (Benchmarking Autonomous Agents in Real-Time Financial Markets). It implements a multi-step agentic system that autonomously queries historical financial data, synthesizes market signals (price vs. moving average), and executes simulated trading actions (Buy/Sell/Hold) over a continuous time-series.

### Modification & Ablation
In accordance with the assignment requirements, the following isolated and measurable modifications were made to the original methodology:
1. **Model Change:** Migrated the underlying LLM to `gemini-2.5-flash`.
2. **Policy Change (Strict Chain-of-Thought):** Enforced a mandatory "Internal Reasoning" step in the System Prompt. The agent is strictly required to output its multi-step mathematical comparisons before issuing a JSON-formatted trade decision.
3. **Tool Robustness:** Implemented defensive integer casting and NaN-filters on the `yfinance` tool interface to prevent serialization crashes caused by LLM parameter type-drift.

---

## 🛠️ Installation Setup

### Prerequisites
- **Python:** 3.10 or higher (Tested on Python 3.12 in Google Colab).
- **API Key:** A valid Google Gemini API Key. (Get one from [Google AI Studio](https://aistudio.google.com/)).

### Install Dependencies
Clone this repository and install the required Python packages:

```bash
# Clone the repository
git clone [https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPO_NAME.git)
cd YOUR_REPO_NAME

# Install required packages
pip install google-generativeai yfinance pandas matplotlib

```

---

## 🚀 How to Run

**Method 1: Running the Jupyter Notebook (Recommended)**

1. Open the `AI_Trader_Reproduction.ipynb` file in Google Colab or your local Jupyter environment.
2. Add your Gemini API Key:
* If using Google Colab: Add a Secret named `GEMINI_API_KEY` in the left panel (🔑 icon).
* If running locally: Set it as an environment variable (`export GEMINI_API_KEY="your_key_here"`).


3. Run all cells sequentially.

**Method 2: Running via Python Script**
If you exported the code to a `.py` file, ensure your API key is configured in your environment, then execute:

```bash
python run_agentic_backtest.py

```

---

## 📊 Expected Output

Upon successful execution, the script will create a local directory named `FTEC5660_Submission_3696/` containing:

1. **`timeseries_backtest_AAPL.csv`**: The full day-by-day trading log, portfolio equity curve, and executed actions.
2. **`CR_Chart_AAPL.png`**: A plotted Cumulative Return (CR) chart comparing the Agent's performance against a Buy & Hold baseline.
3. **`agent_reasoning_log.txt`**: A detailed log capturing the agent's explicit step-by-step "Internal Reasoning" for each trading day.

---
