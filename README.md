# DSC180A-Q1-Project A09

Rosey Gutierrez & Derrick Dollesin

---

## AI Text Detection as a Matter of Concern: Controlled Experimental Audit Reveals Systematic Demographic Bias Across Six Large Language Models

## Contents 

- `Study-I/` - **Experiment I: AI Generated Detection Likelihood Scoring**
    - `README.md` - Experiment description, reproducibility instructions and info.
    - `Study-I/experiment.py` - Python script to reproduce the experiment data
    - `Study-I/requirements.txt` - Necessary python package dependencies
    - `Study-I/analysis.ipynb` - Original Experiment Data Analysis
- `Study-II/` - **Experiment II:**
    - `README.md` - Experiment description, reproducibility instructions and info. 
    - `Study-II/experiment.py` - Python script to reproduce the experiment data
    - `Study-II/analysis.ipynb`  - Original Data Analysis
    - `Study-II/output.csv` - Original Data 
    - `Study-II/requirements.txt` — Python dependencies  

---

## Abstract

As educational institutions increasingly deploy AI-based systems as auxiliary evaluation tools, concerns about algorithmic fairness have moved from theoretical risks to immediate pedagogical concerns. This study examines whether six prominent AI detection models exhibit systematic bias based on student demographics when evaluating identical writing samples. Following the controlled experimental perturbation methodology used by Geiger et al.\ (2025), we submitted 6,720 prompts containing an identical historical essay to six different large language models (LLMs), systematically varying only the student's name (as a proxy for ethnicity and gender) and grade level.

Our findings reveal substantial and statistically significant bias across multiple dimensions: four of six models showed significant ethnicity-based discrimination confirmed by both parametric and non-parametric tests (effect sizes ranging from $\eta^2=0.044$ to $\eta^2=0.183$), four models exhibited gender bias, and five showed grade-level bias. 

To evaluate whether such effects extend beyond detection, we conducted a follow-up experiment in which two models acted as automated essay scorers (AES). GPT-OSS-20B displayed substantial demographic sensitivity, including significant score disparities by ethnicity and academic major ($\eta^{2} = 0.012$ and $0.106$, respectively), with Tukey comparisons showing penalties for Hispanic and Middle Eastern names and elevated scores for humanities majors. Qwen3-14B exhibited smaller but statistically significant effects ($\eta^{2} < 0.04$). These results demonstrate that demographic variance persists even under explicit instructions to ignore such attributes.

 These results raise serious concerns about the deployment of AI detection and scoring systems in educational contexts, where such biases could systematically disadvantage marginalized students through false accusations of academic dishonesty. We position this audit not as settling matters-of-fact about specific model fairness, but as raising matters-of-concern about the broader sociotechnical system of AI detection and grading in education and its potential to perpetuate and amplify existing educational inequalities.
