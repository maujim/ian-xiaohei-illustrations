# Ian Xiaohei Illustrations

> Turn the judgments, workflows, states, and metaphors in English articles into sparse, hand-drawn, absurd yet clean in-article illustrations on a white background.
>
> 16:9 landscape | Xiaohei IP | pure white hand-drawn style | a few red, orange, and blue handwritten English annotations | Codex Skill

---

## What this repository is

Ian Xiaohei Illustrations is a Codex Skill that guides AI Agents to generate in-article illustrations for English articles, posts, blogs, Notion documents, and methodology content.

It is not a generic illustration prompt or a PPT infographic template. Its core goal is to first understand the cognitive anchors in an article, then turn one judgment, workflow, structure, state, or metaphor into a memorable 16:9 hand-drawn explanatory image.

The default visual IP is "Xiaohei": a small character with a solid black body, white dot eyes, thin legs, and a blank expression. Xiaohei is not a mascot, sticker, or decorative figure standing in the corner; Xiaohei is an absurd worker seriously taking part in the system's operation.

In one sentence: **AI should do more than "add an image"; it should draw a key cognitive action from the article.**

---

## Who it is for

Best for:

- People writing English articles who need in-article images and article illustrations
- People creating knowledge content, methodology content, or AI workflow content
- People who want to turn abstract judgments into concrete metaphors
- People who want an illustration style that is lighter, stranger, and more personally recognizable than PPT infographics
- People using Codex for content production who want to reliably reuse one visual language

Not for:

- People who want commercial illustrations, brand key visuals, or polished flat illustrations
- People who want traditional PPT infographics, complex architecture diagrams, or flowcharts
- People who want children's cartoons, cute IP characters, or meme-style images
- People who want to cram large amounts of body text, long explanations, or a full course page into one image
- People who need strictly editable vector source files

---

## What it produces

Default outputs:

- 16:9 landscape in-article illustrations
- A 4-8 image shot list for an article
- The topic, core meaning, structure type, Xiaohei action, and suggested English label text for each image
- Final PNG images saved in the workspace under `assets/<english-article-slug>-illustrations/`

Default non-outputs:

- PPTX / PDF / Keynote
- SVG / HTML / Canvas editable images
- Commercial posters or cover key visuals
- Text-heavy infographics

---

## Visual style

This skill uses Ian's "Xiaohei absurd in-article illustration" style by default:

- Pure white background; no paper texture, beige tone, shadow, or gradient
- Black hand-drawn line art, thin lines, slight wobble
- Lots of white space, with the subject occupying only about 40%-60% of the frame
- A few red, orange, and blue handwritten English annotations
- One image expresses only one core action, structure, state, or metaphor
- Xiaohei must take part in the core action and cannot be merely decorative
- Absurd, creative, and clean, but not childish or cute

---

## Example results

### Two Breakpoints

![Two Breakpoints](examples/images/01-two-breakpoints.png)

### Sort by Purpose

![Sort by Purpose](examples/images/02-sort-by-purpose.png)

### One Fish, Many Uses

![One Fish, Many Uses](examples/images/03-one-fish-many-uses.png)

### Handoff Path

![Handoff Path](examples/images/04-handoff-path.png)

### Information Well

![Information Well](examples/images/05-information-well.png)

### Idea Press

![Idea Press](examples/images/06-idea-press.png)

### Content Fermentation

![Content Fermentation](examples/images/07-content-fermentation.png)

### Trust Bridge

![Trust Bridge](examples/images/08-trust-bridge.png)

These images are style calibration samples, not composition templates. When using the skill, reinvent the metaphor from the current article instead of copying the objects or compositions from old examples.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/helloianneo/ian-xiaohei-illustrations.git
cd ian-xiaohei-illustrations
```

Copy the skill to the Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R ./ian-xiaohei-illustrations "${CODEX_HOME:-$HOME/.codex}/skills/"
```

After installation, use it in Codex:

```text
Use $ian-xiaohei-illustrations to design and generate 5 absurd Xiaohei in-article illustrations for this English article.
```

---

## How to use

### Plan illustrations only

```text
Use $ian-xiaohei-illustrations. Do not generate images yet.
Please analyze which parts of the article below are worth illustrating, and output a shot list of about 5 images.
For each image, clearly state where it should appear, its topic, core meaning, structure type, what Xiaohei is doing, and the suggested English label text.

<Paste article>
```

### Generate in-article illustrations directly

```text
Use $ian-xiaohei-illustrations to generate 4 absurd Xiaohei in-article illustrations for the article below.
Requirements: 16:9 landscape, pure white background, black hand-drawn line art, and a few red, orange, and blue handwritten English annotations.

<Paste article>
```

### Generate one image for a single concept

```text
Use $ian-xiaohei-illustrations to generate one in-article illustration for "Trust is not shouted into existence; it is paved piece by piece with evidence."
The image should be absurd but clean, and Xiaohei must carry the core action.
```

### Remove a title or incorrect text from an image

```text
Use $ian-xiaohei-illustrations to help me edit this image: remove the "flowchart" title in the upper-left corner and keep everything else unchanged.
```

See more examples in [examples/prompts.md](examples/prompts.md).

---

## Workflow

The skill's workflow is:

1. Read the article, Markdown, Notion content, screenshot, or topic provided by the user
2. Extract the core ideas, cognitive turns, workflow structures, and paragraphs suitable for visualization
3. First output a shot list: choose only one cognitive anchor for each image
4. Choose a structure type for each image: Workflow, system detail, before-and-after contrast, character state, conceptual metaphor, method layers, map route, or small comic storyboard
5. Reinvent a low-tech, absurd but coherent physical metaphor
6. Make Xiaohei carry the core action
7. Call the image model separately for each image
8. Check against the QA checklist: white background, white space, Xiaohei's action, English annotations, non-PPT feel, and not a remake of an old example
9. Save the final PNG files, and report their uses and paths

---

## Directory structure

```text
.
├── README.md
├── LICENSE
├── NOTICE.md
├── assets/
│   └── ian-wechat-qr.jpg
├── examples/
│   ├── images/
│   │   ├── 01-two-breakpoints.png
│   │   ├── 02-sort-by-purpose.png
│   │   └── ...
│   └── prompts.md
└── ian-xiaohei-illustrations/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    │   └── examples/
    └── references/
        ├── style-dna.md
        ├── xiaohei-ip.md
        ├── composition-patterns.md
        ├── prompt-template.md
        └── qa-checklist.md
```

The subdirectory that actually needs to be installed into Codex is:

```text
ian-xiaohei-illustrations/
```

The root README, LICENSE, NOTICE, and examples are GitHub sharing documents.

---

## Notes

- The shorter the English text inside an image, the more stable the result.
- Each image should explain only one core structure; do not turn the article into a manual.
- Xiaohei must carry the core action. If the image still works perfectly after removing Xiaohei, Xiaohei is too decorative.
- Example images are only for calibrating line density, white space, color restraint, and Xiaohei's participation. Do not replicate their compositions.
- AI image models may produce typos, hallucinated labels, style drift, or extra titles, so each generated image must be checked afterward.
- If English typos are severe, reduce the annotation words first and regenerate.

---

## Related projects

- [Ian Handdrawn PPT](https://github.com/helloianneo/ian-handdrawn-ppt) — Skill for generating hand-drawn technical PPT-style page images with English labels
- [Awesome Claude Code Skills](https://github.com/helloianneo/awesome-claude-code-skills) — Curated collection of Claude Code Skills / Agents / Plugins
- [Obsidian + Claude AI Second Brain](https://github.com/helloianneo/obsidian-ai-second-brain) — Guide to building a personal knowledge base with Obsidian + Claude AI

---

## About the author

**Ian** — Product designer / one-person company practitioner / AI Builder

Building a one-person company with an AI team.

- GitHub: [helloianneo](https://github.com/helloianneo)
- X/Twitter: [@ianneo_ai](https://x.com/ianneo_ai)
- Website: [www.ianneo.xyz](https://www.ianneo.xyz)
- WeChat: `ianneoxyz`
- Email: hello.neoc@gmail.com

---

## Keep exploring

This Xiaohei illustration Skill is just one small tool in the personal production system I am building with AI.

If you also use AI for content, knowledge bases, workflows, or productization, you can keep reading on my website: [www.ianneo.xyz](https://www.ianneo.xyz).

If you only want to observe for now, follow me on [X/Twitter](https://x.com/ianneo_ai).

To learn about Indie Builders Club, add me on WeChat: `ianneoxyz`, and mention "OPC".

<p>
  <img src="assets/ian-wechat-qr.jpg" alt="Ian WeChat QR code" width="120">
</p>

If scanning the QR code is inconvenient, you can also search WeChat for `ianneoxyz`.

---

## License

MIT License. See [LICENSE](LICENSE).
