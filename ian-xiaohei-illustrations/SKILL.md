---
name: ian-xiaohei-illustrations
description: Generate Ian-style article illustrations in English. Use this when the user asks for illustrations for articles, posts, blogs, Notion docs, workflow docs, methodologies, processes, structures, states, metaphors, viewpoints, shot lists, title removal, or image revisions in a "grotesque", "Xiaohei", "hand-drawn", "article illustration", or "illustration suggestion" style; default to the Xiaohei IP, pure white hand-drawn visuals, a few red-orange-blue annotations, and a clean, concise, wildly imaginative visual style.
---

# Ian Xiaohei Grotesque Article Illustrations

## Core Positioning

Design and generate 16:9 landscape article illustrations. The goal is not commercial illustration, PPT infographics, or cute cartoons; it is to turn the article's key judgments, processes, structures, states, or metaphors into clean, grotesque, creative, readable hand-drawn explanatory images that do not feel like instruction manuals.

The default visual IP is "Xiaohei": a solid black figure with white dot eyes, thin legs, and a blank expression, earnestly doing something absurd but coherent. Xiaohei must participate in the image's core action, not stand nearby as decoration.

## Read These References First

Read only what the task needs; do not load all of them into context at once:

- `references/style-dna.md`: style DNA, colors, text, and prohibitions.
- `references/xiaohei-ip.md`: Xiaohei IP appearance, personality, action library, and prohibitions.
- `references/composition-patterns.md`: structure types, original metaphor methods, and anti-repetition rules.
- `references/prompt-template.md`: prompt template for a single generated image.
- `references/qa-checklist.md`: post-generation checks and iteration rules.
- `assets/examples/`: use only for low-frequency visual calibration, not in the default generation path. Do not copy the compositions, objects, or labels from these examples.

## Workflow

### 1. Digest the Article

First read the user's article, link, Notion page, Markdown file, or screenshot content. Extract:

- What the core argument is
- Which paragraphs carry cognitive turns
- Which content is suitable to explain with an image
- Which parts are better left as text and do not need an image

Do not distribute illustrations evenly. Prioritize "cognitive anchors", such as the core judgment, two breakpoints, an input-output loop, branching, before-and-after contrast, one asset used in multiple ways, a handoff path, common pitfalls, or role state changes.

### 2. Produce an Illustration Strategy First

If the user only asks to "analyze how to illustrate this / think through which parts need illustrations", provide a shot list first. For each image, state clearly:

- Which paragraph it should follow
- The image topic
- The core meaning
- The structure type
- What Xiaohei is doing in the image
- Suggested elements
- Suggested English label text

Default to 4-8 images. Use 1-3 images for a very short article; even for a long article, do not exceed 9 images lightly. Use only as many as needed, and avoid turning the article into a picture book.

### 3. Generate Individual Images

If the user explicitly asks to "generate / output / make images / help me generate", do not stop to wait for confirmation; use the built-in `image_gen` to generate each image separately. Do not combine multiple images into one.

Each image should communicate only one core structure. The prompt must include:

- 16:9 landscape English article illustration
- Pure white background
- Black hand-drawn line art
- A few red/orange/blue handwritten English annotations
- Lots of white space
- Xiaohei as the core action subject
- No PPT style, commercial illustration, childish cuteness, complex architecture, or type title in the upper-left corner

Do not reproduce past examples. Examples only provide style density and ways for Xiaohei to participate; do not directly reuse existing compositions such as "conveyor-belt breakpoint / Xiaohei pulling a wire / asset fish / stamped toolbox / common-pitfall path" unless the user explicitly asks to reproduce a specific image. Every time, reinvent a strange but coherent metaphor from the current article.

### 4. Check and Iterate

After generation, check `references/qa-checklist.md`. If any of the following problems appear, prioritize regenerating or locally editing:

- Xiaohei is only decorative
- The image is too crowded
- It looks too much like a flowchart/PPT
- There is too much English text or serious misspelling
- A title such as "Common Pitfalls / Flowchart / System Architecture" appears in the upper-left corner
- The style is too cute, childish, or rigid
- The background is not clean white

### 5. Save the Deliverables

If the user is working inside the workspace, copy the final images to an English-slug output path:

```text
assets/<english-article-slug>-illustrations/
```

Name them in order with English topic filenames:

```text
01-english-topic-name.png
02-english-topic-name.png
```

Keep the original generated files. Do not overwrite existing assets unless the user explicitly asks for replacement.

## Output Requirements

Strategy output before generation should be short and precise. Delivery after generation should include:

- How many images were generated
- The purpose of each image
- Save paths
- Which images are strongest and which are optional

Do not write a long explanation of style theory; let the images speak for themselves.
