# CLAUDE.md — Editing conventions for the System Design Study Guide

This folder is a **system-design study guide** for engineers preparing for system-design
interviews at product companies. Read this file before creating or editing any chapter, so
edits stay consistent with the established style. When something here conflicts with a
general instinct, **this file wins** for this project.

---

## 1. What this guide is (and who it's for)

- **Audience:** developers of *all* backgrounds preparing for system-design interviews —
  front-end, back-end-but-new-to-scale, full-stack, mobile, data. Assume general
  programming fluency (variables, APIs, HTTP, JSON) but **no prior infrastructure or
  distributed-systems experience.**
- **Goal:** one chapter per platform or foundational concept, studyable at **one section
  per day, one chapter per week**. Reader has a **short attention span** — favor clarity
  and concreteness over length.

---

## 2. Golden rules (non-negotiable)

1. **Developer-general framing.** Analogies must be universal (restaurant host, textbook index, dictionary, ballot counting). 
2. **The FoodDash running example runs through every chapter.** FoodDash is a
   food-delivery app. Each chapter shows where that platform fits into the *same* evolving
   system. Keep FoodDash facts consistent with the **canon in §7 below**.
3. **Restraint is the through-line.** The single most important lesson is *don't
   over-engineer* — start simple, justify every addition with a real requirement, name
   trade-offs. Every chapter's §8 ("Avoiding overkill") trains this. Never add a component
   no requirement justifies.
4. **Tight, not padded.** Sections may run up to ~1 page and chapters up to ~12 pages, but
   that is a *ceiling, not a quota*. Expand only where it builds foundation. Prefer tables,
   diagrams, and concrete examples over long prose.
5. **Accuracy.** These are stable CS fundamentals; keep product facts at the conceptual
   level and avoid volatile specifics (exact prices, version numbers). If unsure of a
   current fact, check rather than guess.

---

## 3. File & naming conventions

- One chapter per file, named `NN-topic.md` (zero-padded), e.g. `07-caching.md`.
- Chapter order is deliberate and builds up FoodDash. Chapters 01–04 are foundational
  concepts every later chapter assumes; 05–13 are platform chapters; 14 is the final,
  synthesis chapter (Putting It All Together).
  Current set:

  | File | Chapter |
  |---|---|
  | `README.md` | Curriculum & how to use |
  | `01-horizontal-vs-vertical-scaling.md` | Horizontal vs. vertical scaling |
  | `02-monolith-vs-microservices.md` | Monolith vs. microservices |
  | `03-cap-theorem.md` | The CAP theorem |
  | `04-algorithms-for-scale.md` | Algorithms for scale (Bloom filters, HyperLogLog, Roaring Bitmaps, consistent hashing) |
  | `05-relational-databases.md` | Relational databases (SQL) |
  | `06-nosql-databases.md` | NoSQL databases |
  | `07-caching.md` | Caching |
  | `08-object-storage.md` | Blob / object storage |
  | `09-message-queues-and-streaming.md` | Message queues & streaming |
  | `10-search-engines.md` | Search engines |
  | `11-load-balancers.md` | Load balancers |
  | `12-cdn.md` | CDN |
  | `13-data-processing.md` | Data processing (MapReduce & Spark) |
  | `14-putting-it-all-together.md` | Putting It All Together (must always be the **last** chapter) |

- **The final chapter stays last.** To insert a new chapter, place it before the final
  chapter and **renumber** everything after it so the final chapter keeps the highest
  number (see §8).

---

## 4. Chapter anatomy (chapters 01–13)

Every platform chapter follows this exact skeleton, in this order:

1. **`# Chapter N — <Title>`** — the H1. The number here **must match the filename**.
2. **Front-matter callout** (a single `>` blockquote) containing, in order:
   - **One-line summary** — what the platform is, in one sentence.
   - **Interview bar by company** — three tiers: *Startup* / *Mid-size* / *Big-tech*,
     each one line, describing how deep the answer should go.
   - **Running example** — the FoodDash situation this chapter addresses.
3. **The nine numbered sections** (see §5).
4. **Real-world use cases** — 3–4 bullets of real companies/systems, ending with a
   one-line **Theme:**.
5. **Interview questions where <platform> is the key decision** — a numbered list of
   prompts, each with a `→` note on the expected answer, then a **"How to answer well:"**
   paragraph.
6. **60-second recap** — a tight bullet summary (this doubles as the seed for the cheat
   sheets), and the chapter ends there.

**No footer.** Chapters do not link to "the next file" — navigation is the chapter map in
`README.md` §4 and the final chapter's cheat table (§6 of `14-putting-it-all-together.md`).
A footer was tried early on and dropped: it went stale every time a chapter was inserted or
renumbered, so don't reintroduce one.

Non-platform chapters differ: **`00` (curriculum)** and **`14` (Putting It All Together)**
do NOT use the nine-section template — Chapter 14 uses worked examples + the interview
method; the curriculum uses framing/schedule/glossary. **`04` (algorithms for scale) is a
partial exception** — it covers four techniques rather than one platform, so it uses a
shorter, lettered format (§A–§D) instead of the nine numbered sections, while keeping the
front-matter
callout, real-world use cases, interview questions, and 60-second recap. `01`–`03` use the
full nine-section template like any platform chapter. Don't force the strict nine-section
template onto `00`, `04`, or `14`.

---

## 5. The nine sections (platform chapters)

Use these exact headings and intent. Each is `## §N — <heading>`.

- **§1 — Why the platform exists** — the pain that created it; introduce core vocabulary.
- **§2 — When to use it** — the signals in a problem that point to this tool.
- **§3 — When *not* to use it** — where it fails; when it's overkill.
- **§4 — Popular products** — the real names to say in an interview (a table).
- **§5 — Quick product comparison** — head-to-head (e.g. PostgreSQL vs MySQL vs Oracle).
- **§6 — How it compares to other platforms** — cross-platform decision (e.g. SQL vs NoSQL,
  cache vs replica, CDN vs load balancer). Reinforce that platforms are *partners*.
- **§7 — Factors to consider when designing with it** — what to reason about out loud.
- **§8 — Avoiding overkill** — the restraint section; **must include a "Red flags that make
  interviewers wince 🚩" list.**
- **§9 — Hello-world exercise (~30 min)** — a hands-on task (real, runnable code/commands),
  ending with a **"You understand <platform> when you can:"** checklist.

---

## 6. Per-section internal rhythm & recurring devices

**Every numbered section follows this shape:**
`**The scenario.**` (a concrete FoodDash situation) → explanation → **one visual** (a
mermaid diagram or a markdown table) → a worked example (usually FoodDash) → a closing
**`> **Say this in the interview:** *"…"*`** line — except §9, whose closer is its
"You understand <platform> when you can:" checklist instead.

**Required recurring devices — keep them everywhere:**
- **"Say this in the interview:"** — a quoted, speakable answer at the end of every
  numbered section *except* §9. §9 is the one stated exception: per §5 above, it closes
  with its own "You understand <platform> when you can:" checklist instead. This is the
  guide's signature device for §1–§8; never drop it there.
- **Interview-bar-by-company callout** — in the front-matter of every platform chapter.
- **Red-flags 🚩 box** — in §8.
- **60-second recap** — the last thing in the chapter.
- **A visual in (almost) every section** — mermaid diagram or table; keep a good rhythm.

**Tone:** warm, direct, second person ("you"), concrete. No emojis except the 🚩 red-flag
marker and the ✅/❌ used in decision diagrams/lists. Avoid "genuinely", "honestly",
"actually". Don't hedge; state the trade-off.

---

## 7. FoodDash canon (keep consistent across chapters)

FoodDash = a food-delivery app. Keep the platform-to-data mapping consistent:

| Data / concern | Platform | Notes |
|---|---|---|
| Users, restaurants, orders, order_items, payments, dishes | **Relational / PostgreSQL** | The transactional core; ACID; the "money" |
| Driver GPS pings | **NoSQL key-value / wide-column** (DynamoDB / Cassandra) | Millions of writes, one-key access, staleness OK |
| Live order-status feed | **NoSQL wide-column** (Cassandra) | High write volume, time-ordered |
| Flexible per-restaurant menu attributes | **Document DB** (MongoDB) | Optional; only when flexibility is the point |
| Menus, sessions, "top restaurants" list, rate limiting | **Redis cache** | Read-often, change-rarely, low latency |
| Dish photos, restaurant banners, order receipts | **Object storage / S3** | Bytes in S3, URL + metadata in the DB |
| "Order placed" → notify restaurant, assign driver, push customer, update analytics | **Message queue** | Async workers; idempotent; dinner-rush spike buffering |
| Restaurant/dish search, autocomplete, filters (veg, price, rating, distance) | **Search engine / Elasticsearch** | Derived index synced from the DB |
| Dinner-rush (7–9pm) traffic, autoscaling, stateless app servers | **Load balancer** | Sessions in Redis so servers stay stateless |
| Dish photos + app assets served globally | **CDN** | Live per-user order tracking is **NOT** CDN-cached |
| Nightly revenue/city, top-restaurant rankings, ML features | **Data processing / Spark** | Events → Kafka → S3 data lake → Spark → warehouse/cache |

**City/currency flavor:** examples use cities like Bengaluru/London and ₹ where money
appears. Sample people: Asha, Ravi. Keep these consistent when adding examples.

---

## 8. Cross-reference discipline & how to add/renumber a chapter

There is no footer chain to maintain (see §4) — but chapters still reference each other
by number in prose (`"Chapter 7"`, `"Ch. 7"`) and by filename in backticks
(`` `07-caching.md` ``), and three places summarize the whole guide. All of these must
stay in sync:

- **In-chapter cross-references** — every `Chapter N` / `Chapters N–M` / `Ch. N` mention
  and every `` `NN-topic.md` `` filename reference, anywhere in any chapter.
- **`README.md` §4** — the chapter-map table and its mermaid
  dependency diagram list every chapter by number and title.
- **The final chapter's `§6` cheat table and `§9` recap** — list every chapter's core
  decision. **When you add or remove a chapter, update the final chapter's cheat table,
  its recap, and its intro's "Chapters 1–N" range.**
- **The H1 chapter number must always equal the filename number.** (This has bitten us —
  a rename without an H1 update leaves a "Chapter 9" titled file named `10-…`.)

**To insert a new chapter:**
1. Decide where it belongs pedagogically — don't just tack it onto the end to minimize
   changes. If it's foundational, it likely belongs early; if it's a specific platform,
   it belongs near the platforms it relates to.
2. Rename every chapter from that slot onward (including the final chapter) up by however many
   slots you're inserting, **highest number first** to avoid collisions, and fix each
   renamed chapter's H1 to match its new filename number.
3. Shift every in-chapter cross-reference (`Chapter N`, `Ch. N`, `` `NN-topic.md` ``)
   across every file by the same amount — a small script beats doing this by hand.
4. Write the new chapter, following §4–§6 (or the `04`-style exception if it's a grouped
   set of techniques rather than one platform).
5. Update `README.md` §4 (table + mermaid diagram) and the final chapter's cheat table,
   recap, and intro range to include the new chapter.
6. Run the QA checklist (§9).

---

## 9. QA checklist (run after any edit)

From the folder, quick greps:

- **No front-end references:** `grep -rni "front-end\|frontend\|front end" .` → must be
  empty.
- **No stale cross-references:** after a rename, `grep -rl "OLD-FILENAME" .` → must be
  empty.
- **H1 matches filename number** for every chapter.
- **Every numbered section §1–§8 ends with a "Say this in the interview" line; §9 ends
  with its "You understand <platform> when you can:" checklist instead (the one stated
  exception — see §5 and §6).**
- **§8 (or its equivalent) has a red-flags 🚩 list; chapter ends with a 60-second recap
  and no footer.**
- **No garbled characters.** Intended non-ASCII is limited to: `✅ ❌ ✔ → 🚩 — ’ “ ” × §
  ₹ ≫`. Anything else (e.g. mojibake like `�`) must be fixed. Quick check:
  `grep -rnP '[^\x00-\x7F]' . | grep -vP '[✅❌✔→🚩—’“”×§₹≫]'`
- **Mermaid blocks** are fenced with ```` ```mermaid ```` and render (no stray characters
  inside node labels).

---

## 10. Diagrams

- Use **mermaid** fenced code blocks for all diagrams (they render in the markdown
  preview, GitHub, Notion, Obsidian).
- Prefer `graph TD` / `graph LR` for architecture and decision flows; `sequenceDiagram`
  for request/response walk-throughs (e.g. cache-aside, presigned uploads).
- Keep node labels short; use `<br/>` for line breaks inside a node. Avoid characters that
  break mermaid parsing inside labels.

---

## 11. Pending / planned work (not yet built)

- **Per-chapter cheat sheets** — one page each, distilled from the 60-second recaps +
  the "when to use / when not / products / one-line comparison" tables.
- **Mock interview Q&A bank** — practice questions with model answers and a scoring rubric,
  spanning all fourteen chapters.

When these are built, follow the same audience, tone, and FoodDash conventions above.

---

## 12. Quick "don't" list

- ❌ Don't reintroduce front-end-specific framing or analogies.
- ❌ Don't pad sections to hit a page count.
- ❌ Don't add architectural components to examples without a stated requirement (it
  contradicts the guide's core lesson).
- ❌ Don't let the final chapter drift from the platform chapters (keep its tables in sync).
- ❌ Don't rename a chapter file without updating its H1 and all cross-references.
- ❌ Don't change FoodDash's platform-to-data mapping (§7) without updating it everywhere.
- ❌ Don't add a footer ("Next: ...") line to a chapter — footers were removed on purpose
  (§4); navigation lives in `00`'s chapter map and the final chapter's cheat table instead.
- ❌ Don't force a grouped, multi-technique addition (like `04`) into a single-platform
  nine-section shape, and don't split a genuinely single-platform topic into the `04`-style
  lettered format just to avoid writing nine sections.
- ❌ Don't insert a new chapter at the end just because renumbering the rest is more work —
  place it where it teaches best (see §8's insertion steps).
