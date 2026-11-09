# Organizing it in a really nice way

## The idea

**You never organize. It organizes for you, and gives you a place you can browse.**

Both halves matter:

- **People find their own things mostly by browsing, not searching.** Even when given better search tools, people [browsed for 56 to 68% of the times they looked for a file, and searched for only 4 to 15%](https://dl.acm.org/doi/10.1145/1402256.1402259). Browsing your own folders even [activates the same brain regions as finding your way around a real place](https://www.nature.com/articles/srep14719).
- **People don't want to do the filing.** A 1983 study of how people organize their desks concluded that systems should [classify things automatically and allow untitled piles](https://dl.acm.org/doi/10.1145/800210.806476). Later research found people are [unwilling or unable to spell out structure up front](https://link.springer.com/article/10.1023/A:1008716330212), so the system should suggest structure and add it gradually.
- **Apps like [mymind](https://mymind.com/what) go all the way the other way:** no folders and no categories, just AI tags and search. That removes the filing, but it also removes the browsing. We want both: a structure you can walk through, built for you.

## Design rules

1. **It files, you correct.**
   - Saves go to the thread you're working in.
   - Anything it isn't sure about goes into a small pile with one-tap suggestions.
   - Nothing ever gets filed in the wrong place without you seeing it.
2. **Shallow and stable.**
   - There are at most two levels: threads, then sections inside a thread. Deep and very large folders [make things slower to find](https://www.researchgate.net/publication/220432870_The_Effect_of_Folder_Structure_on_Personal_File_Navigation).
   - Each thread keeps its place, icon and color, because people [remember where they put things](https://www.microsoft.com/en-us/research/publication/data-mountain-using-spatial-memory-for-document-management/).
3. **Structure grows with use.** A thread starts as a plain list. Once it has enough in it, it offers a view: a comparison, a checklist, or claims with sources.
4. **Your words come first.**
   - Your question and notes are shown exactly as you wrote them.
   - Anything the AI drafted appears in grey with a small "drafted" label until you keep it.
5. **Every card leads back to its source.** Each save has a source chip that opens the exact spot it came from.
6. **Quiet.**
   - No badges, streaks or red dots.
   - The home screen never shows more than five things that need you.

## Home: your threads

```
YOUR THREADS                                          Search   + New

NOW
┌──────────────────────────────┐  ┌──────────────────────────────┐
│ 🚲 Choosing a bike           │  │ 🧠 How attention works       │
│ Deciding · 14 saves          │  │ Learning · 3 of 7 topics     │
│ You were: checking Bike A    │  │ You were: why scores are     │
│ in the rain                  │  │ divided by √d                │
│ [Open where I was]           │  │ [Open where I was]           │
└──────────────────────────────┘  └──────────────────────────────┘

PAUSED
  ✈️  Goa trip           next: compare two hotels near the beach    5 days ago
  📄 Thesis chapter 2   next: find a source from after 2024        2 weeks ago

DONE
  🎧 Headphones         chose pair B, reasons saved                August

LOOSE SAVES (6)         4 of these look like "Goa trip"   [Move them]
```

- **Now:** threads you've touched in the last few days, each showing where you were.
- **Paused:** threads you've closed and kept, each with its next step.
- **Done:** finished threads, each with its outcome. In one survey, [only about half of everyday research tasks ended with any sense of closure](https://arxiv.org/abs/2411.07206). Marking a thread done with a one-line outcome gives it that closure.
- **Loose saves:** the unsorted pile. It stays small because it suggests where each item belongs.

Threads move between shelves on their own:
- A thread you haven't touched for a week moves to Paused.
- When you make a choice or finish, it asks for a one-line outcome and moves to Done.

## Inside a thread

Everything is on one scrolling page, in this order.

```
🚲 CHOOSING A BIKE                                              Deciding
"Which city bike handles rain and a 10 km commute, within my budget?"

WHERE YOU WERE · 3 days ago
Checking Bike A in the rain. Your note: "B's brakes might be a dealbreaker."
[Open where I was]      Next: owner reviews of Bike A in the rain

COMPARISON
              Bike A           Bike B               Bike C
  Price       ✓ in budget      ✓ in budget          ✓ 15% off until Sunday
  Rain        ? no evidence    ✗ brakes squeak      ~ sources disagree
  Comfort     ✓ 2 reviews      ✓ 1 owner            ✗ your take: seat
  Leaning: A, if the rain question checks out

SAVES (14)                                               Group by: bike ▾
  Bike B  ✗  "Brakes squeak after a few weeks of rain"   Reddit · your take: dealbreaker
  Bike A  ✓  Frame and build quality                      YouTube 7:32
  Bike C  ✓  15% off until Sunday                         Shop page · seen 2 Nov

STILL OPEN
  • How does Bike A handle rain?
  • What does servicing cost for each one?

NOTES AND CHATS
  Your note from the shop (photo, kept as you wrote it)
  ChatGPT: "compare these three bikes" · opens at the message

Ask this thread...
```

The page changes with the kind of thread. In a learning thread, the comparison becomes a topic checklist:

```
🧠 HOW ATTENTION WORKS                       Learning · interview in 3 weeks
"Understand attention well enough to explain it in an interview"

TOPICS
  ✓ Tokens and embeddings
  ✓ Softmax
  ● Attention                                   3 of 5 parts
      ✓ Queries, keys, values    clicked: search analogy (YouTube 4:10)
      ● Dividing by √d           following
      ○ Multi-head attention
      ○ Masking                  suggested: in 4 of 5 course outlines
  ○ Positional encoding           parked
  ! Tokenization                  fading: you only watched one video
```

In a research thread, it becomes questions, claims and sources.

## Your trail: the chain of thought as a timeline

Every thread also has a trail view, which shows the order your thinking happened in:

```
YOUR TRAIL · How attention works

Mon   Asked Claude for a plan               → kept 7 topics
Mon   Confused: "why separate queries and keys?"
        asked ChatGPT on the side           → still fuzzy
Tue   Clicked: the search analogy           YouTube 4:10
Tue   Started √d                            got: big dot products make softmax too sharp
Wed   Paused for interview prep             ← you are here
```

Use the trail to retrace how you got somewhere, to explain it to someone else, or to spot where you went in circles.

## How it keeps itself tidy

- **Names and icons.** Each thread is named after your question and gets an icon and a color. You can rename it with one tap.
- **Sections.** Saves group themselves by option, topic or question, and you can switch the grouping.
- **Duplicates.** If you save the same page twice, it becomes one card that keeps both of your takes.
- **Merge and split.** It suggests changes like "These two threads look like the same thing. Merge?" or "This thread has two separate questions. Split it?"
- **Shelves.** Threads move from Now to Paused on their own, and to Done when you finish.
- **Letting go.** Once a month, it asks something like "22 read-later tabs haven't been opened in 30 days. Let them go?" Anything you let go can be brought back for 30 days.
- **Stable places.** Nothing moves around unless you touch it.

## Small touches that make it feel good

- Every thread starts with your question, in your own words.
- AI-drafted text looks different until you keep it, so you always know what's yours.
- Source chips show where every point came from, and tapping one opens the exact spot.
- Closing a thread gives you a moment of closure: one line on what you decided or learned.
- Each card shows a small preview of its source, such as the page, the video frame or your photo.
- Every thread can be exported as a clean page you can share or print.
