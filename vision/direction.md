# Direction: is there a better product?

Based on public pages, store listings, GitHub and papers, checked in November 2026. GitHub stars measure developer interest rather than everyday use.

## Short answer

The current idea holds up better than the alternatives, and nobody has built it, open source or otherwise. What should change is what sits at its center.

Every AI tool today is built to help you find more: more answers, more summaries, longer reports. None is built to help you finish, meaning get from a pile of tabs and AI chats to a conclusion that's yours. Current AI can now do that, and the product should be built around it.

- **The way in** stays the tab rescue: close your tabs and AI chats without losing anything.
- **What it does every day** stays the same: threads that keep your reasoning and let you resume.
- **What's new** is finishing. The "done" standard we designed for learning becomes the center of every kind of thread.

## Why no open-source version exists

- **Open-source attention goes to developer tools and to agents that act for you.** Personal research tools for everyday people get far less (see the table below).
- **Consumer apps need polish and years of upkeep,** which volunteer projects rarely sustain.
  - Omnivore, an open-source read-later app, [shut down within weeks](https://techcrunch.com/?p=2907694) after its team was hired by ElevenLabs.
  - The Carnegie Mellon prototypes that proved these ideas (Unakite, Crystalline, Fuse) stayed as research code.
- **Free, private AI inside the browser is new.** Chrome's built-in model only became [stable for extensions in Chrome 138](https://dev.to/kenyalba/chromes-prompt-api-is-stable-on-device-ai-for-your-website-no-api-key-and-no-per-token-bill-555e), in 2025. Before that, an open-source tool had to ask for an API key or send your tabs to a server, and privacy-minded users won't accept either.
- **It falls between communities.** Tab managers, note apps, AI memory tools and research agents each build their own piece.
- **People don't go looking for research tools.** Researchers call this the ["almost there" effect](https://arxiv.org/abs/2411.07206): people feel they're nearly done, so they never set up a tool.

## What gets attention in open source now

| Project | What it does | GitHub stars |
|---|---|---|
| [OpenClaw](https://docker.similarlabs.com/blog/openclaw-ai-agent-trend-2026) | Personal AI agent inside your messaging apps | 250,000+ by March 2026 |
| [Firecrawl](https://www.firecrawl.dev/blog/best-browser-agents) | Turns websites into data for AI | 190,000+ |
| [Browser Use](https://www.firecrawl.dev/blog/best-browser-agents) | Lets AI agents use a browser | 118,000+ |
| [claude-mem](https://www.augmentcode.com/learn/claude-mem-65k-stars) | Memory for Claude Code | 65,800 |
| [Open Notebook](https://localnotebook.dev/) | Open-source NotebookLM | 31,000+ |
| [GPT Researcher](https://rywalker.com/research/gpt-researcher) | AI writes research reports | 27,600 |
| [LLM Council](https://gist.github.com/conradcaffier03/3c0d0d9c41ed6e0c648a97d6465a9047) (Karpathy) | Several AIs answer and review each other | 22,900 |
| [Karakeep](https://github.com/karakeep-app/karakeep/discussions/2106) | Save everything and let AI tag it | 20,000+ |

**What to take from OpenClaw:**
- **What made it work:** it [runs on your own hardware and works inside the messaging apps you already use](https://github.com/qhkm/awesome-claw/blob/main/OPENCLAW_INTELLIGENCE_REPORT.md). For us, that means living inside the browser and AI chats people already use, keeping the data on their device, and making the first minute pay off.
- **The risk:** according to one security write-up, [more than 42,000 OpenClaw instances were found exposed online](https://maordayanofficial.medium.com/the-sovereign-ai-security-crisis-42-000-exposed-openclaw-instances-and-the-collapse-of-1e3f2687b951). Nothing we build should be reachable from the internet.

## Other directions I checked

| Direction | What I found | Verdict |
|---|---|---|
| An open-source AI research agent | Crowded: GPT Researcher, STORM, Open Notebook, and deep research inside every major AI. Their citations are also shaky. In a 2026 test, top models' citations were factually accurate [only 39 to 77% of the time](https://arxiv.org/html/2605.06635), and accuracy fell about 42% as the agents searched more | Don't build another one |
| A checker for AI answers | At least six extensions already do this ([Sereno](https://chromewebstore.google.com/detail/sereno/pfbjaidamobfcfncmfjlodjpnbbhhfpf), [Verity](https://chromewebstore.google.com/detail/verity/nfhbehkpoheciabpnnfhdjkiimnndgkc), [Aretify](https://www.aretify.com/), [Theia](https://gettheia.org/), [Factaa](https://chromewebstore.google.com/detail/factaa/hdbimkefkfbebffchgpgfkpkglmmkpab), [AI FactScan](https://aifactscan.com/)), and Gemini has its own [double-check](https://workspaceupdates.googleblog.com/2024/09/related-content-links-in-gemini-responses.html?hl=in_ID) | A feature inside threads |
| An AI tab organizer | Dozens exist, including [open-source ones that use Chrome's built-in AI](https://github.com/MoussaabBadla/TabWhisperer) | The way in, not the product |
| Memory for AI | Crowded: claude-mem, mem0, Supermemory, Basic Memory, plus each AI's own memory | Not the product |
| A personal agent like OpenClaw | OpenClaw dominates | No |
| Proof of your own thinking, for students | A real pain. [75% of AI-using students report significant stress about being wrongly flagged](https://www.timeshighereducation.com/news/fear-being-flagged-ai-detectors-drives-stress-among-students), and courses are moving to process evidence such as [drafts and annotated bibliographies](https://sites.lsa.umich.edu/learningteachingconsulting/2026/01/29/if-chatgpt-writes-it-did-the-student-learn-it-4-practical-ways-to-keep-essay-assessment-authentic/). [Grammarly Authorship](https://www.grammarly.com/authorship) covers the writing, but nothing covers the research behind it | A strong use of threads, worth testing |
| The current idea, centered on finishing | The pieces exist, but nobody has combined them | Build this |

## The idea that should exist: AI that helps you finish

A 2026 paper named the problem you described at the start: [**doom researching**](https://arxiv.org/html/2607.02723v1).
- **What it is:** asking AI over and over for explanations, comparisons and reassurance without turning any of it into understanding, decisions or finished work.
- **Where the author saw it:** in their own thesis work. Hours of AI conversations led to little written and less remembered.
- **Why it happens:** the paper argues that smooth, effortless AI answers make people feel they know more, which leads them to ask even more.

Current AI can now do something no product offers. It can read everything you gathered across tabs, notes and chats, compare it with what your question needs, and help you close the question. In each thread:

1. **"Do I have enough?"** It checks your evidence against what the question needs:
   - every option against every criterion
   - every topic against the depth your goal needs
   - every sub-question against sources

   It shows what's settled, what's still open, and the one open question that could still change the outcome. This matters because only [about half of everyday research tasks end with any closure](https://arxiv.org/abs/2411.07206), and people usually stop when they feel they've seen enough rather than when they actually have.
2. **"You're circling."** When you ask a second AI the same thing, or reopen pages you've already read, it shows what you already found: "You asked this on Tuesday. This is what clicked."
3. **Conclude with receipts.** One tap drafts a conclusion from your own takes, with each reason linked to its evidence. You edit the draft, and the thread closes with the reasons saved. You can share it with family, a teammate or a teacher. For students, this is the process evidence their courses now ask for.
4. **Point and dig.** On anything you save, you can ask it to dig further:
   - Do other owners say the same?
   - Does the AI's source really support the claim?
   - Is there a newer source that disagrees?

   The results come back as evidence for you to accept or reject. The AI works on your question instead of starting its own.

> **Choosing a bike** · ready to decide
>
> **Settled:** price (all three) · comfort (A and B) · Bike B's brakes are a dealbreaker (your take, and 3 owners agree)
>
> **Open:** how Bike A handles rain. This is the only thing that could change your choice. [Dig into it] [Decide anyway]
>
> **Draft conclusion:** "Bike A: comfortable and in budget, and B's brakes fail in the rain." [Edit] [Close the thread]

For learning, the same check might say: "You can explain 3 of the 5 parts of attention. √d is still at 'following'. Explain it in one line to finish."

**Evidence for this approach, and its trade-off.**
- **What supports it:** in a Microsoft Research study, an AI that [built on people's own reasoning fit better into their thinking and led to slightly better decisions](https://arxiv.org/abs/2504.06771) than an AI that simply recommended answers.
- **The trade-off:** the recommending AI produced more new ideas with less effort. So "dig" should still bring in things you didn't think of.
- **Who's close:** a few early tools aim at decision closure, such as [Pro Decider](https://ciderhousetools.com/). None of them builds on what you've gathered across your browser and AI chats.

## How it gets traction

1. **People download it for the tab rescue** ("63 tabs → 4, nothing lost").
   - A correction to the earlier plan: Arc's shutdown on 22 December is a smaller opening than it looked. [Zen Browser can now import Arc Spaces](https://browsers.to/articles/arc-to-zen), and so can Dia.
   - Arc users will only switch to us for what those browsers don't do.
2. **Free and private by default.** Chrome's built-in AI does the organizing, so there's no API key, no cost, and nothing leaves the device. Bigger models for "dig" are optional.
3. **A hook for developers.** Publish a thread as a plain Markdown file, plus an MCP server, so Claude Code, Cursor and other agents can read and write threads. Simple formats spread: by mid-2026, [AGENTS.md was in more than 60,000 open-source repositories and supported by over 25 coding tools](https://ai.miraheze.org/wiki/AGENTS.md).
4. **A story people repeat.** "Doom researching" is new and relatable, and this is a tool built to end it. A small public study of your own would give communities and press something to share, such as how often people ask several AIs the same question.

## Check it in two weeks

1. **Landing pages.** Test three promises with the same budget:
   - "Close your tabs and AI chats. Keep your train of thought."
   - "Stop doom researching. Finish what you started."
   - "Never re-explain yourself to an AI."
2. **Five "finish" sessions.** Take someone's open decision or study topic and build the thread with them by hand. Show them the "do I have enough?" view, and see whether they decide or understand faster than they otherwise would.
3. **A GitHub repo** with the thread format and a short demo. Watch whether developers star it, open issues or build on it.

**Decision rule:** build around finishing if both of these hold:
- the finishing promise does at least as well as the tab promise
- at least 3 of the 5 people reach a conclusion they're happy with during the session
