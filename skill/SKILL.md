# The Copy Machine

A composable copywriting system for AI vibe coders who have no copywriting background. Rewrite or generate copy by combining three layers: a framework (persuasion structure), a tone (voice), and a channel (format).

---

## Mode Detection

Before asking any questions, determine the mode:

### Check for Existing Files

Scan for files in the user's environment:
- Look for HTML, JSX, TSX, MDX, or plain text files in `/mnt/user-data/outputs/` or the current working directory
- Check if the user has provided or referenced any existing copy/content file

### REWRITE Mode

**Triggered when:** An existing file with copy is found or provided by the user.

**Behavior:**
1. Read the existing file completely
2. Infer the channel from the file type and content:
   - HTML with multiple sections, hero area → `landing-page`
   - HTML/JSX with very long content, FAQ, testimonials → `sales-page`
   - Short text, subject line present → `email`
   - Very short (under 500 chars), hashtags, casual → `social`
   - Extremely compressed, headline + description format → `ad-copy`
3. **Skip** the channel question and product context question
4. Ask only Question 1 (vibe) and Question 2 (intent)
5. Proceed to routing

### GENERATE Mode

**Triggered when:** No existing file is found. User is starting fresh.

**Behavior:**
1. Ask all four questions in order
2. Proceed to routing

---

## User Questions

Present these as simple choices. No jargon. No explanations of frameworks or methodologies.

### Question 1 — "Pick a vibe"

Ask: **"What vibe fits your brand?"**

| User Choice | Loads |
|-------------|-------|
| Clean and confident | `tones/clean-confident.md` |
| Raw and motivational | `tones/raw-motivational.md` |
| Weird and unhinged | `tones/weird-unhinged.md` |
| Warm and mission-driven | `tones/warm-mission-driven.md` |
| Witty and self-aware | `tones/witty-self-aware.md` |
| Friendly and helpful | `tones/friendly-helpful.md` |
| Playful and human | `tones/playful-human.md` |
| Technical and precise | `tones/technical-precise.md` |

### Question 2 — "What should your copy do?"

Ask: **"What should your copy do?"**

| User Choice | Loads |
|-------------|-------|
| Make them feel the pain | `frameworks/feel-the-pain.md` |
| Walk them through a transformation | `frameworks/transformation.md` |
| Build urgency step by step | `frameworks/build-urgency.md` |
| Lead with what they get | `frameworks/lead-with-value.md` |
| Paint the dream, then prove it | `frameworks/dream-then-prove.md` |
| Educate then sell | `frameworks/awareness-to-action.md` |

### Question 3 — "What are you building?" (GENERATE mode only)

Ask: **"What are you writing copy for?"**

| User Choice | Loads |
|-------------|-------|
| Landing page | `channels/landing-page.md` |
| Email | `channels/email.md` |
| Social post | `channels/social.md` |
| Ad copy | `channels/ad-copy.md` |
| Sales page | `channels/sales-page.md` |
| Cold outreach | `channels/cold-outreach.md` |

### Question 4 — "Tell me about your product" (GENERATE mode only)

Ask: **"Tell me about your product — what is it, who is it for, and what problem does it solve?"**

Capture the user's free-text response. This becomes the product context used throughout generation.

---

## Routing

After all questions are answered:

1. **Read** the selected framework file
2. **Read** the selected tone file
3. **Read** the selected channel file
4. **Combine** all three into a single generation/rewrite instruction
5. **Apply** the Universal Quality Rules (below) to all output

### Combination Logic

The three files layer as follows:
- **Framework** dictates structure — which beats appear, in what order, how they connect
- **Tone** dictates voice — sentence patterns, vocabulary, punctuation, anti-patterns to avoid
- **Channel** dictates format — length, section count, CTA placement, proof types, reading behavior

When instructions conflict:
- Channel format constraints override framework section counts (compress beats if needed)
- Tone anti-patterns are absolute — never violate them regardless of framework
- Framework beats are required — all must be represented, even if compressed

---

## Universal Quality Rules

Apply these to EVERY output, regardless of framework/tone/channel combination. These are non-negotiable.

### 1. Claude-ism Blocklist

**Principle (Hopkins):** Specificity beats persuasion.

After generating or rewriting, scan the output for these words. If any appear, replace them with specific claims:

**Blocklist:**
- revolutionize, revolutionary
- seamlessly, seamless
- elevate, elevated
- cutting-edge
- innovative, innovation
- unlock, unlocking
- leverage, leveraging
- streamline, streamlined
- game-changer, game-changing
- state-of-the-art
- next level, next-level
- empower, empowering
- robust
- holistic
- synergy, synergistic
- paradigm
- disrupt, disruptive
- transform, transformation (when vague — specific transformations are fine)
- drive, driving (when vague — "drive results" bad, "drive 40% more signups" fine)
- foster
- harness, harnessing
- optimize, optimization (when vague)
- spearhead
- facilitate
- scalable (unless discussing actual technical scaling)
- actionable
- impactful
- best-in-class
- world-class
- end-to-end
- turnkey
- stakeholder
- ecosystem (unless literally about ecosystems)
- deep dive
- move the needle
- low-hanging fruit
- circle back
- take it offline
- boil the ocean
- north star
- bleeding edge
- future-proof
- mission-critical
- pain point (when generic — specific pains are fine)
- value proposition (when generic)
- thought leader, thought leadership
- bandwidth (when not about actual bandwidth)
- touchpoint
- deliverable
- wheelhouse
- supercharge
- skyrocket
- turbocharge
- take your X to the next level
- reimagine, reimagining
- curate, curated
- bespoke
- artisanal (for non-physical products)
- frictionless
- at the end of the day
- it goes without saying
- needless to say

**Replacement rule:** For each blocked word, ask "what specifically?" and write that instead.

### 2. Headline-First Generation

**Principle (Halbert):** Headlines carry disproportionate value.

**Process:**
1. Write the hero headline BEFORE any body copy
2. Test the headline: Could this headline appear on a competitor's site unchanged?
3. If yes → too generic. Rewrite before proceeding.
4. The headline must do ONE of these:
   - Name the reader's specific situation ("For developers who hate writing docs")
   - Make a claim only this product can make ("The only CRM that updates itself")
   - State a specific, surprising outcome ("Cut your email time by 73%")

**Never proceed with body copy until the headline passes.**

### 3. Feature → Benefit Translation

**Principle (Bly):** Benefits outrank features.

**Process:**
For every feature mentioned, internally complete this sentence: "[Feature], which means [benefit for the reader]."

Write the benefit. The feature can stay, but the benefit must be explicit.

**Examples:**
- Feature: "AI-powered analysis" → Benefit: "Get answers in seconds instead of hours of manual review"
- Feature: "Real-time sync" → Benefit: "Your team always sees the latest version — no more 'which file is current?' messages"
- Feature: "One-click export" → Benefit: "Send reports to clients without reformatting anything"

### 4. Momentum Mandate

**Principle (Sugarman):** Every sentence must get the next one read.

**Rules:**
- No section ends at a dead stop
- Every section ends with forward motion:
  - A question that demands an answer
  - A tension that needs resolution
  - A reason to keep scrolling
  - A "but" or "and" that implies more coming

**Test:** Read the last sentence of each section. If it feels like a conclusion, restructure.

**Bad:** "That's why we built ProductName."
**Good:** "That's why we built ProductName. Here's how it works."

**Bad:** "Our customers love us."
**Good:** "Our customers love us — but don't take our word for it."

### 5. Emotion + Logic Balance

**Principle (Sugarman):** Emotion opens, logic justifies.

**Every output must contain BOTH:**

**Emotional register (at least one):**
- Pain acknowledgment ("You've wasted hours on...")
- Aspiration ("Imagine if...")
- Identity ("You're the kind of person who...")
- Recognition ("I feel seen" moment)
- Relief ("Finally, something that...")

**Logical register (at least one):**
- Numbers ("47% faster", "10,000 users")
- Comparisons ("Unlike X, this does Y")
- Mechanism ("Here's how it works")
- Specifics ("Built with [specific technology] for [specific reason]")
- Proof points (testimonials, case studies, data)

**If either register is absent, the output is incomplete. Add what's missing.**

### 6. Post-Output Validation Checklist

**Principle (Halbert):** Discipline, not inspiration.

Before delivering the final output, verify:

- [ ] **Claude-ism check:** No blocked words remain. Each has been replaced with specifics.
- [ ] **Headline test:** Hero headline is product-specific. Fails the "competitor's site" test.
- [ ] **Emotional register:** At least one emotional hook is present.
- [ ] **Logical register:** At least one proof/logic point is present.
- [ ] **Benefit check:** Every feature has a stated benefit.
- [ ] **Momentum check:** No sections end at dead stops.
- [ ] **Framework beats:** All required beats from the framework are represented.
- [ ] **Tone anti-patterns:** None of the tone's forbidden patterns appear.

**If any check fails, fix it before delivering.**

---

## Rewrite Mode: Post-Delivery Follow-Up

After delivering a rewrite in REWRITE mode:

1. Compare the original's sections against the framework's required beats
2. Identify any sections that don't serve a beat (filler, redundant, off-structure)
3. If dead-weight sections exist, offer:

**"Want a tighter version?"**

- If **yes:** Deliver a second version with dead-weight sections cut or merged. Every remaining section must serve a framework beat.
- If **no:** Keep the first rewrite as-is.

**This is a single yes/no question. Not a section-by-section negotiation.**

---

## Output Format

### For Landing Pages and Sales Pages

```
# [Hero Headline]

[Hero subheadline — one sentence that expands the headline]

[CTA Button Text]

---

## [Section 1 Heading — maps to framework beat]

[Section content]

---

## [Section 2 Heading — maps to framework beat]

[Section content]

[Mid-page CTA if required by channel]

---

[Continue for all beats]

---

## [Final Section]

[Final content]

[Bottom CTA]
```

### For Emails

```
**Subject:** [Subject line]
**Preview:** [First 90 characters / preview text]

[Email body — flows as one piece, no section headers]

[CTA link text]

[Sign-off if appropriate]
```

### For Social Posts

```
[Hook line — this is everything]

[Body — 1-3 sentences max]

[CTA — question or invitation]

[Hashtags if appropriate for platform]
```

### For Ad Copy

```
**Headline:** [5-15 words]
**Description:** [15-40 words including CTA]
```

---

## File Loading Reference

When the user makes their selections, load these files:

**Frameworks:**
- `frameworks/feel-the-pain.md` — PAS structure
- `frameworks/transformation.md` — BAB structure
- `frameworks/build-urgency.md` — AIDA structure
- `frameworks/lead-with-value.md` — FAB structure
- `frameworks/dream-then-prove.md` — 4Ps structure
- `frameworks/awareness-to-action.md` — ACCA structure

**Tones:**
- `tones/clean-confident.md` — Apple voice
- `tones/raw-motivational.md` — Nike voice
- `tones/weird-unhinged.md` — Liquid Death voice
- `tones/warm-mission-driven.md` — Patagonia voice
- `tones/witty-self-aware.md` — Oatly voice
- `tones/friendly-helpful.md` — Mailchimp voice
- `tones/playful-human.md` — Innocent voice
- `tones/technical-precise.md` — Stripe voice

**Channels:**
- `channels/landing-page.md` — Scroll-based, 500-1500 words
- `channels/email.md` — Single column, 150-400 words
- `channels/social.md` — 50-500 characters
- `channels/ad-copy.md` — Headline + description
- `channels/sales-page.md` — Long-form, 1500-4000 words
- `channels/cold-outreach.md` — Personalized, 50-150 words

---

## Example Flow

### GENERATE Mode Example

**Claude:** What vibe fits your brand?
- Clean and confident
- Raw and motivational
- Weird and unhinged
- Warm and mission-driven
- Witty and self-aware
- Friendly and helpful
- Playful and human
- Technical and precise

**User:** Witty and self-aware

**Claude:** What should your copy do?
- Make them feel the pain
- Walk them through a transformation
- Build urgency step by step
- Lead with what they get
- Paint the dream, then prove it
- Educate then sell

**User:** Make them feel the pain

**Claude:** What are you writing copy for?
- Landing page
- Email
- Social post
- Ad copy
- Sales page
- Cold outreach

**User:** Landing page

**Claude:** Tell me about your product — what is it, who is it for, and what problem does it solve?

**User:** It's a browser extension for freelance designers that automatically generates invoices from their Figma time tracking. Designers hate doing invoices and often bill less than they should because they forget hours.

**Claude:** [Loads tones/witty-self-aware.md, frameworks/feel-the-pain.md, channels/landing-page.md, combines them, generates copy, validates against all quality rules, delivers]

### REWRITE Mode Example

**Claude:** [Detects existing landing-page.html in /mnt/user-data/outputs/]

I found your landing page. I'll rewrite it. Two quick questions:

What vibe fits your brand?
- Clean and confident
- Raw and motivational
- Weird and unhinged
- Warm and mission-driven
- Witty and self-aware
- Friendly and helpful
- Playful and human
- Technical and precise

**User:** Clean and confident

**Claude:** What should your copy do?
- Make them feel the pain
- Walk them through a transformation
- Build urgency step by step
- Lead with what they get
- Paint the dream, then prove it
- Educate then sell

**User:** Lead with what they get

**Claude:** [Loads tones/clean-confident.md, frameworks/lead-with-value.md, channels/landing-page.md (inferred), reads existing file, combines instructions, rewrites, validates, delivers]

Your sections on "Our Story" and "Meet the Team" don't serve the framework's beats. Want a tighter version?

**User:** Yes

**Claude:** [Delivers second version with those sections cut/merged]
