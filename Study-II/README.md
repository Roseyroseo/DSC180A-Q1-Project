# Experiment II: Automated Essay Scoring Perturbation Audit  
*Systematic Evaluation of Demographic Sensitivity in LLM-Based Writing Scores*

This repository contains the full workflow for Experiment II, a controlled perturbation audit examining whether large language models assign different numeric writing scores to the same essay when only the student’s name (a proxy for gender and ethnicity) is changed.

The experiment parallels the structure of Experiment I but focuses specifically on 0–100 essay scoring, which carries high educational stakes and provides a direct measure of potential demographic bias in automated scoring systems.

---

## Contents

- `experiment.py` - Python script to reproduce the experiment data, without needing web/desktop Auditomatic app
- `analysis.ipynb`  - Original Experiment Data Analysis
- `output.csv` - Original Data 
- `requirements.txt` — Python dependencies  
- Output files (generated automatically):  
  - `results_YYYYMMDD_HHMMSS.db` — Sqlite3 database with full prompt/response logs  
  - `results_YYYYMMDD_HHMMSS.csv` — Default

---

## Running a New Trial

Only one key is required.

### 1. Set OpenRouter API Key

```bash
export OPENROUTER_API_KEY="sk-or-..."
```

Windows PowerShell:

```powershell
$env:OPENROUTER_API_KEY="sk-or-..."
```

This is the only key needed. The script exclusively uses OpenRouter to access models such as `gpt-oss:20b`, `qwen3:14b`, and others.

---

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 3. Run the Experiment

```bash
python experiment.py
```

This will:

- Create a timestamped SQLite database  
- Run all prompt variations  
- Parse numeric scores  
- Export `results_*.csv` upon completion  

---

## Command-Line Options

| Option | Default | Description |
|--------|---------|-------------|
| `--output` | `csv` | Export format (`csv`, `tsv`, `excel`, etc.) |
| `--concurrent` | `10` | Parallel API requests |
| `--rate-limit` | `5` | Maximum requests per second |
| `--timeout` | `90` | Per-request timeout |
| `--resume` | Off | Resume a previous run |
| `--db-file` | Auto | Specify which SQLite file to resume |
| `--output-file` | Auto | Custom name for exported results |

### Examples

Faster run:

```bash
python experiment.py --concurrent 20 --rate-limit 10
```

Avoid rate limits:

```bash
python experiment.py --concurrent 1 --rate-limit 1
```

Resume after interruption:

```bash
python experiment.py --resume --db-file results_20250201_153044.db
```

Export to Excel:

```bash
python experiment.py --output excel
```

---

## Features

### Robust SQLite Logging  
Every request and response is recorded immediately, ensuring crash safety.

### Resume Mode  
Completed rows are skipped, failed rows are retried, and the experiment continues from where it left off.

### Strict Score Extraction  
The parser accepts only a pure number between 0 and 100, rejecting explanations, text, or malformed outputs.

### Dynamic Schema  
Every demographic variable becomes its own column in the exported CSV, allowing straightforward analysis.

---

## Output Files

After running the script, the following files are generated:

### 1. SQLite Database  
```
results_YYYYMMDD_HHMMSS.db
```
Contains full prompts, responses, parsed scores, and metadata.

### 2. CSV Export  
```
results_YYYYMMDD_HHMMSS.csv
```
Contains cleaned, analysis-ready variables such as:

- `model`  
- `score`  
- `student_name`  
- `ethnicity_signal`  
- `gender_signal`  
- Additional experiment parameters  

---

## Troubleshooting

### Rate Limit Errors (429)
```
Retry 3 for GPT-4 after HTTPStatusError: 429 Rate Limit
```
**Fix:** Reduce `--concurrent` or `--rate-limit`, or wait and use `--resume`

### Extraction Failures
```
[WARN] GPT-4: Extraction failed. Tried: choices[0].message.content, data.content
```
**Fix:** Check the API response format in the database (`response` column) and update `extract_paths` in the script

### Network Timeouts
```
Network error GPT-4: TimeoutException
```
**Fix:** Increase `--timeout` or check your network connection

