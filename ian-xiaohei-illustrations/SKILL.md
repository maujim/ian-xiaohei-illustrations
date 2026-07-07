---
name: ian-xiaohei-illustrations
description: "Generate sparse English Xiaohei-style article graphics using Google Nano Banana 2 Lite (`gemini-3.1-flash-lite-image`) through the Gemini Interactions API. Use for article illustrations, conceptual metaphors, workflow graphics, shot lists, simple image revisions, and optional sample-guided generations; default to pure white hand-drawn visuals, one serious Xiaohei character doing the core action, and a few short English labels."
---

# Ian Xiaohei Illustrations

Generate 16:9 Xiaohei-style article graphics with Google's Nano Banana 2 Lite image model. Use the Gemini Interactions API directly, with curl preferred for basic one-shot generations and Python available for multi-image runs, decoding, saving, image editing, or sample-reference inputs. Do not use any built-in image-generation tool for this skill.

## API contract

Use this model and endpoint for every generation unless the user explicitly asks for a different Google image model:

- Endpoint: `https://generativelanguage.googleapis.com/v1beta/interactions`
- Model: `gemini-3.1-flash-lite-image`
- API key: read `GEMINI_API_KEY` from the environment or local `.env`; never print the key.
- Response: decode base64 from `interaction.output_image.data` and save the image as `.jpg`.
- Default output: `response_format.type = "image"`, `mime_type = "image/jpeg"`, `aspect_ratio = "16:9"`; Lite returns 1K output by default.
- Default storage: include `"store": false` so one-shot generations are stateless.

## Preferred curl method

Use curl for basic one-shot generations because it needs no package install:

```bash
curl -s -X POST \
  "https://generativelanguage.googleapis.com/v1beta/interactions" \
  -H "x-goog-api-key: $GEMINI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.1-flash-lite-image",
    "store": false,
    "input": [
      {"type": "text", "text": "<full prompt>"}
    ],
    "response_format": {
      "type": "image",
      "mime_type": "image/jpeg",
      "aspect_ratio": "16:9"
    }
  }'
```

Decode `interaction.output_image.data` from the JSON response and save it as a `.jpg`.

## Python SDK method

Use Python when you need to decode/save files in code, loop over many prompts, or include image inputs for editing/reference. Install the SDK only if needed:

```bash
uv pip install google-genai
```

```python
import base64
from pathlib import Path
from google import genai

client = genai.Client()

prompt = "<full prompt>"
interaction = client.interactions.create(
    model="gemini-3.1-flash-lite-image",
    input=[{"type": "text", "text": prompt}],
    response_format={
        "type": "image",
        "mime_type": "image/jpeg",
        "aspect_ratio": "16:9",
    },
    store=False,
)

out = Path("outputs/<english-slug>/01-topic.jpg")
out.parent.mkdir(parents=True, exist_ok=True)
out.write_bytes(base64.b64decode(interaction.output_image.data))
print(out)
```

For image editing or optional sample-reference generation, include one source image as an additional input block after the text instruction:

```python
{
    "type": "image",
    "mime_type": "image/jpeg",
    "data": "<base64 image bytes>",
}
```

Nano Banana 2 Lite supports image generation and editing, but it is not optimized for many reference images or long multi-turn sequential editing. It does not support Google Search grounding. Do not add Google Search tools while using this model. Use at most one or two sample images as visual references; do not attach the entire sample directory by default.

If `interaction.output_image.data` is absent, inspect `interaction.steps` and save the first image content block with base64 data. If no image data exists, report the API response error; do not silently switch models.

## Sample references

Five Lite-generated samples live in `assets/samples/` inside this skill:

- `assets/samples/01-evidence-bridge.jpg`
- `assets/samples/02-idea-filter-machine.jpg`
- `assets/samples/03-context-ladder.jpg`
- `assets/samples/04-feedback-compass.jpg`
- `assets/samples/05-one-page-factory.jpg`

Use these samples only for visual calibration when the prompt alone is not enough. Pick the closest one or two samples by structure, send them as image input blocks with the text prompt, and explicitly tell the model to follow the style density and Xiaohei treatment without copying the exact composition.

## Workflow

1. Read the user's article, topic, Markdown, link summary, screenshot text, or image-edit request.
2. Identify cognitive anchors: the core judgment, a workflow transition, a before/after contrast, an input-output loop, a failure point, a handoff, a role state, or a concrete metaphor.
3. If the user asks for planning only, return a short shot list. For each image include: placement, topic, core idea, structure type, Xiaohei action, key objects, and suggested English labels.
4. If the user asks to generate images, create one image per anchor. Default to 4-8 images for a full article, 1-3 images for a short article or a single concept, and never exceed 9 images unless the user explicitly asks.
5. Build one full prompt per image using the template below.
6. Call the Gemini Interactions API once per image. Prefer curl for a single/basic image; use Python for loops, decoding, saving, editing inputs, or sample-reference inputs. Do not combine multiple images into one canvas.
7. Save outputs under `outputs/<english-slug>/` with ordered English filenames, for example `outputs/trust-building/01-evidence-bridge.jpg`.
8. Inspect each image before reporting paths. Regenerate once if it violates a must-pass style rule.

## Prompt template

Use this template for every text-to-image request. Replace bracketed fields with specifics from the article; keep the fixed style clauses.

```text
Generate one standalone 16:9 horizontal English article graphic.

Visual DNA:
Pure white background. Minimalist black hand-drawn line art. Thin slightly wobbly pen lines. Lots of empty white space. Sparse red, orange, and blue handwritten English annotations. Clean absurd product-sketch feeling. No gradients, no shadows, no paper texture, no complex background, no commercial vector style, no PPT infographic look, no cute mascot poster, no children's illustration, no realistic UI.

Recurring character:
Xiaohei, a small solid-black absurd creature with white dot eyes, tiny thin legs, blank serious expression, and a slightly uneven hand-drawn body. Xiaohei must perform the core conceptual action, not decorate the scene. Make Xiaohei serious, deadpan, and slightly bizarre, not cute.

Theme:
[image topic]

Structure type:
[Workflow / System Slice / Before and After / Character State / Conceptual Metaphor / Method Layers / Map Route / Mini Comic Panels]

Core idea:
[one sentence explaining what the image should make the reader understand]

Composition:
[where Xiaohei is, what Xiaohei is doing, the main low-tech object or physical metaphor, and how information/action moves across the image]

Suggested elements:
[element 1] / [element 2] / [element 3] / [element 4]

English handwritten labels:
[label 1] / [label 2] / [label 3] / [label 4] / [optional label 5]

Color use:
Black for line art, Xiaohei, and primary labels. Orange only for the main flow/path/arrows. Red only for one key warning/problem/result. Blue only for secondary notes or feedback/system state.

Constraints:
One image explains only one core structure. Keep the main subject around 40%-60% of the canvas. Preserve at least 35% blank white space. Use at most 5 short English labels. Do not write a title in the top-left corner. Do not write the structure type on the image. Do not make it a formal diagram, course slide, dense explainer, cute cartoon, or UI screenshot. Invent a fresh low-tech metaphor for this specific article.
```

## Style rules

Must pass:

- 16:9 horizontal image.
- Pure white background.
- Mostly black hand-drawn line art.
- Xiaohei appears and performs the core action.
- The image uses one clear metaphor or structure, not several.
- English labels are few, short, readable, and not title-like.
- Orange, red, and blue are accent colors only.
- The composition is sparse, absurd, clean, and not copied from old examples.

Regenerate or locally edit if:

- Xiaohei is only decorative.
- The image looks like a PPT slide, formal flowchart, UI, or course page.
- The top-left corner contains a title such as "Workflow" or "System Diagram".
- Labels become long explanations or contain severe spelling errors.
- The image is cute, childish, polished commercial illustration, or visually crowded.
- The background has paper texture, gradients, shadows, beige, or noise.

## Metaphor rules

Use low-tech, physical metaphors. Good object families: cardboard boxes, drawers, old machines, funnels, scales, mailboxes, doors, wells, ladders, pipes, string, gates, turntables, black boxes, hole punches, noodle presses, clotheslines, and strange workstations.

Make Xiaohei do an action that explains the idea: pull, carry, stuff, fish out, press, weigh, sew, cut, twist, guard, push, catch, dismantle, mark, recycle, patch, climb, or operate. Do not make Xiaohei stand beside the structure as a mascot.
