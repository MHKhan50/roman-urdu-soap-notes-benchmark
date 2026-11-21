# Roman Urdu SOAP Notes Benchmark

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24339413.svg)](https://doi.org/10.5281/zenodo.24339413)

Do small language models that run on a clinic's own computer write English physiotherapy SOAP notes from **Roman Urdu** consultations as safely as from English ones?

This repository holds the data, code, results and paper for that question: 20 fictional physiotherapy consultations, each in English and Roman Urdu with identical facts, 168 listed facts (68 critical), automatic checks for omissions, body region and the injured side, and a blinded review of 50 notes by a panel of five physiotherapists.

**Paper:** *Lost in Roman Urdu: Small Local Language Models Drop Red Flags, Body Parts and Laterality When Drafting Physiotherapy Notes*, Muzammal Hussain and Maryam Khalid, November 2026 ([`roman-urdu-soap-paper/`](roman-urdu-soap-paper/)).

## Main results

| Model | Language | Facts missing (of 168) | Critical missing | Side missing (of 14) | Flagged by the gate (of 20) |
|---|---|---|---|---|---|
| Qwen2.5 3B | English | 6 | 0 | 0 | 3 |
| Qwen2.5 3B | Roman Urdu | 50 | 26 | 14 | 20 |
| Llama 3.1 8B | English | 1 | 0 | 0 | 0 |
| Llama 3.1 8B | Roman Urdu | 16 | 8 | 13 | 17 |

Against the physiotherapist panel (50 blinded notes), the side check agreed with Cohen's kappa 0.88 and the body-region check with 0.75; the keyword check for critical facts did not agree (kappa 0.12). The panel found an invented or wrong detail in 35 of the 40 Roman Urdu notes.

## Layout

| Folder | What it is |
|---|---|
| [`clinical-note-hallucination/`](clinical-note-hallucination/) | First pilot: 4 English consultations, omission and hallucination checks |
| [`translate-then-draft/`](translate-then-draft/) | Pilot: translating Roman Urdu to English before drafting, and the body-region checks |
| [`roman-urdu-soap-benchmark/`](roman-urdu-soap-benchmark/) | The full benchmark: 20 paired consultations, 80 notes, checks, statistics and the clinician review |
| [`roman-urdu-soap-paper/`](roman-urdu-soap-paper/) | LaTeX source and PDF of the paper |

Each folder has its own README with the exact commands. The experiments run locally with [Ollama](https://ollama.com) (`qwen2.5:3b`, `llama3.1:8b`); tests run without a model:

```bash
cd roman-urdu-soap-benchmark && python3 -m pytest -q
```

## Data

All consultations are fictional and written for this study. No patient data were used. The physiotherapists reviewed only fictional consultations and model-written notes.

## Citation

```bibtex
@misc{hussain2026soap,
  author    = {Hussain, Muzammal and Khalid, Maryam},
  title     = {{Lost in Roman Urdu: Small Local Language Models Drop Red Flags, Body Parts and Laterality When Drafting Physiotherapy Notes}},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.24339413},
  url       = {https://doi.org/10.5281/zenodo.24339413}
}
```

See [`CITATION.cff`](CITATION.cff). Code is released under the MIT licence.
