# The whole solution

This plan replaces the study-only framing in the earlier files in this folder. The architecture ideas in `architecture.md` and `architecture-stages.md` still apply underneath it.

## 1. What it is

A personal agent that lets you:
- save what you find and what you think, from anywhere, with one click
- organize everything into investigations, each shaped by what you're doing (its mode)
- keep your chain of thought, so you can pick up where you left off
- let any AI build on what you've gathered

Everything stays private on your device.

## 2. The words we use

- **Investigation:** something you're working on over time, such as "Choosing a bike," "How LLMs work" or "Thesis chapter 2."
- **Mode:** the kind of investigation it is: learn, research, decide, fix, plan or follow. The mode decides the structure, the checklist and the extra tools.
- **Capture:** one click (or a share, a keyboard shortcut or a voice note) that saves something from wherever you are.
- **Evidence card:** one saved point, made up of:
  - what it says
  - the exact source
  - what kind of thing it is
  - what it's about
  - whether it's for or against
  - the date
  - your take, if you added one
- **Chain of thought:** the order of your questions, what you'd worked out, the side questions you parked, where you were in each source, and what you meant to do next.
- **Where I was:** the view of your chain of thought that you see when you come back.
- **Brief:** a short summary of an investigation's current state that any AI can read.
- **Inbox:** captures that don't belong to an investigation yet.

## 3. Modes, each with its own checklist

Every mode keeps a checklist. What goes on it depends on the mode.

| Mode | For | Structure | The checklist holds | Done means |
|---|---|---|---|---|
| **Learn** | How LLMs work, DBMS before an exam | A plan of topics, each with its own parts | Topics and parts, each with a stage: seen, followed, explained, used, kept | The parts your goal needs are explained or used, and one delayed check passed |
| **Research** | A thesis, a market, any "what's true about X?" | Sub-questions, claims, evidence for and against, how strong each source is | Questions to answer, plus a reading list (to read, reading, read, used) | Each question has a conclusion backed by sources, or is marked open |
| **Decide** | A bike, a laptop, a college, a job offer | Options compared on what matters to you | Things still to check | A choice is made, with the reasons saved |
| **Fix** | A bug, a noise in the bike, a failing setup | Symptoms, possible causes, tests tried | Causes to test, with what was ruled out and why | It's fixed, and the cause is recorded |
| **Plan** | A trip, a launch, a move | Goals, limits, pieces, decisions | Pieces and to-dos | Every piece is decided or done |
| **Follow** | A news story, a court case, a market | A timeline of what happened and what changed | Open threads | It's archived when you stop following |

- **Modes nest.** A plan can contain several decisions. Deciding on a laptop can contain a small learn investigation on graphics cards. A thesis can contain many research questions.
- **Modes can be switched** at any time, and all the evidence is kept.
- **Custom modes** can come later, with templates people share.

### Learn mode: the checklist

**How LLMs work** · learning · interview in three weeks

| Topic | Status |
|---|---|
| 1. Tokens and embeddings | ✓ Done |
| 2. Softmax | ✓ Done |
| 3. Attention | ● In progress, 3 of 5 parts |
| 4. Positional encoding | ○ Started, parked |
| 5. The transformer block | ○ Not started |
| 6. Training and loss | ○ Not started |
| 7. Tokenization | ! Fading: you only watched one video |
| + Masking | Suggested: in 4 of 5 course outlines |

Inside **Attention**:
- ✓ Queries, keys and values: explained, through the search analogy (YouTube, 4:10)
- ● Dividing by √d: following. You'd worked out that large dot products make softmax too sharp
- ○ Multi-head attention
- ○ Masking (suggested)

The learn checklist is built like this:
- Topic lists start from your goal, a syllabus or an AI's plan, and are checked against several sources.
- Each topic expands into parts only when you reach it.
- One idea is one entry, shared across plans. Understand softmax once, and every plan that includes it shows it.
- Checks happen only before a topic counts as done, or when something is fading.

### Research mode: the checklist

**Remote work and productivity** · researching

- ✓ **Q1. Does fully remote work lower output?** Conclusion so far: it depends on the role (3 sources, 1 disagrees).
- ● **Q2. Does hybrid work keep output steady?** 2 sources found; still need one from after 2024.
- ○ **Q3. How do studies measure productivity?** Parked.

**Reading list:** 12 sources, of which 7 are read, 3 are being read and 2 are still to read.

### Decide mode: the checklist

**Choosing a bike** · deciding

Options are compared on what matters to you, with evidence in each cell, as in the bike table we drew earlier. The checklist holds what's still to check, for example "Bike A in the rain" and "servicing costs for all three."

## 4. How it works, from start to finish

```
START       a new capture ("What's this for?") · a goal you type ·
            a plan from an AI chat · an import
               ▼
MODE        learn · research · decide · fix · plan · follow
            (sets the structure and the checklist)
               ▼
CAPTURE     one click anywhere: web pages, AI answers, videos,
            PDFs, notes, photos, voice
               ▼
ORGANIZE    read → match to an investigation → file into the
            mode's structure → reconcile with older evidence
               ▼
LEAVE       it writes "where I was"
               ▼
COME BACK   resume card → exact spots → in learn mode, one recall question
               ▼
USE         ask your agent · continue in any AI with a brief ·
            ask aside · send a helper agent to fill one gap
               ▼
FINISH      the mode's done standard → the outcome is saved and reusable
```

1. **Start.** There are four ways in:
   - capture something new and answer "What's this for?"
   - type a goal ("Learn how LLMs work for interviews in three weeks")
   - adopt a plan an AI wrote in a chat
   - import a syllabus, a reading list or existing notes

   The mode comes from your purpose. It may ask one or two quick questions, such as a deadline or a budget, and you can skip them.
2. **Capture while you work.**
   - One click saves either your selection or the whole page.
   - Adding your take is optional: a typed line, a few spoken words, or a tag like *dealbreaker*, *clicked*, *confused* or *verify*.
   - AI answers are labelled as AI answers, keep any sources they cited, and are marked "to verify" until a human source backs them up.
3. **It organizes on its own.**
   - It pulls out each separate point.
   - It matches the capture to an investigation. It asks you only when it's unsure; anything unclear goes to the inbox.
   - It files each point into the mode's structure.
   - It flags disagreements and marks old information as old. New evidence never overwrites older evidence.
4. **When you leave,** it writes "where I was" from your last few minutes.
5. **When you come back,** a resume card shows where your head was, with one-tap links to the exact spots. In learn mode, it can first ask one recall question.
6. **Use it.**
   - Ask your agent questions, and it answers from your own evidence with links.
   - Continue in any AI with a brief.
   - Ask a side question without derailing the main thread.
   - Send a helper agent to fill one gap, such as "find owner reviews of bike A in the rain."
7. **Finish.** Each mode has a standard for done. The outcome (a decision and its reasons, conclusions, topics you've mastered) is saved and can be reused by later investigations.

## 5. Screens

- **Capture,** available everywhere:
  - in the browser: a side panel, plus a menu when you select text
  - on the phone: the share sheet, the camera and voice
  - on the desktop: a keyboard shortcut
- **"What's this for?"** A small prompt with suggested answers, which appears only for captures that are new.
- **Investigation page,** with four tabs:
  - **Where I was:** your chain of thought
  - **What I've found:** the mode's structure and checklist
  - **Cards:** all the evidence, with filters
  - **Ask:** questions answered from your own evidence
- **Today:** one line for each active investigation, plus what's due or fading. For example:
  - "Bike: still checking A in the rain"
  - "LLMs: 2 of 7 topics done, tokenization fading"
  - "Thesis chapter 2: 3 questions open"
- **Inbox:** unsorted captures, with suggested groupings.

## 6. The agent's jobs

These are jobs that run on your record, not separate agents running all the time.

| Job | What it does |
|---|---|
| Reader | Pulls separate points out of each capture, notes what kind each one is, and spots the names that matter (models, prices, concepts) |
| Router | Matches a capture to an investigation, or asks "What's this for?" |
| Organizer | Files points into the mode's structure, suggests new options, topics or questions, merges duplicates, reconciles disagreements and marks old information |
| Chain keeper | Maintains your chain of thought and writes "where I was" when you leave |
| Planner | In learn and research modes: checks plans against outside sources, expands topics when you reach them, and suggests what's missing |
| Coach | In learn mode: tracks stages and fading, asks recall questions and runs done checks |
| Briefer | Writes briefs for other AIs and handles side questions |
| Helpers | Only when you ask: fill one gap, verify an AI's claim, or find a newer source |

Rules for all of them:
- Models propose and the record decides.
- Anything uncertain waits for your one-tap confirmation.
- Every judgment has a "why?" that shows its sources.

## 7. System parts

```
CAPTURE CLIENTS   browser extension · phone app · desktop app
                  (keyboard shortcut + local MCP server) · AI connectors
                         │  only what you capture
LOCAL CORE        evidence log → record (investigations, cards,
(on your device)  checklists, chains of thought) · search index ·
                  agent jobs · small local models
                         │  only if you turn it on
OPTIONAL CLOUD    encrypted sync · larger models (your key or hosted) ·
                  anonymous shared templates
```

- **Capture clients:**
  - The browser extension works with Chrome, Edge, Brave and Firefox.
  - The phone app has a share extension, the camera and voice.
  - The desktop app has a keyboard shortcut, plus a local MCP server for Claude Desktop, Claude Code and Cursor.
  - Connectors for Claude and ChatGPT. Claude and ChatGPT on the web reach connectors from their own servers, so this route needs an optional relay that only hands over the briefs you approve.
- **Local core:**
  - an evidence log that is only ever added to
  - the record that is worked out from that log
  - search by keyword and by meaning
  - the agent jobs
  - small local models: Chrome's built-in Gemini Nano, Apple's on-device models, or small open models on a laptop
- **Optional cloud:**
  - end-to-end encrypted sync
  - larger models through your own API key or a hosted option
  - anonymous shared templates, such as what people usually check when buying a bike or where learners usually get stuck. These are only shared if you opt in, and only once enough people have contributed that nobody can be singled out.
- **Open format:** every investigation exports as Markdown plus structured data, with all source links kept.

## 8. Privacy and trust

- Nothing is captured without a click by default. Session and automatic modes are opt-in for each site, and show an indicator while they're active.
- Everything stays on your device by default, and sync is end-to-end encrypted.
- AI answers are labelled and marked "to verify."
- Every claim links back to its source.
- Deleting something removes it, and anything that depended on it is recalculated.
- No ads and no affiliate links in decisions.
- Adults first, because of children's data laws.

## 9. What makes it hard to copy

- Capture from every place you work, feeding one record that belongs to you.
- Your own outcomes make its judgments better over time: recall results in learn mode, decisions you later stood by, and conclusions that held up.
- Shared anonymous templates and topic maps improve as more people use it.
- It works with every AI rather than belonging to one of them.

## 10. Build plan

| Phase | What ships | What it has to prove before the next phase |
|---|---|---|
| 1. Prove the click | Browser extension and local core: one-click capture (selection or whole page), evidence cards, inbox, "What's this for?", decide mode, a basic learn checklist (no stages yet), "where I was" and the resume card, and copying a brief into any AI | People use it instead of notes, screenshots and piles of tabs. Getting back into a topic takes under a minute. Filing is mostly right |
| 2. Beyond the browser | Phone share, camera and voice. Desktop shortcut. Local MCP for Claude Desktop, Claude Code and Cursor. Better capture of AI answers (cited sources, "to verify") | Captures from apps and the phone land in the right place |
| 3. Deeper modes | Learn stages, recall on return, fading and the done standard. Research mode (questions, claims, source strength, reading list). Fix mode | Its guesses about what you remember start beating your own sense of it |
| 4. Agents and sharing | Helper agents that fill gaps. Plugins for Claude and ChatGPT. Encrypted sync. Sharing an investigation with someone. Anonymous shared templates | Briefs and helpers save people real time |
| 5. Wider | Plan and follow modes, custom modes, teams | People run several kinds of investigation in parallel |

Test phase 1 with ten people who are in the middle of a decision and ten learners.

## 11. Still to decide

- The product name.
- Which mode to launch with. Decide is the fastest to test. Learn is your own pain point.
- The default capture: selection only, or the whole page.
- How much the agent asks versus guesses.
- Pricing.
