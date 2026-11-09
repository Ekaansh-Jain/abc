# Architecture: how it would actually work

## Why a wrapper fails, and what replaces it

A wrapper sends your text to an AI model and shows you what comes back. It has no memory of its own, so every answer is a fresh guess. It can't fit months of history into one request, can't show where a claim came from, and can't tell what you actually understood.

Our system keeps its own structured record of you, and AI models are parts inside it. The design is sophisticated where it matters (the record and the judgments about understanding) and simple everywhere else. Five rules hold it together:

1. **Keep the raw evidence and work everything else out from it.** Every capture is stored once and never edited. Everything else (topics, stages, "you are here") is calculated from that log. That means it can be recalculated when models improve, explained when you ask "why does it think that?", and cleanly removed when you delete something.
2. **Every claim points to evidence.** "You understood queries and keys through the search analogy" links to the second of the video where that happened. If there's no evidence, there's no claim.
3. **Models propose, the record decides.** AI models suggest what an event means, with a confidence level. Rules and probability models decide what changes. Anything uncertain waits for a one-tap confirmation from you.
4. **What a subject contains is separate from what you know.** Topic maps describe a subject and are shared. Your understanding is a personal layer on top of them.
5. **Where your head is now is separate from what you know long term.** One is today's working state. The other is understanding built over months.

## The whole flow

```
SOURCES    AI chats · YouTube · web pages · your notes · coding agents
              │  you choose: one click · a session you start · automatic per site
              ▼
CAPTURE    adapters turn each action into an event, anchored to the exact spot
              ▼
EVIDENCE   a log on your device that is only ever added to
              ▼
PROCESS    read signals → link to a topic → update the record → consolidate
           (models propose, rules and probabilities decide,
            anything uncertain waits for you)
              ▼
RECORD     working state    where your head is: threads, open questions,
                            positions, "where I was"
           understanding    one keeper per topic: stages, what clicked,
                            fading, done
           topic maps       what a subject contains (shared, no personal data)
           profile          how explanations work for you
              ▼
USE        you are here · briefs for any AI · checks only when needed ·
           fading · gaps in the plan
              │
              └─► your taps, corrections and check results go back into the log
```

## 1. Capture

**Modes (your choice, per site)**
- **Click:** nothing is captured until you tap "this clicked," "I'm confused here," "park this" or "add to topic."
- **Session:** you start "studying attention," and only the sites you allowed are read until you stop.
- **Automatic:** turned on per site, with a visible indicator whenever it's reading.

**Adapters (one per kind of source)**
- **AI chats on the web** (ChatGPT, Claude, Gemini): a browser extension that only runs on those sites reads the conversation and where each message sits in it. Official exports are imported once to fill in your history.
- **AI apps with connectors:** the AI itself can report things like "explained X," "the student said they got it" or "confused about Y," and ask for a brief (see section 6).
- **Coding agents:** session logs and git history on your machine.
- **YouTube:** the video, the second you're at, and the transcript around it when one exists. On a phone, the share button sends the link with the timestamp.
- **Web pages** (GfG, Reddit, docs): the exact sentence plus a little of the text before and after it. This is how the [W3C Web Annotation standard](https://www.w3.org/TR/annotation-model/) anchors highlights, so the spot can be found again even if the page changes.
- **Your notes:** photos kept as they are, with handwriting read on your device so the notes can be linked to topics. Imports from Notion, Obsidian or Goodnotes, and short voice notes.
- **Plans and syllabi:** a syllabus, course outline or past papers you add.

**Every capture becomes one event**, containing:
- what happened (asked, explained, watched, read, marked a click, marked confusion, parked, paused, solved, answered a check)
- who did it (you, an AI, an author)
- exactly where (chat and message, video and second, page and sentence, note and region)
- when, and which thread of study it belongs to
- the quoted content
- which capture mode and permission it came through

**The most important capture happens when you leave.** When you pause, close the tab or go idle, it writes a "where I was" note from your last few minutes. The note holds the open question, the last step you got and the next step. Research on interruptions found that a quick [ready-to-resume plan](https://sciencedaily.com/releases/2018/01/180116151600.htm), noting where you left off and what's left, reduces how much the unfinished task keeps pulling at your attention. The system writes the note for you, and only asks you for one line when it isn't sure.

## 2. Processing

These steps run as events arrive:

1. **Normalize.** Chats are split into turns, videos into short transcript windows, and pages into paragraphs.
2. **Read signals.** A small model on your device, plus simple rules, marks each event:
   - a question, and whether it's a side question (a shift away from the current thread)
   - confusion: "I don't get it," asking the same thing again in new words, or jumping to another source right after an answer
   - resolution: "oh, got it," "so basically…," a next question that builds on the last answer, or moving on to the next topic
   - your own paraphrase
   - a statement of yours that a source contradicts (a possible misconception)
   - a plan (an AI listing topics)
3. **Link.** The event is attached to the right topic and part on the map. The strongest hint is what you're working on right now, and after that, meaning and the map's structure. For example, "attention" in an LLM thread links to transformers rather than psychology. If nothing fits, it proposes a new part.
4. **Update the record.**
   - **Working state:** open, close or park questions, move "you are here," and save your position in each source.
   - **Understanding:** move a part to a new stage when the evidence supports it. Save the explanation that worked and your own words, save misconceptions along with the source that corrected them, and update how fast the part is fading.
   - **Profile:** note which kinds of explanation work for you (analogy, diagram, code, maths, video or text, which language).
5. **Consolidate.** At each pause, and overnight:
   - merge duplicates
   - shorten long evidence while keeping its anchors
   - find branches you left behind
   - re-check what's done
   - refresh the "where I was" note
   - plan the few checks that are actually needed

**How a click is detected.** A click is a part going from confused to resolved. The explanation that clicked is the last one you took in before that happened: an AI message, a video segment or a paragraph. Confidence goes up if your next words echo that explanation, and again if a later check passes. In click mode, your tap is simply taken as true. In session and automatic modes, it infers the click, shows you what it inferred, and you can fix it with one tap.

**The review queue.** Only low-confidence proposals reach you, in batches, as yes, no or move somewhere else. That should be a few a day at most.

## 3. Storage

Everything lives on your device: one database file, a folder for images, and a plain-text export.

| Store | What it holds | Shared? |
|---|---|---|
| Evidence log | Every event with its anchor. Only ever added to | No |
| Topic maps | What a subject contains: parts, prerequisites, depth levels (intuition, formula, derivation, implementation), common confusions, and how many sources agree on each part | Yes, with no personal data |
| Your understanding | For each part you've touched: stage, confidence, how fast it's fading, the explanation that worked, your own words, misconceptions, open questions, and the evidence behind each | No |
| Working state | Goals, threads, the questions you're in the middle of, parked questions, your position in each source, "where I was" notes, and each AI's lesson plan and teaching style | No |
| Profile | How explanations work for you, with evidence | No |
| Change history | Every change to the record, with the events and the model version that caused it | No |

- **One file:** a local database (SQLite or similar) holds all of it, including a search index for meaning. It works offline and can be backed up by copying the file.
- **Open format:** each topic exports as a readable Markdown page plus structured data with all its anchors, usable without the app.
- **Sync:** your devices exchange encrypted events and rebuild the same record. The server only ever sees scrambled data.
- **Forgetting:** deleting something removes its events and recalculates everything that depended on them, so nothing worked out from it survives.

## 4. Judging understanding

This is the hardest part, so it can't rest on one AI model's opinion.

**Each stage needs its own kind of evidence**

| Stage | Evidence |
|---|---|
| Seen | You watched or read it |
| Followed | No confusion after an explanation, or you said you got it |
| Explained | Your own words match the sources, checked by a stronger model against the anchored sources |
| Used | You solved a problem or applied it correctly |
| Kept | You recalled it correctly after a delay |

- **Many weak signals, one estimate.** For each part, it combines your behaviour, your words, your answers, timing and whether sources agree. This follows the knowledge-tracing models that tutoring systems use to estimate mastery.
- **Fading, part by part.** A memory model like [FSRS](https://docs.ankiweb.net/faqs/what-spaced-repetition-algorithm), which Anki uses, tracks how strong each memory is and how fast it fades. Parts that stopped at "seen" or "followed" start weak and fade fast. That's how it can answer "was it shallow, and is that why it disappeared?"
- **Done** means all of these hold:
  - the parts your goal needs are covered
  - each is at least at "explained" (or "used" for skills)
  - your notes and your sources agree
  - one delayed check has passed

  After that, the topic goes quiet.
- **Checks** happen only when a topic is about to be marked done, or when a part is likely to fade before your goal date. They're aimed at you. You might rebuild your own analogy, apply the idea to a new case, or face the exact mistake you made before.
- **Calibration.** It tracks how often "done" topics fail a later check and how often you correct it, and adjusts its thresholds for you.

## 5. Retrieval

Most retrieval reads the record directly instead of searching text. Plain search finds similar text, but it doesn't know where you are or what's weak.

- **"You are here"** is read straight from the working state: goal, thread, open questions, your last position in each source, and the "where I was" note. It's instant and works offline.
- **"Where did my understanding of tokenization go?"** is read from your understanding history: the stage it reached and when, the last evidence, and how far it has faded, with links.
- **"Is this AI's topic list right?"** compares the plan with the topic maps and reports missing or extra parts, with how many sources agree.
- **Searching your own learning** combines keywords, meaning and neighbouring topics on the map. Results are ranked by your current goal and your weak spots rather than by similarity alone.
- **Catching up after agents** shows what changed since you left, who changed it, and why.

**Briefs for any AI** are built at the moment you need them, from structured fields, within a strict length limit. When space is tight, the exact confusion goes in first, then what's solid, then the explanation style, then misconceptions. A small model only smooths the wording. A brief for the attention example would look like this:

> **Attention** (How LLMs work, topic 3 of 7)
>
> **Goal:** intuition, the formula and one example worked by hand. No matrix calculus.
>
> **Solid, don't re-teach:** embeddings as points where similar words sit close together. Queries and keys, through a search analogy.
>
> **Shaky:** softmax. They once thought it only picks the biggest score.
>
> **Where we are:** why the scores are divided by √d. They've understood that large dot products push softmax to put nearly all the weight on one word.
>
> **Didn't land:** the matrix-only explanation.
>
> **Explain like this:** intuition first, then one small numeric example, building on the search analogy.
>
> **Lesson so far (from Claude):** step 2 of 4 in this topic, one idea per message, check before moving on.
>
> **Their question:** "Why √d and not d?"

After the AI replies, the reply is read back in as evidence: a new explanation, and whether it landed.

## 6. Getting briefs into tools, and events back out

- **Web AI apps:** the extension puts the brief into the message box with one tap. In session or automatic mode, it also reads the replies.
- **Connectors:** Claude and ChatGPT both support MCP connectors (a standard way for AI apps to talk to outside tools). However, [Claude reaches them from Anthropic's cloud](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp), and [ChatGPT needs them reachable over HTTPS](https://developers.openai.com/apps-sdk/deploy/connect-chatgpt/), with [support that differs by plan](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt). A server on your laptop can't be reached directly by the web apps. So:
  - desktop and coding tools (Claude Desktop, Claude Code, Cursor) use a server running on your machine
  - web apps use the extension, or an optional relay that serves only the briefs you approve and holds nothing else
- **Side questions:** "ask aside" opens a side chat, in the same AI or another one, starting from the brief. The answer comes back as one line in your record, and the main lesson continues from its saved plan and style.
- **Phone:** the share button for videos and pages, the camera for notes, a resume card, and offline use.

## 7. Models

- **Small and local, for frequent work:** reading signals, linking, search indexing, transcription and reading handwriting. Options include [Chrome's built-in Gemini Nano](https://developer.chrome.com/docs/ai/prompt-api), which extensions can call on supported hardware, Apple's on-device models, or a local model on a laptop.
- **Large and occasional, for hard work:** judging your explanations, checking misconceptions, comparing plans and writing briefs. These use your own API key or a hosted option.
- **Fixed-format outputs only.** Each output carries a confidence level and is checked before anything in the record changes.
- **Swappable.** The record belongs to you, so models can be replaced without losing anything.
- **A test set.** Real study sessions, used with consent and labelled by people: where confusion started, where it clicked, and what caused it. Every model change is measured against this set before it ships.

## 8. Safety and privacy

- **Hidden instructions in captured content.** A page or chat you save can contain text meant to steer an AI, and [OpenAI warns about exactly this with connectors](https://developers.openai.com/api/docs/guides/custom-mcp-server). Captured content is only ever treated as data. Models fill fixed fields from it, and briefs are built from those fields, never from raw page text.
- **Permissions** per site and per mode, with a visible indicator while it reads.
- **Encryption** on the device, with keys stored in the system keychain.
- **Sharing scopes:** personal, shared with people you choose, and public topic maps that never contain personal data.
- **Adults first,** because of children's data laws.

## 9. What makes it hard to copy

- Your record and its evidence, which grow every week and belong to you.
- Topic maps that improve as more people learn (which parts matter, where people get stuck), without anyone's personal data leaving their device.
- Calibration data showing which signals actually predict understanding.
- Adapters and connectors kept working across many tools.
- Neutrality: it works with every AI and stays on your device.

## 10. Choices to make

- **One agent per topic, or records plus jobs?** My lean: each topic is a record, and the "agents" are jobs (consolidation, checks, briefs) that read and write those records. That's cheaper and more consistent than many agents running at once.
- **Sync by replaying events, or by merging records?** My lean: replay the encrypted event log, since the record is calculated from it anyway.
- **How much to infer in automatic mode?** My lean: infer, but never act on a low-confidence guess without showing you.
- **A relay for web connectors?** My lean: optional and off by default, with the extension as the default route.
- **Topic maps generated or edited by people?** My lean: generated from many sources with agreement counts, then corrected by users.

## 11. What to prove first

1. **Click detection and linking.** On real sessions in session mode, does it find where you got stuck and what fixed it, matching your own account most of the time?
2. **Resuming.** Does the "where I was" note get people back into a topic faster than their own notes do?
3. **Briefs.** In a blind comparison, does an AI with the brief give better help than one without?
4. **Judgment.** Do topics marked done pass later checks?

The build order follows from that. First the record, click capture, resuming and briefs, with no inference. Then inference in session mode. Automatic mode comes last.
