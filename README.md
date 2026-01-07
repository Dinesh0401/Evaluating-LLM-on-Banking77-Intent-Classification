# Banking77 Intent Classification Benchmarking with LLMs

This repository evaluates the performance of multiple LLM  on the Banking77 intent classification dataset.  
The goal is to measure how accurately modern LLMs can categorize real-world banking customer queries into predefined intent labels.

The project compares OpenAI and Anthropic models using a consistent evaluation pipeline, with additional prompt optimization using DSPy.

--- 

## 🎯 Project Goal

The primary objective of this project is to:

- Evaluate and compare intent classification accuracy across LLMs
- Understand model strengths and weaknesses in a banking domain
- Measure the impact of prompt optimization techniques (DSPy MiPROv2)
- Identify practical challenges such as label drift and invalid outputs

This evaluation is designed to reflect **real customer-support scenarios** in banking applications.
 
---

## 📂 Dataset

### Banking77 Dataset

- **Task**: Intent classification
- **Number of intents**: 77
- **Domain**: Retail banking customer queries
- **Sample size used**: 500 queries

Each sample consists of:
- `user_query`: A natural language customer question
- `gold_label`: The ground-truth intent category

The dataset serves as a strong benchmark for testing semantic understanding and intent disambiguation.

---

## 🤖 Models Evaluated

### 🔹 GPT-5.2 (OpenAI)
- General-purpose, high-capacity language model
- Strong reasoning and language understanding

### 🔹 GPT-5-mini (OpenAI)
- Lightweight and cost-efficient variant
- Optimized for faster inference and lower latency

### 🔹 Claude-4.5-Sonnet (Anthropic)
- State-of-the-art reasoning-focused model
- Optimized using DSPy for this task

---

## 🧪 Evaluation Methodology

### 1️⃣ Data Preparation
- Randomly sampled 500 queries from the Banking77 dataset
- Each query paired with its ground-truth intent label

---

### 2️⃣ Prompt Engineering
- A **single, consistent system prompt** is used across models
- The prompt:
  - Lists all 77 valid intent labels
  - Instructs the model to output exactly one label
  - Enforces strict output formatting to reduce ambiguity

---

### 3️⃣ DSPy Optimization (Claude Only)
- Claude-4.5-Sonnet’s classification pipeline is optimized using:
  - **DSPy MiPROv2 teleprompter**
  - `auto="heavy"` configuration
- The process includes:
  - Bootstrapping few-shot examples
  - Proposing instruction candidates
  - Refining prompt logic for higher accuracy

This step demonstrates how automated prompt optimization can improve intent classification performance.

---

### 4️⃣ Inference
- Each model processes all 500 queries
- For each query, the model outputs a predicted intent label
- Custom label-extraction logic ensures:
  - Only valid Banking77 labels are accepted
  - Out-of-vocabulary outputs are handled safely (especially for Claude)

---

### 5️⃣ Accuracy Measurement
- **Exact match metric** is used
- A prediction is considered correct only if:
predicted_label == gold_label

yaml
Copy code
- Accuracy is reported as a percentage of correct predictions

---

### 6️⃣ Results Reporting
- Per-model CSV files generated containing:
- User query
- Gold label
- Predicted label
- Match status (True / False)
- Results are also uploaded to **Google Sheets** for:
- Easy inspection
- Side-by-side model comparison
- Error analysis

---

## 📊 Key Results

### Initial Direct API Evaluation
GPT-5.2 accuracy : 62.00%
GPT-5-mini accuracy: 60.40%

shell
Copy code

### Optimized Evaluation (500 Samples)

GPT-5.2 (optimized prompt): 318 / 500 → 63.6%
GPT-5-mini (optimized prompt): 300 / 500 → 60.0%
Claude-4.5-Sonnet (DSPy MiPROv2): 65.75%

yaml
Copy code

---

## 🔍 Key Findings

- Claude-4.5-Sonnet achieves the **highest accuracy** after DSPy optimization
- Prompt optimization has a measurable impact on performance
- Label extraction and output validation are critical for reliable evaluation
- Smaller models trade accuracy for efficiency but remain competitive
- Intent classification remains challenging even for advanced LLMs due to:
  - Fine-grained intent overlap
  - Domain-specific phrasing
  - Ambiguous customer queries

---

## 🧩 Challenges Addressed

- Out-of-vocabulary label generation
- Inconsistent output formatting
- Prompt sensitivity across models
- Fair comparison under identical evaluation conditions

---

## 🏦 Real-World Relevance

This benchmark is directly applicable to:
- Banking chatbots
- Customer support automation
- IVR and conversational AI systems
- Financial domain NLP evaluation

---

## 🔧 Extensibility

You can easily extend this project to:
- Add more models (open-source or proprietary)
- Increase dataset size
- Use macro-F1 or per-intent metrics
- Perform detailed error analysis per intent
- Deploy as a continuous evaluation pipeline

---

## 📜 License & Usage

This project is intended for research and evaluation purposes.  
Ensure compliance with:
- OpenAI API policies
- Anthropic API policies
- Banking77 dataset license

---

## ✨ Final Note

This project focuses on **realistic evaluation**, not leaderboard chasing.  
If a model performs well here, it’s far more likely to survive contact with real banking users.
