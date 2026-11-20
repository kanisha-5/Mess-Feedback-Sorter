# Mess Feedback Sorter

A console-based Python project for the CIT AI-Native Engineering Programme, Semester 1, Assessment 5.

## What it does
Reads `feedback.csv`, labels every non-empty comment, validates the LLM JSON, applies a health-risk keyword safety net, and writes:
- `results.csv` — all comments and labels
- `urgent.csv` — urgent comments with original text for the warden
- `summary.txt` — category counts, negative percentage and urgent list

The program labels and sorts only. The warden reads every row in `urgent.csv`; a person decides what action to take.

## Requirements
- Python 3.9 or later
- Internet connection and Gemini API key for live LLM mode
- No third-party Python packages required

## Run offline (mock demonstration)
```bash
python mess_feedback_sorter.py --mock
python mess_feedback_sorter.py --eval --mock
```

## Run with Gemini API
1. Obtain an API key from Google AI Studio and check current free-tier limits.
2. Set the key as an environment variable.

Windows Command Prompt:
```bat
set MESS_LLM_API_KEY=YOUR_KEY_HERE
python mess_feedback_sorter.py
```

Windows PowerShell:
```powershell
$env:MESS_LLM_API_KEY="YOUR_KEY_HERE"
python mess_feedback_sorter.py
```

Optional model:
```bash
python mess_feedback_sorter.py --model gemini-2.0-flash
```

Never paste the API key into the Python file or commit it to GitHub. `.gitignore` excludes local secret files.

## Project files
- `mess_feedback_sorter.py` — complete Python program
- `feedback.csv` — sample input (22 comments; English and Tanglish)
- `system_prompt.txt` — five-role system prompt
- `one_page_specification.pdf` — one-page specification
- `evaluation_report.txt` — five evaluation checks and three red-team checks
- `judgment_framework.csv` — AI/human responsibility table
- `cost_latency_note.txt` — API-call, latency and cost estimate
- `AI_decision_journal.txt` — design decisions and controls
- `400_word_reflection.txt` — project reflection
- `results.csv`, `urgent.csv`, `summary.txt` — generated output examples

## Function map
- `classify()` — handles empty input, API/mock call, retry and fallback
- `parse_reply()` — converts JSON text to a dictionary
- `is_valid()` — checks exact fields, values, types and summary length
- `contains_health_risk()` — checks the safety-net keywords
- `write_reports()` — creates all three output reports
- `run()` — runs the complete workflow

## Suggested GitHub commits
Run these as separate commits after creating a Git repository:
```bash
git init
git add README.md .gitignore feedback.csv one_page_specification.pdf system_prompt.txt
git commit -m "Add project specification and sample feedback input"
git add mess_feedback_sorter.py
git commit -m "Implement classifier validation and safety net"
git add results.csv urgent.csv summary.txt evaluation_report.txt judgment_framework.csv cost_latency_note.txt AI_decision_journal.txt 400_word_reflection.txt
git commit -m "Add reports evaluation and project documentation"
```

## Important limitation

## Output Files

- results.csv – Contains all feedback with classification.
- urgent.csv – Contains urgent feedback for warden review.
- summary.txt – Contains category counts and feedback summary.

## Running the Project

Run `mess_feedback_sorter.py` using Python IDLE.
Use mock mode to test the project without an API key.
The offline mock mode is for repeatable demonstration and testing. For the actual LLM assessment, set `MESS_LLM_API_KEY` and run without `--mock`. Review the provider's current model availability, pricing and free-tier quota before presenting.
