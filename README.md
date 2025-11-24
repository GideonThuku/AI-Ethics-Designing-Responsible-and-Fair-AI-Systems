# AI Ethics Assignment: Designing Responsible and Fair AI Systems 🌍⚖️

## 📌 Project Overview

This repository serves as our group submission for the AI Ethics module. The project focuses on "Designing Responsible and Fair AI Systems," tackling the critical challenge of algorithmic bias in high-stakes decision-making environments.

Our work consists of two main components:

- **Theoretical Analysis**: A deep dive into ethical frameworks (EU Guidelines, GDPR), case study analysis (Amazon Hiring, Facial Recognition), and policy proposals.
- **Technical Fairness Audit**: A practical implementation of fairness metrics using Python to audit a recidivism prediction algorithm, modeled after the controversial COMPAS dataset.

## 📂 Repository Structure

| File | Description |
|------|-------------|
| `fairness_audit.py` | A standalone Python script that performs the technical audit. It generates synthetic data statistically similar to the COMPAS dataset, calculates key fairness metrics, and renders visualization plots. |
| `ai_ethics_submission.md` | The comprehensive written report containing our answers to the theoretical questions, case study remediation strategies, and the healthcare policy proposal. |
| `requirements.txt` | A list of necessary Python libraries (pandas, numpy, matplotlib, seaborn) to reproduce our findings. |

## ⚙️ Methodology: The Fairness Audit

The `fairness_audit.py` script mimics an audit of the COMPAS recidivism algorithm. We focused on **Group Fairness** metrics to identify racial bias.

### Key Metrics Implemented:

- **False Positive Rate (FPR)**: The percentage of defendants who were predicted to be "High Risk" but did not actually re-offend. A significant difference in FPR between groups indicates that innocent members of one group are being penalized more often than another.
- **Disparate Impact Ratio**: Compares the selection rates (rate of being labeled "High Risk") between the unprivileged group (African-American) and the privileged group (Caucasian).

### Data Simulation:

**Note**: Due to file access restrictions in some environments, the script uses a synthetic data generator (`generate_mock_compas_data`).

This generator is calibrated to replicate the statistical biases found in the original ProPublica analysis (e.g., higher base FPR for African-American defendants due to systemic data bias).

## 🚀 Getting Started

### Prerequisites

Ensure you have Python 3.x installed. Install the dependencies using pip:

```bash
pip install -r requirements.txt

### Running the Audit

Execute the script to run the simulation and generate the bias visualization charts:

```bash
python fairness_audit.py

### Expected Output:

- Console logs showing the confusion matrix (TP, FP, TN, FN) for each demographic group
- A calculation of the Disparate Impact Ratio with a "Bias Detected" or "Fair" verdict
- A pop-up bar chart visualizing the discrepancy in False Positive Rates# AI-Ethics-Designing-Responsible-and-Fair-AI-Systems
