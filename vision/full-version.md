# The full version: how it should actually work

This builds on `product-definition.md` (the core) and `execution-plan.md` (how each layer is built, release by release).

## The shift underneath

The core stays: one click, threads, next moves, the bridge, and finishing. What changes is what sits underneath.

- **Simple version:** threads hold the things you saved.
- **Full version:** the product keeps a private, growing model of four things: what you're figuring out, what's true, what matters to you, and how your past decisions turned out. Threads are views of that model, and every next move is chosen from it.

## Where the simple version breaks, and what fixes it

| Simple version | Where it breaks | Full version |
|---|---|---|
| Each thread stands alone | You research the same things twice, and re-enter your budget, city and preferences in every thread | A shared knowledge base under all threads, plus a profile of you that every thread uses |
| Seven fixed modes | Real tasks don't fit one shape. A visa application is part tracking, part checklist, part research | Each thread gets a blueprint generated for its purpose, built from the seven base shapes |
| Counting sources | Three "owners" repeating one viral post look like strong evidence, and a review paid through affiliate links looks neutral | Evidence is weighted by kind, independence, recency and conflicts of interest |
| A fixed list of next moves | Suggestions feel generic | A planner ranks moves by how much each could change your outcome, and by your deadline |
| AI does a job in one shot | You can't see what it did or what it cost | Helpers show a plan, you approve it, they work within a budget, and they keep an activity log |
| Nothing happens between sessions | You come back to stale prices and missed replies | Background work on your saved data, plus watchers you turn on |
| The story ends at "Conclude" | It never learns whether your decision was good | Outcome check-ins and a decision journal feed lessons back into your profile |
| Capture is browser-only | Half of research happens on a phone, in email or in a shop | Phone share, photos, voice, emails forwarded to a thread, and imports |
| One person per thread | Most big decisions involve someone else | Shared threads where each person's takes stay separate |
| The bridge matches page addresses | It misses when you search the same topic again | It also matches search queries, which appear in the address, and, on AI sites you've allowed, the first message of a new chat |

## The seven layers

### 1. Knowledge: what you've found, shared across threads

- **What it holds:**
  - things (products, companies, people, concepts, places)
  - claims about those things, with the evidence behind each claim
  - questions, open or answered
- **How it works:**
  - Every card links to the things it mentions.
  - Names are matched carefully, so "Sprint Pro 26T," "the Sprint" and "Sprint 26" count as one bike.
  - When it isn't sure two names are the same thing, you merge or split them with one tap.
- **What you see:**
  - **A page for each thing,** such as "Everything you know about Bike B": prices seen, owner reports, your takes, and which threads it appears in.
  - **"What did I already find?"** searches across all your threads and years.
  - **New threads start with what you know.** For example: "You researched helmets in March. Bring that in?"

### 2. You: what matters to you, visible and editable

- **What it holds:**
  - constraints: budget ranges, city, height, commute
  - preferences: for example, owner reviews over influencers, or video explanations
  - trusted and distrusted sources
  - languages, goals and deadlines
  - for learning, what you already understand
- **How it learns:**
  - from answers you give once, like "How tall are you?" when choosing a bike frame
  - from your takes, like "dealbreaker"
  - from patterns, offered only as suggestions you confirm: "You've rejected three options for poor rain performance. Treat rain as important for you?"
- **What you see:** a "You" page listing every fact and where it came from. You can edit or delete any of it, nothing is hidden, and it lives only on your device.
- **Why it matters:** this is the "AI that knows me" you described at the start. Every brief sent to ChatGPT or Claude includes it.

### 3. Blueprints: what this particular task needs

- **What it is:** a structure generated for each thread's purpose and built from the seven base shapes. It sets out:
  - the parts of the task
  - what to record about each part
  - what experts check
  - what "done" means
- **Examples:**
  - **Choosing a bike:**
    - options
    - criteria: budget, rain, comfort, maintenance
    - facts per option: price, weight, frame sizes
    - what experts check: frame size for your height, local servicing, spare parts
  - **A visa application:** Track stages, plus a Plan checklist (documents, appointments), plus Research (rules, fees). Done means the visa is received.
  - **Choosing a doctor for your mother:** Decide (doctors compared on criteria), plus Follow (a timeline of appointments), plus questions for each visit.
- **How it works:**
  - The model proposes a blueprint from your purpose, and you adjust it with taps.
  - It keeps adapting as evidence arrives.
  - Later, a public template library collects blueprints that people choose to contribute. Only the structure is shared, never anyone's content.

### 4. Reasoning: what the evidence adds up to

- **Evidence weight.** Each card counts according to five things:
  - **Kind:** an owner's experience, an expert test, official data, a seller's claim, or an AI answer.
  - **Independence:** three posts repeating one source count once.
  - **Recency:** a complaint about last year's model counts for less.
  - **Specificity:** "brakes squeak after two weeks of rain" counts for more than "brakes are bad."
  - **Conflicts of interest:** reviews with affiliate links or sponsorships are labelled.
- **Contradictions and patterns.** It shows where sources disagree and offers a possible explanation, such as "All four complaints about Bike B are about the 2025 model."
- **What-if and value of information.** It knows which open question could change your outcome, and by how much.
- **"Why?" everywhere.** Asking "Why is Bike A ahead?" shows your weights and the cards behind each cell.

### 5. Action: the next move, and helpers to do the legwork

- **The planner.** It ranks next moves by expected value and shows the top three. Expected value covers:
  - how much the move could change the outcome or move the thread toward done
  - what it costs in time and money
  - your deadline. If you set "decide by Saturday," it favours moves that settle the decision quickly.
- **Helpers with a leash.** A delegated job, such as "find owner reports of Bike A in heavy rain," runs in four steps:
  1. **Plan:** it shows the searches it will run and the sites it will read.
  2. **Approve:** you approve the plan with a budget, for example at most 5 searches and 10 pages.
  3. **Run:** it works in the background.
  4. **Report:** results arrive as proposed cards with quotes, links and confidence, along with an activity log of everything it read.

  Helpers never post, apply, buy or log in for you.
- **Watchers you turn on.** Watchers are opt-in, and price checks run at most once a day. They can watch for:
  - price drops on pages in your thread
  - replies to your community post, checked when you open the site
  - a job posting about to close
  - new papers citing one you saved
- **Finishing aids.**
  - **How thorough to be:** choose "good enough" or "thorough." Small choices finish faster.
  - **Weights in three taps:** questions like "Rain or comfort: which matters more?" set your weights without sliders.
  - **A pre-mortem before you conclude:** "It's three months later and you regret this. Why?" Imagining an outcome has already happened helps people find [about 30% more reasons for it](https://www.researchgate.net/publication/3229642_Performing_a_Project_Premortem), so this brings out risks you missed.

### 6. Time: what happened since, and how it turned out

- **Coming back.** The bridge and "where I was" now include "since you left": new replies you added, prices that changed if watchers are on, and anything a helper found.
- **Background work on your saved data,** never on your browsing:
  - It merges duplicates, refreshes summaries, spots contradictions, marks old information, and keeps the "where I was" note current.
  - It runs when your laptop is idle.
- **Living decisions.** Every conclusion keeps its reasons. If a reason later stops holding, for example "B's brakes were fixed in the 2027 model," it tells you. This keeps long-lived decisions like a job, a course or an investment honest.
- **Outcome check-ins.** It asks a short question at the right time, such as "One month in: how's Bike A in the rain?" Your answer becomes evidence for your future self.
- **Lessons.** Across many threads, it shows patterns in your own decisions and learning, such as "You often underweight maintenance" or "Topics you only watched faded within a week." These become suggestions for your profile. This loop makes it more accurate the longer you use it, and a skill or plugin can't copy that.
- **Learning.** Recall checks when you return, fading tracked for each part, and "done" only after one delayed check.

### 7. Reach: everywhere you are, with everyone involved

- **Capture from more places:**
  - the browser
  - the phone's share button. Saves wait in a queue until your laptop or your key processes them, because Chrome's built-in model runs only on desktop.
  - photos (shop visits, whiteboards, handwritten notes) and voice takes
  - **emails forwarded to a thread.** Each thread gets its own address, and a forwarded confirmation, seller reply or interview invite becomes a card. It's the same idea as [TripIt's plans@tripit.com](https://www.tripit.com/web/free/how-it-works), and it needs no access to your inbox.
  - imports: ChatGPT and Claude exports, Kindle and Readwise highlights, Zotero, and bookmarks
- **Together:**
  - Threads can be shared, with roles. Each person's takes stay separate and labelled.
  - Votes and "decide together" show where people agree and where they don't.
  - You can hand a thread to a colleague along with its "where I was."
- **Agents:**
  - An MCP server with scopes, for example "Claude Code can read and add to *Fix: login bug*, and nothing else."
  - Anything an agent adds lands in the review tray, labelled with the agent's name.
- **Open files:** every thread is a Markdown file that can live in an Obsidian or Notion folder.
- **Languages:**
  - Chrome's built-in model [handles English, Spanish, Japanese, German and French from Chrome 149](https://developer.chrome.com/docs/ai/get-started).
  - Hindi or Hinglish takes and Hindi video lectures go to the cloud model with your key.
  - Matching uses a multilingual embedding model, so it works in any language.

**Running through every layer:**
- **Calm design:** three moves at most, a weekly limit on nudges, nothing in red.
- **Trust:** every claim links to its source, every AI action can be undone, and the profile is fully visible.

## The bike thread in the full version

1. **Start.** You save ChatGPT's three bikes. It recognizes a purchase and asks one question: "Decide by when, and good enough or thorough?" You pick "Saturday, good enough," and the blueprint appears: criteria, facts per bike, and what experts check.
2. **What it already knows.** "You researched helmets in March. You're 175 cm, so frame size M fits." Both facts come from your profile and past threads.
3. **Weights.** It suggests rain as your top criterion, because your profile says you commute in heavy rain and you've rejected options for rain before. Three taps ("Rain or comfort?") confirm the weights.
4. **Evidence.** Three Reddit complaints about Bike B count as one source, because two of them quote the same post. A YouTube review is labelled "affiliate links." The table shows how confident each cell is, not just ticks.
5. **Planner.** The top move is "Owner reports of Bike A in rain," because that's the only cell that could change the winner. You send a helper: it shows a plan of 5 searches, and you approve it. Twenty minutes later, four owner reports are waiting in the tray. Two are independent, and one is negative.
6. **Bridge.** On Thursday you search Google for "best bike for heavy rain." The bridge shows: "You have a thread on this. Bike A is ahead. Open where I was?"
7. **Finish.** "Do I have enough?" says you're ready. A one-tap pre-mortem raises "the service centre is far away," which becomes one last check. You conclude, and the reasons are saved.
8. **After.** A month later it asks, "How's Bike A in the rain?" You answer "great, but the chain rusts." That becomes evidence and a lesson, "check the chain coating on rain bikes," which is added to the blueprint for next time.

## The same layers in other threads

| | Learn: LLMs for interviews | Track: job search | Work: choosing a tool for the team |
|---|---|---|---|
| Knowledge | Links to concepts from other courses, such as matrix multiplication | Each company is a thing with all its pages, people and notes | Vendors as things, shared with the team |
| You | Learns best with visuals, interview in 3 weeks, already solid on embeddings | Target roles, salary floor, locations, visa needs | Team constraints: budget, security rules |
| Blueprint | Topics at interview depth, with a done check for each part | Stages, documents, follow-up rules | Criteria from the team, plus what IT always checks |
| Reasoning | Which parts are only "seen" and likely to fade | Which applications have stalled, and response rates by source | Evidence weighted, with vendor claims labelled |
| Action | Best explanation for √d, a quiz on what confused you | Company research helper, interview prep, follow-up drafts | A helper gathers security documents, then a decision memo with receipts |
| Time | Recall checks, fading, done after a delayed check | Reminders, an outcome for each application, lessons such as "referrals got you three times the interviews" | A check-in at 3 months: did the tool deliver? |
| Reach | A study group shares a thread, each person with their own progress | Recruiter emails forwarded to the thread | A shared thread, with each person's takes labelled |

## How the system fits together

```
CAPTURE      browser · phone share · photos · voice · forwarded email ·
             imports · agents (through MCP, with scopes)
                 ▼
EVIDENCE     event log on your device (only ever added to)
                 ▼
KNOWLEDGE    things · claims · evidence · questions, shared across threads
                 ▲  background work: merge, contradictions, staleness
YOU          constraints · preferences · trusted sources · learning state
                 ▼
THREADS      blueprint (generated for the purpose) + state + where I was
                 ▼
REASONING    evidence weight · contradictions · what-if · value of information
                 ▼
ACTION       planner → next moves → helpers (plan, approve, budget, log) · watchers
                 ▼
FINISH       enough? → pre-mortem → conclude → outcome check-in → lessons
                 │                                   └──► back into YOU and BLUEPRINTS
                 ▼
REACH        shared threads · Markdown files · MCP · exports
```

## What this changes in the build

The version 1 scope in `product-definition.md` stays. Small, cheap versions of each layer go in from the start, so the data has the right shape from day one.

| Layer | Version 1 (lite) | Version 2 | Version 3 |
|---|---|---|---|
| Knowledge | Names linked inside a thread, duplicates merged | Shared across threads, pages for each thing, "you researched this before" | Years of history, lessons across threads |
| You | Facts from "What matters?" and dealbreakers, shown on a You page | Learned suggestions you confirm, used in every brief | Lessons from outcomes |
| Blueprints | Base shapes with generated criteria, weights in three taps | Combined blueprints for mixed tasks, what experts check | A public template library (structure only, contributed by hand) |
| Reasoning | Source kind labels, "sources disagree," what-if, "Why?" on the ranking | Independence, recency and affiliate labels, "Why?" everywhere | Crowd signals as weak evidence, only if a privacy design passes public review |
| Action | Rules-based planner, Dig with your key | Expected-value planner, helpers with plans, budgets and logs, watchers | Agents that add to threads through MCP |
| Time | Bridge, "where I was" | Background work, "since you left," living decisions, outcome check-ins, recall | Lessons |
| Reach | Browser, Markdown export | Phone share, photos, voice, email forwarding, imports, a read-only MCP server | Shared threads, team spaces, a desktop shortcut |

Version 2 ships in four releases (2.1 to 2.4). Outcome check-ins moved up from version 3, so lessons have months of outcomes to learn from. `execution-plan.md` has the order and timing.

## Hard parts of the full version

| Problem | How to handle it |
|---|---|
| Name-matching mistakes, like Sprint the bike versus Sprint the company | Match within a thread first, show every merge, and allow a one-tap split |
| A profile that feels creepy | Show everything with its source, make it suggestions only, keep it on the device, and allow one-tap delete |
| Helpers running up costs or reading junk | Plans you approve, hard budgets, activity logs, and your trusted-source preferences |
| Mistakes in deciding whether sources are independent | Start with simple rules (same text, same original link, same author) and label the result as an estimate |
| Background work slowing the laptop | Run only when the laptop is idle, with limits |
| Helpers reading sites that don't allow it | Read logged out, follow robots.txt, and list those pages for you to open yourself |
| Email forwarding needs a server | An optional relay that seals each email on arrival and deletes it after pickup. Off by default, open source, and self-hostable |
