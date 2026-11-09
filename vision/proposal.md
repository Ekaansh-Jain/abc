# Proposal: a personal agent that saves your chain of thought

*Working name to be decided.*

## Summary

Research anything your own way, wherever you look. One click saves what you found and what you thought about it. Your agent organizes it, keeps your chain of thought so you can pick up exactly where you left off, and lets any AI build on it. Everything stays private, on your device.

## 1. The problem

People now think across many tools at once: two or three AI chats, Google, YouTube, Reddit, PDFs and their own notes. None of these tools share anything with each other, so the thread of their thinking gets lost:
- They can't find again what they saw ("where did I read that?").
- They lose where they were when they take a break, hit a usage limit or switch tools.
- They forget why they ruled something out, or what made something finally make sense.
- Their notes are messy, out of date, or never written at all.
- They act on AI answers without checking them.

**What it looks like:**
- **Learning:** a student learning how LLMs work asks Claude for a topic list and gets confused. They ask ChatGPT, switch to a YouTube video, then work something out on GeeksforGeeks. A few hours later they can't find where they were or what they'd understood.
- **Deciding:** someone buying a bike asks ChatGPT, reads owners on Reddit, watches reviews and visits shops. They lose track of who said what about which bike.
- **Researching:** a researcher spends months across papers, chats and notes, and can't trace a claim back to where it came from.
- **Building:** a developer's coding session with an AI agent ends halfway through debugging, and the next tool starts without knowing what was already ruled out.

**Evidence that it's real and widespread:**
- AI use is close to universal. [95% of UK undergraduates use AI](https://www.hepi.ac.uk/2026/10/09/every-student-needs-a-minimum-ai-requirement/), ChatGPT has [1.2 billion weekly users](https://www.forbes.com/sites/gabrielalinzainescu/2026/11/05/chatgpt-search-hits-20-of-googles-query-volume-openai-says/), and [84% of researchers use AI](https://www.sspnet.org/ai-adoption-jumps-to-84-among-researchers-as-expectations-undergo-significant-reality-check/).
- People use several AIs. One survey found [over 80% use two or more](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6436999).
- Understanding things is one of the biggest uses of AI. About [10% of ChatGPT messages are tutoring or teaching](https://blogs.worldbank.org/en/impactevaluations/ai-chatbots), and [about half are people asking for information or advice](https://www.nber.org/papers/w34255).
- Finding things again was a problem even before AI chats. [Up to 40% of search queries](https://dl.acm.org/doi/abs/10.1145/1277741.1277770) were people looking for something they had already seen.
- People act on AI without checking it. [78.5% have made a real-life decision based on AI, but only 17.4% always verify what it says](https://natlawreview.com/press-releases/nearly-80-americans-make-decisions-based-ai-only-17-consistently-check).
- People already build workarounds, such as ["handoff prompts"](https://dev.to/novaelvaris/the-handoff-prompt-transfer-ai-context-between-models-without-losing-state-39a4) for moving context between AIs, and pasted summaries to restart chats that hit their limit.
- Interruptions are constant. Workers are [interrupted by a meeting, email or chat ping about every two minutes](https://blogs.microsoft.com/blog/2025/04/23/the-2025-annual-work-trend-index-the-frontier-firm-is-born/).

## 2. Why it hasn't been solved

| What blocked it | Evidence | What's different now |
|---|---|---|
| Models of what a learner knows only worked inside a company's own lessons | Knewton raised more than $180 million and was [sold for less than $17 million](https://www.edsurge.com/news/2019-09-07-knewton-was-acquired-for-less-than-17m-and-former-ceo-brian-kibby-has-left) | AI can now judge a free-form explanation, so understanding can be measured anywhere |
| Apps never agreed to read from a store the user owns | Solid, Tim Berners-Lee's personal data project, [needed companies to adopt it](https://www.theregister.com/2020/11/10/inrupt_server_bernereslee/) | We don't need apps to adopt anything. The user's own browser, data exports and MCP (now a shared standard) are enough |
| Capturing everything feels like surveillance | Microsoft's Recall was called a ["privacy nightmare"](https://www.bbc.co.uk/news/articles/c869glx8endo), and [Rewind was shut down](https://9to5mac.com/2025/12/05/rewind-limitless-meta-acquisition/) | Capture only happens when the user clicks, stays on their device, and gives something back straight away |
| Tools that need effort get dropped | Writing good flashcards is hard, which is [a big reason most people never stick with Anki](https://www.marknagelberg.com/notes-on-developing-transformative-tools-for-thought/) | Capturing is a by-product of doing the work, taking one click and an optional few words |
| No AI company gains from making rival tools smarter | AI memory imports are [one-time snapshots, and nothing keeps AIs in sync](https://blog.memoryplugin.com/sync-memory-across-chatgpt-claude-gemini-perplexity-grok/) | That leaves room for a neutral layer that works with every AI |
| Thinking tools are easy to copy | Matuschak and Nielsen describe them as [public goods](https://numinous.productions/ttft/): expensive to build, cheap to copy | The product becomes hard to copy through data that builds up over time and across users, not through features |

## 3. Why now

- **AI can grade explanations.** One study found AI graders [agreed with human graders in 70 to 80% of cases](https://arxiv.org/pdf/2412.06910v2), about as often as two human graders agree with each other.
- **AI apps share a connection standard.** MCP is [used by ChatGPT, Gemini, Copilot and Cursor](https://www.anthropic.com/news/donating-the-model-context-protocol-and-establishing-of-the-agentic-ai-foundation) and has been run by a Linux Foundation body since December 2025.
- **AI models run on the device.** Small models built into browsers and phones make processing cheap and private.
- **Confusion now gets written down.** In AI chats, people type out exactly what they don't understand, which wasn't recorded anywhere before.
- **Using several AIs at once** has made the problem new, and worse.

## 4. The solution

### What it does

1. **Capture from anywhere.** One click saves web pages, AI answers, videos, PDFs, notes, photos and voice notes, from a browser, a desktop app or a phone.
2. **Organize automatically.** Everything is sorted into investigations, each shaped by what you're doing.
3. **Keep your chain of thought.** When you come back, you see where your head was.
4. **Let any AI build on it.** You can continue in any AI with a short brief, ask a side question without derailing the main thread, or send a helper agent to fill one gap.

### Our approach

Most agents try to do the research for you and hand you a summary. This one lets you research your own way, and keeps your reasoning together with the evidence. It works alongside other agents instead of competing with them.

### Key terms

- **Investigation:** something you're working on over time, such as "Choosing a bike," "How LLMs work" or "Thesis chapter 2."
- **Mode:** the kind of investigation it is. The mode sets the structure, the checklist and the extra tools.
- **Evidence card:** one saved point. It records:
  - what it says
  - the exact source
  - what kind of thing it is
  - what it's about
  - whether it's for or against
  - the date
  - your own take, if you added one
- **Chain of thought:** the order of your questions, what you'd worked out, the side questions you set aside, where you were in each source, and what you meant to do next.
- **Brief:** a short summary of where an investigation stands, written so any AI can read it.
- **Inbox:** captures that don't belong to an investigation yet.

### Modes, each with its own checklist

| Mode | For | Structure | The checklist holds | Done means |
|---|---|---|---|---|
| **Learn** | How LLMs work, DBMS before an exam | A plan of topics, each with its own parts | Topics and parts, each with a stage: seen, followed, explained, used, kept | The parts your goal needs are explained or used, and you've passed one check a few days later |
| **Research** | A thesis, a market, any "what's true about X?" | Sub-questions, claims, evidence for and against, and how strong each source is | Questions to answer, plus a reading list (to read, reading, read, used) | Each question has a conclusion backed by sources, or is marked open |
| **Decide** | A bike, a laptop, a college, a job offer | Options compared on what matters to you | Things still to check | A choice is made and the reasons are saved |
| **Fix** | A bug, a noise in the bike, a broken setup | Symptoms, possible causes, tests tried | Causes to test, with what was ruled out and why | It's fixed and the cause is recorded |
| **Plan** | A trip, a launch, a move | Goals, limits, pieces, decisions | Pieces and to-dos | Every piece is decided or done |
| **Follow** | A news story, a court case, a market | A timeline of what happened and what changed | Open threads | You archive it when you stop following |

Modes can nest inside each other. Deciding on a laptop can contain a small learn investigation on graphics cards, and a thesis can contain many research questions. You can switch an investigation's mode at any time, and all its evidence is kept.

### Example: deciding on a bike

1. ChatGPT suggests three bikes, and one click saves them as options.
2. On Reddit, an owner says Bike B's brakes squeak after rain. You select it, tap **Con** and say "dealbreaker."
3. A YouTube review shows Bike A's frame at 7:32. You tap **Pro**.
4. A shop page has Bike C on sale, and you save it with the price and date.
5. At the store, you photograph the spec sheet and say "seat is uncomfortable."

A week later:

**Choosing a bike** · deciding · 14 pieces of evidence

What matters to you: within budget · handles rain · comfortable for 10 km a day

| | Bike A | Bike B | Bike C |
|---|---|---|---|
| **Price** | Within budget | Within budget | 15% off until Sunday |
| **Rain** | No evidence yet | ✗ Brakes squeak after rain (3 owners on Reddit) | Mixed: an owner says it's fine, a reviewer says the chain rusts |
| **Comfort** | ✓ (2 reviews) | ✓ (1 owner) | ✗ Your take: the seat is uncomfortable |

- **Dealbreaker:** Bike B's brakes
- **Sources disagree:** Bike C in the rain
- **Since Tuesday:** 2 owner reports were added for Bike A, and Bike C's price changed
- **Still to check:** how Bike A does in the rain
- **You're leaning towards:** A, if the rain question checks out

### Example: the learn checklist

**How LLMs work** · learning · interview in three weeks

| Topic | Status |
|---|---|
| 1. Tokens and embeddings | ✓ Done |
| 2. Softmax | ✓ Done |
| 3. Attention | ● In progress, 3 of 5 parts |
| 4. Positional encoding | ○ Started, set aside |
| 5. The transformer block | ○ Not started |
| 6. Training and loss | ○ Not started |
| 7. Tokenization | ! Fading: you only watched one video |
| + Masking | Suggested: in 4 of 5 course outlines |

Topic lists start from your goal, a syllabus or a plan an AI suggested, and are checked against several other sources. A topic only breaks down into parts once you reach it. Each idea exists once and is shared across your plans, so if you understand softmax once, every plan that includes it shows it.

### Example: coming back

> **Learning:** You were working out why attention scores are divided by √d. You'd got as far as large dot products making softmax too sharp. Next: try it with numbers. Set aside: why positional encoding uses sine and cosine.

> **Research:** You were checking whether claim 2 holds for small teams. Last source: section 4 of the Lee paper. Still needed: a source from after 2024.

> **Deciding:** You were checking how Bike A handles rain. You'd read 23 of the 40 comments in an owners' thread. Next: compare servicing costs.

> **Fixing:** You'd ruled out token expiry. You were about to test the cookie domain.

### How it works, start to finish

```
START       a new capture ("What's this for?") · a goal you type ·
            a plan from an AI chat · an import
               ▼
MODE        learn · research · decide · fix · plan · follow
               ▼
CAPTURE     one click anywhere: web pages, AI answers, videos,
            PDFs, notes, photos, voice
               ▼
ORGANIZE    read → match to an investigation → file into the mode's
            structure → reconcile with older evidence
               ▼
LEAVE       it writes "where I was"
               ▼
COME BACK   resume card → exact spots → in learn mode, one recall question
               ▼
USE         ask your agent · continue in any AI · ask aside ·
            send a helper agent
               ▼
FINISH      the mode's done standard → the outcome is saved and reusable
```

- **Starting:** capture something new and answer "What's this for?", type a goal, adopt a plan from an AI chat, or import a syllabus or reading list. The mode follows from your purpose. It may ask one or two quick questions, such as a deadline or budget, and you can skip them.
- **Capturing:** one click saves your selection or the whole page. Adding your take is optional: a typed line, a few spoken words, or a tag like *dealbreaker*, *clicked*, *confused* or *verify*.
- **Organizing:** it pulls out each separate point and matches it to an investigation, asking only when unsure. It files each point into the mode's structure, flags disagreements and marks old information as out of date. New evidence never overwrites older evidence.
- **Leaving and coming back:** when you leave, it writes "where I was." When you return, a resume card takes you to the exact spots.
- **Finishing:** each mode has its own standard for done. The outcome (a decision and its reasons, a set of conclusions, or the topics you've mastered) is saved and can be reused by later investigations.

### Where it works

| Where you are | How you capture |
|---|---|
| Any page, chat or video in a browser | Extension buttons, or select text |
| ChatGPT or Claude desktop apps, PDFs, documents | A keyboard shortcut saves what you've selected. Claude Desktop can also save through a local connector |
| Phone apps | The share button, screenshots, photos and voice |
| Any AI that supports connectors | Ask the AI to save something, and it sends it to your agent |

Nothing watches you between clicks. Session and automatic capture are optional, turned on per site, and show an indicator while active.

### AI answers are labelled

An AI answer is saved as an AI answer, along with the model, the date and any sources it cited. It's marked "to verify" until a human source backs it up. Your agent can offer to find that backing.

## 5. Who it's for

- **First:** people who learn and research with AI across several tools, such as students, self-learners, grad students and developers. Also people in the middle of a decision, because a decision takes days, so it's the fastest thing to test.
- **Later:**
  - professional researchers: analysts, consultants, UX researchers and product managers
  - developers and teams passing work between AI agents
  - anyone with a long investigation, such as understanding a family member's diagnosis

## 6. Competition

| Category | Examples | What they do | What we add |
|---|---|---|---|
| AI chats and study modes | ChatGPT, Claude, Gemini | Remember your past sessions, but only in their own app | One record that works across every AI and every other source |
| AI study notebooks | [Gemini notebooks](https://blog.google/products-and-platforms/products/education/gemini-finals-study-tips/), NotebookLM | Study the sources you upload, and remember your progress inside a notebook | Follows your thinking wherever it goes, keeps your own take, and stays on your device |
| Notes apps with AI | [Notability Learn](https://blog.notability.com/post/inside-notability-learn), Goodnotes | Turn your notes into quizzes and summaries | Knows what happened outside your notes, and never rewrites them |
| Web clippers and read-later apps | Evernote, Notion, Raindrop, [Recall](https://chromewebstore.google.com/detail/recall-summarizer-youtube/ldbooahljamnocpaahaidnmlgfklbben) | Save and summarize pages | Saves your judgment with the evidence, and builds your decision or argument from it |
| Tutors that track mastery | [Cognaa](https://cognaa.com/), [NoetaMind](https://noetamind.com/), [Knorion](https://knorion.com/) | Track what you know inside their own lessons | Tracks what you understand from wherever you learned it |
| AI memory layers | [Ontomaps](https://www.ontomaps.com/), [e-xo](https://e-xo.ai/), [knowledge-worker](https://github.com/rahulmranga/knowledge-worker) | Share goals, decisions and facts with many AI tools | Holds evidence, your reasoning and your chain of thought, beyond AI chats |
| Chat-structure tools | ChatGPT branching, [Offthread](https://chromewebstore.google.com/detail/offthread/ieekphhmaohoodalgaboiolcmmpoagmi?hl=en), [Branch Barber](https://chromewebstore.google.com/detail/branch-barber/pancajifpbhmoajlpbnmoigjbdeghifl), [GraphAqal](https://www.graphaqal.com/) | Branch and map individual chats | Works across all your tools, organized by investigation |
| Research agents | Deep research in ChatGPT and Gemini, Perplexity | Do the research for you and hand you a summary | Lets you lead, and keeps your reasoning with the sources |
| Screen recorders | Rewind, Microsoft Recall | Record everything on your screen | Captures only what you click, and understands what it captured |

None of the tools we found combines all of this: capturing from every place you look, keeping your judgment with the evidence, organizing it by what you're doing, and keeping your chain of thought, privately and with every AI.

## 7. What makes it hard to copy

- **A simple skill or plugin can't do it.** A skill lives inside one AI, only runs when it's called, can't tell when you leave, never finds out whether its judgments were right, and only ever sees one person.
- **Data that builds up over time:**
  - Your own outcomes make its judgments better: what you remembered when tested, decisions you stood by, conclusions that held up.
  - Anonymous shared templates and topic maps improve as more people use it, for example what people usually check when buying a bike, or where learners usually get stuck.
- **Capture from every place you work,** feeding one record that belongs to you.
- **Neutrality.** It works with every AI and belongs to none of them.

## 8. Privacy and trust

- By default, nothing is captured without a click.
- Everything stays on your device by default, and sync is end-to-end encrypted.
- AI answers are labelled and marked "to verify."
- Every claim links back to its source.
- Deleting something removes it everywhere.
- No ads, and no affiliate links in decisions.
- Adults first, because of children's data laws.

## 9. How it's built

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

**The agent's jobs:**
- **Reader:** pulls separate points out of each capture.
- **Router:** matches a capture to an investigation, or asks "What's this for?"
- **Organizer:** files points, merges duplicates, reconciles disagreements and marks old information.
- **Chain keeper:** writes "where I was" when you leave.
- **Planner:** checks plans against sources and suggests what's missing.
- **Coach:** in learn mode, runs stages, recall questions and done checks.
- **Briefer:** writes briefs for other AIs.
- **Helpers:** only when you ask, fill one gap or verify a claim.

**Rules:**
- The models suggest changes, and the record decides.
- Anything uncertain waits for your one-tap confirmation.
- Every judgment has a "why?" that shows its sources.
- Each investigation can be exported as plain Markdown plus structured data, with every source link kept.

## 10. Business model

- **Free and open-source core.** It runs on local models or your own AI key.
- **Paid plan for convenience:** encrypted sync, hosted models, helper agents and sharing.
- **Later:** plans for teams and institutions, such as research groups, coaching centres, universities and companies.
- **Never ads or affiliate links,** because trust is the product.

## 11. Build plan

| Phase | What ships | What it has to prove before moving on |
|---|---|---|
| 1. Prove the click | Browser extension and local core: one-click capture, evidence cards, the inbox, "What's this for?", decide mode, a basic learn checklist, "where I was," and briefs to copy into any AI | People use it instead of notes, screenshots and piles of tabs. Getting back into a topic takes under a minute. Captures mostly land in the right place |
| 2. Beyond the browser | Phone share, camera and voice. The desktop shortcut. Local MCP for Claude Desktop, Claude Code and Cursor. Better capture of AI answers | Captures from apps and the phone land in the right place |
| 3. Deeper modes | Learn stages, recall when you return, fading and done checks. Research mode and fix mode | Its guesses about what you remember start beating your own sense of it |
| 4. Agents and sharing | Helper agents, plugins for Claude and ChatGPT, encrypted sync, sharing, anonymous templates | Briefs and helpers save people real time |
| 5. Wider | Plan and follow modes, custom modes, teams | People run several kinds of investigation side by side |

**How we'll measure success:**
- Getting back into a topic takes under a minute.
- People re-explain themselves to AIs less often.
- Most captures land in the right place without being corrected.
- Its guesses about what someone remembers beat that person's own confidence.
- People come back every week without reminders, and some of them pay.

## 12. Risks and how we handle them

| Risk | How we handle it |
|---|---|
| Judging understanding wrongly | Each stage needs its own evidence, including one proof (explaining something or solving a problem), and the system checks itself against later results |
| No easy access to AI chats, and sites change | Several routes in (extension, shortcut, share, connectors, imports), and a link, timestamp and your own words saved with everything |
| Big AI companies add similar pieces | Stay neutral across AIs, private, and built around your reasoning rather than generated material |
| People don't build the habit | No new routine. It shows up where you already work and pays off the first time you come back |
| People won't pay | A free core, paid convenience, and later teams and institutions |
| Filing mistakes and organizing too much | One-tap fixes, an inbox for anything unsure, and structure that grows only as evidence arrives |
| Wrong flags hurt trust | Flag only with a cited source, and stay conservative |
| Children's data laws | Start with adults |

## 13. Next steps

1. Talk to ten people (some in the middle of a decision, some learning, some researching) about how they keep track today and what they lose.
2. Build phase 1 and test it for two weeks with ten people making a decision and ten learners.
3. Pick the launch mode based on what the test shows.
4. Choose a name.
