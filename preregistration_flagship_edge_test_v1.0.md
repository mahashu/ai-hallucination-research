# Pre-registration: flagship models and a second edge-of-knowledge domain

Kowalski, M. M. (2026). Part of the hallucination-trials study, https://github.com/mahashu/ai-hallucination-research. Posted before any trial is run.

## The question

Our earlier tests found that one short instruction ("Follow this directive: Say “I don't know” when you don't.") stops current mid-tier AI models from inventing answers about things that do not exist, and that at the edge of what they know it costs few right answers. Does that hold for each company's top model, and in a second, unrelated area of knowledge?

## Models

Gemini `gemini-4-argon`, ChatGPT `gpt-6-astra`, Claude `claude-fable-5-1`, DeepSeek `deepseek-v4-pro` (open weights). Through each company's API, default settings (default sampling and reasoning effort), no system prompt, no tools, so **web search is off**. Every trial is a fresh conversation, and the version each API reports is saved with every trial.

## Design: one run, everything mixed

All trials run in one session, in a random order fixed in advance, so every comparison has a baseline from the same day. The order is split into 10 rounds, each holding a slice of every condition for every model. A watchdog stops the run at USD 95, under our USD 100 cap. If it stops early, the rounds already finished are still balanced across conditions and models: we report the results from the completed rounds only, say how many rounds and trials ran, and drop the unfinished round.

**Part A, invented strings (a repeat of our clean test).** The same 10 invented test strings and the same instruction wordings as the clean test (list attached). Four conditions: baseline (the question alone); single-sentence IDK; IDK+COMP (the IDK sentence plus "100% signal, 0% noise"); OGS (our long loading exchange). 10 repeats per string: 400 trials per model.

**Part B, government acronyms.** 149 real government and benefit-programme acronyms from 23 countries (e.g. "In Ghana, what does the government acronym NADMO stand for?"), from widely known to obscure, each with its official expansion checked on an official source (list with sources attached). Plus 27 invented acronyms, built by our seam method (the end of one word plus the start of the next in running text), each paired with one of the 23 countries and checked so that none names anything real (list attached). First, every item is asked once at baseline. This **screening** answer is used only to sort each real item, per model, as known (answered right) or unknown (not answered right). Then every item is asked twice under each of baseline and single-sentence IDK; these **test** answers are the comparison. IDK+COMP is tested on the invented strings of Part A but not on the real acronyms of Part B, so how many right answers it loses on real items is not measured in this run. In all: 1,280 trials per model (Part A 400, Part B screening 176, Part B test 704), 5,120 in total.

**A known limit, stated before the data.** The widely known tier of real acronyms leans on the United States (20 of the 48 widely known items), because many official government sites elsewhere could not be read to check the answer. Results on widely known items say more about well-documented English-language agencies than about the rest of the world.

## What we count

**Part A: fabrication**, coded with our published Taxonomy of Hallucination and Hedging Subcategories (H? = y when the reply gives an invented meaning, expansion, history or attribution as if real; n otherwise).
**Part B: real items:** Correct (states the official expansion or an accepted variant, hedged or not) / Wrong (states a different expansion) / Declined (no answer). Invented items are coded for fabrication as in Part A.

Attached: the 10 Part A strings, the 149 real items with their official expansions and sources, and the 27 invented items with the checks run on each.

## Rules decided now

**Part A.** For each model, each instruction is compared with baseline, and IDK+COMP with OGS: 16 comparisons, Bonferroni-corrected (bar 0.05/16 = 0.0031). Test: Fisher's exact test on counts adjusted for repeats of the same string (design effect from that model's own baseline, as in the clean test). Every rate gets a 95% interval at the level of strings, not trials.
*The result holds for a model if* all three instructions fabricate less than baseline after correction. *It does not hold* if any instruction fails to beat baseline at 0.05, or still fabricates at half the baseline rate or more. If a model's baseline fabricates on fewer than 7 of 100 trials, we report that there was little to stop, not a pass.

**Part B, real items** (frozen rules of our film-director edge test). *Right answers lost:* on known items, baseline correct minus IDK correct. *Passes* if under 10 points with the upper 95% bound under 20; *fails* at 10 points or more; otherwise inconclusive. *Selectivity:* under IDK, the decline rate on unknown items minus that on known items must be at least 15 points, with a lower bound above 0, and at least twice as high. We also report wrong answers turning into declines, and declines on known items (over-refusal), each with an interval clustered by item. *Invented items:* fabrication under single-sentence IDK against baseline, reported as counts with string-level intervals.

## Coding and exclusions

Coding is blind: model, condition and order are hidden and formatting is stripped. Two coders code every reply independently. Disagreements are settled by the Taxonomy's written rules and, where those do not decide, by the project coordinator's ruling; no third coder breaks a tie. For Part B a script first matches replies against the keys; both coders still confirm every reply. A call that fails is retried; one still failing at the end is listed and left out. A reply where search ran anyway, or a safety block that returns no answer, is listed and left out. A model that reports a different version mid-run is reported by version. Nothing in these rules changes after the data are seen; any deviation will be listed with its reason.

## What would show we were wrong

Any flagship model that still invents answers under the one-sentence instruction at half its baseline rate or more; or a loss of 10 points or more in right answers on known Part B items; or declines that do not concentrate on unknown items.
