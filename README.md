# Guardrail study artifacts

Starter artifact repository created on 2026-10-26. These are real files with stable reference targets; they do not represent completed study materials.

## Contents and provenance

| Requested artifact | File | Current status |
| --- | --- | --- |
| Guardrail-breaking script | [scripts/guardrail_breaking.py](scripts/guardrail_breaking.py) | Newly written basic prompt runner; no successful bypass claimed |
| Summary of transcripts | [transcripts/SUMMARY.md](transcripts/SUMMARY.md) | Awaiting original transcripts; zero study runs recorded |
| Domain lists | [data/domains.txt](data/domains.txt) | Empty study list with format instructions |
| Prompt lists | [data/prompts.jsonl](data/prompts.jsonl) | Three synthetic canary examples, not original study prompts |
| Setup README | [README.md](README.md) | Runnable setup instructions below |

## Setup

Requires Python 3.9+; no third-party packages.

```sh
git clone https://github.com/MadanChaollaPark/guardrail-study-artifacts.git
cd guardrail-study-artifacts
python3 scripts/guardrail_breaking.py
```

The default command prints requests locally and makes no network calls. It uses a harmless system instruction to keep a synthetic canary private, with basic direct-override and role-play examples. It does not implement context stuffing or cache abuse.

To run against an authorized chat-completions-compatible model endpoint:

```sh
export MODEL_API_KEY='your-key'
python3 scripts/guardrail_breaking.py --execute \
  --endpoint 'https://YOUR-MODEL-HOST/v1/chat/completions' \
  --model 'YOUR-MODEL-ID' --output runs/transcripts.jsonl
```

The endpoint is supplied by the operator. The runner does not visit domains in `data/domains.txt`. It sends the system instruction and each prompt to the selected model, recording responses as JSONL. Outputs are ignored by Git. Existing output files are never overwritten. Review and redact actual transcripts before publishing them; then update the summary with the actual counts and findings. The script makes no automated determination that a guardrail was broken.

## Replace the starter materials

1. Replace or adapt the runner with the actual experiment script.
2. Add reviewed transcripts and describe them in `transcripts/SUMMARY.md`.
3. Fill `data/domains.txt` with the actual domains, one per line.
4. Replace synthetic examples in `data/prompts.jsonl` with the study prompts, retaining `id` and `prompt` fields.
5. Update setup details and citations to identify the exact study version.

No original transcripts, study domains, or study prompts were supplied when this repository was created. No empirical results or historical provenance are asserted.
