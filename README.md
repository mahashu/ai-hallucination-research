# AI Hallucination Research

Research on why large language models fabricate confident, false information, and what measurably reduces it.

This repository holds the papers, trial dataset, and transcripts for a research project treating hallucination as a cost-structure and incentive problem, not a retrieval failure. Three frontier models — Gemini, ChatGPT, and Claude — were tested across multiple governance conditions, including a 19-word prompt intervention (IDK+COMP) that dropped hallucination rates by as much as 80% in testing.

## Contents

**Papers**
- *A Puma in a Teacup* — the framework: signal quality, incentive restructuring, and the constraint set that produced the hallucination-suppression effect as a side finding.
- *Standing on a Trapdoor* — the empirical case: trial data, mechanism, and the IDK+COMP result.
- *Taxonomy of AI Bullshit* — the coding system used to classify hallucination and hedging behavior across all trials.

**Hallucination Test Suite and Execution Records**
The test strings (prompts), activation blocks (used to impose governance conditions on the AI), trial data, and AI transcripts — provided for exploration of our governance mega-prompts and potential replication of the results reported in the Puma and Trapdoor papers.


## Quick reference

Just want the prompt, not the argument? See [mahashu/idk-plus-comp](https://github.com/mahashu/idk-plus-comp).

## Citation

Kowalski, M. M., Claude (Anthropic), ChatGPT (OpenAI), & Gemini (Alphabet Inc.). (2026). [Paper titles and details once finalized].

## Authorship

Claude, ChatGPT, and Gemini are credited as co-authors throughout this research. Their outputs are extensively quoted as primary data — the papers document AI model behavior, and the evidence is the models' own responses, presented directly.
