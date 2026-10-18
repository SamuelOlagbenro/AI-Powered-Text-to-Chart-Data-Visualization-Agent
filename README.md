# 📊 AI-Powered (Text to Chart) Data Visualization Agent

Ask questions about a CSV file in plain English and get answers *and* charts back. This project builds a conversational data agent with **LangChain** and **Llama 4 Maverick** (hosted on IBM watsonx.ai) that writes and runs the pandas/matplotlib code for you.

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![LangChain](https://img.shields.io/badge/LangChain-Pandas_Agent-green)
![watsonx.ai](https://img.shields.io/badge/IBM-watsonx.ai-052FAD)
![Llama 4 Maverick](https://img.shields.io/badge/Meta-Llama_4_Maverick-0467DF?logo=meta&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)

---

## 🎯 Overview

Traditional exploratory analysis means writing queries, wrangling data, and hand-coding every plot. This agent removes that friction: a user types a question such as *"Generate a pie chart of average weekend alcohol consumption by gender"* and the agent translates it into Python, executes it, and renders the visualization.

It makes data exploration accessible to non-technical stakeholders while still exposing the generated code, so every result can be verified.

## ✨ Features

- **Conversational analysis**: ask questions about the data in natural language
- **Dynamic chart generation**: bar charts, pie charts, box plots, and scatter plots on request
- **Transparent code**: inspect the exact Python the LLM generated via `intermediate_steps`
- **Self-correcting agent**: the agent iterates on its own code until it produces a suitable answer
- **Result verification**: agent outputs are cross-checked against plain pandas (e.g., row count)

## 🧱 Tech Stack

| Component | Tool |
|-----------|------|
| LLM | `meta-llama/llama-4-maverick-17b-128e-instruct-fp8` on IBM watsonx.ai |
| Agent framework | LangChain (`create_pandas_dataframe_agent`) |
| LLM integration | `ibm-watsonx-ai`, `langchain-ibm`, `langchain-experimental` |
| Data & plotting | pandas, matplotlib, seaborn |
| Environment | Jupyter Notebook |

## 📁 Dataset

[Student Alcohol Consumption (math course)](https://www.kaggle.com/datasets/uciml/student-alcohol-consumption) from the UCI Machine Learning Repository: **395 students** from two Portuguese secondary schools, with demographic, family, lifestyle, alcohol consumption, and grade (`G1`, `G2`, `G3`) attributes.

## ⚙️ Architecture

```
Natural language question
        ↓
Pandas DataFrame Agent (LangChain + Llama 4 Maverick)
        ↓
LLM writes Python code → code is executed on the DataFrame
        ↓
Answer or chart returned  (+ generated code available for review)
```

The LLM is configured with `temperature=0` for deterministic output, and the agent is created with `return_intermediate_steps=True` so the generated code can be retrieved and reviewed.

## 💬 Example Prompts

| Prompt | Output |
|--------|--------|
| "How many rows of data are in this file?" | Row count (395), verified with `len(df)` |
| "Generate a bar chart to plot the gender count." | Bar chart |
| "Generate a pie chart to display average value of Walc for each gender." | Pie chart |
| "Create box plots to analyze the relationship between 'freetime' and 'G3'." | Box plots |
| "Generate scatter plots to examine the correlation between 'Dalc' and 'G3', and between 'Walc' and 'G3'." | Scatter plots |

Additional exercises explore parental education vs. grades, internet access vs. grades, and absences vs. grades.

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/ai-powered-data-visualization-agent.git
cd ai-powered-data-visualization-agent
```

### 2. Install dependencies

```bash
pip install "ibm-watsonx-ai==0.2.6" "langchain==0.1.16" "langchain-ibm==0.1.4" \
            "langchain-experimental==0.0.57" "matplotlib==3.8.4" "seaborn==0.13.2"
```

### 3. Configure watsonx.ai credentials

The notebook was developed in the IBM Skills Network lab environment, which supplies credentials automatically. To run it elsewhere, add your own watsonx.ai API key and project ID:

```python
credentials = {
    "url": "https://us-south.ml.cloud.ibm.com",
    "api_key": "<your-api-key>"
}
```

> ⚠️ Never commit API keys. Store them in environment variables or a `.env` file.

### 4. Run the notebook

```bash
jupyter notebook Text-to-chart_in_Jupyter_notebook_Visualization_Agent.ipynb
```

## 🔍 Key Takeaways

- LLM agents can turn plain-English questions into working analysis and visualization code.
- Exposing intermediate steps keeps the process transparent and auditable.
- Always validate agent output against known results, since LLM-generated code can be imperfect.

## ⚠️ Limitations

- Uses a small, single-table dataset, so results are illustrative rather than statistical conclusions.
- Generated charts can vary with prompt wording and may need rephrasing.
- The pandas agent executes LLM-generated code, so run it only in a trusted, sandboxed environment.

## 🙏 Acknowledgements

IBM Skills Network. 
Dataset courtesy of UCI Machine Learning.

## 📬 Contact

**Samuel** Data Scientist & AI Engineer · [LinkedIn](https://www.linkedin.com/in/samuel-olagbenro) · [GitHub](https://github.com/SamuelOlagbenro)
