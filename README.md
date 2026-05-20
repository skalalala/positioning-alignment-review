# positioning-alignment-review
A Claude Skill for marketers who need to check whether a marketing draft actually matches the product’s internal messaging and positioning brief.

## What it does

Give it a draft marketing asset and the relevant positioning brief. It compares the public-facing copy against the internal source of truth and shows where the draft is aligned, weak, missing, unsupported, or off-brief.

It helps marketers:

- Extract the core positioning, audience, value pillars, differentiators, proof points, and approved language from a brief
- Review landing pages, launch blogs, GTM posts, press releases, executive posts, campaign copy, and related assets
- Compare draft passages directly against the source messaging
- Flag missing messages, weak emphasis, audience drift, category drift, unsupported claims, and terminology drift
- Suggest focused fixes without rewriting the whole asset unnecessarily

## Why this exists

Marketing drafts often sound polished before they are actually on-message.

A landing page, launch blog, press release, or LinkedIn post can read well while still missing the product’s core value proposition, skipping proof points, using outdated language, or emphasizing the wrong benefit. In fast-moving launches, that review often happens manually across product marketing, content, brand, legal, and leadership feedback.

This skill gives marketers a structured first-pass review before stakeholder review. It does not replace strategic, legal, compliance, or product review. It gives the marketer a practical positioning diff: what the brief says, what the draft says, and what needs to change.

## What this skill is opinionated about

1. **Brand alignment is not the same as tone.** A draft can sound polished and still fail to communicate the intended positioning.
2. **Missing messages are as important as incorrect messages.** Omissions, weak emphasis, and buried proof points can make otherwise good copy underperform.
3. **Feedback should be tied to evidence.** Every major alignment or misalignment should point back to language from the draft and the source brief.
4. **The best first fix is usually focus, not a full rewrite.** The skill recommends targeted additions, cuts, swaps, and reframes before rewriting the asset from scratch.

## Repository structure

```text
positioning-alignment-review/
├── README.md
├── SKILL.md
└── examples/
    ├── example-input.md
    └── example-output.md
```

`SKILL.md` is the actual Claude Skill file. The examples show the expected input style and the kind of review the skill should return.

## Requirements

- A Claude environment that supports custom Skills
- A top-level `SKILL.md` file in this skill folder
- A draft marketing document
- An internal messaging and positioning brief for the relevant product, campaign, or announcement

Recommended input formats:

- Markdown
- Plain text
- Copied/pasted Google Doc or Notion text
- Exported text from a landing page, blog post, press release, or campaign brief

The skill can still work with partial inputs, but the review will be less confident if the brief is thin or the draft is incomplete.

## Install

Clone this repository into your local Claude Code skills directory.

```bash
git clone https://github.com/skalalala/positioning-alignment-review ~/.claude/skills/positioning-alignment-review
```

Restart Claude so it can detect the new skill.

Anthropic’s Agent Skills format requires a `SKILL.md` file at the top level of the skill folder with YAML frontmatter containing a `name` and `description`.

## Usage

Ask Claude to use the skill, then provide both inputs.

```text
Use the positioning-alignment-review skill to review this landing page draft against the positioning brief below.
```

Then paste or attach:

1. The draft marketing asset
2. The internal messaging and positioning brief

You can also include optional supporting context, such as:

- Brand voice guidelines
- ICP or audience notes
- Claims, legal, or compliance guidance
- Product one-pagers
- Conversion goal or funnel stage
- Competitor positioning notes
- Terms or claims to avoid

## Inputs

| Input | Required? | Description |
|---|---:|---|
| Draft marketing asset | Yes | The public-facing asset being reviewed, such as a landing page, blog post, press release, LinkedIn post, or campaign draft. |
| Messaging and positioning brief | Yes | The internal source-of-truth document containing product positioning, audience, value pillars, differentiators, proof points, and approved language. |
| Brand voice guidelines | No | Tone, style, editorial, and brand rules. Useful, but secondary to positioning alignment. |
| Claims or compliance guidance | No | Rules for what the draft can or cannot say. Useful for regulated or high-stakes categories. |
| ICP or audience notes | No | Additional context about who the draft should speak to. |
| Conversion goal | No | The intended action or business goal of the asset. |

## Output

The skill returns a structured review with:

| Output | Description |
|---|---|
| Quick verdict | Overall alignment score, review status, and the most important fix. |
| Inputs reviewed | What materials were reviewed and what context was missing. |
| Positioning map | Extracted source-of-truth messages from the brief, labeled with IDs. |
| Pillar-by-pillar alignment | A comparison of each key positioning item against the draft. |
| Evidence table | Specific draft passages matched against relevant brief passages. |
| Misalignment and omission flags | Prioritized notes on missing, weak, unsupported, contradictory, or off-brief language. |
| Suggested fixes | Focused recommendations for improving alignment without rewriting the whole asset. |
| Stakeholder-readiness note | Whether the draft is ready for product, brand, legal, leadership, or other stakeholder review. |
| Confidence note | A short explanation of how complete or limited the review is based on the inputs. |

## Alignment scoring

The skill uses a directional 0–100 score. It is not a benchmark or scientific measure. It is a structured way to indicate how much work the draft needs before stakeholder review.

Default weighting:

| Area | Weight |
|---|---:|
| Core positioning and category framing | 25 |
| Audience and use-case fit | 15 |
| Value pillars | 25 |
| Proof points and substantiation | 15 |
| Differentiation | 10 |
| Approved language and terminology | 10 |

## Example use case

A product marketer is preparing a landing page for an upcoming launch. The draft is readable, but before sending it to product and leadership, they want to check whether it reflects the approved positioning.

They run this skill with the landing page draft and the internal messaging brief. The skill identifies that the page includes the main value proposition, but underplays two differentiators, omits a key proof point, and uses language that makes the product sound broader than intended.

The marketer uses the review to tighten the page before stakeholder feedback begins.

See:

- [`examples/example-input.md`](examples/example-input.md)
- [`examples/example-output.md`](examples/example-output.md)

## What this skill does not do

- It does not replace legal, brand, product, compliance, or leadership review.
- It does not decide whether the underlying positioning strategy is correct.
- It does not rewrite the entire asset unless explicitly asked.
- It does not publish, edit, or update live content.
- It does not verify claims against external sources unless additional research inputs are provided.
- It does not invent proof points, metrics, customer names, or technical claims that are not present in the source materials.

## MVP design notes

This MVP is intentionally simple.

It does not require a database, API integration, external research workflow, or scoring dashboard. The core value comes from a repeatable review pattern:

```text
brief → positioning map → draft passage review → evidence table → prioritized fixes
```

That makes it useful as a lightweight marketing workflow skill and easy to extend later.

Possible future additions:

- Separate claim-substantiation mode
- Brand voice review mode
- Competitive positioning comparison
- JSON or CSV export for team QA workflows
- Batch review for multiple campaign assets
- Custom scoring rubrics for specific companies or product lines

## Built by

Built by Sam Kahler (@skalalala). PRs welcome.
