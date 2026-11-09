# Trail (working name): final product definition

This is everything to settle before building. `full-version.md` explains the seven layers in depth, `how-it-runs.md` explains what one click does and where the data goes, `execution-plan.md` covers how each part is built and when, and the other files in `vision/` hold the research behind each decision.

## In one line

**Save where you are and what you think, from anywhere, in one click. It organizes everything, suggests your next move, brings you back where you left off, and helps you finish.**

Underneath, it keeps a private model of what you're figuring out, what's true, what matters to you, and how your past decisions turned out. Every thread and every next move draws on that model, so it gets more useful the longer you use it.

## The pain points, in plain words

| Pain | What it looks like |
|---|---|
| "I can't close my tabs." | Dozens of tabs stay open because closing them feels like losing the thought behind them |
| "I lose my place." | After a break, a usage limit or a switch to another AI, you have to rebuild where you were from memory |
| "My research is everywhere." | Pieces live in two AIs, Google, YouTube, Reddit, your notes and screenshots |
| "I forget what I found." | A week later you can't remember who said what, why you dropped an option, or how something finally clicked. Months later you research the same thing again |
| "Every AI starts from zero." | You re-explain yourself, your budget, your city and what you've ruled out every time you open a new chat or a different AI |
| "My notes don't help." | They're messy, out of date, or never written |
| "I keep researching and never finish." | Hours of asking AI and opening tabs, but no decision, nothing written, and little remembered |
| "I can't tell what's true." | AI answers sound sure, three posts repeating one viral claim look like three sources, and checking takes effort nobody spends |
| "I do the same busywork every time." | Copying job details into a spreadsheet, scrolling YouTube for the right review, writing the same question for a forum |
| "I don't know what to do next." | You aren't sure what to check, who to ask, or when you have enough |
| "Things change while I'm away." | Prices move, replies arrive and job postings close, and you find out late or never |
| "Half of it isn't in my browser." | Photos from a shop visit, screenshots on your phone, and replies from sellers and recruiters in your email |
| "I never find out if I chose well." | Nothing connects a decision to how it turned out, so the same mistakes come back |
| "I'm not deciding alone." | A partner, your family or your team weighs in across different chats, and nobody sees the whole picture |

## How it works

1. **Save.** One click saves anything: a page, a sentence, an AI answer, a video moment, a Reddit comment, a job post, a photo or a voice note. You can add your take if you like.
2. **Thread.** It files the save into the right thread, or asks "What's this for?" once. Each thread is organized around what you're doing.
3. **Next moves.** It suggests the next useful step, and each one takes one click: compare, watch the best videos, ask a community, dig deeper, or set a reminder.
4. **Bridge.** Close everything when you're done for now. When you come back to anything related, whether a page, an AI chat or the app, your thread is waiting right there with where you were.
5. **Finish.** It tells you when you have enough, then drafts a conclusion from your own takes with every reason linked to its evidence, and closes the thread.

## Underneath: seven layers

The five steps are what you do. Seven layers underneath decide what the product knows and suggests. Each one ships in a small form in version 1, so the data has the right shape from day one, and grows in versions 2 and 3.

| Layer | What it keeps | What you notice | In version 1 |
|---|---|---|---|
| **Knowledge** | Things (products, companies, people, concepts, places), claims about them, the evidence for each claim, and open questions, shared across threads | A page for each thing, and "You researched helmets in March. Bring that in?" | Names linked inside a thread, with duplicates merged |
| **You** | Your constraints, preferences, trusted sources, goals and deadlines, and what you already understand | Fewer questions, briefs that already know you, and a You page you can edit | Facts from "What matters?" and your dealbreakers, on a You page |
| **Blueprints** | The structure each task needs, built from the base shapes: the parts, what to record, what experts check, and what done means | Criteria and checks you didn't have to think of | The base shapes, with criteria generated from your purpose and weights set in three taps |
| **Reasoning** | How much each piece of evidence counts, where sources disagree, and which open question could change the outcome | "Why?" on every ranking, and three repeats of one post counting once | Source kind labels, "sources disagree," the what-if check, and "Why?" on the ranking |
| **Action** | The planner, helpers and watchers | The move that matters most, and legwork done within a budget you set | The rules-based planner, and Dig with your key |
| **Time** | What happened while you were away, and how your decisions turned out | "Since you left," check-ins, and lessons about your own habits | The bridge and "where I was" |
| **Reach** | Every way in and out: browser, phone, photos, voice, email, imports, files, agents and other people | Saves from your phone and email, shared threads, and threads any agent can read | The browser and Markdown export |

`full-version.md` walks through the bike thread with every layer switched on.

## Why a skill or plugin can't do this

A skill or plugin lives inside one AI and sees only that chat. This product works across all of them:

- **It sees every source you choose.** Saves come from any AI, any site, your phone and your email, not one chat window.
- **It keeps a record no single AI holds.** Threads, things, evidence and your profile last across AIs, devices and months, and any AI can pick them up through a brief or MCP.
- **Its reasoning is code over evidence.** Evidence weights, independence, the what-if check and the planner are computed from a structured record, the same way every time, with the numbers shown. A chat model asked to weigh the evidence can give a different answer each time, and its explanation isn't a calculation you can check.
- **It works between sessions.** The bridge, watchers, "since you left," check-ins and lessons happen while you're away. A plugin exists only while you're chatting.
- **It improves with use.** Check-ins and lessons tune your profile and blueprints, so a year of use beats day one.

## Key terms

- **Thread:** one thing you're working on, such as "Choosing a bike" or "Job search 2026."
- **Save:** one click that captures something from wherever you are.
- **Take:** your own reaction to a save. It can be a line of text, a few spoken words, or a tag like *dealbreaker*, *clicked* or *verify*.
- **Card:** one saved point, with its exact source, the date and your take.
- **Mode:** the kind of thread. It sets the layout, the checklist and the next moves.
- **Next move:** a suggested one-click action.
- **Bridge:** closing and keeping your work, then having it waiting for you when you return.
- **Brief:** a short summary of where a thread stands, written so any AI can pick it up.
- **Thing:** a product, company, person, concept or place that your saves mention. It has one page across all your threads.
- **Claim:** something a source says about a thing, such as "Bike B's brakes squeak in the rain," with the cards behind it.
- **You page:** everything the product knows about you, each fact with where it came from. You can edit or delete any of it.
- **Blueprint:** the structure a thread gets for its purpose: the parts, what to record, what experts check, and what done means.
- **Evidence weight:** how much a card counts, from its kind, independence, recency, specificity and conflicts of interest.
- **Planner:** the part that ranks next moves by how much each could change your outcome, against its cost and your deadline.
- **Helper:** a delegated job with a plan you approve, a budget and an activity log.
- **Watcher:** an opt-in check on something that changes, such as a price.
- **Review tray:** where everything you didn't do yourself waits for your OK: AI suggestions, helper results, forwarded emails and agent additions.
- **Check-in:** a short question after a decision about how it turned out.
- **Lesson:** a pattern across your own decisions or learning, offered as a suggestion.
- **Relay:** an optional server that passes sealed data between your devices and receives forwarded email. It can't read what it stores.

## Kinds of threads (the base shapes)

| Mode | For | Layout | Done means |
|---|---|---|---|
| Decide | A bike, a laptop, an apartment, a college | Options compared on what matters to you | You chose, and the reasons are saved |
| Learn | An exam, a new skill, LLMs for interviews | Topics with stages: seen, followed, explained, used | You can explain what your goal needs |
| Research | A thesis, a market, "is this true?" | Questions, claims, and sources for and against | Each question has a conclusion with sources |
| Track | Job applications, college applications, apartments viewed, grants | A list of items moving through stages | Every item has an outcome |
| Fix | A bug, a broken appliance, a setup that won't work | Symptoms, causes tried, what's ruled out | It's fixed and the cause is recorded |
| Plan | A trip, a move, an event | Pieces, bookings, budget, to-dos | Everything is booked or done |
| Follow | A news story, a court case, a product launch | A timeline of what changed | You stop following |

Track is new. It came from the job-search example and covers anything that moves through stages.

In the full version, each thread gets a blueprint built from one or more of these shapes. A visa application combines Track (stages), Plan (documents and appointments) and Research (rules and fees). Choosing a doctor for a parent combines Decide and Follow. Version 1 ships Decide, a simple Learn checklist, and Track if the job-search sessions show demand.

## One-click next moves

### In every thread

Version 1 ships the moves marked v1. The rest arrive in the release shown (2.1 to 2.4 are the four releases of version 2).

| Move | What it does | When |
|---|---|---|
| Close and keep | Moves the thread's tabs and AI chats into the thread and closes them, with a "where you were" note | v1 |
| Open where I was | Reopens the thread's tabs at the spots it kept: the comment, the scroll position, the chat message, the video second. `how-it-runs.md` explains which spots Chrome lets it keep | v1 |
| Continue in any AI | Opens ChatGPT, Claude or Gemini with a brief, so it picks up where you are. The brief shows which facts about you it includes before you send it | v1 |
| Ask people | Gathers your facts, your criteria, what you've already checked and your own photos into a draft for the one community most likely to help. It shows that community's rules and opens its post page with your draft copied, ready to paste. You rewrite it and post it yourself. Replies are added to the thread when you open the post | v1 |
| Watch list | Lists the most useful videos for your open question, each with the relevant chapter. They're ranked by relevance, how established the channel is, and how recent the video is. Clicking one opens the video at that part | v1 |
| Dig | Checks a saved point: do other sources say the same, does the AI's source really support it, is there something newer. In 2.2 it becomes a helper with a plan, a budget and an activity log | v1 |
| Do I have enough? | Shows what's settled, what's open, and the one open question that could change the outcome | v1 |
| Conclude | Drafts a conclusion from your takes, with each reason linked to its evidence. You edit it, then the thread closes | v1 |
| Remind me | Brings the thread back on a date, or when something changes, like a price drop | v1 |
| Why? | Shows how a ranking or a cell was worked out: your weights, the cards behind it and how much each counted | v1 for the ranking, 2.1 everywhere |
| What did I already find? | Before you search again, shows what you found last time, even months ago | 2.1 |
| Send a helper | Hands off legwork such as "find owner reports of Bike A in heavy rain." It shows a plan, you approve a budget, and the results come back as proposed cards with an activity log | 2.2 |
| Watch this | Turns on a watcher: a price on a saved page, replies to your post, a closing date, or new papers citing one you saved | 2.2 |
| Give me 20 minutes | Picks the three most useful steps for a short session | 2.2 |
| Pre-mortem | Before you conclude, asks "It's three months later and you regret this. Why?" Each answer can become one last check | 2.2 |
| Since you left | Shows what changed while you were away: helper results, price changes, replies, forwarded emails and phone saves | 2.2 |
| Check in | After a decision, asks at the right time how it turned out. Your answer becomes evidence for next time | 2.2 |
| Ask aside | Answers a side question in a bubble without derailing the main chat | 2.3 |
| Reading list | Lists the best few sources for your open question, labelled by kind: owner, expert, official or AI | 2.3 |
| Find the other side | Shows the strongest evidence against the option you're leaning toward | 2.3 |
| What would an expert check? | Lists things experienced people check that you haven't yet | 2.3 |
| Turn into | Makes a doc, a spreadsheet, a checklist, an email draft, a calendar event, or Markdown for Notion or Obsidian | v1 for Markdown, 2.3 for the rest |
| Ask a friend | Sends one question and the options as a link. Their vote and comment come back as a take | 2.4 |
| Share | Shares a read-only link or PDF of the thread, or invites someone to add their takes | 2.4 read-only, v3 invites |

### By kind of thread

Version 1 has Compare these for Decide threads, a simple topic checklist for Learn, and for Track (if it ships) Add from this page, Mark as applied and the follow-up reminder. The rest arrive in 2.3, except where marked.

- **Decide:**
  - Compare these
  - Owner complaints for each option
  - Price check across shops
  - Total cost, including servicing and accessories
  - Questions for the seller or the test ride
  - Decide
- **Learn:**
  - Plan from my syllabus
  - Best explanation: the video moment others found clearest
  - Quiz me on what confused me
  - Explain it back
  - Recall check when you come back
  - One page in my own words
  - What am I missing?
  - Ask a good question: a draft for a learning community that includes what you already tried
  - Review reminders, in your calendar or Anki
- **Research:**
  - Find sources
  - Check this claim
  - Who disagrees?
  - Find the original source of a number
  - Cite in APA or MLA, or send to Zotero
  - Annotated bibliography
  - Outline from my takes
  - A record of my thinking: what I read, asked and concluded
- **Track:**
  - Add from this page
  - Mark as applied, on the confirmation page
  - Follow-up reminder
  - Forward an email to the thread: an interview invite or a rejection updates the stage after your OK (2.4)
  - Research the company, in a small thread of its own
  - Interview prep from the job description and your notes
  - Why I want this role: one line, kept for interviews
  - Draft a thank-you or follow-up email
  - Send deadlines to your calendar
  - Pipeline view
- **Fix:**
  - Search this exact error
  - What I've ruled out
  - Send to Claude Code or Cursor with context
  - Draft a bug report, or a post for a repair community, with steps and photos
- **Plan:**
  - Add to itinerary
  - Map it
  - Budget
  - Checklist
  - Bookings
  - Share and vote
- **Follow:**
  - What changed since I last looked
  - Timeline
  - Who's saying what
  - Alert me

## Two examples, start to finish

### Choosing a bike

1. ChatGPT suggests three city bikes. You click Save, answer "Choosing a bike," and it becomes a Decide thread.
2. These next moves appear: **Compare these three** · **Watch reviews** · **Ask owners** · **What matters to you?**
3. **Watch reviews** lists five videos. One opens at 7:32, where the reviewer rides in the rain, and you save that moment.
4. **Ask owners** prepares a draft for r/bikecommuting. It includes your budget, your 10 km commute, the three models, what you've already learned and your shop photos. You rewrite it and post it. When you open your post a few days later, the replies are added to your thread.
5. On a Reddit comment about Bike B's brakes, you tap **Con** and say "dealbreaker." Then you tap **Dig**: 3 other owners agree, and 1 says new brake pads fixed it.
6. **Close and keep** turns 9 tabs into one thread. The next week you open a bike shop's site, and the toolbar icon shows a dot. One click shows: "Your bike thread: you were checking Bike A in the rain."
7. **Do I have enough?** shows: "Ready to decide. Still open: Bike A in the rain." **Conclude** drafts: "Bike A: comfortable, in budget, and B's brakes fail in the rain." The thread closes with the reasons saved.

**In the full version**, the same thread goes further:
- It already knows you're 175 cm and commute in heavy rain, so frame size and rain are set before you ask.
- Two of the three complaints about Bike B quote the same post, so they count once, and a review with affiliate links is labelled.
- The top move becomes a helper that finds owner reports of Bike A in the rain, because that's the only open cell that could change the winner. You approve a plan of 5 searches.
- A pre-mortem before Conclude raises the far-away service centre, which becomes one last check.
- A month later, a check-in asks how Bike A handles the rain. "Great, but the chain rusts" becomes a lesson for next time: check the chain coating on rain bikes.

### Looking for a job

1. On a company's careers page, you click Save. A row appears in your "Job search 2026" Track thread with the role, company, link, location, salary if listed, deadline and key requirements.
2. These next moves appear: **Research the company** · **Prep notes** · **Why I want this role** · **Add deadline to calendar**.
3. You apply on the site yourself. On the "application received" page, one click marks it Applied with today's date and sets a follow-up reminder for 7 days later.
4. When an interview invite arrives, one click marks it Interview, adds it to your calendar, and opens interview prep with your notes for that role.
5. The pipeline view shows Saved 14 · Applied 9 · Interviews 2, plus the follow-ups that are due.
6. The next time you open that company's site, the bridge shows your notes and where you were.

**In the full version:**
- Forward a recruiter's email to the thread's address, and it proposes "Interview on Tuesday" with a calendar draft.
- Each company is a thing, so its pages, people and your notes collect in one place, even across threads.
- The planner puts stalled applications and due follow-ups first, and "since you left" shows replies that came in.
- After a few months, it shows what worked, with counts: "Referrals: 3 interviews from 5. Cold applications: 2 from 20."

Dedicated trackers already do the tracking part well. [Teal](https://www.tealhq.com/tool/job-search-chrome-extension) saves jobs from more than 40 job boards. [Simplify](https://www.wobo.ai/blog/simplify-review) autofills applications on more than 100 application systems and has about half a million installs. What we add is the thread around each application, and one tool that covers job hunting along with everything else you research.

## Use cases

| You're… | You save | You get |
|---|---|---|
| Buying a bike, laptop or phone | Options from AI chats, Reddit, reviews and shops | A comparison with evidence, owner advice, and a decision with reasons |
| Hunting for an apartment | Listings, visit photos, commute checks | A shortlist with commute times, questions for landlords, and deadlines |
| Planning a trip with friends | Places, stays, flights | An itinerary, a budget and everyone's votes |
| Choosing a college or course | Programs, fees, student reviews, deadlines | A comparison plus an application tracker |
| Fixing something at home | The problem, photos, guides | What you've tried, and a ready post for a repair community |
| Preparing for an exam | The syllabus, AI explanations, video moments | A topic checklist, where you were, and quizzes on what confused you |
| Learning a skill | Chats across AIs, videos, docs | Pick up anywhere, continue in any AI, and know you're done when you can explain it |
| Writing an assignment | Sources and your notes | An annotated bibliography, citations, and a record of your own thinking |
| Job hunting | Job pages on company sites and job boards | A tracker with status, follow-ups, company research and interview prep |
| Choosing a tool for your team | Vendor pages, reviews, demos | A comparison with receipts to share with your manager |
| Preparing for a meeting | Their site, news, past notes | A one-page brief and questions to ask |
| Researching a market | Reports, claims, competitor pages | Claims with sources, who disagrees, and an exportable summary |
| Interrupted all day | Close and keep before each meeting | Back where you were within a minute |
| Debugging | Errors, docs, answers, AI chats | What's ruled out, a brief for your coding agent, and a ready bug report |
| Learning a new codebase | Docs, chats, examples | A checklist per area, and pick up anywhere |
| Writing a thesis | Papers, claims, notes | A reading list, claims with evidence, and citations |
| Following a news story | Updates from several sources | A timeline and what changed since you last looked |
| Helping a parent with a diagnosis | Photos of doctor's notes, trusted sources, questions | Questions for the next appointment and a timeline, with sources (not medical advice) |
| Deciding as a family or group | A shared thread or one question | Everyone's takes and votes in one place |

## Rules for every move and every layer

1. **Draft, never send.** Posts, emails, messages and applications are drafts. You review them and send them yourself, from your own account.
2. **One community at a time, in your own words.**
   - Posting the same question everywhere looks like spam.
   - Many communities have rules against AI-generated posts, and [these rules are more common in larger communities](https://arxiv.org/abs/2410.11698), which are the ones people most want to ask.
   - So a draft gathers your facts, and you write the post.
3. **Only what you click.**
   - It reads a page's content only when you save it or close and keep it.
   - To show the bridge, it checks the address of the page you open against your threads, on your device. That includes the search words in the address of a search page.
   - Remembering your place on every open tab, and showing the bridge bar on the page itself, need access to every site. Both are opt-in. By default, the bridge shows on the toolbar icon and in the side panel.
   - From version 2, you can let it read the first message of a new AI chat, site by site, only to find a matching thread. That text stays on your device.
   - It stays off sites that forbid extensions. LinkedIn [doesn't allow extensions that scrape, change or automate its pages](https://www.linkedin.com/help/linkedin/answer/a1340567/), so jobs are saved from company sites and other job boards, or by pasting the link.
   - Banking, email and health portals are off by default.
4. **Official routes only.**
   - Community posts go through the site's own post page. Reddit requires [approval before any API access](https://reddit.zendesk.com/hc/fr/articles/16471395473812-Bots-et-outils-de-mod%C3%A9ration).
   - The watch list uses YouTube's official search. It allows [100 searches a day per app by default](https://developers.google.com/youtube/data/determine_quota_cost), so the watch list needs a quota increase, the user's own key, or YouTube pages the user opens.
5. **Your photos, and links to everyone else's.** Attach your own photos, and link to listings instead of copying other people's images.
6. **No paid placement.** No suggestion includes affiliate links or sponsored results.
7. **Labels on everything.** AI content is marked as AI. Health, legal and money topics show sources and say they aren't advice.
8. **Nothing leaves the device unless you turn it on.** Organizing runs on your device. Dig, helpers, watchers, the watch list and the relay are opt-in, and each one says what it sends and to whom.
9. **Helpers stay on a leash.**
   - They show a plan, you approve a budget, and they stop at the limit and keep an activity log.
   - They read public pages logged out and follow each site's robots.txt. Pages on sites that don't allow automated reading go on a list for you to open yourself.
   - They never post, apply, buy, log in or fill in forms.
10. **Background work touches only what you saved.** It never looks at your browsing, and it runs only while your laptop is idle.
11. **The You page is complete.** Every fact the product holds about you is on it, with its source. Learned facts stay suggestions until you confirm them, and a brief shows which facts it includes before you send it.
12. **Anything you didn't do waits for your OK.** AI suggestions, helper results, forwarded emails and agent additions go to the review tray, labelled with where they came from.
13. **Calm by default.** At most three moves at a time, a weekly limit on nudges that you set, and nothing in red.
14. **The relay can't read what it stores.** It's off by default, open source, and you can run your own. It seals each forwarded email the moment it arrives, and deletes everything once your devices pick it up.

## Version 1

**In:**
- A Chrome extension that saves pages with a take, AI answers and YouTube moments
- Decide threads and a simple Learn checklist, plus Track threads if the job-search sessions show demand (job tracking is crowded)
- The bridge: tab rescue (close and keep), open where I was, and the "you have a thread on this" signal. It shows on the toolbar icon and in the side panel, or as a bar on the page if you allow every site, and it also matches the search words in a search page's address
- Eight next moves: Compare · Watch list · Ask people · Dig · Do I have enough? · Conclude · Continue in any AI · Remind me
- Organizing on the device with Chrome's built-in AI, and Dig and the watch list with an optional key
- Threads export as Markdown
- Small versions of each layer:
  - **Knowledge:** names linked inside a thread, duplicates merged, one-tap split
  - **You:** a You page with facts from "What matters?" and your dealbreakers
  - **Blueprints:** criteria generated from your purpose, and weights set in three taps
  - **Reasoning:** source kind labels, "sources disagree," the what-if check, and "Why?" on the ranking
  - **Action:** the rules-based planner, and Dig with your key
  - **Time:** the bridge and "where I was"
  - **Reach:** the browser and Markdown export

**Version 2, in four releases.** This is the default order. The beta decides the real one.
- **2.1 Knows what you found:** knowledge shared across threads, a page for each thing, "you researched this before," What did I already find?, profile suggestions you confirm, and independence, recency and affiliate labels on evidence
- **2.2 Works while you're away:** a planner that ranks by expected value, helpers with plans, budgets and logs, watchers, background work, "since you left," living decisions, outcome check-ins, the pre-mortem, and "good enough or thorough"
- **2.3 Every shape:** Research, Fix, Plan and Follow threads, combined blueprints for mixed tasks, what experts check, Learn stages with recall checks and fading, and the other next moves
- **2.4 Everywhere:** the optional relay, phone share, photos and voice takes, email forwarding, imports, a thread folder with a read-only MCP server, Ask a friend, and read-only share links

**Version 3:**
- Lessons from your outcomes (they need months of check-ins, which start in 2.2)
- Shared threads with roles, then team spaces
- Agents that add to threads through MCP, landing in the review tray
- A desktop shortcut that saves from any app, such as the ChatGPT or Claude desktop apps or a PDF reader, through a small companion app
- A public library of blueprint templates, structure only, contributed by hand
- Crowd signals as weak evidence, only if a privacy design passes public review

## Before we build: checklist

**Decide**
- [ ] Name and one-line promise
- [ ] First users: people in the middle of a purchase decision or a job search, plus learners
- [ ] Freeze the version 1 scope above, including the small versions of each layer

**Check with real people (two weeks)**
- [ ] Landing pages for three promises
- [ ] Five hand-run sessions each for Decide, Track and Learn
- [ ] Run the same tasks through the closest tools: Edge Journeys, Gemini in Chrome, Glasp, Teal, Simplify, OneTab, Skipper

**Design**
- [ ] Clickable mockups: tab rescue, home, a Decide thread, a Track thread, the next-moves panel, the bridge bar, the finish card, the You page, and "Why?"
- [ ] Exact behavior of "What's this for?", the three-tap weights, and each of the eight next moves

**Trust and rules**
- [ ] Site permissions and the default off-list
- [ ] Platform check: Reddit's post page and community rules, YouTube's quota, job sites' terms
- [ ] A privacy policy in plain words, including what goes to an AI provider when Dig is on

**Tech**
- [ ] Thread format spec (Markdown plus metadata, with things, claims and the facts about you that a thread uses)
- [ ] Model plan, and the cost of each Dig, watch list and conclusion
- [ ] Data model with things, claims, questions, facts about you, and an author on every event, so later layers need no migration (`execution-plan.md`, section 3)
- [ ] Test set: 20 real threads, labelled with where each save belongs and which names are the same thing
- [ ] The seven technical tests in `how-it-runs.md`, section 7, with throwaway code

**Open source and launch**
- [ ] License, repo, contribution guide, and a README with a demo
- [ ] Demo videos: "63 tabs → 4" and "a bike decided in a week"
- [ ] Waitlist and 20 testers

**Before version 2**
- [ ] Rules for helpers and watchers: robots.txt, per-site permissions, logged-out reading, budgets
- [ ] A threat model for the relay, and an outside security review before anyone turns it on
- [ ] A legal check on forwarded emails, which contain other people's details
- [ ] Confirm the phone routes: Android's share sheet for web apps, and what iPhone allows today
- [ ] The release order for 2.1 to 2.4, from beta findings

## How we'll know version 1 works

- Most testers close most of their tabs on day one.
- People get back into a thread within a minute, and 4 in 10 reopen a thread within a week.
- Most saves land in the right thread without needing a fix.
- Each active thread uses at least one next move a week.
- At least 3 of 5 test decisions end with a conclusion the person is happy with.
- Half of testers still use it after two weeks.

## How we'll know the full version works

- People bring in what they found before in most new threads where it applies.
- Most cards that helpers propose are accepted, and no helper run goes over its budget.
- Most people answer their first outcome check-in.
- People still use it after three months, which is when lessons start to appear.

## Still open

- The name
- Which promise leads
- Whether Track ships in version 1, given how crowded job tracking is
- Pricing for the moves that cost money to run (Dig, helpers and the watch list)
- Who pays for the hosted relay, and whether it's free up to a limit
- Whether crowd signals happen at all
- The license
