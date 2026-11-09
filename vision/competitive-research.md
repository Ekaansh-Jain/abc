# Competitor and open-source research

Based on public documentation, store listings and papers, checked in November 2026. Features change quickly, so the top five should be tested hands-on before decisions are final.

## The verdict

**The gap is real, but narrower than the proposal makes it sound.** Most of the individual pieces already exist, and several are very good. Here's what's still open:

1. **A lasting record of an investigation that you lead.** Your own judgment is kept next to the evidence, and organized by what you're doing: options compared against what matters to you, topics with stages, or questions with claims.
2. **Built from every place you work,** including AI chats in any company's app.
3. **Neutral across AI companies, and kept on your device.**
4. **A resume that brings back your reasoning,** not just your tabs or topics.

**The closest match is academic, not commercial.** Carnegie Mellon's prototypes Unakite, Mesh, Crystalline, Fuse and Selenite proved parts of this in studies. None of them is a mainstream product.

**The biggest threat is AI browsers.** Gemini in Chrome, Edge Copilot, ChatGPT's Chrome extension, Claude in Chrome, Comet and Dia sit exactly where capture happens. They already do searching your history, resuming and comparing tabs.

**The biggest do-it-yourself alternative** is Obsidian Web Clipper with its AI "Interpreter," or Notion's clipper with AI-filled properties.

## Gap check, claim by claim

| Our claim | Who already does it | Verdict | What it means for us |
|---|---|---|---|
| One-click capture from any page, with a note | [Glasp](https://glasp.co/web-highlighter), [Obsidian Web Clipper](https://www.dsebastien.net/obsidian-web-clipper/), [Readwise](https://readwise.io/pricing), [Memex](https://github.com/WorldBrain/Memex), [Karakeep](https://docs.hoarder.app/), [Fabric](https://www.stork.ai/en/fabric) | **Not a gap** | Basic capture is expected of any tool like this. Reuse open-source work instead of selling it as new |
| Capture from AI chats across companies | Mem0's [OpenMemory extension](https://mem0.ai/blog/introducing-the-openmemory-chrome-extension) (saves facts; [archived in March 2026](https://www.memoryplugin.com/alternatives/openmemory)), [Personal AI Memory](https://www.scriptbyai.com/personal-ai-memory/), [Supermemory](https://chromewebstore.google.com/detail/supermemory/afpgkkipfdpeaflnpoaffkcankadgjfc?hl=en-US), Foldif | **Partly covered** | They keep facts or whole chats. Our angle is AI answers as labelled evidence inside an investigation |
| Capture on phone and desktop apps | Fabric (including automatic screenshot sync), Karakeep apps, [Tana voice memos](https://tana.inc/docs/mobile-voice-memos), Glasp for Safari | **Covered in pieces** | Use the phone's share sheet. This isn't what sets us apart |
| Organizing into a structure that fits your purpose (such as options compared on criteria) | Research prototypes ([Unakite](https://dl.acm.org/doi/abs/10.1145/3332165.3347908), [Mesh](https://dl.acm.org/doi/10.1145/3379337.3415865), [Crystalline](https://arxiv.org/abs/2202.02175v1), [Selenite](https://arxiv.org/abs/2310.02161)). Gemini [comparing up to 10 open tabs](https://support.google.com/chrome/answer/16283624?co=GENIE.Platform%3DDesktop&hl=en-FM), but only for that moment. [ChatGPT shopping research](https://openai.com/index/chatgpt-shopping-research/), where the AI leads. [DualyzeAI](https://dualyzeai.com/). Notion AI and Tana, where you design the structure yourself | **Gap holds for products**: no product keeps it lasting, evidence-based and led by you | This is the main thing that sets us apart. Build on what the prototypes proved |
| Your take stored with the evidence and used in the structure | Glasp and Readwise notes, which are free text and not structured | **Partly holds** | Make takes structured (pro, con, dealbreaker, verify) so they drive the view |
| "Where I was" resume | [Edge Copilot Journeys](https://support.microsoft.com/en-us/microsoft-copilot/copilot-journeys) (summary plus a suggested next step), [Gemini in Chrome history search](https://support.google.com/gemini/answer/16716225), [Comet memory](https://www.perplexity.ai/help-center/comet/en/articles/12658438-comet-memory), [Basic Memory](https://github.com/basicmachines-co/basic-memory), Fuse (a prototype) | **Crowded at a basic level.** A deep, cross-source resume is still a gap | Our resume has to beat Journeys: open question, what you'd worked out and your place in each source, across AI chats and every browser |
| Working with every AI (MCP, briefs) | Basic Memory, OpenMemory MCP, Supermemory, [Readwise MCP](https://readwise.io/pricing), [Heptabase MCP](https://support.heptabase.com/en/articles/12679581-heptabase-mcp), [Zotero MCP](https://github.com/54yyyu/zotero-mcp) | **Not a gap on its own** | Expected of any tool like this. Support MCP from the start |
| Learn mode: stages, recall, fading, done | Tutors inside their own lessons (Cognaa, NoetaMind, Knorion), Anki and FSRS, Dodo | **Gap holds when learning comes from your own sources** | Keep it, for a later phase |
| Research mode: claims, evidence, source strength, reading list | Elicit and Consensus (AI-led, papers only), Zotero plus MCP plugins ([Zotero has no built-in AI](https://coursiv.io/blog/zotero-ai)), Heptabase (manual whiteboards), [Readwise's library-wide chat with citations](https://blog.readwise.io/update-aug2026/) | **Partly covered** | Connect to Zotero and Readwise instead of replacing them |
| Stored on your device, open source | Karakeep, Obsidian, Basic Memory, [Khoj](https://github.com/khoj-ai/khoj), [SurfSense](https://github.com/MODSetter/SurfSense/blob/main/README.md), [Screenpipe](https://www.screenpi.pe/about) | **Not unique** | Still essential for trust. The point is the combination |
| Nothing captured without a click | Most memory tools work from passive history or screen recording (Edge Journeys, Gemini history, Screenpipe) | **A real difference in values** | Keep it, and say it clearly |

## The closest competitors

1. **Edge Copilot Journeys.** It automatically groups your browsing into journeys, each with a summary and a suggested next step, so you can continue where you left off.
   - **Threat to our resume:** high.
   - **Limits:** Edge only, built from browsing history, no takes of your own, and it watches your history passively.
2. **Gemini in Chrome.** It searches your synced history to help you [rediscover a page and resume what you were doing](https://support.google.com/gemini/answer/16716225), and it compares products across up to 10 tabs.
   - **Threat:** high, because of Chrome's reach.
   - **Limits:** needs a Google account with synced history, comparisons only last for the moment, and it works with one AI company.
3. **Obsidian Web Clipper with Interpreter and Bases.** It's free and open source, and its [Interpreter](https://retypeapp.github.io/obsidian/web-clipper/interpreter/) uses an AI model to pull page data into your templates.
   - **Threat:** medium, for power users.
   - **Limits:** you have to set up templates, nothing is sent to the right investigation automatically, there's no resume, and it doesn't capture AI chats.
4. **Glasp and Readwise Reader.** Highlights with notes, saved with source and date, plus AI over your whole library with citations, and MCP.
   - **Threat:** medium.
   - **Limits:** built around a library, with no investigations, modes or resume.
5. **Fabric, Karakeep and Recall.** Capture anything, automatic tags and AI search. Recall also [brings up related saved items while you browse](https://docs.getrecall.ai/deep-dives/recall-augmented-browsing).
   - **Threat:** medium.
   - **Limits:** organized around content, not around your judgment or your purpose.
6. **The Carnegie Mellon prototypes.** Closest in concept, but not products. They're a source of proven ideas.

## AI browsers are moving into this space

| Product | What it does now | Lesson for us |
|---|---|---|
| [Edge Copilot Journeys](https://support.microsoft.com/en-us/microsoft-copilot/copilot-journeys) | Groups browsing into journeys with summaries and next steps | Resume alone won't be enough |
| [Gemini in Chrome](https://support.google.com/chrome/answer/16283624?co=GENIE.Platform%3DDesktop&hl=en-FM) | Searches your history to resume, compares up to 10 tabs, auto browse | Comparing in the moment is free. Lasting evidence with your judgment isn't offered |
| [ChatGPT's Chrome extension](https://www.technerdiness.com/chatgpt/chatgpt-chrome-tab-control/) | Since October 2026, reads your open tabs, acts in them and groups them | OpenAI is in the browser too, but it does tasks rather than keep your record |
| [Claude in Chrome](https://support.claude.com/en/articles/12012173-get-started-with-claude-in-chrome) | Reads, clicks and navigates on paid plans | The same: an agent that does things, not a record |
| [Perplexity Comet](https://www.perplexity.ai/help-center/comet/en/articles/12658438-comet-memory) | Memory of your searches so you can pick up where you left off, on every platform | AI-led research with memory |
| [Dia (Atlassian)](https://www.atlassian.com/blog/company-news/atlassian-acquires-the-browser-company) | Personal work memory across apps and tabs | Heading towards work use |
| [ChatGPT Atlas](https://www.therundown.ai/tools/atlas) | Retired on 9 August 2026. Its browser memories were folded into ChatGPT | Even OpenAI's own browser with memory didn't last as a standalone product |

**What this means:** each of these belongs to one AI company and focuses on doing tasks. None of them keeps a neutral, lasting record of your evidence and reasoning that the others can read. That record, open to all of them through MCP, is our place. Building another AI sidebar or agent isn't.

## What research and past failures teach us

1. **People don't think they need a tool until it's too late.** In a survey of everyday online research, [Kuznetsov and colleagues](https://arxiv.org/abs/2411.07206) found:
   - People spend about 38 minutes a day, or 4.4 hours a week, on open-ended online research.
   - Only about half of these tasks end with any closure.
   - The main reason people don't use support tools is that they don't believe they need them, even though keeping everything in their heads is clearly hard. The authors call this the "almost there" effect.
   - They suggest helping people define the task early, and making earlier work feel like part of a longer journey rather than wasted effort.

   **For us:** the first capture should need no setup. "What's this for?" defines the task early. The payoff should come later, when you resume or reuse the work.
2. **Comparison shopping is the biggest category.** It was 29% of everyday research tasks in the same study, with hobby research at 24%. **For us:** launching with decide mode is well supported. One caveat: the survey ran in September 2022, before ChatGPT was widely available.
3. **Capturing trade-offs and building tables works:**
   - Unakite cut the cost of capturing trade-offs by 45%, and made it [about three times faster](https://dl.acm.org/doi/abs/10.1145/3332165.3347908) for someone else to understand them later.
   - Crystalline made comparison tables about [20% faster, with 60% less effort](https://arxiv.org/abs/2202.02175v1).
   - Selenite used AI to produce an [overview of options and criteria](https://arxiv.org/abs/2310.02161) at the start, which solved the empty-start problem.

   **For us:** build all three ideas into decide mode.
4. **Hosted tools disappear:**
   - Omnivore was [shut down within weeks](https://techcrunch.com/?p=2907694) after its team joined ElevenLabs.
   - Mem0's OpenMemory extension was archived.
   - ChatGPT Atlas was retired.
   - Rewind was shut down.

   **For us:** keep data on the device, use an open format and offer export from day one, so nobody ever loses an investigation.
5. **People distrust AI browser extensions.** One study found [52% of AI Chrome extensions collect user data](https://about.fast.io/resources/best-ai-extensions-for-chrome-2026/). **For us:** ask for as few permissions as possible, publish the code, keep data local, and show a clear indicator while capturing.
6. **Clipped content gets left behind.** A review of web clippers notes that clipped content often [sits untouched, stripped of context](https://blog.pixiebrix.com/blog/the-best-web-clippers-in-2026-capture-the-web-without-losing-context). **For us:** the value has to come from the structure and the resume, not from saving.

## Open-source building blocks

These already exist, so we shouldn't rebuild them.

| Need | Open-source option | How we'd use it |
|---|---|---|
| Web capture with templates and AI extraction | [Obsidian Web Clipper](https://www.dsebastien.net/obsidian-web-clipper/) | Learn from its templates and Interpreter, or work alongside it |
| Saving, tagging and searching links, PDFs and images, with mobile apps | [Karakeep](https://docs.hoarder.app/) | Reference for archiving and self-hosting |
| Highlight and annotation extension | [Memex](https://github.com/WorldBrain/Memex), Hypothesis | Reference for anchoring highlights and the sidebar design |
| Memory that AI tools can read, stored as Markdown | [Basic Memory](https://github.com/basicmachines-co/basic-memory) | Reference for MCP tools and storing everything as plain files |
| Pulling facts out of chats | [Mem0 / OpenMemory](https://mem0.ai/blog/introducing-openmemory-mcp), [Supermemory](https://github.com/supermemoryai/supermemory-mcp) | Patterns for extracting facts and handling contradictions |
| Research libraries | [Zotero MCP](https://github.com/54yyyu/zotero-mcp) | Connect research mode to Zotero |
| AI research over many sources | [SurfSense](https://github.com/MODSetter/SurfSense/blob/main/README.md) | For helper agents, or simply as a reference |
| Spaced repetition | [FSRS](https://docs.ankiweb.net/faqs/what-spaced-repetition-algorithm) | Fading and recall in learn mode |
| AI on the device | [Chrome's Prompt API (Gemini Nano)](https://developer.chrome.com/docs/ai/prompt-api) | Cheap, private processing inside the extension |

## Changes to the proposal

1. **Stop presenting one-click capture as new.** It's expected. Lead with: *your investigations, organized by what you're doing, with your judgment next to the evidence.*
2. **Launch with decide mode,** built on what the prototypes proved:
   - automatic collection into a comparison table
   - an AI-generated overview of options and criteria at the start
   - saving the reasons behind each choice
3. **Make "What's this for?" the centre of onboarding,** because defining the task early is what gets people past the "almost there" effect.
4. **Make the resume deeper than Edge Journeys:**
   - the open question
   - what you'd worked out
   - your place in each source, including AI chats
   - working in every browser
5. **Build on open source, and store investigations as Markdown files** that work with tools like Obsidian, so people trust the format and can always leave with their data.
6. **Be the neutral record that AI browsers and agents read** through MCP. Don't compete with them as another sidebar or agent.
7. **Treat permissions and open code as features,** given how widely people distrust AI extensions.
8. **Plan for big companies copying the basic features.** If Google or Microsoft add "save to a journey with a note," what keeps us ahead is:
   - neutrality across AI companies
   - structured takes
   - learn and research modes
   - storage on the device

## Still uncertain

- This research is based on public pages and papers, not hands-on testing. Next, test Edge Journeys, Gemini in Chrome, Obsidian Web Clipper, Glasp and Fabric on the same bike decision.
- Small startups launch weekly. A search a month from now may find something closer.
- The sensemaking survey ran before ChatGPT was widely used. Behaviour has probably shifted towards AI chats, which would make capturing AI answers more important.
