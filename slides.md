---
theme: dracula
title: Commit Messages,<br>On My Terms
info: |
  ## Commit Messages, On My Terms
  A configurable Windsurf workflow that writes semantic commit messages
  for my staged changes — in the format I control.
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
duration: 12min
---

<div class="flex flex-col items-center justify-center text-center">

# Commit Messages,<br><span class="text-purple-300">On My Terms</span>

<p class="max-w-xl mx-auto text-balance leading-relaxed opacity-90">
A configurable <b>Windsurf workflow</b> that writes semantic commit messages
for my staged changes — in the format <em>I</em> control.
</p>

<div class="mt-6 text-sm opacity-50">
  Ivo Karaneshev · June 2026
</div>

<div @click="$slidev.nav.next" class="mt-12 py-1 opacity-60 hover:opacity-100 transition cursor-pointer">
  Press <kbd>space</kbd> to start <carbon:arrow-right class="inline"/>
</div>

</div>

<!--
This is a short show-and-tell of a tiny workflow I built in Windsurf.
It nags an AI to write my commit messages for me — but in MY format, with MY rules.
Two-minute idea, but it removed a paper cut I hit a dozen times a day.
Let's start with why I bothered.
-->

---
layout: section
---

# The problem

<div class="opacity-70 mt-4">We're lazy when it comes to commit messages.</div>

<!--
Be honest: writing a good commit message is the most skippable step in the whole loop.
The code works, the PR is open, and the message is an afterthought.
-->

---

# The git log nobody is proud of

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

```bash
$ git log --oneline
a1b2c3d  wip
4d5e6f7  fix
8g9h0i1  stuff
2j3k4l5  asdf
6m7n8o9  fix again
0p1q2r3  please work
4s5t6u7  final fix (real)
```

</div>
<div>

<v-clicks>

- 🔍 **Bisect & blame** become useless
- 👀 **Reviewers** can't see intent at a glance
- 📝 **Changelogs** can't be generated
- 🕰️ **Future-you** has zero context
- 🤝 The whole **team** pays the tax

</v-clicks>

</div>
</div>

<div v-click class="mt-8 text-center text-lg opacity-80">
The diff already says <em>what</em> changed. A good message says it <span v-mark.purple="6">at a glance.</span>
</div>

<!--
We all have this log. WIP, fix, asdf, "please work".
The cost isn't felt today — it's felt three months from now when you're bisecting a regression,
or when someone tries to auto-generate a changelog and gets garbage.
The information IS there, in the diff. We're just too lazy to summarize it. So... let's not be.
-->

---
layout: fact
---

# AI is _good enough_ for this

<div class="text-xl opacity-80 mt-6 max-w-2xl mx-auto">
Reading a diff and summarizing it is <span class="text-green-300">exactly</span> what an LLM is great at.
</div>

<div v-click class="mt-10 text-base opacity-70 max-w-2xl mx-auto">
The bottleneck was never capability — it's <span v-mark.circle.orange="1">friction.</span>
Make the good message the <em>lazy</em> option, and laziness starts working <em>for</em> you.
</div>

<!--
Here's the key insight. Summarizing a diff is squarely in the model's wheelhouse —
it's literally text-in, text-out summarization.
So the question isn't "can AI do it" — it can. The question is how do I remove the friction
AND keep control of the output format. Make the right thing the path of least resistance.
-->

---

# The built-in option

Windsurf already ships a **"Generate commit message"** ✨ button. So why not just use it?

<div class="grid grid-cols-2 gap-6 mt-6">
<div v-click class="p-4 rounded-lg border border-yellow-500/30 bg-yellow-500/5">

### ⚠️ It's in beta + documented limits

- "Large or complex commits may result in **more generic messages**"
- "Specialized **terminology** might not always be captured"
- "Generated messages are suggestions and **may need editing**"

</div>
<div v-click class="p-4 rounded-lg border border-red-500/30 bg-red-500/5">

### 🚫 And the dealbreaker for me

- **Not configurable** — I can't enforce my
  `#TICKET - type(scope): title` convention
- No control over **types**, **ticket prefix**, or **guardrails**
- It's a black box I can't tune

</div>
</div>

<div v-click class="mt-6 text-center opacity-70 text-sm">
Source: <a href="https://docs.devin.ai/desktop/ai-commit-message#limitations" target="_blank">docs.devin.ai — AI commit message · Limitations</a>
</div>

<!--
The obvious objection: Windsurf already has a sparkle button for this. I tried it.
It's fine! But it's beta, and their own docs list these limits — generic on big commits,
misses jargon, always needs a pass.
The real dealbreaker though is the last column: I can't make it follow my team's format.
No ticket prefix, no fixed type list. It's a black box. I wanted a glass box.
-->

---
layout: two-cols
layoutClass: gap-8
---

# The Approach

Not a button — a **workflow + a rule**.
Two small markdown files I own and version.

<v-clicks>

- 🧠 The **rule** defines _what good looks like_
- 🪜 The **workflow** defines _the procedure_
- ✍️ I own both → I own the output

</v-clicks>

::right::

```md
.windsurf/
├── rules/
│   └── commit-message.md   # always_on
│       → format, types,
│         ticket convention
└── workflows/
    └── commit.md           # /commit
        → stage-check, diff,
          review, commit
```

<div v-click class="mt-4 text-sm opacity-70">
Plain markdown. Diffable. Tweakable in 10 seconds.
</div>

<!--
So here's what I built instead. Two markdown files.
One is a RULE — always-on context that teaches the model my format, my allowed types,
my ticket convention. The other is a WORKFLOW, invoked with slash-commit, that's the actual
procedure: check staging, read the diff, propose, let me approve, commit.
Both are plain markdown in my repo. I can tweak them in seconds, and they're versioned with the project.
-->

---

# How it flows

<div class="grid grid-cols-2 gap-10 mt-2 items-center">
<div class="flex flex-col gap-4 text-sm">
<div v-click class="p-3 rounded border border-purple-500/30 bg-purple-500/5">
🔒 <b>Never stages for me</b><br/><span class="opacity-70">I stage manually — only staged changes get committed</span>
</div>
<div v-click class="p-3 rounded border border-purple-500/30 bg-purple-500/5">
👀 <b>Always reviewable</b><br/><span class="opacity-70">Message shown in chat before anything is committed</span>
</div>
<div v-click class="p-3 rounded border border-purple-500/30 bg-purple-500/5">
🧹 <b>No AI ads</b><br/><span class="opacity-70">No "Generated with…" noise in my history</span>
</div>
</div>
<div class="flex justify-center">

```mermaid {scale: 0.62}
flowchart TD
  A([stage]) --> B[/commit/]
  B --> C[read staged diff]
  C --> D[draft message]
  D --> E{review}
  E -- edit --> D
  E -- go --> F([commit ✅])
```

</div>
</div>

<!--
The flow itself. I stage what I want — deliberately, because staging IS my intent.
I run slash-commit. It reads only the staged diff, drafts a message using the rule,
and shows it to me in chat. I can ask for tweaks, or say "proceed" / "commit" / "go" and it commits.
Three guardrails I care about, along the bottom: it never stages for me — that's sacred, staging is intent.
It always shows me the message first. And no "Generated with AI" ad in my history.
-->

---

# The format

A strict, parseable convention — ticket auto-derived from the branch name.

```md {1|3-4}
#<ticket> - <type>(<scope>): <title>     ← lowercase title, ≤50 chars, no period

- optional bullet explaining the *why*
- another high-level point
```

<div class="mt-4 mb-2 text-sm opacity-70">Allowed types — a fixed, predictable set:</div>

<div class="flex flex-wrap gap-2 text-sm">
  <span class="px-2 py-1 rounded bg-green-500/15 border border-green-500/30">feat</span>
  <span class="px-2 py-1 rounded bg-red-500/15 border border-red-500/30">fix</span>
  <span class="px-2 py-1 rounded bg-purple-500/15 border border-purple-500/30">refactor</span>
  <span class="px-2 py-1 rounded bg-blue-500/15 border border-blue-500/30">docs</span>
  <span class="px-2 py-1 rounded bg-yellow-500/15 border border-yellow-500/30">test</span>
  <span class="px-2 py-1 rounded bg-pink-500/15 border border-pink-500/30">chore</span>
  <span class="px-2 py-1 rounded bg-cyan-500/15 border border-cyan-500/30">style</span>
  <span class="px-2 py-1 rounded bg-orange-500/15 border border-orange-500/30">perf</span>
</div>

<div v-click class="mt-6 text-sm opacity-80">
On branch <code>CALI-3250</code>? → the message starts with <code>#CALI-3250</code> automatically. No copy-paste.
</div>

<!--
Here's the actual format the rule enforces. Ticket prefix, conventional-commit type and scope,
a lowercase title under 50 chars with no trailing period, and an optional body for the WHY.
The type list is fixed — eight options — so it's predictable and greppable.
And the nice touch: it pulls the ticket number straight from the branch name. I name branches
after the ticket anyway, so I never type the ticket again.
-->

---

# Before → after

The same staged change, two worlds apart:

<div class="relative h-6 mb-1 text-sm">
  <span class="absolute inset-x-0 transition-opacity duration-1200" :class="$clicks < 1 ? 'opacity-80' : 'opacity-0'">What the laziest dev would type…</span>
  <span class="absolute inset-x-0 transition-opacity duration-1200" :class="$clicks === 1 ? 'opacity-80' : 'opacity-0'">What the workflow proposes instead…</span>
  <span class="absolute inset-x-0 transition-opacity duration-1200" :class="$clicks >= 2 ? 'opacity-80' : 'opacity-0'">…and the body, when the change earns it.</span>
</div>

````md magic-move
```
WIP
```

```
#CALI-3250 - feat(auth): add JWT login flow
```

```
#CALI-3250 - feat(auth): add JWT login flow

- Implemented JWT token validation logic
- Added login form component
- Updated auth service methods
```
````

<div v-click class="mt-6 text-center opacity-80">
Same effort for me. Wildly more useful for everyone reading it later.
</div>

<!--
This is the whole pitch in one slide. Left to right, same staged diff.
Top: what I'd actually type at 6pm on a Friday — "fix".
Then what the workflow gives me: a proper semantic message with the ticket.
And when the change deserves it, a body explaining the why.
My effort is identical — I stage and say "go". The payoff lands on every future reader.
-->

---

# Comparison

<div class="text-sm">


|  | ✨ Windsurf button | 🛠️ My workflow |
|---|---|---|
| **Format** (`#TICKET - type(scope)`) | ❌ not configurable | ✅ enforced by rule |
| **Ticket from branch** | ❌ | ✅ automatic |
| **Fixed type vocabulary** | ❌ | ✅ 8 defined types |
| **Guardrails** (never-stage, no AI ads) | ❌ | ✅ I define them |
| **Reviewable before commit** | ⚠️ in the box | ✅ in chat, with edits |
| **Evolves with me** | ❌ beta black box | ✅ plain markdown, versioned |

</div>

<div v-click class="mt-6 text-center text-lg opacity-85">
The button is someone else's opinion. <span class="text-purple-300">This is mine — and it's a text file.</span>
</div>

<!--
Side by side. The button covers the happy path, but every row where I want control, it's a no.
Mine is yes across the board because it's just markdown I wrote.
The one-liner I'd leave them with: the button is someone else's opinion baked into beta software.
Mine is my opinion, and it's a text file I can change whenever my team's convention changes.
-->

---
layout: statement
---

# Make the good commit<br/>the _lazy_ commit.

<div class="text-lg opacity-75 mt-8 max-w-xl mx-auto">
Low friction <span class="opacity-50">+</span> my rules <span class="opacity-50">=</span>
a history I'm actually proud of.
</div>

<div v-click class="mt-12 text-sm opacity-60">
Two markdown files. Steal them, bend them to your convention, commit better.
</div>

<!--
The takeaway. The trick isn't "use AI" — it's removing friction while keeping control,
so the good message becomes the path of least resistance.
Two small markdown files did that for me. Steal them, change the format to your team's,
and your git log stops being something you apologize for. That's it — thanks!
-->
