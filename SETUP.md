# Group 8 — LLM Theorem Prover Setup Guide

## Prerequisites

- macOS (these instructions are for Mac)
- Python 3.10–3.12 (NOT 3.13)
- Node.js (for Gemini CLI)

---

## 1. Clone the Repo

```bash
git clone https://github.com/campbell-purdie/LLM_Theorem_Prover_Group8.git
cd LLM_Theorem_Prover_Group8
```

---

## 2. Install Isabelle2025

Download from: https://isabelle.in.tum.de/

1. Open the `.dmg` and drag `Isabelle2025` into your Applications folder.
2. Find the exact app name in your Applications folder:
```bash
ls /Applications/ | grep -i isabelle
```
3. Add Isabelle to your PATH (replace `Isabelle2025-2.app` with whatever name appeared above):
```bash
echo 'export PATH="/Applications/Isabelle2025-2.app/bin:$PATH"' >> ~/.zprofile
source ~/.zprofile
```
4. Verify it works:
```bash
isabelle version
# Should print: Isabelle2025 or Isabelle2025-2
```

---

## 3. Python Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements.txt
pip install isabelle-client==0.5.9
```

> Every time you open a new terminal, you need to reactivate the venv with `source .venv/bin/activate`

---

## 4. Set Up Gemini

1. Install the Gemini CLI:
```bash
sudo npm install -g @google/gemini-cli
```

2. Get a free API key from: https://aistudio.google.com/app/apikey

3. Set your API key permanently:
```bash
echo 'export GEMINI_API_KEY=your_key_here' >> ~/.zprofile
source ~/.zprofile
```

---

## 5. Verify Everything Works

Run the quick demo:
```bash
python3 -m prover.cli --goal 'rev (rev xs) = xs' --model 'gemini:gemini-2.0-flash'
```

You should see:
```
SUCCESS | depth: 1
lemma "rev (rev xs) = xs"
by simp
```

The Ollama warning at the start is harmless — we are using Gemini, not Ollama.

---

## Notes

- Never commit the `.venv` folder — it is in `.gitignore`
- Each team member needs their own Gemini API key
- Isabelle must be on your PATH before running any prover commands
