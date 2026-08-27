# App Savvy

**A judgment-training environment for business people who direct software without becoming engineers.**

Live: [ms-amapostol.github.io/app-savvy](https://ms-amapostol.github.io/app-savvy/)

It is easy to finish a technical course able to recognize the word "API" and still unsure whether the integration your vendor just proposed is a reasonable one. App Savvy is built for the second half of that: the judgment to sit in a design conversation, understand what is being traded away, and argue for the right option.

It is one HTML file. No build step, no framework, no backend. Everything a learner does stays in their browser.

---

## What's in it

| | |
|---|---|
| **39 units** across 6 chapters | Each with a history beat, a live-tools section, and a working vocabulary |
| **60 decision doors** | Two defensible options, a choice, and the documented cost of the road not taken |
| **28 SQL exercises** in 6 stages | Graded against a real in-browser SQLite database, from `SELECT` to window functions and cohort retention |
| **11 sabotage rounds** | A working thing is broken; find the break |
| **A live Agent Lab** | Real Anthropic API calls, real tool definitions, a real loop, including one tool that reaches an external public API |
| **Two writing rooms** | A requirements brief and an ROI model, both reviewed against a rubric |
| **A competency record** | Exportable evidence of what was actually completed, built to be checked |

### The chapters

1. **Foundations** — how software actually works
2. **Building and running it** — what happens after it works
3. **Working with data** — answers you can defend
4. **Turning work into systems** — where this gets paid for
5. **Holding your own** — the technical half of the job
6. **Building agents** — the part where you make one

---

## Design decisions

Everything below was a real choice with a live alternative. Several were reversed mid-build after they failed in use.

### Instruction and practice live in separate rooms

The Learn tab teaches. The Practice tab and the labs apply. These never mix.

The tempting design is a lesson with exercises embedded in it. It feels efficient and it demos well. In actual use it breaks down: when a question interrupts a lesson, the learner starts optimizing for finishing the question, and comprehension quietly degrades into pattern-matching. Separating the rooms costs some perceived cohesion. It buys the thing the app exists for.

### Doors show what the other choice would have cost

A decision door presents a real design decision with two options a competent person could defend. The learner picks, argues for the pick in their own words, and then sees two things: what happened downstream, and **what the other door would have cost.**

That second half is the whole mechanism. A multiple-choice question with one right answer trains recall. A door with a real price attached to the option you declined trains what senior people actually do, which is hold two defensible paths in mind and choose deliberately.

Doors carry no score. They carry a principle, and the principles accumulate into the competency record as architecture decision records — the same format working engineering teams use for exactly this.

### The SQL Lab runs a real database

The lab loads SQLite compiled to WebAssembly (`sql.js`) with a seeded schema. It grades submitted queries by comparing result sets. A learner can write a query I never anticipated, and if it returns the right rows, it passes.

String-matching the expected answer would have been far cheaper to build. It also teaches the shape of an answer, which is a different skill from getting one. The real engine costs a 1.5MB WebAssembly download and a fallback path for browsers that block it. Worth it.

### The Agent Lab makes real calls

The agent chapter ends with a lab that runs the loop from the lesson against the live Anthropic API: real tool schemas, real `tool_use` blocks, a turn ceiling, a token counter, and a write-tool that pauses for human confirmation before it fires. The capstone adds a tool that calls a public weather API over the actual internet, so the learner watches a tool fail and recover for real.

A simulated agent would have been simpler and would never break. It would also let a learner finish the chapter having never seen a model choose a tool they did not expect, and that experience is the entire point of the chapter.

### Every history beat is cited

Each unit carries a history beat, and every claim in one traces back to a primary source: the RAG paper at NeurIPS 2020, IEEE 830, Lewin in *Human Relations* 1947, Kotter in *HBR* 1995, Solow's productivity-paradox remark in 1987, the NIST AI RMF.

These exist because knowing why a pattern won tells you when it stops applying. That is judgment. Trivia would be knowing the year alone.

### Progress exports as evidence

XP and badges exist, and they are deliberately secondary. The primary output is an exportable competency record listing units completed, exercises solved, how many were solved without hints, and every architecture decision argued — with a note explaining how a reader could verify it.

It is built to survive a skeptical hiring manager reading it closely, which meant designing for auditability first and impressiveness second.

### Everything stays in the browser

State lives in `localStorage`. There is no account, no server, and no telemetry. A learner's API key, if they add one, never leaves their machine.

This rules out cross-device sync and cohort analytics. In exchange, the app can be forked, opened from a hard drive, and used by anyone without a signup. For what this is meant to do, that was the better trade.

### One file

The entire application — markup, styles, curriculum, exercise bank, database seed, and logic — is a single `index.html`. Deployment is a `git push`. There is no build pipeline to break, no dependency tree to age, and no version of this project that becomes unusable because a package was deprecated.

The cost is real. The file is large, and finding things in it takes discipline. For a project maintained by one person and deployed to static hosting, that trade was worth making.

---

## Running it

Open `index.html` in a browser. That is the whole setup.

To serve it locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening the file directly from disk works for everything except the SQL Lab, whose WebAssembly engine is blocked by browser security on `file://` origins. Serving it over HTTP fixes that.

**Optional:** the Agent Lab, the AI teach-back grader, and the brief reviewer call the Anthropic API. Add a key under the **AI & Data** tab to enable them. Everything else works without one.

---

## Built with

- **Vanilla JavaScript** — no framework, no build step
- **[sql.js](https://sql.js.org/)** 1.10.3 — SQLite compiled to WebAssembly, loaded from CDN with a local fallback
- **Anthropic API** — Claude, called directly from the browser for the optional AI features
- **GitHub Pages** — static hosting

---

## Status

Actively built and actively used. I am working through the curriculum as a learner while extending it, which is the point: every unit has to survive being read by someone who needs it.

*Part of the [Your Next Step](https://yournextstepai.com) family.*
