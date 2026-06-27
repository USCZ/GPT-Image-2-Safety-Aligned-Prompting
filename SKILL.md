---
name: gpt-image-2-prompt-couture
description: "GPT Image 2 safety-aligned prompting skill pack. Core: sensitive-to-safe prompt conversion, modular low-intersection prompting, prompt expansion and repair, parameter-director system, image-to-prompt distillation, expression control, full workflow management."
---

# GPT Image 2 Prompt Couture

A skill pack for AI agents (Hermes Agent, OpenClaw Codex, Claude Code) to master GPT Image 2 prompting.

## How This Skill Works

```
User Input (sensitive prompt / short idea / messy prompt / image / parameters)
        │
        ▼
Skill Router → Classify → Select Mode
        │
        ├── Sensitive→Safe Conversion (core)
        ├── Short Idea Expansion
        ├── Messy Prompt Repair
        ├── Image-to-Prompt Distillation
        ├── Expression Control
        └── Parameter Director System
        │
        ▼
Methods + Patterns + Recipes
        │
        ▼
Clean GPT Image 2 Prompt
```

## Reference Files

| File | When to Read |
|------|-------------|
| `references/core-methods.md` | Subtraction, low-intersection modules, conflict audit, image distillation, expression control, workflows |
| `references/prompt-patterns.md` | User gives a specific image type or style |
| `references/prompt-recipes.md` | Templates, parameter locking, 4K, repair, variants |
| `references/sensitive-to-safe-dictionary.md` | User input contains sensitive/raw words needing safety conversion |

## Core Function ①: Sensitive→Safe Conversion

### Three Principles (信·雅·达)
- **信 (Fidelity)**: Preserve the user's core aesthetic intent
- **雅 (Elegance)**: Replace raw/risky words with professional visual language
- **达 (Deliverability)**: Output a prompt that safely produces the desired image

### Conversion Flow
```
Input → Identify Risk Points → Extract Core Intent → Rewrite Professionally → Output
```

### Key Conversion Dictionary (Full version in references/)

| User Says | Professional Translation |
|-----------|------------------------|
| sexy/alluring | mature appeal, refined sensuality, emotional tension |
| curvy/full-figured | healthy full figure, natural balanced curves |
| revealing/deep V | bold cut with safe coverage, draped neckline with lining |
| see-through/sheer | layered chiffon with safe inner lining |
| swimwear/bikini | fashion resort photography, full fabric coverage |
| boudoir/bed photo | bedroom editorial, cinematic room portrait |
| intimate/romantic mood | restrained emotional tension, light-and-shadow interplay |

### Complete Conversion Example

**Input**: "A sexy woman in revealing black lace lingerie on a bed with an alluring pose"

**Output**: "Indoor mood portrait photography, a young adult East Asian woman, black lace-trimmed camisole dress (fully lined, lace as decorative texture only), reclining on white bed sheets, soft morning window light, restrained calm expression, warm beige and black tones, clean professional photography quality, shallow depth of field, realistic skin texture, no text, no watermark."

## Core Function ②: Low-Intersection Modular Prompting

### Core Principle
- Don't write prompts as continuous narrative paragraphs
- When wardrobe + body emphasis + interaction + emotional state + close camera all bind together, AI misreads high risk
- Split into independent modules with weak connections

### Module Format
```
[visual texture] + [subject aesthetic] + [wardrobe material]
[pose/action]
[visual focus]
[lighting method]
[interaction object]
[character state]
[scene mood]
[text/no-text limits]
```

### Rewriting Others' Prompts
1. First extract structure: what does each section control?
2. Identify the problematic module
3. Only replace that module, not the whole prompt

### Merging Two Prompts (Module Docking)
- Prompt A contributes: composition + outfit + accessories
- Prompt B contributes: scene + lighting + typography
- Personal vocabulary: aesthetic + style identity
- Dock by visual function, not by text blending

## Function ③: Full Workflow System

### 8-Step Workflow
```
Idea → Feasibility Check → Requirement Breakdown → Template Design → Parameter Combination → Final Prompt → Test Output → Review & Iterate
```

### Template Design (5 Elements)
1. **Fixed Aesthetic Skeleton** — what stays constant (realism/illustration, genre, mood)
2. **User Input Parameters** — what the user changes (scene, outfit, makeup, lens, ratio)
3. **Auto-Completion Rules** — details the LLM fills (texture, lighting, background)
4. **Negative Constraints** — type-specific boundaries
5. **Final Output Format** — consistent structure

### 6-Step Beginner Template
1. Describe idea → 2. Feasibility analysis → 3. Design template → 4. Generate parameter combos → 5. Output prompt → 6. Review after testing

### 7 Testing Dimensions
Character consistency / Style consistency / Outfit quality / Makeup accuracy / Background cleanliness / Color harmony / Reusability

## Function ④: Virtual Character Iteration

### Character Card Structure
```
Purpose / Character / Core Vibe / Style / Scene / Outfit / Ratio / Avoids
```

### Key Methods
- Translate aesthetic words into visible details (e.g. "pure/clean" = clear eyes + natural brows + near-bare skin + soft light)
- Two-layer design: character card (constraints) + photographic moment (shootable instant)
- One major fix per iteration round
- At ~70% quality, generate 3 branches for comparison
- Post-generation 8-point check: adult boundary, resemblance, face shape, eyes, nose, skin, expression, artifacts


## Function ⑤: Parameter Director System

### Parameter Layers
Fixed Skeleton + User Parameters + Auto-Completion + Negatives + Output Format

Common parameters: style / scene / outfit / vibe / face direction / body direction / lens / lighting / filter / ratio

### Core Rules
- One primary style per image
- When output fails, only change the corresponding parameter
- Parameters are about precision, not quantity

### Beginner Formula
```
"I want a [ratio] image. Subject is [person/product]. Style is [primary]. Scene is [environment]. Pose/state is [action/pose]. Lighting/color is [atmosphere]. I want it to feel [mood]. Avoid [problems]."
```


## Function ⑥: Expression Control

```
Disdain/tsk → furrowed brows, narrowed side-glance, wrinkled nose, slightly pursed lips, head tilted away
Cold → relaxed mouth, low-intensity gaze, minimal smile, still posture
Wounded → moist eyes, slightly lowered brows, soft mouth, restrained expression
Tender → relaxed eyes, slight smile, softened cheeks, open posture
Confident → direct gaze, lifted chin, stable shoulders, controlled mouth
```


## Function ⑦: Image-to-Prompt Distillation

### Output Format
```
Visual Analysis: type / composition / first visual hook
Reusable Method: subject / pose / light / material / palette
Generated Prompt: [complete prompt]
```


## Output Rules

1. User-asserted parameters must be preserved
2. Simple portraits → compact high-signal prompt first
3. Complex interaction scenes → low-intersection modular format
4. Sensitive words → professional translation
5. When output fails, change only one issue per round
6. Output: clean, professional, GPT Image 2-ready Chinese or English prompt
