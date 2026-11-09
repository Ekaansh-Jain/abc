# Execution plan: how it works inside, and how we build it

This builds on `product-definition.md` (what we're building), `full-version.md` (the seven layers), `how-it-runs.md` (what one click does, in plain terms) and `architecture.md` (the design ideas underneath). Each part is marked with when it arrives: **v1**, one of the four releases of version 2 (**2.1** to **2.4**), or **v3**.

## 1. The system at a glance

### Version 1

```
YOUR BROWSER (Chrome, desktop)
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  Any page you're on            click Save                        │
│  ┌──────────────────┐  ─────────────────────▶  ┌───────────────┐ │
│  │ Page helper      │                          │ Coordinator   │ │
│  │ (captures,       │  ◀─────────────────────  │ (receives     │ │
│  │  restores spots, │   "you have a thread"    │  saves, sees  │ │
│  │  shows the bar)  │                          │  tab addresses│ │
│  └──────────────────┘                          │  reminders)   │ │
│                                                └───────┬───────┘ │
│  ┌──────────────────┐                          ┌───────▼───────┐ │
│  │ Side panel       │  ◀────────────────────▶  │ Worker page   │ │
│  │ (threads, cards, │                          │ (AI jobs,     │ │
│  │  next moves,     │                          │  matching,    │ │
│  │  review tray)    │                          │  organizing)  │ │
│  └──────────────────┘                          └───────┬───────┘ │
│                                                ┌───────▼───────┐ │
│                                                │ Local store   │ │
│                                                │ event log →   │ │
│                                                │ your record   │ │
│                                                └───────────────┘ │
└───────────────────────────────┬──────────────────────────────────┘
                                │ only for moves you turn on
               ┌────────────────▼─────────────────┐
               │ Outside services                  │
               │ AI provider (your key) ·          │
               │ web search · YouTube search       │
               └───────────────────────────────────┘
```

| Part | Chrome piece | Job |
|---|---|---|
| Page helper | Content script | Captures what you save and restores exact spots. It runs on a page only after your click, or on sites you've allowed. On sites you've allowed, it also shows the bridge bar on the page |
| Coordinator | Service worker | Receives saves, writes them to the store, watches tab addresses for the bridge, sets the toolbar icon's dot, and runs reminders. Chrome stops it when idle, so it never does long work |
| Worker page | Offscreen document | Does the slow work: AI calls, matching saves to threads, organizing |
| Side panel | Side panel | Your screen: threads, cards, next moves, and a tray of AI suggestions waiting for your OK |
| Local store | IndexedDB | The event log, your record built from it, and the search index |
| Outside services | Network calls | Only for moves you turn on, using your key |

### The full system

```
WAYS IN
  browser ──▶ page helper ─────────────────────────────────┐
  phone app ───────┐                                       │
  forwarded email ─┴──▶ relay (optional, sealed) ──────────┤
  imports ─────────────────────────────────────────────────┤
  agents ──▶ MCP server ──▶ inbox folder ──────────────────┤
                                                           ▼
INSIDE CHROME
  side panel ◀── local store ◀── worker page ◀── coordinator
                 event log →     AI jobs,        saves, tabs,
                 your record     job queue       alarms, idle

WAYS OUT (only what you turn on)
  AI provider · search · YouTube · OpenAlex · pages that helpers and watchers read
  thread folder (Markdown) ──▶ MCP server ──▶ your agents
  relay ──▶ your other devices, and from v3 the people you share with
```

| Added after version 1 | Where it runs | Job | From |
|---|---|---|---|
| Job queue | Worker page | Runs background work, helpers and watchers one job at a time, and resumes after Chrome restarts | 2.2 |
| Helper runner | Worker page | Runs an approved plan within its budget and writes the activity log | 2.2 |
| Watchers | Coordinator (alarms) and worker page | The daily checks you turned on | 2.2 |
| Folder writer | Extension pages | Keeps the Markdown thread folder up to date | 2.4 |
| Phone app | Your phone, as an installable web app | Share, photo and voice saves, held in a queue | 2.4 |
| Relay | A small server, optional and self-hostable | Passes sealed envelopes between your devices, and receives forwarded email | 2.4 |
| MCP server | Your computer, outside Chrome | Lets AI agents read the threads you allow, and in v3 propose additions | 2.4 read, v3 add |

### One save, traced through the system (v1)

You're on a Reddit thread and save a comment about Bike B's brakes.

1. **Page helper.** It copies the comment, the sentences around it, a link straight to that sentence, the page address and the date. It also adds your take: you tapped **Con** and said "dealbreaker."
2. **Coordinator.** It writes the capture to the event log right away, so nothing is lost even if a later step fails. It shows "Saved."
3. **Worker page, fast lane.** Without any language model, it matches the save to "Choosing a bike," because you saved there 5 minutes ago and the comment names Bike B. It shows "Saved to Choosing a bike" within half a second.
4. **Worker page, slow lane.** The built-in model fills the thread's form: an owner's experience, about Bike B, on the rain criterion, against, with the exact quote. Code checks the quote and links "the B" in the comment to the thing Bike B.
5. **Local store.** The claim "Bike B handles rain" gains a card and now reads "against, 1 owner." Your dealbreaker takes Bike B out of the ranking and adds "Dealbreaker: brakes that fail in rain" to the You page for this thread. The trail adds a line, and the next moves are recalculated. "Dig: do other owners say this?" moves to the top, because a dealbreaker resting on one comment is worth checking.
6. **Side panel.** It shows "Saved to Choosing a bike · Bike B · rain · con" with **Undo** and **Move**.

**The same save in the full version:**
- **2.1:** Bike B is also in your "Commute gear" thread, so the claim shows on Bike B's page there too. The comment repeats a post you saved yesterday, so the two count as one source.
- **2.2:** The planner stops suggesting checks on Bike B's other features, since the dealbreaker already rules it out.
- **2.2:** After you conclude, if later owners say new brake pads fixed the problem, the conclusion is marked "a reason changed."

## 2. The AI layer: which model does what

| Tier | Model | Used for | Notes |
|---|---|---|---|
| 1 | Chrome's built-in model (Gemini Nano, through the Prompt API) | Filling each thread's form (splitting saves into points and labelling them), naming threads, "where I was" notes, criteria for new threads, polishing drafts and briefs. From 2.1, confirming unclear name matches and rating how specific a card is. From 2.4, reading photos and voice takes | Free and private. Desktop only. It needs [about 22 GB of free disk and either 16 GB of RAM with 4+ CPU cores or a GPU with more than 4 GB](https://developer.chrome.com/docs/ai/prompt-api). It accepts text, image and audio input (audio needs a GPU) and answers in English, Japanese, Spanish, German or French. Its context window is small, so each job gets only what it needs |
| 2 | Small embedding model on the device, run with Transformers.js (as [Branch Barber does](https://chromewebstore.google.com/detail/branch-barber/pancajifpbhmoajlpbnmoigjbdeghifl)) | Filing saves into threads, tab rescue groups, the bridge, finding duplicates, choosing which chunks of a long page the model sees. From 2.1, matching names across threads and finding repeated text | Use a small multilingual model (for example multilingual-e5-small) so Hindi and Hinglish saves match too, and compare it with MiniLM on the test set. Manifest V3 doesn't allow [remotely hosted code, including WASM](https://developer.chrome.com/docs/extensions/develop/migrate/remote-hosted-code), so the runtime ships inside the extension. Model weights are data and download on first use. Runs on almost any laptop |
| 3 | Cloud model with the user's own key (optional) | Dig, ranking the watch list, conclusions on long threads, and everything tier 1 does when tier 1 isn't available. From 2.2, helper plans, reading pages and pre-mortems. From 2.3, blueprints for mixed tasks. Hindi, Hinglish and other languages | Calls go straight from the browser to the provider |
| Always | Plain code, no model | Placing points, the ranking, evidence weights, independence, the what-if check, value of information, the planner, budgets, recall scheduling and lessons | The reasoning runs the same way every time, and "Why?" can show the exact numbers |
| Basic mode | No language model | Rules, embeddings and templates. You tap pro or con yourself | Keeps the product working on 8 GB laptops with no key |

**Where and when the built-in model runs**
- It needs a page, and the coordinator is a service worker, so it runs in the worker page. Projects such as [ReviewWise](https://devpost.com/software/question-analyzer) do the same. Confirm it in the first technical test.
- Chrome downloads the model the first time it's used. [The download needs a click to start](https://developer.chrome.com/docs/ai/prompt-api) and an unmetered connection, so setup has a "Turn on on-device AI" button. Basic mode works until the download finishes.
- If free disk space drops below 10 GB, Chrome removes the model. The settings page shows the model's state.
- The worker page keeps a session warm while you're working and closes it after about 10 minutes without saves, to free memory. The first job after a cold start is slower, because the model has to load.

**Rules for every AI call**
- Ask for a fixed format. The Prompt API accepts a [JSON Schema](https://developer.chrome.com/docs/ai/structured-output-for-prompt-api), and the thread's own lists (its options, criteria or topics) become the only allowed values. Check every answer against the schema before anything changes.
- Keep answers short: a few fields, never paragraphs, because on a small model the answer's length drives most of the wait.
- Send only the relevant text. Long pages are cut into chunks, and only the two or three chunks closest to the thread's question go to the model.
- Use low randomness. [Extensions can set the temperature](https://developer.chrome.com/docs/ai/prompt-api), so the same save gets the same answer.
- Confidence decides what happens. High confidence: apply it and show it. Medium: put it in the review tray. Low: keep the save as a plain card for you to tag.
- Treat captured text as data, never as instructions. Page content, pages a helper reads, forwarded emails and imports can't trigger moves, send anything or change settings.
- Show model output as plain text, never as HTML. This is [Chrome's own guidance](https://developer.chrome.com/docs/modern-web-guidance/guides/built-in-ai/language-model?hl=en).
- Keep one base session with the instructions, clone it for each job, destroy clones when done, and cache results for repeated inputs.
- Quotes must match. A point is dropped unless its quote appears word for word in the source text.
- Fixed steps, not open-ended agents. Helpers follow the approved plan. Text they read can become cards, but it can't add steps, change the budget or start other moves.
- Only relevant facts about you. A prompt gets only the profile facts that apply to the thread, and never facts marked sensitive unless the thread is about them.
- Learn from corrections. When you move a save or fix a label, the correction is stored on the device as an example, and later prompts include the two examples most like the new save.

## 3. What gets stored

The event log is the source of truth, and every other record is built from it. That makes undo, merging and splitting, sync and replay tests simple. Views are stored and updated as events arrive. A full rebuild from the log serves as a test and a repair tool.

From day one, every event carries an author (you, the AI, a helper, a watcher, an agent or another person) and a device, so later layers need no migration.

| Record | What it holds | From |
|---|---|---|
| Event | Every action, in order: saved, filed, merged, split, moved, take added, move run, thread closed, reopened. Each has an author, a device and a counter for ordering. Only ever added to | v1 |
| Capture | One save: kind (selection, page, AI answer, video moment, job page, product page, photo, voice), link, title, site, quoted text with the words around it, link to the exact sentence, video second, structured page data, AI model name and cited links, your take, the date. Never the raw HTML. From 2.4, also where it came from: browser, phone, email, import or agent | v1 |
| Card | One point from a capture: the text, a one-line gist, kind (fact, spec, price, owner, expert, official, seller, AI), the things it's about, stance (for, against, neutral), confidence. From 2.1, also its weight factors: independence group, the date of what it describes (such as a model year), specificity, and conflict-of-interest flags | v1 |
| Thing | Name, kind (product, company, person, concept, place), other names, identifiers where they exist (product codes from page data, DOI, ISBN, a company's website), and its merge history. Belongs to one thread in v1, shared across threads from 2.1 | v1 |
| Claim | Something said about a thing: an attribute or criterion, a value or stance, the cards behind it, its confidence, and a status (open, settled, disputed, stale). A Decide cell is a claim, and so is each price seen | v1 |
| Question | The text, what it's about, its status and answer, and whether it could change the outcome | v1 |
| Progress | Your own status, which needs no evidence: a Track stage with dates, a Learn stage, a Plan to-do. From 2.3, the recall schedule for each Learn part | v1 |
| Spot | One kept tab or saved place: link, title, site icon, the thread it belongs to, the position if Chrome allowed reading it (scroll position and nearest sentence, video second, or chat message), when you last looked, and when it was closed | v1 |
| Thread | Title, your question, blueprint, shelf (Now, Paused, Done), goal or deadline, "where I was" (note, spots, next step), when you last opened it, and the outcome. From 2.2, "good enough" or "thorough" | v1 |
| Blueprint | The shape, the parts, criteria and weights, fields for each item, the form the model fills, and what done means. From 2.2, when to check in. From 2.3, what experts check | v1 |
| Fact about you | Label, value, scope (one thread, a kind of thread, or everywhere), the event it came from, status (confirmed or suggested), and a sensitive flag | v1 |
| Correction | A save you moved or a label you fixed, kept as an example for later prompts | v1 |
| Move | A suggested or running next move: type, inputs, status, results waiting for your OK. From 2.2, also its expected-value parts | v1 |
| Conclusion | The text and its reasons, each linked to a claim. From 2.2, pre-mortem notes and whether every reason still holds | v1 |
| Helper run | Plan, budget, approval, status, the activity log (every search and page, read or skipped, with the reason and the time), and results | 2.2 |
| Watcher | What it watches, the rule, the schedule, the last value and the history | 2.2 |
| Check-in | When, the question, your answer, and the conclusion it belongs to | 2.2 |
| Lesson | The pattern, the cases behind it with counts, and its status (suggested, accepted, dismissed) | v3 |
| Member | People in a shared thread, their roles and device keys | v3 |
| Settings | Allowed sites, the off-list, capture mode, your keys (encrypted on the device), the nudge limit. From 2.2, watcher limits. From 2.4, the relay and MCP scopes | v1 |
| Index | Embeddings for threads, cards, spots and things. From 2.1, the names and search words used for matching | v1 |

**The open format.** Every thread exports as one Markdown file that people and other tools can read. Things link with double brackets, so the folder also works as an Obsidian vault. Here's a thread file once 2.2 ships. Version 1 files have the same layout without the weights and the "counted once" notes.

```markdown
---
id: thr_bike_2026
blueprint: decide/city-bike
question: Which city bike handles rain and a 10 km commute, within my budget?
deadline: 2026-11-07
thoroughness: good-enough
status: paused
created: 2026-11-02
---

## Where I was
Checking Bike A in the rain. Next: owner reports of Bike A in the rain.

## About me (used here)
Commute: 10 km, often in heavy rain · Height: 175 cm · Dealbreaker: brakes that fail in rain

## What matters
1. Handles rain (weight 0.61) · 2. Comfort for 10 km (0.28) · 3. Price (0.11)

## Options
- [[Bike A]]: leading
- [[Bike B]]: out (dealbreaker: brakes in rain)
- [[Bike C]]: behind on comfort

## Evidence
- **[[Bike B]] · rain · against** · owner experience · counted once (2 of 3 posts quote the same one)
  "Brakes squeak after a few weeks of rain"
  [Reddit](https://www.reddit.com/r/bikecommuting/comments/...#:~:text=brakes%20squeak) · seen 2026-11-03 · take: dealbreaker

## Spots
- [Bike A review, 7:32](https://www.youtube.com/watch?v=...&t=452s)
- [Shop page: Bike A](https://shop.example/bike-a#:~:text=frame%20sizes)

## Open
- How does [[Bike A]] handle rain? (could change the winner)
```

From 2.4 the extension keeps a whole folder:

```
Trail/
  threads/choosing-a-bike.md
  things/bike-a.md
  you.md
  inbox/        what agents propose, waiting for the review tray
```

## 4. The information flows

Flows 1 to 6 are version 1, with later additions marked. Flows 7 to 17 come after version 1.

### Flow 1: Save (v1)

1. **You click Save**, using the toolbar button, a keyboard shortcut, the right-click menu, or a Save button beside an answer or comment on sites you've allowed. Chrome's [activeTab permission](https://developer.chrome.com/docs/extensions/develop/concepts/activeTab) gives temporary access to this one tab, and only after your click. It shows no install warning.
2. **The page helper reads the page already open in the tab.** It downloads nothing and uses no site API. It picks the piece you meant:
   - **Selected text:** the exact words, a little text before and after, and a [text-fragment link](https://developer.mozilla.org/en-US/docs/Web/URI/Reference/Fragment/Text_fragments) that scrolls to and highlights that sentence.
   - **A site with an adapter** (AI chats, Reddit, X, YouTube): the piece in the middle of the screen, briefly highlighted so you can click a different one if the guess is wrong. On sites you've allowed, Save buttons beside each piece remove the guess.
   - **Any other page:** the main text, pulled out with Mozilla's Readability (the library behind Firefox's reader view), with the paragraph you were on as the spot. If the page isn't an article, as with apps, feeds and unknown chat sites, it keeps the text on screen.
3. **It adds what the page already says about itself:**
   - **Structured data:** many pages describe themselves for search engines. Job posts carry [job data](https://developers.google.com/search/docs/appearance/structured-data/job-posting) (title, company, location, dates, often salary). Shop pages carry [product data](https://developers.google.com/search/docs/appearance/structured-data/merchant-listing) (price, availability). These fields are read directly, with no AI.
   - **AI answers:** your question just before the answer, the model name if shown, any cited links, and the chat's address. Each AI site has its own small adapter.
   - **YouTube:** the current second, the title, the channel and the chapter, a link that starts at that second, and the captions around that moment if the video has them.
   - **Your take:** a typed line, a few spoken words, or a tag.
4. **It never keeps the raw HTML**, other people's images (only links to them), or anything from off-list sites.
5. **The coordinator writes it to the event log** and shows "Saved" in about a tenth of a second.
6. **The worker page organizes it** (Flow 2).

`how-it-runs.md` has a site-by-site table, including desktop AI apps, which a browser extension can't read.

### Flow 2: Organize (v1)

Step 1 is the fast lane: rules and embeddings only, finished in under half a second. Steps 3 to 5 are the slow lane: one built-in model job, usually 1 to 5 seconds, shown when ready.

1. **Find the thread.** Each thread gets a score from four signals:
   - you saved to it in this window within the last 30 minutes
   - the same site or link is already in it
   - the save is similar in meaning to the thread (embeddings)
   - they share names, such as a bike model or a company

   What happens next depends on the scores:
   - **Clear winner:** it files the save and shows "Saved to … · Undo · Move".
   - **Close call:** you pick one of two with one tap.
   - **No match:** it asks "What's this for?" and suggests two or three names, plus "Just save it" for the inbox.
2. **Start a new thread** from your answer:
   - **Shape:** the page type comes first (job data means Track, product data means Decide). Then your words: "buy" or "choose" means Decide, "learn" or "exam" means Learn, "fix" or "error" means Fix. If it's still unclear, the built-in model picks one of the seven shapes. You can switch at any time, and the saves are read again against the new form.
   - **Blueprint:** for Decide, the criteria come from a template if one fits ("city bike"), from your own material if you saved some (a syllabus, a job description), or as a draft from the built-in model. You keep or drop them with taps.
   - **Weights in three taps:** two or three "this or that" questions ("Rain or comfort: which matters more?") put your top criteria in order. [Rank-order centroid weights](https://pubsonline.informs.org/doi/10.1287/mnsc.42.11.1515) turn the order into numbers: 0.61, 0.28 and 0.11 for three criteria. Barron and Barrett found these more accurate than other weights based only on rank.
   - **Facts about you:** answers like "10 km commute" or "175 cm" go on the You page, scoped to this thread. You can mark any of them "use everywhere."
3. **Fill the form.** The model gets the thread's question, its lists, the facts about you that apply, two past corrections as examples, and the relevant chunks of the save. It returns points in the shape's fixed format, each with the exact quote. Structured page data skips this step. `how-it-runs.md` shows the form for each shape and a worked example.
4. **Link names.** Each name in a point links to a thing in the thread. Exact and near-exact names merge on their own ("Sprint Pro 26T" and "Sprint 26"), with a one-tap split. Unclear pairs go to the review tray. A new name becomes a suggestion such as "Add Bike D as an option?" and is never added silently.
5. **File the points** as claims under the thread's things and criteria. A dealbreaker take also adds a fact to the You page, such as "Dealbreaker: brakes that fail in rain."
6. **Reconcile.**
   - The same claim from the same source merges into one card.
   - Opposite stances on the same cell show as "sources disagree."
   - Prices and dates are kept, and older ones are marked as old.
7. **Update everything downstream:** the views, the trail, the matching index and the next moves.
8. **Learn from corrections.** If you move the save or change a label, the correction is stored as an example for later prompts, and the filing thresholds adjust.

### Flow 3: The bridge (v1, with additions in 2.2)

**Closing (Close and keep)**

It comes in three sizes: this tab, this thread's tabs, or every tab (the full tab rescue, which is also the first screen after install).

1. **Read the tabs.** The [tabs permission](https://developer.chrome.com/docs/extensions/reference/api/tabs) gives each tab's title and address, plus when you last looked at it and which group it's in. Nothing inside the pages is read at this step.
2. **Group them.** Tabs already in a thread go to that thread. The rest are grouped by meaning (embeddings of title and site), matched against your threads, or named by the built-in model if new. Chrome tab groups you made stay together. Inboxes, calendars and music players are marked "keep open," and home pages and search results "just close."
3. **Show the plan** ("63 tabs → 4 threads, 9 to close, 5 to keep open"), let you drag anything that's wrong, and wait for your OK.
4. **Save the spots.** Each tab becomes a spot. Chrome lets an extension read inside a tab only if it has access to it, and an unloaded tab has no position to read. So the position is kept for:
   - the tab you're on, through your click
   - AI chats and YouTube, which you allow in v1: the message, and the video second
   - every other tab that's still loaded, if you turned on "remember my place on every site"

   Every other tab keeps its link and title. Anything you saved earlier keeps its exact sentence anyway.
5. **Write the "where I was" note.** The built-in model writes three lines from your last few actions and spots. Without the model, it fills a template. You can edit the note.
6. **Close the tabs** and move the thread to Paused. Tabs that fit no thread go into a "Loose tabs" list you can search. Once a month, one tap clears the old ones.

**Coming back**
1. **"Open where I was"** reopens the thread's spots in a new window, or as a named tab group if you allow the tab-group permission:
   - pages through text-fragment links
   - videos at the saved second
   - chats at their address, then scrolled to the saved message

   If a page doesn't jump to its sentence, which happens on apps that load their text late, one click on the toolbar icon takes you there.
2. **The bridge signal.** Each time a tab loads a new address, the coordinator checks it on the device against your threads: the same link, the same site, a similar title, or the search words in the address of a search page (Google, Bing, DuckDuckGo, YouTube and others). On a match:
   - **By default:** the toolbar icon shows a dot for that tab, and the side panel, if it's open, shows "Your bike thread: you were checking Bike A in the rain · Open where I was · Not now".
   - **With "every site" turned on:** a small bar with the same words appears on the page. The bar is added to that one tab only when there's a match, so there's no script running on every page.
   - Either way, it shows at most once per thread per day, you can snooze it, and it never appears on off-list sites.
3. **AI chats.** When you open ChatGPT, Claude or Gemini, the bridge offers "Continue a thread," which puts the brief into the message box. From 2.2, on AI sites where you turn it on, the page helper also compares the first message of a new chat with your threads, on the device, and offers the match. The message isn't stored unless you save it.
4. **Since you left (2.2).** When you reopen a thread, the side panel first lists what happened while you were away and wasn't done by you: helper results, watcher changes, forwarded emails, phone saves and replies added. It's built from the events after your last visit.

### Flow 4: Next moves (v1, with the planner in 2.2)

1. **After every change, a rules engine reads the thread's state:**
   - empty cells and missing criteria
   - open questions
   - days since you last touched the thread
   - signs that you're circling
   - which keys you've added
2. **Each rule proposes moves with a score.** The score weighs how much the move could change the outcome, how recently things changed, and what it costs. From 2.2 the planner (Flow 9) replaces these scores.
3. **The top three show under the thread.** Moves that need a key you haven't added show an "add a key" hint instead.
4. **Clicking a move runs a job.** It runs on the device, in the cloud, or by opening a page for you. Results land in the review tray as proposed cards or drafts. Nothing changes the thread until you accept it.
5. **"Why?"** On the ranking (v1) and on every cell (2.1), it shows your weights, the cards behind the result, and how much each counted. It uses the same numbers the code used.

Moves are shared across shapes. Each declares what it needs (for example, Compare needs two or more things and one field) and when it's worth showing, so a new shape mostly reuses existing moves.

| Move (version 1) | Reads from the thread | What runs | What you get |
|---|---|---|---|
| Compare | Options, what matters, cards | On the device; no AI needed to build the table. If nothing is marked as mattering yet, it asks "What matters to you?" first | The comparison table |
| Watch list | The open question and the options | YouTube's official search (with your key or our quota), or a YouTube search page opened for you and ranked. Ranking uses relevance, channel size, recency and matching chapters | A clickable list. Opening one jumps to the chapter |
| Ask people | What matters, options, what you've checked, your photos | Suggests two or three communities, opens one's rules for you, and drafts a post. It copies the draft and opens the post page. You rewrite it and post it. Later, when you open your post, the bridge asks "Add 6 replies to the thread?" | A draft, then replies as evidence |
| Dig | One card | Web search (your key), reads the top pages, and checks whether each supports or contradicts the card. In 2.2 it runs as a helper (Flow 10) | Proposed cards with quotes and links |
| Do I have enough? | The whole structure | On the device. Decide: the ranking plus a what-if check (Flow 5). Learn: parts against your goal. Track: items without an outcome | What's settled, what's open, and the one question that could change the outcome |
| Conclude | Your takes and the cards | A model drafts a conclusion, each reason linked to its claim | A draft you edit. Then the thread moves to Done with the outcome saved |
| Continue in any AI | The whole record | A brief built from fixed fields within a length limit: confusion first, then what's settled, then relevant facts about you, then style. It opens the AI and fills the message box, or copies the brief if the site blocks that | The AI picks up where you are |
| Remind me | A date, a deadline or a follow-up | Chrome's alarms and notifications, or a calendar link or file | The thread comes back on time |

### Flow 5: Finish (v1, with additions in 2.2)

1. **Rank the options (Decide).** Each option is scored on your criteria with the three-tap weights, using the claims (for, against, how many sources agree) and your takes. Any option with a dealbreaker is out.
2. **The what-if check.** For each empty or disputed cell, it asks: if this came back good, or bad, would the top option change?
   - If no cell can change the winner, the thread is **ready to decide**.
   - If one can, that cell becomes **the open question** and gets a Dig button.
3. **Other modes.** Learn checks parts against the depth your goal needs. Track checks that every item has an outcome. Research checks that every question has a conclusion with sources.
4. **Conclude.** The draft conclusion is written to the thread's file, with each reason stored as a link to its claim, so that from 2.2 the product can tell you when a reason stops holding. The thread moves to Done, and its outcome can be reused later ("What did I already find?").
5. **Added in 2.2:**
   - **Good enough or thorough** sets the bar for "ready." Good enough means no open cell can change the winner. Thorough also needs at least two independent sources behind every cell that decides the ranking.
   - **Pre-mortem.** Before Conclude, one tap asks "It's three months later and you regret this. Why?" The model drafts three reasons from the thread and the blueprint's expert checks. In basic mode, it lists the expert checks you haven't done. Any reason can become one last question.
   - **Check-in.** Conclude schedules one from the blueprint (Flow 13).

### Flow 6: Track threads for job pages (v1, with email in 2.4)

1. **Saving a job page.** If the page has job data, the row fills from those fields. If not, the model fills the Track form (title, company, location, salary, requirements) from the page text.
2. **Marking it applied.** On the same employer's site, when a page title reads like "Thank you for applying," the bridge asks "Mark as applied?" This uses only the page's address and title.
3. **Reminders and deadlines.** A follow-up reminder is set for 7 days later, and deadlines get a calendar link.
4. **LinkedIn stays off-limits**, because [LinkedIn forbids extensions that scrape, change or automate its pages](https://www.linkedin.com/help/linkedin/answer/a1340567/). Jobs found on LinkedIn are saved from the employer's own page or by pasting the link.
5. **Forwarded emails (2.4).** An interview invite or a rejection forwarded to the thread's address proposes a stage change in the review tray: "Company X: interview on Tuesday at 10:00. Update and add to calendar?"

### Flow 7: Knowledge across threads (2.1)

1. **Find candidates.** When a card mentions a name, it looks for the same thing in every thread:
   - the same identifier: a product code from page data, a DOI, an ISBN, or a company's website
   - the same name once cleaned up (lowercase, no punctuation, model numbers kept)
   - a known other name
   - a close match in meaning between the name with its context and the thing
2. **Decide.**
   - Same thread and a strong match: merge, and show it with a split button.
   - Different threads: suggest. "Is 'the Sprint' in Commute gear the same as Sprint Pro 26T?"
   - Different kinds, such as Sprint the bike and Sprint the company: never merge.
3. **Undo is exact.** Merges and splits are events, so a split puts every card back where it was.
4. **Thing pages** are views over the claims: prices seen with dates, owner reports, your takes, and the threads the thing appears in.
5. **"You researched this before."** When a new thread starts, or a save names a thing you know, it offers to bring in what you found. It links the claims instead of copying them, so new evidence shows in both threads.
6. **"What did I already find?"** searches every thread on the device by meaning, by name, and by filters such as kind, date and thread.

### Flow 8: Evidence weight and contradictions (kind labels in v1, the rest in 2.1)

Each card's weight comes from five factors, and all of them show in "Why?". The starting values below get tuned on the labelled test set.

| Factor | How it's worked out | Starting value |
|---|---|---|
| Kind | From the source: official data or a measurement, an expert test, an owner's experience, a seller's claim, or an AI answer. An AI answer whose cited source checks out counts as that source | 1.0 · 0.8 · 0.6 · 0.3 · 0.2 |
| Independence | Cards are grouped when they share the original link, repeat the same text (near-duplicates found with embeddings or long shared phrases), or come from the same author or channel | A group counts once |
| Recency | Older evidence counts for less, at a rate set by the blueprint. A card about a different model year or version than the option gets a label, such as "about the 2025 model" | Halves every 12 months for products, every 6 for software |
| Specificity | The built-in model rates it as vague, some detail, or specific (numbers, conditions, how long). Basic mode uses rules: numbers, units and time words | ×0.7 · ×1.0 · ×1.2 |
| Conflicts of interest | Affiliate links in the page (known patterns such as store tracking tags and affiliate network addresses), sponsorship words ("sponsored," "paid partnership," "#ad"), and pages run by the seller | Labelled, and ×0.5 |

- **Cell confidence.** Weights for and against add up to strong, some, thin or disputed. Disputed means both sides carry real weight.
- **Patterns.** When the cards on one side share a field, such as the same model year, shop or month, it offers that as a possible explanation: "All four complaints about Bike B are about the 2025 model." Code finds the pattern, and the model only phrases it.

### Flow 9: The planner (rules in v1, expected value in 2.2)

For each possible move, the planner estimates four things:
- **Change:** the chance the move settles a cell or question that could change the outcome (from the what-if check), times how uncertain that cell is now.
- **Progress:** how many open items toward "done" it closes.
- **Urgency:** rises as the deadline gets close. With "good enough," it drops to zero once the winner is stable.
- **Cost:** your minutes, days of waiting, and money.

Score = (change + progress) × urgency ÷ cost. The top three show, each with a one-line reason such as "could change your pick," "due Friday," or "fading."

The estimates start as fixed values (for example, a helper finds owner reports 7 times in 10) and adjust on the device from your own history: which moves you skip, how long they take you, and what they found.

- **Bike:** "Owner reports of Bike A in rain" could change the winner and costs none of your time, so it ranks first. "Ask people" could also change it, but it costs 10 minutes and two days of waiting, and you want to decide by Saturday.
- **Learn:** parts likely to fade before the exam date rank high.
- **Track:** deadlines, and applications with no reply after the follow-up date, rank high.

### Flow 10: Helpers (2.2)

1. **Plan.** The cloud model drafts a plan in a fixed format from the question, your trusted and distrusted sources, and the blueprint's expert checks: the searches, the kinds of sources to prefer, and an estimated cost. Each page read is roughly 3,000 tokens, so 10 pages come to about 30,000 tokens plus the searches, priced at your provider's current rates.
2. **Approve.** You see the plan and the budget (searches, pages, money, time), edit it if you like, and approve. The plan is then frozen.
3. **Search.** It runs the approved searches through your AI provider's web search tool or a search API key.
4. **Choose pages.** Code picks the pages: no distrusted sites, a mix of sites, and newer pages first.
5. **Ask once for the sites.** "Read 10 pages on 6 sites?" Chrome then asks for access to just those sites. You can choose to always let helpers read public pages, which Chrome shows as broader access.
6. **Read.** Pages are fetched logged out, with no cookies, and the helper follows each site's robots.txt. Sites that don't allow automated reading go on an "Open these yourself" list. Reddit, for example, [requires approval for automated access](https://reddit.zendesk.com/hc/fr/articles/16471395473812-Bots-et-outils-de-mod%C3%A9ration). When you open one of those pages, the page helper reads it after your click.
7. **Extract.** The model proposes cards in a fixed format: the quote, stance, kind and the thing they're about. A card is dropped unless its quote appears word for word in the page.
8. **Stop at the limit.** Budget counters live in code, not in the model. When one runs out, the helper stops and reports what it has.
9. **Report.** Proposed cards land in the review tray, grouped as for, against and neutral, with confidence and the activity log: every search, every page read or skipped and why, the time and the cost.

Each step is saved as it finishes, so a helper picks up where it stopped if Chrome closes it. Helpers never post, apply, buy, log in, fill in forms or click on pages.

### Flow 11: Watchers (2.2)

| Watcher | How it checks | How often |
|---|---|---|
| A price on a saved page | Fetches the page logged out and reads the price from its product data, following robots.txt. If the site blocks this or has no product data, it checks when you next open the page instead | At most once a day |
| Replies to your community post | Counts new replies when you open the post | When you visit |
| A job posting about to close | Uses the closing date in the posting's job data, with no fetching | A reminder before the date |
| New papers citing one you saved | Asks [OpenAlex](https://help.openalex.org/access/pricing/), whose free key includes $1 of use a day | Once a day |

- A watcher that fetches pages needs Chrome's access to that one site, asked when you turn it on.
- Results go to "since you left." A notification comes only for a target you set, such as a price below one you named.

### Flow 12: Background work (2.2)

- **When:** Chrome's idle API reports you've been away for a few minutes and, on laptops that report their battery, it's charging. Work stops the moment you're back.
- **What:** only saved data. It merges duplicates, refreshes summaries and "where I was" notes, recomputes weights and contradictions, marks stale claims, checks living decisions, and prepares check-ins.
- **How:** an extension can have only one offscreen document open at a time, so the worker page runs a single job queue, stored in IndexedDB. Jobs are small and resumable, with a daily time limit.

### Flow 13: Living decisions, check-ins and lessons (2.2, lessons in v3)

1. **Living decisions.** Each reason in a conclusion links to a claim. When new evidence flips that claim, a watcher sees a change, or the claim goes stale, the conclusion is marked "a reason changed" and shows in "since you left."
2. **Check-ins.** The blueprint sets when to ask: a purchase after a month, a new job at 30 and 90 days, a course at the end of term, a team tool at 3 months. There's one question with one-tap answers and an optional line. The answer becomes a card on the conclusion, of the kind "your own experience."
3. **Lessons (v3).** Code looks across your check-ins and decisions for patterns:
   - complaints that match criteria you weighted low, three times or more: "You often underweight maintenance"
   - in Learn, parts you only watched that later failed a check
   - in Track, results by source, always with counts: "Referrals: 3 interviews from 5. Cold applications: 2 from 20."

   A lesson shows only with at least three cases and always lists them. It becomes a suggestion for your profile or blueprints, which you accept or dismiss.

### Flow 14: Learn stages, recall and fading (2.3)

1. Each part of a topic is a thing of the kind "concept," with a stage: seen, followed, explained or used.
2. When you return to a Learn thread, it asks one to three short questions on parts that are due, written from your own explanations and saved moments. You grade yourself: got it, partly, or not yet. Quizzes appear only for parts you marked as confusing or parts that are due, never as homework.
3. [FSRS](https://github.com/open-spaced-repetition/ts-fsrs), the open-source scheduler that Anki also offers, sets each part's next check from your grades.
4. A part counts as done only after you pass a check at least two days after you explained it.

### Flow 15: Phone, email, photos, voice and imports (2.4)

**The relay.** One small open-source server with one job: passing sealed envelopes between your devices.
- It's off by default. You can use the hosted one or run your own.
- Your laptop shows a QR code and your phone scans it to pair. Keys stay on your devices, so the relay sees only sealed data, its size and its time.
- Envelopes are deleted once your devices pick them up, or after 14 days.
- Encryption uses standard libraries (libsodium or the browser's WebCrypto), never home-made cryptography, and gets an outside review before launch.

**Phone share.** The phone app is an installable web app.
- On Android, it appears in the share sheet, as [installed web apps can](https://developer.chrome.com/docs/capabilities/web-apis/web-share-target).
- On iPhone, Safari doesn't let web apps receive shares, and web apps [can't run in the background](https://www.mobiloud.com/blog/progressive-web-apps-ios). So the iPhone route starts with an Apple Shortcut in the share sheet that sends to the relay, and a small native app comes only if testers need it. Confirm both on current iOS before building.
- A phone save holds a link, text, a photo or a voice note, plus your take. It waits in the queue until your laptop processes it, because the built-in model runs only on desktop. If you allow it, your key can process it on the phone instead.

**Email forwarding.**
- Each thread can get its own address, such as bike-7k2q@in.example.org, and one general address feeds the inbox.
- The relay accepts only mail forwarded from your own addresses that pass the standard sender checks (DMARC). It seals each message to your device key the moment it arrives and keeps nothing readable.
- The extension opens the message on the device and proposes cards or Track updates in the review tray. Order confirmations, seller replies, interview invites and bookings are the first kinds to support.
- Emails are data. Instructions inside them can't trigger anything.

**Photos.** The built-in model reads images, so price tags, whiteboards and handwritten notes become text you confirm. Without it, your key does this, or the photo is saved with your take.

**Voice takes.** Chrome's speech recognition can [send audio to Google's servers](https://www.assemblyai.com/blog/speech-recognition-javascript-web-speech-api), so voice takes always ask for [on-device recognition](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition/processLocally). Where that isn't available, the built-in model's audio input or your key transcribes the take. Otherwise the audio is saved and transcribed later.

**Imports.** They run in the worker page in batches, and everything lands in the review tray first.
- ChatGPT and Claude data exports: each conversation becomes captures of the kind "AI answer"
- Kindle highlights, from the "My Clippings" file
- Readwise, with your token
- Zotero, from an export file
- Bookmarks, asking for Chrome's bookmarks permission only when you import

### Flow 16: Agents and the thread folder (read in 2.4, add in v3)

1. **The folder.** You pick a folder once. The extension keeps one Markdown file per thread there, plus `things/` and `you.md`, updated after each change. It uses the File System Access API, where Chrome 122 added an ["Allow on every visit" option](https://developer.chrome.com/blog/persistent-permissions-for-the-file-system-access-api). Test early whether that works for extension pages. If it doesn't, allowing the folder again after Chrome restarts takes one click.
2. **The MCP server** is a separate open-source package that runs on your computer and reads the folder. Its tools list threads, get a brief, get open questions, and search what you found. Apps that support MCP, such as Claude Desktop, can also use it to save into a thread, which covers desktop AI apps a browser extension can't read. Those saves land in the review tray. In v3 agents can also propose cards and takes directly.
3. **Scopes** for each agent live in a settings file: which threads, and read or add. For example, Claude Code can read and add to "Fix: login bug" and nothing else.
4. **Additions wait.** What an agent proposes is written to the `inbox/` folder. The extension moves it into the review tray with the agent's name on it. Nothing goes straight into a thread.
5. **An honest limit.** Scopes control what the MCP tools show. An agent that already has full access to your disk could read the folder anyway, so keep the folder outside the folders your agents work in.

### Flow 17: Shared threads (v3)

1. A shared thread has its own key. An invite is a link that carries the key after the "#", the part of a link that browsers never send to a server, so the relay still stores only sealed data.
2. Each person's events are signed with their device key and carry their name. Takes and votes stay separate, and "decide together" shows where people agree and disagree on each criterion.
3. Roles: owner, contributor (adds saves and takes) and viewer.
4. Events from everyone merge in order, using the counter on each event. Long text, such as a conclusion draft, uses a text-merging library (Automerge or Yjs, chosen in a spike) or one editor at a time.
5. Removing someone changes the thread's key from then on. What they already saw can't be taken back, and the product says so.

## 5. Permissions and privacy

| Permission | Why | When we ask | From |
|---|---|---|---|
| activeTab | Save from the tab you're on, only after your click | Built in, with no warning | v1 |
| sidePanel, storage, unlimitedStorage, alarms, notifications, contextMenus, offscreen, scripting | The app itself: its screen, local storage, reminders, the right-click Save, background work | At install | v1 |
| tabs | Tab rescue and the bridge, which need tab titles and addresses. These are checked on the device and never sent anywhere. Chrome's prompt calls this "Read your browsing history," so setup explains it first | At the first tab rescue. If you decline, Close and keep works only for the tab you're on | v1 |
| Access to chatgpt.com, claude.ai, gemini.google.com and youtube.com | Save buttons beside answers, and exact spots in chats and videos. From 2.2, the optional first-message match, with its own switch per site | The first time you use each site | v1 |
| Every site (optional) | Remembering your place on every open tab at Close and keep, the bridge bar on the page itself, and Save buttons beside comments and posts on any site. Chrome's prompt reads "Read and change all your data on all websites" | One question at the first tab rescue: "Remember your place on every site?" Off unless you say yes | v1 |
| tabGroups (optional) | Reopening a thread as a named tab group instead of a window. Chrome's prompt reads "View and manage your tab groups" | The first time you choose tab groups | v1 |
| Off-list | LinkedIn, banking, email and health portals: no page helper, and Save is blocked with an explanation | Always on, and editable | v1 |
| Keys | Stored encrypted on the device. Calls go straight to the provider | When you turn on a move that needs one | v1 |
| idle | Background work only while you're away | No prompt. Chrome [shows no warning for it](https://developer.chrome.com/docs/extensions/reference/permissions-list) | 2.2 |
| Access to one site at a time (optional) | Helpers and watchers reading public pages | When you approve a helper's reading list or turn on a watcher, for those sites only | 2.2 |
| bookmarks (optional) | Importing bookmarks | When you start the import | 2.4 |
| A folder you pick | The thread folder for MCP and other apps | When you pick the folder | 2.4 |
| Microphone | Voice takes | Chrome's own prompt, the first time | 2.4 |

**What each outside service sees**

| Service | What it sees | When |
|---|---|---|
| Your AI provider | The text of the job: the cards, brief, page or photo being processed | Only for moves that use your key |
| Your search provider | The search words in a helper's plan | When a helper runs |
| Sites that helpers and watchers read | A logged-out visit from your internet address | When a helper runs, or once a day per watcher |
| YouTube | The search words for the watch list | When you run the watch list |
| OpenAlex | The IDs of the papers you watch | Once a day per paper watcher |
| The relay | Sealed envelopes, with their size and time, and each forwarded email for the moment it takes to seal it | Only if you turn it on |
| AI chat sites | Nothing new. A brief goes into their message box, and you choose whether to send it | When you use Continue in any AI |

## 6. How we know it works

- **Technical tests before the build.** The seven quick tests in `how-it-runs.md` (capture, speed, filing without a model, form-filling accuracy, tab grouping, the model in the worker page, reopening at the sentence), with throwaway code in weeks 1–2.
- **Capture tests.** Keep saved copies of ChatGPT, Claude, Gemini, YouTube, Reddit, X, job and shop pages, and run the capture tests on every change. Run them on the live sites weekly, because those sites change.
- **A labelled test set.** Collect 20 real threads (about 300 saves) labelled with the right thread, points, stance, mode and which names are the same thing. Measure filing and extraction accuracy separately for the built-in model, the cloud model and basic mode.
- **Speed.** Measure the three targets on every build: "Saved" in about 0.1 s, filed in under 0.5 s, labelled in 1 to 5 s, on an 8 GB and a 16 GB laptop.
- **Shadow mode in the beta.** It makes its guesses silently, and we compare them with what users chose.
- **Devices.** Test on an 8 GB laptop (basic mode), a 16 GB laptop (built-in model) and a Mac.
- **Safety tests.** Use pages with hidden instructions to check that captured text can't trigger anything.
- **Replay tests.** Rebuild every view from the event log and compare it with the stored views.
- **Matching set (2.1).** 500 pairs of names from real threads, labelled same or different. Wrong automatic merges must stay under 1 in 50.
- **Independence set (2.1).** Cards grouped by hand into "same source" groups, to check the grouping rules.
- **Planner checks (2.2).** Made-up decision tables where the right next move is known, such as a table where only one cell can change the winner.
- **Helper checks (2.2).** No run goes over budget, every quote matches its page, and pages with hidden instructions can't change a plan.
- **Background load (2.2).** CPU, memory and battery measured on an 8 GB laptop.
- **Relay (2.4).** An outside security review, encryption test vectors, and fuzz tests for the email parser.
- **Metrics stay on the device.** Testers can export them to share.

## 7. Tech stack

- TypeScript, Chrome Manifest V3, and the WXT extension framework
- Preact or React for the side panel
- Dexie for the local database (IndexedDB)
- Zod to check every AI answer against its format
- Transformers.js for on-device embeddings, with a small multilingual model and the runtime files bundled in the extension
- Mozilla Readability for page text
- Chrome's Prompt API, plus provider APIs through the user's key
- Blueprints as plain YAML files in the repo, one per shape and template
- Vitest and Playwright for tests, GitHub Actions for builds
- ts-fsrs for recall scheduling (2.3)
- The relay (2.4): TypeScript, with a reference deployment on a serverless platform that can receive email (for example Cloudflare Workers with Email Routing), a Docker image for self-hosting, and libsodium or WebCrypto for encryption
- The phone app (2.4): an installable web app that reuses the side panel's components
- The MCP server (2.4): TypeScript with the official MCP SDK, reading the thread folder
- An email parser that runs on the device (2.4)
- Automerge or Yjs for shared text (v3)

## 8. Build plan

### Version 1 (weeks 1–14)

Sized for one or two experienced developers. If you're learning as you go, expect roughly double. The small versions of the layers add about a week, mostly in weeks 3–6. If time runs short, Track is the first thing to cut.

| Weeks | Build | Done when |
|---|---|---|
| 1–2 | **Validate:** landing pages, 15 hand-run sessions (Decide, Track, Learn), competitor run-through, clickable mockups including the You page and "Why?", and the seven technical tests from `how-it-runs.md` with throwaway code | A promise is chosen, the sessions pass the decision rule, and the technical tests show no blocker |
| 3–4 | **Foundation:** extension skeleton, side panel, local store with the full record shape (things, claims, questions, spots, facts about you, an author on every event), Save with the page helper (selection, site adapters, main text, structured data), inbox, threads, Markdown export | You can save from any page into a thread and export it, with "Saved" in about 0.1 s |
| 5–6 | **Organizing:** the AI tiers and basic mode, the fast and slow lanes, filing, "What's this for?", blueprint files and templates, the form for each shape, names linked inside a thread with merge and split, generated criteria, the Decide table, Track rows, the You page, corrections as examples, the trail, test set v1 | At least 8 in 10 test saves land in the right thread, filed in under 0.5 s |
| 7–8 | **Bridge:** tab rescue with the plan screen, spots, "where I was" notes, open where I was, the bridge signal (toolbar icon and side panel, plus the bar on the page with "every site"), search words in addresses, AI chat and YouTube spots | Testers get back into a thread within a minute |
| 9–10 | **Next moves:** the rules engine, the eight moves, weights in three taps, and "Why?" on the ranking | Each move works end to end on the bike and job examples |
| 11–12 | **Hardening:** permissions review, basic mode on an 8 GB laptop, safety tests, speed, "delete everything," Chrome Web Store submission (review can take a while), private beta with 20 testers | Testers use it for a week without blocking bugs |
| 13–14 | **Learn from the beta:** fix the top problems, then decide on public launch and the open-source release | The version 1 success measures in `product-definition.md` are met |

### Version 2 (weeks 15–38, four releases)

This is the default order. The beta findings set the real one.

| Weeks | Release | Build | Done when |
|---|---|---|---|
| 15–19 | **2.1 Knows what you found** | Things shared across threads, thing pages, "you researched this before," What did I already find?, profile suggestions, evidence weights (independence, recency, specificity, affiliate labels), "Why?" on every cell | Wrong automatic merges stay under 1 in 50, and most "bring this in" suggestions are accepted |
| 20–25 | **2.2 Works while you're away** | The job queue, background work, the expected-value planner, helpers, watchers, "since you left," the first-message bridge, living decisions, check-ins, the pre-mortem, "good enough or thorough" | No helper run goes over budget, every quote matches its page, most helper cards are accepted, and background work goes unnoticed on an 8 GB laptop |
| 26–30 | **2.3 Every shape** | Research, Fix, Plan and Follow threads, combined blueprints, what experts check, Learn stages, recall checks with FSRS, the other next moves | Five hand-run mixed tasks (a visa, a doctor for a parent, a move) each get a usable blueprint with three edits or fewer |
| 31–38 | **2.4 Everywhere** | The relay and pairing, the phone app, email forwarding, photos and voice takes, imports, the thread folder, the read-only MCP server, Ask a friend, read-only share links, and the outside security review | A phone save reaches the laptop within a minute when both are online, the relay passes review, and five common kinds of email become the right cards |

### Version 3 (from week 39)

- Lessons, once testers have months of check-ins
- Shared threads with roles, then team spaces
- Agents that add through MCP, into the review tray
- A desktop shortcut that saves from any app, through a small companion app
- The public blueprint template library
- Crowd signals, only if a privacy design passes public review

Contributors can take separate pieces in parallel: site adapters, imports, blueprint templates and translations.

## 9. Execution risks

- **Many laptops can't run the built-in model.** Basic mode and the optional key cover them. Measure how many testers can run it.
- **The built-in model is slow on some laptops.** Filing never depends on it, and labels arrive when ready. If form-filling is too slow, the cloud model takes it for users with a key, and basic mode for the rest.
- **AI sites change their layout.** Each site has a small adapter with tests. Selecting text and saving always works as a fallback.
- **Exact spots depend on permissions.** Without "every site," background tabs keep only their link and title. Make the one-click "keep my place" on the current tab fast and obvious, so the common case needs no extra permission.
- **Chrome Web Store review of permissions.** Ask for as little as possible, request extras only when needed, and publish a clear privacy policy.
- **Chrome Web Store's single-purpose rule.** An extension [must have one narrow purpose](https://developer.chrome.com/docs/webstore/program-policies/quality-guidelines), though [several functions within one focus area are allowed](https://developer.chrome.com/docs/webstore/program-policies/quality-guidelines-faq). State the purpose as "save your research into threads and pick it up where you left off," and make every feature serve it.
- **Cloud costs for Dig, helpers and the watch list.** Start with the user's own key, show the estimated cost before every helper run, and add a hosted option with limits later.
- **The relay is our first server.** It brings security, cost, spam and legal questions, since forwarded emails contain other people's details. Keep it off by default and self-hostable, and get it reviewed from outside before launch.
- **Helpers and site rules.** Hard budgets, per-site access, logged-out reading and robots.txt keep helpers polite. Sites that forbid automated reading go on the "open these yourself" list.
- **A profile that feels creepy.** Show every fact with its source, keep learned facts as suggestions, keep it on the device, and allow one-tap delete.
- **Lessons need time.** Check-ins start in 2.2, so lessons in version 3 have months of outcomes to learn from.
- **Building too much.** Freeze the version 1 scope. Each later release must be useful on its own, and when time runs short, cut features from a release rather than delaying it.
