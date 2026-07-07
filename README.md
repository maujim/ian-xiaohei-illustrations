# Ian Xiaohei Illustrations

A minimal Codex Skill for generating sparse Xiaohei-style article graphics with Google's Nano Banana 2 Lite image model (`gemini-3.1-flash-lite-image`).

The skill turns one judgment, workflow, structure, state, or metaphor from an English article into a 16:9 hand-drawn explanatory image: pure white background, thin black line art, lots of whitespace, one serious absurd Xiaohei character doing the core action, and a few short English handwritten labels in black with restrained red/orange/blue accents.

## Model and API

Use the Gemini Interactions API directly:

- Endpoint: `https://generativelanguage.googleapis.com/v1beta/interactions`
- Model: `gemini-3.1-flash-lite-image`
- Auth header: `x-goog-api-key: $GEMINI_API_KEY`
- Default response format: JPEG, `16:9`; Lite returns 1K output by default
- Generated image data: base64 in `interaction.output_image.data`
- Storage: send `"store": false` for stateless one-shot generations

Nano Banana 2 Lite is chosen because it is Google's fast, low-cost Gemini image model for high-volume generation and editing. It supports text and image inputs, image generation/editing, and 16:9 output; it does not support Google Search grounding. Generated images include SynthID watermarking.

## Install as a Codex Skill

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R ./ian-xiaohei-illustrations "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Provide an API key in your environment or local `.env` file:

```bash
GEMINI_API_KEY=your-key-here
```

Do not commit `.env`.

## Use

```text
Use $ian-xiaohei-illustrations to generate 5 Xiaohei article graphics for this English article.

<paste article>
```

```text
Use $ian-xiaohei-illustrations to generate one Xiaohei article graphic for this point:

Trust is not declared out loud; it is laid down piece by piece with evidence.
```

## Preferred curl method

Use curl for basic one-shot generations because it needs no package install or helper code:

```bash
curl -s -X POST \
  "https://generativelanguage.googleapis.com/v1beta/interactions" \
  -H "x-goog-api-key: $GEMINI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3.1-flash-lite-image",
    "store": false,
    "input": [
      {"type": "text", "text": "<full Xiaohei prompt>"}
    ],
    "response_format": {
      "type": "image",
      "mime_type": "image/jpeg",
      "aspect_ratio": "16:9"
    }
  }'
```

Decode `interaction.output_image.data` from base64 and save it as `outputs/<english-slug>/01-topic.jpg`.

## Python SDK method

Use Python when it is more convenient to decode and save images programmatically, generate many images, or include image inputs for editing.

Install the SDK only if it is not already available:

```bash
uv pip install google-genai
```

```python
import base64
from pathlib import Path
from google import genai

client = genai.Client()

prompt = "<full Xiaohei prompt>"
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

## Sample images

The repo includes five small Nano Banana 2 Lite-generated samples under `ian-xiaohei-illustrations/assets/samples/`:

- `01-evidence-bridge.jpg`
- `02-idea-filter-machine.jpg`
- `03-context-ladder.jpg`
- `04-feedback-compass.jpg`
- `05-one-page-factory.jpg`

Send one or two of these sample images alongside a prompt only when a visual reference is useful. Do not send the whole sample set by default, and do not copy a sample composition exactly.

## Style contract

- 16:9 horizontal article graphic.
- Pure white background; no paper texture, gradients, shadows, or complex scene.
- Minimal black hand-drawn line art with slightly wobbly thin strokes.
- Xiaohei is a small solid-black absurd creature with white dot eyes, tiny thin legs, and a blank serious expression.
- Xiaohei must perform the core conceptual action, not stand beside the diagram.
- Use at most 5 short English handwritten labels.
- Orange only for main flow/path/arrows; red only for key warnings/problems/results; blue only for secondary notes or system state.
- Do not create PPT infographics, course slides, formal flowcharts, cute mascot art, UI screenshots, or dense explainers.

## Output convention

Save generated files under `outputs/<english-slug>/`:

```text
outputs/<english-slug>/01-topic.jpg
outputs/<english-slug>/02-topic.jpg
```

Generated outputs are local files and are ignored by git. The only tracked images are the five sample references in the skill directory.
