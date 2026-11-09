# Architecture, stage by stage

## The stages

1. **Starting:** where the plan comes from, how it's checked, and how suggestions appear.
2. **Getting evidence in:** reading AI chats, YouTube, websites and notes.
3. **Knowing what each piece means:** which topic it belongs to, and how it cleared things up.
4. **Keeping the topic list deep:** each topic owns its own checklist.
5. **Managing the data.**
6. **Showing it to the user.**
7. **Choosing models.**
8. **Making decisions, and testing them.**
9. **"Where was I" in under a second.**
10. **Retention, and juggling many things at once.**

## Stage 1: Starting

**Five ways in, all ending in the same place: a goal with a plan**
- **Say a goal.** For example, "Learn how LLMs work for interviews, in three weeks." If the purpose or the deadline is missing, it asks for that and nothing else.
- **Bring a list.** Paste or photograph a syllabus, a course outline, past papers, or a list an AI gave you.
- **Adopt a list from a chat.** When Claude lists topics for you, a small prompt appears: "Track this as your plan?" One tap. This is the smoothest route, because you were going to ask an AI anyway.
- **Just start.** Study without a plan. Later it suggests: "These look like one goal, How LLMs work. Make it a plan?"
- **Start from history.** After importing past chats, it says: "You've already studied these. Track any of them?"

**How the plan is checked**
- Your list (or the AI's) stays as the base. Nothing gets replaced.
- In the background, it compares that list with other sources:
  - shared topic maps built from other learners' plans
  - reference outlines: official syllabi, exam syllabi, well-known course pages and textbook contents, plus datasets of real syllabi such as [Open Syllabus](https://blog.opensyllabus.org/about-os) (21 million of them) where licensing allows
  - two or three different AI models, each asked separately for a list
  - past papers, if you added any
- It matches items that are the same idea under different names, counts how many sources include each one, and orders them so prerequisites come first.
- It sets a depth for each topic based on your purpose:
  - curiosity: the intuition
  - interviews: the intuition plus the formula
  - exams: whatever the syllabus and past papers stress
  - building something: how to implement it

**How suggestions appear**

They show up inside your list, each with a reason and one tap to accept:

> \+ **Masking**: in 4 of 5 outlines. Add?
>
> ↑ **Softmax** before **Attention**: attention uses it. Move?
>
> ○ **RLHF**: deeper than your goal needs. Keep as optional?
>
> ⇄ **Tokenization** and **BPE** are the same topic here. Merge?

Rules that keep it smooth:
- You can start studying straight away. The checking runs in the background.
- Only a few suggestions at the start. The rest wait until you reach that topic.
- Every topic shows why it matters ("everything after it depends on it," "in 9 of 10 past papers") and how deep to go.
- A short "people often miss these" list comes from the shared maps.
- "Why?" on any suggestion shows its sources.

## Stage 2: Getting evidence in

**What I found on the MCP idea.** An MCP server can't see your browser on its own. The tools that do what you described pair a local MCP server with a small browser extension, so an AI can work in your real, logged-in tabs. [Playwright's extension mode](https://playwright.dev/mcp/configuration/browser-extension) and [Browser MCP](https://github.com/BrowserMCP/mcp) both work this way. The only ways to read a web page without an extension are reading the screen (the monitoring you ruled out) or making people browse inside our own app. So the answer is to use both MCP and an extension:

- **A companion app on your computer** that owns the record and runs an MCP server. Claude Desktop, Claude Code and Cursor read briefs from it and report events to it.
- **A thin extension** that acts as the app's eyes. It only watches the sites you allowed, in the mode you chose, and passes what it sees to the companion app over a local connection. It stores nothing itself.
- **Connectors**, so AI apps can report to the companion app directly (more on this below).

**Watching instead of scraping.** Having an AI drive the browser to scrape pages is slow, costs a model call each time, and can get in your way. Watching the page is cheap and instant: the extension notices each new message as it appears. So instead of rewriting after every update, it adds after every update. A new message becomes a new event, and an edited or regenerated reply becomes a new version linked to the old one. History is never overwritten.

**The AI can report to the app itself.** Claude's custom connectors work [in every Claude app, including mobile](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp). You can put a standing instruction in a Claude project, such as "after each explanation, log what you explained and whether it landed." Then the AI can record the moment itself, even on a phone. In ChatGPT, [connector support differs by plan](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt), so this only works where the plan allows writing.

**YouTube transcripts**
- The official YouTube API only lets you download captions [for your own videos, or when the owner allows it](https://stackoverflow.com/questions/69054635/). It doesn't work for the videos students actually watch.
- Unofficial transcript tools work from home connections, but [YouTube blocks most cloud-server addresses](https://dev.to/heyitsgautham/youtube-transcript-api-requestblocked-and-ipblocked-on-cloud-servers-and-what-actually-fixes-it-41da), so a server can't fetch transcripts reliably.
- The better route is reading the transcript on your own device, from the page you're already watching, along with the second you're at. It runs from your own connection, where YouTube doesn't block it, instead of from a server.
- If a video has no captions, it keeps the second, the chapter title and your one-line note.
- On a phone, YouTube's share sheet has [a toggle to include the current time](https://www.sendible.com/insights/youtube-timestamp-link). Sharing to our app with that toggle on captures the moment.

**The best route for each source**

| Source | Main route | Backup |
|---|---|---|
| ChatGPT, Claude and Gemini on the web | The extension watches the conversation as it updates | Official exports, or the AI reporting through a connector |
| Claude Desktop, Claude Code, Cursor | The local MCP server | Session files on disk (Claude Code) |
| AI apps on a phone | The AI reporting through a connector, where the plan allows | Sharing the chat link to our app, or exports |
| YouTube in a browser | The extension reads the transcript and the current second | Chapters and your one-line note |
| YouTube on a phone | Share with the timestamp toggle on | Your one-line note |
| GfG, Reddit, documentation | The extension takes the main text and anchors the exact sentence. On Reddit, the exact comment | Share the link |
| PDFs | Our own viewer | Upload |
| Handwritten notes | A photo, kept as it is, with the handwriting read on your device | A typed line |

## Stage 3: Knowing what each piece means

**AI chats mostly explain themselves.** The questions, the confusion and the moment it resolves are all in the text, so they can be read automatically.

**Videos and sites need a moment card.** As you suggested, the app fills it in and you confirm it.
- **When it appears:**
  - when you tap "this clicked" or "confused here"
  - in session mode, possibly also when you leave a video or page where something seems to have happened: you rewound a part, paused for a while, or moved straight to the next topic
  - in click mode, only when you tap
- **What's already filled in:**
  - **Topic:** its best guess from your current thread and the transcript or page, with two alternatives one tap away.
  - **The moment:** the video segment trimmed to whole sentences (say, 4:02 to 4:40), or the exact paragraph, code block or Reddit comment.
  - **What cleared it:** a one-line draft taken from that segment, such as "the query is what a word looks for, the key is what each word offers, like searching a library."
  - **Language:** detected automatically, for example Hindi with English terms.
  - **Your words:** optional, one line, typed or spoken. It offers a draft you can edit.
- **One tap saves it.** You only edit when its guess is wrong.
- **It learns from you.** Each confirmation or fix improves its guesses about your topics and your wording, so cards need fewer edits over time.
- **If there's no transcript,** the card asks for just one line, with the topic already filled in.

## Stage 4: Keeping the topic list deep

The decentralized list works as a tree where each topic owns its own checklist.

- **The plan only lists top-level topics.** It doesn't need to know what's inside them.
- **Each topic keeps its own list.** Attention holds queries, keys and values; dividing by √d; softmax weights; multi-head attention; masking.
- **Lists grow when you get there.** A topic's parts are generated when you start it, at the depth your goal needs, and checked against sources. That keeps the start light and the depth real.
- **Any part can become a topic of its own** when it needs more depth. Softmax can grow its own list: exponentials, normalizing, temperature, saturation.
- **One idea, one node.** If softmax is in your machine learning course and your LLM plan, it's the same node. Understand it once and both plans show it. Plans are views over one shared graph of your topics.
- **Items show stages, not ticks.** Each one shows seen, followed, explained, used or kept, and whether it's fading.
- **Done rolls up.** A topic is done when its required parts are done, and a plan's progress comes from its topics.
- **Changes travel up.** Finishing a part updates its topic and every plan that contains it. A syllabus added later only re-checks the topics it touches.
- **Suggestions stay local.** Each topic suggests changes to its own list when you open it ("4 of 5 sources include masking here"), instead of one huge list at the start.

## Stage 5: Managing the data

- **What's stored:** the evidence log (which is only ever added to), the record calculated from it, the shared topic maps and your profile, as described in `architecture.md`.
- **Hot, warm and cold:** current threads and active topics are available instantly. This term's material is indexed. Older material is compressed and archived but still searchable.
- **Trimming:** long transcripts and chats are cut down to the anchored parts the record actually uses, with an option to keep everything.
- **Size:** text is small and photos take up most of the space, so originals are kept alongside small previews.
- **Sync, backup and deletion:** events sync encrypted, you can export everything in a readable form, and deleting something recalculates everything it touched.

## Stage 6: Showing it to the user

- **Resume card:** the first thing you see when you come back to a topic. Three lines, with buttons that open the exact spots.
- **Today:** one short list across all subjects showing what's open, what's fading before each deadline and what's parked. Three to five items at most.
- **Topic page:** parts with their stages, what clicked (with links), your notes as you wrote them, open questions and suggestions.
- **Plan:** topics with their progress, importance, depth and anything missing.
- **Map:** how topics connect, shown only when you ask for it.
- **Browser side panel:** the "you are here" line, plus one-tap buttons for clicked, confused, park, ask aside and insert brief.
- **Phone:** the resume card, quick capture (share, photo, voice) and two-minute reviews.

Design rules:
- Nothing demands your attention.
- At most one prompt at a time.
- Everything is editable.
- Every judgment has a "why?" button.

## Stage 7: Choosing models

- **On the device, for frequent work:** reading signals, linking events to topics, drafting moment cards, search indexing, voice transcription and reading handwriting. Options include Chrome's built-in Gemini Nano for the extension, Apple's on-device models, and small open models on a laptop.
- **Large models, used rarely:** drafting and checking plans (comparing two or three different models), judging explanations, checking misconceptions and writing hard briefs. These run on your own API key or a hosted option.
- **Swappable per task.** Each task has a fixed output format, so a model can be replaced whenever the tests show a better one.

## Stage 8: Making decisions, and testing them

**Every decision has the same shape.** This covers linking to a topic, detecting a click, changing a stage, marking a topic done, flagging a misconception and suggesting a plan change. Each one takes inputs, gets a score from rules plus a small probability model, and gets a confidence level that decides what happens:
- high confidence: apply it and show it
- medium: show it as a suggestion and ask in the review queue
- low: don't apply it

Your taps and corrections become labels that tune these thresholds for you.

**Testing**
- **A labelled test set:** real study sessions, used with consent, where people have marked the topics, where confusion started, where it clicked and what caused it.
- **Replay tests:** recorded sessions are run through the pipeline and scored against those labels.
- **Shadow mode:** in click mode, the system quietly makes its own guess each time you tap, and compares the two. Automatic mode for each kind of decision only switches on once its guesses have matched your taps often enough.
- **Brief tests:** blind comparisons of AI answers with and without a brief.
- **Done checks:** how often topics marked done pass a later check.
- **Release gates:** no model or prompt change ships if it lowers any score on the test set.
- **Start with yourself:** your own sessions, plus a few friends', make up the first test set.

## Stage 9: "Where was I" in under a second

- **Written when you leave, read when you return.** The note is made when you pause, close the tab, go idle or end a session, so opening it needs no AI call.
- **One small record per thread,** cached on the phone too, so it works offline.
- **Exact links** to the chat message, the video second and the paragraph, each one tap away.
- **Refreshed in the background,** but only if something new happened since, such as studying on your phone.
- **Three lines:** where you are, what you'd worked out, and what's next.

## Stage 10: Retention, and juggling many things

Your notes, textbooks and lectures stay at the centre, and the app works around them.

- **The resume can double as the review.** When you come back, it can first ask "what had you worked out about √d?" and then show your note. That one act of recall is the review, and it happens in a moment you already have. You can turn this off.
- **Reviews use your own words and your past mistakes,** so they're short and personal.
- **It works on paper.** Print a page of questions from your open and fading parts, answer them in your notebook, and photograph the answers back in.
- **It works with what you already use.** Fading parts can go to Anki or your calendar, and notes in Notion or Goodnotes stay where they are.
- **Many subjects at once:**
  - Each subject or project has its own thread. Switching saves where you were automatically, so switching costs nothing.
  - Side questions from every subject go in one parking place, each tied to its topic, and come back when you return to that topic.
  - Each goal has a deadline. Today puts the nearest deadline and the parts fading fastest first.
  - A weekly glance shows one line per subject.
- **Quiet by default:** no streaks, no badges, no daily nagging. The only reminders are for parts fading before a deadline and for done checks.
