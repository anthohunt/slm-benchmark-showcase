**English** · [Français](README.fr.md)

**Anthony Hunt** · [Project page on ingevision.cloud](https://ingevision.cloud/?lang=en&p=banc-slm) · [LinkedIn](https://www.linkedin.com/in/anthony-hunt-3948a9196) · [GitHub profile](https://github.com/anthohunt)

> Showcase repository: the code and data of this project are private; this README describes it.

# Small-model benchmark

A web bench that puts the same set of 28 questions to small language models (SLMs) and scores their answers without a human or LLM judge.

## The problem

Choosing a small model for an on-device agent (virtual reality headset, smartphone) requires knowing what it actually gets right, with which instructions and within which memory. The bench was built for a supervised internship at an engineering school: the student runs series and reads the results on their own.

## How it works

- Three settings: the model, the target hardware (Quest 3 headset, 8 or 12 GB smartphone, 16 GB laptop, 32 GB workstation, server) and the system prompt. The hardware sets the context size; devices the model does not fit on are removed.
- 28 questions in three families: 5 performance indicator trees, 6 causal chains, 17 multiple-choice questions on a course, with retrieval from that course (RAG).
- Each answer is validated against a schema, then scored by deterministic rules: tree or chain structure, allowed transitions between node types, exact letter for multiple-choice questions.
- The main score is the number of fully correct questions; alongside it, first-attempt successes and the average of rules passed.
- Each question expands: failed checks, raw answer, 3D graph of the model's answer next to a reference answer.

## What is built

Running continuously on the institution's internal network.

- Three models available: Gemma 4 26B, Gemma 4 8B and LFM2.5-1.2B, the target small model.
- System prompts saved as versions per family; a prompt modified without being saved is flagged and marked in the history.
- Run history and a curve that only links comparable runs.
- Check before handover: 6 combinations out of 6 with no technical error. Time per question: 120 to 175 s for the 26B, 40 to 57 s for the 8B, 14 s for LFM2.5.
- Models run on CPU: measured latencies say nothing about a GPU or a headset.
- Not done yet: archiving the exact prompt text with each run, repeating a question to measure variance, keeping raw output from complete failures.

## What is public

This showcase is public; the code, questions and results remain private, in the institution's repository.

## Tech stack

- Python, uv
- Ollama, pydantic-ai and Pydantic for structured outputs
- LangChain, Chroma and nomic-embed-text for course retrieval
- Three.js for 3D graphs
- Docker Compose
