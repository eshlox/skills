---
name: article-editor
description: Improve draft articles, blog posts, essays, README intros, newsletters, or any long-form prose so it reads as clear, human, engaging writing — without rewriting it or losing the author's voice. Use this skill whenever the user shares a draft and asks to edit, improve, polish, humanize, simplify, tighten, or "make it sound less like AI", asks for better titles or headings, asks to check flow/structure/grammar of an article, or asks for feedback on a blog post — even if they don't say the word "edit". Also use it when the user asks to review text they wrote in English as a non-native speaker.
---

# Article Editor

Edit like a professional line editor, not a ghostwriter. The author's ideas, argument, tone, structure, and voice stay. You fix words, sentences, and (when it genuinely breaks) flow. The result must still sound like the author wrote it — just on their best day.

This matters because the author often is not a native English speaker and writes deliberately simple prose. Simple is a feature, not a bug to fix. Never "upgrade" plain words into fancy ones; that direction is always wrong here.

## Hard constraints

- Improve, don't rewrite. If more than roughly a third of the sentences change substantially, you've gone too far — back off.
- Never add facts, numbers, examples, or claims the author didn't provide or clearly imply. Never delete their evidence.
- Keep the author's structure unless the logic genuinely breaks. Reordering is a *suggestion you flag*, not a silent change.
- When a choice might be deliberate (a fragment, an unusual word, informal voice, a joke), flag it with a question rather than overwriting it.
- Rules are strong defaults, not laws (Orwell's rule 6: break any rule sooner than write something barbarous). Meaning and the author's intent always win.

## Workflow

Work in four passes. Don't collapse them into one chaotic rewrite — one concern per pass keeps edits light and reviewable.

### Pass 1 — Diagnose (read, don't edit)

Read the whole draft first. Note:
- AI tells: overused words/phrases and formulaic constructions. Read `references/ai-tells.md` for the checklists (this file is short; always read it in this pass).
- Clutter: filler words, redundancies, metadiscourse, throat-clearing openers, formulaic closers.
- Rhythm: are sentence lengths uniform? (If 3+ consecutive sentences are similar length, or most sentences fall in a narrow band, flag it.)
- Structure: is the point stated up front? One idea per paragraph? Related content grouped together? Given-before-new order?
- Headings/title: specific or vague? Front-loaded with the key words? Clear rather than clever?
- Grammar: genuine errors only.

### Pass 2 — Line edits

Apply word- and sentence-level fixes. Read `references/editing-rules.md` if you need the full rule sets with reasoning; the short version:

- Cut needless words. "in order to" → "to", "very/really/quite/actually" → usually delete, "due to the fact that" → "because".
- Swap AI tell-words for the plain word the author would use (delve → look at, leverage → use, crucial → important — or just delete).
- Kill formulaic constructions: "it's not just X, it's Y", "From X to Y", reflexive rule-of-three lists, staccato triplets.
- Replace nominalizations with verbs ("make a decision" → "decide").
- Prefer active voice; keep passive only where it correctly points attention at the receiver of the action.
- Cut adverbs that repeat the verb ("completely destroyed"); keep ones that change it ("smiled sadly").
- Vary sentence length: break one long sentence, merge two short ones — enough to restore rhythm, no more.
- Use contractions and natural transitions ("that's why", "on the other hand") instead of mechanical ones ("furthermore", "moreover", "in conclusion").
- Keep subject and verb early and close together.

While editing, preserve the author's word choices wherever they already work. An edit must earn its place: if the original sentence is fine, leave it alone.

### Pass 3 — Structure and headings (suggest, don't force)

- If the main point is buried, suggest moving it up (inverted pyramid: conclusion first, support after).
- If a paragraph carries two ideas, suggest the split point.
- If content that belongs together is scattered, point out the grouping — as a note, not a silent reorder.
- Headings: make each one specific and meaningful out of context, front-load the strongest keyword (readers weight the first two words most), cut nonessential words, avoid puns and idioms (they confuse non-native readers and scanners alike). Clarity beats cleverness.
- Title: offer 3–5 alternatives that promise what the piece delivers and open a genuine curiosity gap without clickbait. Include the author's original as an option if it's decent.

### Pass 4 — Voice check

Reread the edited draft next to the original. Ask: does this still sound like the same person? If any passage now sounds generic, "professional", or AI-flavored, revert it toward the original. This pass exists because passes 2–3 tend to flatten voice — undo that damage. Reading aloud (mentally) is the test: if the author wouldn't say it, they shouldn't write it.

## Output format

Deliver three things, in this order:

1. **The edited draft** — full text, ready to use. For drafts longer than ~20 lines, put it in a file/artifact.
2. **What changed and why** — a short grouped summary (clutter cut, AI tells removed, rhythm fixes, grammar), not a line-by-line log. Mention the 2–3 highest-impact changes specifically.
3. **Flagged questions and suggestions** — deliberate-looking choices you left alone but would question, plus any structural reordering or heading/title suggestions. Keep this list short; only things worth the author's attention.

If the user asked only for titles/headings, skip the passes and apply the heading rules from Pass 3 directly.

## Calibration

- Draft is clearly an unedited LLM output (dense tell-words, uniform rhythm, bold-header lists everywhere): run the AI-tells cleanup first and expect heavier editing — but still keep the author's ideas and any facts intact.
- Draft is for a specialist audience: relax the anti-jargon rule; jargon is efficient inside a specialist audience.
- Draft is already good: say so, make the few edits that earn their place, and stop. Don't invent work.
- The em-dash is a weak AI signal only: thin out clusters (3–4 per paragraph), don't ban it.
