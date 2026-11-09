# How it runs: what one click does, where the data goes, and what the AI does

This answers the practical questions. It covers what one click keeps on different sites, how a save gets organized without waiting, how each mode gets its checklist, and how the tabs feature works. `execution-plan.md` has the build details.

## The short answers

| Question | Answer |
|---|---|
| Does it load the HTML again? | No. It reads the page that's already open in your tab, the same text you see. Nothing is downloaded again, and nothing is sent anywhere to organize it |
| Does the whole page go, or the link? | Both, but never the raw HTML. It keeps the link, the piece you meant (your selection, one AI answer, one comment, one post, or an article's main text) and a few facts about the page |
| Where does it go? | Into a database inside Chrome on your laptop. It leaves your laptop only for moves you turn on, like Dig with your own key |
| How does the AI arrange it by mode? | It doesn't arrange anything freely. The thread gives it a short form to fill: which option, which criterion, for or against, what kind of source, and the exact quote. The model fills the form, and ordinary code puts the answer in the right place |
| Is it fast? | Saving never waits for AI. "Saved" shows in about a tenth of a second, the thread in under half a second without any language model, and the labels a few seconds later |
| Each mode has so many features. Who builds them all? | They aren't separate features. About 15 moves work across seven shapes, and each mode is a small configuration file |
| How does the tabs feature work? | It's one button, Close and keep, for this tab, this thread or everything. Each tab becomes a spot: a bookmark that knows its thread and, where Chrome allows, where you were on the page |

## 1. One click: what it reads and keeps

### What actually runs

1. You click Save. That can be the toolbar button, a keyboard shortcut, the right-click menu, or a small Save button beside an answer or comment on sites you've allowed.
2. The click gives the extension access to this one tab for a moment. Chrome calls this [activeTab](https://developer.chrome.com/docs/extensions/develop/concepts/activeTab).
3. The extension's page helper runs inside the tab and reads the page as it is now. It needs no API from the site and no second download.
4. It hands the result to the extension's coordinator, which writes it to the local database.

On this chat right now, the page helper would read the Kiro page as your browser shows it. Kiro has no adapter, so it would use the general method below.

### Which piece it keeps

The page helper works out what you meant, in this order:

1. **You selected text:** exactly that text, a sentence or two around it for context, and a link that scrolls to and highlights it.
2. **A site it knows:** the piece in the middle of your screen. That's one AI answer with your question before it, one comment, one post, one video moment, one product or one job. It highlights its guess for a moment, and if the guess is wrong, you click the piece you meant.
3. **Any other page:** if the page is an article, its main text and the paragraph you were on. The main text comes from Mozilla's Readability, the code behind Firefox's reader view. If it's an app, a feed or a chat it doesn't know, it keeps the text on your screen.

Every save also keeps the link, a link to the exact sentence, the title, the site, the time, the author and date if the page lists them, and any structured data the page carries for search engines, such as product prices and job details.

On sites you've allowed, small Save buttons sit beside each answer, comment or post, so there's nothing to guess.

### Site by site

| Where you are | What one click keeps |
|---|---|
| ChatGPT, Claude or Gemini on the web | The answer you're on, your question before it, the model name if shown, any cited links, and the chat's link |
| An AI chat it doesn't know yet, like this Kiro chat | Your selection, or the messages on your screen, plus the page link. Adapters for more chat sites get added one at a time |
| ChatGPT or Claude desktop apps | A browser extension can't see inside desktop apps. In v1, you paste into the side panel, or open the same chat on the web and save there. In 2.4, apps that support MCP, such as Claude Desktop, can save through the MCP server. In v3, a desktop shortcut works in any app |
| AI apps on your phone | The share button sends to the phone app (2.4) |
| A blog or article | The main text, the author and date, and the paragraph you were on |
| Reddit | The comment or post you're on, with its author, subreddit, time and permanent link |
| X | The post you're on, or the visible thread, with author, time and link. Images and videos are kept as links |
| YouTube | The video, the second you're at, the title, channel and chapter, and the captions around that moment if the video has them |
| A shop page | Product name, price and availability, read from the page's product data with no AI |
| A job page | Title, company, location, dates and salary, read from the page's job data with no AI |
| A PDF in Chrome | Your selection, through the right-click menu (confirm this in Chrome's PDF viewer). Reading a whole PDF needs its own reader |
| LinkedIn, banking, email and health portals | Nothing. Save explains why |

### What it never keeps

- **The raw HTML.** It's heavy, and it holds things you didn't mean to save: your account name, other chats in the sidebar, ads.
- **Other people's images.** It keeps links to them. Your own photos and screenshots are kept.
- **Anything from off-list sites.**

### Why keep the text and not just the link

- Links break. Chats get deleted, posts get removed, prices change.
- Organizing and searching need the words.
- It works offline.

A sentence takes under 1 KB and a long article about 50 KB. Most saves are a few KB, so 10,000 of them take tens of megabytes.

## 2. From click to organized, without waiting

The click never waits for AI. Each step makes the save more useful, and no later step can lose what an earlier one stored.

```
click
  │
  ▼
page helper reads the piece ─▶ coordinator writes it        "Saved"                     about 0.1 s
                                    │
                                    ▼
worker page, fast lane: no language model                   "Saved to Choosing a bike"  under 0.5 s
recent activity · site · names · meaning
                                    │
                                    ▼
worker page, slow lane: the built-in model fills the form   "Bike B · rain · against"   1 to 5 s
then code places the answer
                                    │
                                    ▼
the table, "where I was" and the next moves update
```

| Step | What happens | Runs on | Target |
|---|---|---|---|
| Saved | The capture is written to the local database | Page helper and coordinator | About 0.1 s, the point where a response [feels instant](https://www.nngroup.com/articles/response-times-3-important-limits/) |
| Filed | It picks the thread from four signals: you saved there in the last 30 minutes, the same site or link, shared names, and similar meaning | Worker page, with rules and a small embedding model | Under 0.5 s |
| Labelled | The built-in model fills the thread's form, and code places the result | Worker page | 1 to 5 s, shown when ready |
| Tidied | Duplicates merged, summaries and "where I was" refreshed | Worker page, while you're idle | Whenever |
| Deep work | Dig, helpers, conclusions on long threads | Your key, in the background | Seconds to minutes, with progress shown |

**How it stays fast**
- **Two lanes.** Filing uses only rules and embeddings, which take milliseconds. Language-model jobs wait in a queue and run one at a time.
- **Only the relevant text.** A long page is cut into chunks, and only the two or three chunks closest to the thread's question go to the model.
- **Short answers.** The model returns a few short fields, not paragraphs. On a small model, the length of the answer drives most of the wait.
- **A warm model.** While you're working, the worker page keeps a model session ready and copies it for each job. The first job after Chrome starts is slower, because the model has to load into memory.
- **A cache.** Saving the same link twice reuses the earlier work.
- **A one-time download.** Chrome downloads the built-in model the first time it's used. [The download needs a click to start](https://developer.chrome.com/docs/ai/prompt-api) and an unmetered connection, so setup includes that click. Until the download finishes, basic mode works.

**Where the model runs.** The built-in model needs a page, and the coordinator is a service worker, not a page. So the model runs in the worker page, a hidden page the extension keeps open. Projects such as [ReviewWise](https://devpost.com/software/question-analyzer) do the same. Confirm this in the first week (section 7).

## 3. How the AI arranges a save by mode and context

### The thread hands the model a form

When a thread starts, it gets a shape (Decide, Learn, Track and so on) and its own lists: the options and criteria, or the topics, or the stages. Every later save is read against those lists. The model doesn't decide where things go. It answers a short form, and code does the arranging.

| Shape | What the model fills in for each point |
|---|---|
| Decide | Which option (from the list, or new), which criterion (from the list, or other), for or against, kind of source, exact quote |
| Learn | Which part of the topic (from the list, or new), whether it's an explanation, example, confusion or question, exact quote |
| Research | Which of the thread's questions, supports or contradicts, kind of source, exact quote |
| Track | Usually nothing, because job and product data fill the row. If the page has none: role, company, location, salary, deadline, requirements |
| Fix | Symptom, cause tried, result or fix, whether it worked, exact quote |
| Plan | Place, booking, cost or to-do, date, price, exact quote |
| Follow | Date, what happened, who said it, exact quote |

### What the model sees

Only what the job needs, in a few lines:
- the thread's question
- the lists it has to choose from
- the facts about you that apply here, such as "10 km commute, heavy rain"
- two of your past corrections that look most like this save
- the relevant chunks of the save

### Example: the Reddit comment about Bike B

What the model gets (shortened):

```
Thread: Which city bike handles rain and a 10 km commute, within my budget?
Options: Bike A, Bike B, Bike C
Criteria: budget, rain, comfort, maintenance
Source: Reddit comment, r/bikecommuting
Text: "Had the B for 3 months. Brakes squeak after a few weeks of rain,
and the shop said that's normal for this model. Comfy though."
```

What it returns, in a fixed format:

```json
[
  {"option": "Bike B", "criterion": "rain", "stance": "against", "kind": "owner",
   "quote": "Brakes squeak after a few weeks of rain", "confidence": "high"},
  {"option": "Bike B", "criterion": "comfort", "stance": "for", "kind": "owner",
   "quote": "Comfy though", "confidence": "medium"}
]
```

What code does next:
1. It checks that each quote appears word for word in the text.
2. The high-confidence point goes into the Bike B × rain cell, and the medium one goes to the review tray.
3. It recomputes the ranking and the what-if check, and your "dealbreaker" take puts Bike B out.
4. The next moves update. All of this takes milliseconds.

### Why a small on-device model is enough

- It chooses from short lists and copies words. It doesn't write.
- The answer format is fixed with JSON Schema, and the thread's lists become the only allowed values, so it can't invent an option.
- [Extensions can lower the model's randomness](https://developer.chrome.com/docs/ai/prompt-api), so the same save gets the same answer.
- When it's unsure, the point goes to the review tray instead of the thread.

### It gets better with your corrections

When you move a save to another thread or fix a label, that correction is stored as an example. Later prompts include the two examples most like the new save, and the filing thresholds adjust to how often you correct it. All of this stays on your laptop.

### Picking the mode at the start

1. **The page type.** Job data means Track, product data means Decide, and a syllabus or lecture means Learn.
2. **Your answer to "What's this for?"** Words like buy, choose or which mean Decide. Learn, exam or understand mean Learn. Apply or track mean Track. Fix, error or broken mean Fix. Trip, move or plan mean Plan. "Is it true" or "why" means Research.
3. **Still unclear.** The built-in model picks one of the seven shapes.
4. **You can switch** with one tap, and the saves are read again against the new form.

## 4. Many modes without a pile of features

### A mode is a configuration file

There's one engine. Each mode is a blueprint file that tells the engine what to keep, how to show it, what to ask the model, what done means and which moves apply. Each thread then fills in its own lists, such as this bike's criteria.

```yaml
shape: decide
things: options              # what you compare
fields: criteria             # what matters
view: table
form: [option, criterion, stance, kind, quote]
done: no open cell can change the winner
moves: [compare, watch_list, ask_people, dig, enough, conclude]
```

```yaml
shape: learn
things: parts                # topics and subtopics
stages: [seen, followed, explained, used]
view: checklist
form: [part, type, quote]
done: every part your goal needs is explained, then passes one later check
moves: [plan_from_syllabus, best_explanation, quiz_me, explain_back, continue_in_ai]
```

```yaml
shape: track
things: items
fields: [role, company, location, salary, deadline, requirements]   # job data first
stages: [saved, applied, interview, offer, rejected]
view: pipeline
form: only when the page has no job data
done: every item has an outcome
moves: [add_from_page, mark_applied, follow_up, prep, calendar]
```

Adding a mode means writing one of these files, plus a special move or two if it needs them. That's days of work, not months, and it's an easy place for open-source contributors to help.

### Moves are shared

Each move says what it needs and when it's worth showing, so the same move serves many modes.

| Move | Works on | Shows when |
|---|---|---|
| Compare | Anything with two or more things and at least one field | Options in Decide, offers in Track, stays in Plan |
| Do I have enough? | Every shape, using that shape's done rule | Once there's something to judge |
| Remind me | Anything with a date | Deadlines, follow-ups, reviews |
| Dig | Any card | A key point rests on one source, or on an AI answer nobody checked |
| Watch list | Any open question | A Learn part you're stuck on, or reviews for an option |
| Ask people | Decide, Fix, Learn | A question no saved source answers |
| Continue in any AI | Every shape | Always |
| Conclude | Decide, Research, Fix | The done rule is nearly met |
| Mark as applied | Track only | On a confirmation page |

### Where the checklist comes from

For the criteria of a Decide thread, the topics of a Learn thread or the documents for a visa, it tries three sources in order:

1. **Your own material.** A syllabus, a job description, or an official checklist you saved. The model pulls out the list, with a quote for each item. This is the most reliable source.
2. **A template.** The open library has hand-written lists such as "city bike," "laptop," "rental flat," "job search" and "exam prep." They load instantly and need no AI.
3. **A draft from the model.** When neither exists, it suggests four to six items from your purpose and your first saves, marked as suggestions. Simple tasks use the built-in model. Complex ones, like a visa, use your key and should cite a source.

You keep or drop items with a tap. The list starts short, and grows if you choose "thorough."

### The checklist keeps adjusting

- "Three saves mention frame size. Add it as a criterion?"
- In Learn, a part you keep marking as confusing splits into smaller parts.
- A quiz appears only for a part you marked as confusing, never as homework.

## 5. Tabs: Close and keep

### One button, three sizes

- **This tab:** keep my place here and close it. This also has a keyboard shortcut.
- **This thread:** close every tab that belongs to the thread you're in.
- **Everything:** the full tab rescue. It's the first thing you see after installing.

### What it reads

Only the titles and addresses of your open tabs, when you last looked at each one, and which tabs you'd already grouped. Chrome gives an extension these through the [tabs permission](https://developer.chrome.com/docs/extensions/reference/api/tabs), and its install prompt calls that permission "Read your browsing history." Setup explains that it means the titles and addresses of open tabs, checked on your laptop and never sent anywhere.

### How it groups 60 tabs in a few seconds

1. Tabs that already belong to a thread go to that thread.
2. The rest are compared by meaning, using the title and site, and grouped. Each group is matched against your threads, or named by the built-in model if it's new.
3. Tabs you'd already grouped in Chrome stay together.
4. Your inbox, calendar or music player is marked "keep open." Home pages and search results are marked "just close."
5. It shows the plan: "63 tabs → 4 threads, 9 to close, 5 to keep open." You drag anything that's wrong, then confirm with one click.

### What it stores: spots

Each tab becomes a spot, which is a bookmark that knows more.

| | Chrome bookmark | OneTab list | Spot |
|---|---|---|---|
| Link and title | Yes | Yes | Yes |
| Filed by meaning, with no folder to pick | No | No | Yes |
| Where you were on the page | No | No | Yes, where Chrome allows (below) |
| Why you had it open | No | No | Yes: the thread and its "where I was" note |
| Comes back on its own when it's relevant | No | No | Yes: the bridge |

Spots live in the extension's own database, not in Chrome's bookmarks, so your bookmarks stay as they are. Each thread's Markdown file lists them too. Tabs that fit no thread go into a "Loose tabs" list you can search, and once a month one tap clears the old ones.

### Where you were: what Chrome allows

An extension can read inside a tab only if it has access to that tab. Chrome also unloads tabs you haven't used for a while to save memory, and [an unloaded tab](https://developer.chrome.com/docs/extensions/reference/api/tabs) has no position to read.

| Tab | What the spot remembers |
|---|---|
| The tab you're on when you click | The exact spot: scroll position and the nearest sentence |
| Anything you saved | The exact sentence, because every save has a link to it |
| AI chats and YouTube, which you allow in v1 | The message you were on, and the video second |
| Other open tabs | The link and title. If you turn on "remember my place on every site," also the spot, as long as the tab is still loaded |

For the GeeksforGeeks problem you described, the fix is one click: press Close and keep, or its shortcut, while you're on that page, and it keeps your exact spot.

### Coming back

- **Open where I was** reopens the thread's spots in a new window, or as a named tab group if you allow Chrome's tab-group permission. Pages jump to the saved sentence through a text-fragment link, videos start at the saved second, and chats scroll to the saved message.
- If a page doesn't jump, which happens on apps that load their text late, one click on the toolbar icon takes you there.
- **The bridge signal.** When you open something related, the toolbar icon shows a dot, and the side panel, if it's open, shows "Your bike thread: you were checking Bike A in the rain." If you turn on "every site," a small bar appears on the page itself.

### A correction to the earlier plan

The earlier execution plan said positions are saved for every tab and that the bridge bar appears on the page. Both need access to every site, so both are now opt-in. By default, the bridge uses the toolbar icon and the side panel. `execution-plan.md` now says this.

## 6. The user flow, day one to day seven

**Day 1, install**
1. One screen: "Close your tabs and AI chats. Keep your train of thought." One button: **Rescue my tabs**.
2. Chrome asks for the tabs permission, after a plain explanation.
3. The plan appears in a few seconds. You fix anything, then click **Close and keep**. 63 tabs become 4 threads.
4. One question: "Remember your place on every site?" **Yes**, or **Just the links**.
5. Optional: **Turn on on-device AI**, which starts the model download, and **Add a key** for Dig. Both can wait.

**Day 1, later**
6. On ChatGPT, you click Save on an answer. "Saved" appears, then "What's this for?" with **Choosing a bike** and **New thread**. You pick one, and it shows "Saved to Choosing a bike," then the labels.
7. The side panel shows the comparison table, three next moves and the review tray.

**Day 3**
8. You search "best bike for heavy rain." The toolbar icon shows a dot. You click it, then **Open where I was**, and your spots reopen.

**Day 7**
9. **Do I have enough?** says you're ready. **Conclude** drafts the decision with its reasons. You edit it, and the thread moves to Done.

## 7. What to test first

These are the assumptions most likely to break. Each one can be tested in a few days with throwaway code, before the main build.

| Test | How | Good enough |
|---|---|---|
| Capture picks the right piece | 50 saves each on ChatGPT, Claude, Gemini, an unknown chat site, Reddit, X, YouTube, a blog, a shop and a job board | At least 9 in 10 right on the first guess |
| Speed on real laptops | Time one form-fill (about 1,000 tokens in, under 150 out) on a 16 GB laptop, and embeddings on an 8 GB laptop | Within the targets in section 2 |
| Filing without a language model | Rules and embeddings alone, on the labelled test set | If this scores high, the model only labels |
| Form-filling accuracy | The built-in model against a cloud model, per shape, on the labelled set | Decides which jobs stay on the device |
| Tab grouping | Three real sets of 40 or more tabs | People move fewer than 1 in 10 tabs |
| The model in the worker page | Run it there, and time the first load after Chrome starts | It runs, and the first load is acceptable |
| Reopening at the sentence | Text-fragment links on 50 real pages | Most land on the right sentence |
