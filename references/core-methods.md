# Core Prompt Methods

Use this file for model strategy, prompt diagnosis, image-to-prompt distillation, expression control, and modular low-intersection prompting.

## Method 1: High-Signal Subtraction

GPT Image 2 responds well to clean intent. For most portraits, start with less.

Keep:

```text
subject
adult boundary
style anchor
mood or pose
scene or outfit anchor
one lighting phrase
one quality phrase
```

Remove:

```text
repeated quality stack
excessive camera stack
conflicting texture stack
unnecessary 8K/masterpiece/best quality wording
every detail that does not change the visual direction
```

Good structure:

```text
commercial magazine editorial portrait + adult subject + mood/pose + outfit/scene + natural soft lighting + clean professional photography style
```

When the first result is close, add one correction only:

```text
face looks fake -> realistic skin texture
light is harsh -> natural soft lighting
background is noisy -> minimal clean background
too influencer-like -> commercial editorial style, natural face, not over-retouched
too AI-like -> no plastic skin, no over-sharpening
```

## Method 2: Low-Intersection Modular Prompting

Use for guofeng, cosplay, roleplay, couple/interaction scenes, intimate but non-explicit mood, and any prompt where a prose paragraph causes the model to over-bind concepts.

Problem pattern:

```text
wardrobe + body emphasis + close relationship + emotional state + close camera + dramatic mood
```

If these are written as one continuous sentence, they may become a strong fused narrative. Rewrite as separate visual modules.

Module order:

```text
visual texture
subject aesthetic
wardrobe material
pose/action
visual focus
lighting method
secondary subject or prop
character state
scene mood
boundaries / text limits
```

Compact block template:

```text
[visual texture] + [subject aesthetic] + [wardrobe material]
[pose/action]
[visual focus]
[lighting method]
[secondary subject or prop]
[character state]
[scene mood]
[boundaries / no text / no watermark]
```

Detailed prose template:

```text
Generate a [ratio] image with [visual texture].
The subject is [adult subject aesthetic].
Wardrobe is [wardrobe material and coverage].
Pose is [pose/action], with [visual focus] as the main composition cue.
Lighting is [lighting method].
Optional secondary subject/prop: [safe secondary element].
The emotional mood is [scene mood], restrained and non-explicit.
Boundaries: [negative constraints].
```

Rules:

```text
Keep modules parallel.
Do not write a sensual or romantic scene as a plot paragraph.
If the user wants interaction, describe spatial relationship and composition, not sexual escalation.
If a module creates risk, neutralize it with wardrobe coverage, camera distance, and professional photo/art context.
```

## Method 3: Prompt Conflict Audit

Before final output, scan for conflicts:

```text
quality conflict: ultra realistic + masterpiece + best quality + 8K + sharp focus
camera conflict: many lenses/film stocks/apertures/grain simulations at once
texture conflict: poreless skin + visible pores; soft airy + over-sharp
style conflict: real photo + heavy CG terms; lifestyle snapshot + luxury studio lighting
semantic binding: thin clothing + body focus + close contact + intoxicated state + intimate mood
identity conflict: new face direction while user uploaded a reference identity
age conflict: adult request but childlike styling words
```

Repair:

```text
delete duplicates
choose one style anchor
choose one lighting mode
separate modules if semantic binding is high
add adult identity and coverage boundaries
preserve locked user fields
```

## Method 4: Image-To-Prompt Distillation

When the user uploads an image or asks to learn from an image, extract the visual system instead of copying the image.

Extract:

```text
image type
subject identity category, not private identity
composition
camera distance
pose/action
face and expression
wardrobe shape and coverage
material physics
light direction
color palette
background depth
negative constraints
```

Output format:

```text
视觉识别:
- type:
- composition:
- first visual hook:

可复用方法:
- subject:
- pose:
- light:
- material:
- palette:

生成提示词:
[fresh prompt]
```

For public examples, do not mention the source in the skill output.

## Method 5: Expression Control

If the user provides an emotion word, emoji, kaomoji, or facial expression idea, translate it into facial muscles and camera-readable expression.

Mapping:

```text
嫌弃 / tsk -> furrowed brows, narrowed side glance, wrinkled nose, slightly pursed lips, head slightly tilted away
冷淡 -> relaxed mouth, low-intensity gaze, minimal smile, still posture
委屈 -> moist eyes, slightly lowered brows, soft mouth, restrained expression
轻蔑 -> asymmetric half-smile, raised brow, sideways glance
惊讶 -> widened eyes, parted lips, lifted brows, paused gesture
疲惫 -> half-lidded eyes, relaxed shoulders, muted mouth, soft under-eye shadows
温柔 -> relaxed eyes, slight smile, softened cheek muscles, open posture
自信 -> direct gaze, lifted chin, stable shoulders, controlled mouth shape
```

Rules:

```text
Describe the face, not the emoji graphic.
If the user wants an emoji as a prop, explicitly say visible emoji icon; otherwise convert it into expression.
Use one primary expression and one secondary nuance.
Do not combine more than two strong expressions.
```

## Method 7: Full Workflow System

Use for series production, when the user wants stable results across multiple generations, or when the user wants to build a reusable template.

### 8-Step Workflow
```
idea → feasibility check → requirement breakdown → template design → parameter combination → final prompt → testing → review → iteration
```

### Feasibility Check
Ask the LLM to analyze before writing any prompt:
- Is this idea suitable for a GPT Image 2 template?
- Visual theme, focus, reusability, risk points, fixed parameters, open parameters

### Template Design (5 Elements)
1. **固定审美骨架** — what must stay in every generation (realism/illustration, genre, style, composition)
2. **用户输入参数** — what the user changes (scene, outfit, makeup, lens, ratio)
3. **自动补全规则** — details the LLM fills automatically (material, accessories, lighting, background blur)
4. **负面约束** — type-specific negative constraints (no childlike features, no cheap studio, no fabric artifacts)
5. **最终输出格式** — fixed output structure

### 6-Step Template for Beginners
1. Describe the idea → 2. Feasibility analysis → 3. Design template → 4. Generate parameter combos → 5. Output prompt → 6. Review after testing

### 7 Testing Dimensions
1. 人物稳定性: Does the face stay consistent?
2. 风格稳定性: Does the style stay consistent?
3. 服装匹配度: Does the outfit match the character's status?
4. 妆容还原度: Is the makeup actually appearing as intended?
5. 背景干净度: Is the background clean and non-distracting?
6. 色彩协调度: Are colors harmonious, not monochromatic?
7. 可复用性: Can you change one parameter and still get stable output?

## Method 8: Virtual Character Iteration

Use when the user wants to create an original AI character portrait from scratch.

### Character Card Design (约束表)
```
用途 / 人物 / 核心气质 / 风格 / 场景 / 服装 / 画幅 / 避免项
```

### Two-Layer Design
- Layer 1: Character card (constraint table — what must be preserved)
- Layer 2: Photographic moment (a shootable instant, not a static pose)

### Translating Aesthetic Words Into Visible Details
```
清纯 → clear eyes, natural brows, near-bare skin, warm cheek tint, soft natural light
温婉 → restrained smile, relaxed features, rounded nose tip, naturally approachable gaze
真实 → pores, baby hairs, fabric texture, subtle skin tone variations, natural shadows
过目不忘 → 1-2 low-key identifying features (shallow dimple, faint mole)
```

### Iteration Rules
- One major fix per round — never change face + hair + makeup + background + clothes + lighting at once
- When reaching 70% target quality, generate 3 branches for comparison
- Post-generation check (8 items): adult boundary, celebrity resemblance, face shape, eyes, nose, skin, expression, artifacts

## Method 9: Modular Prompt Merging

Use when the user wants to combine two separate prompt sources into one coherent prompt.

### Problem Pattern
Mixing two prompts by pasting fragments → conflicting visual systems compete for dominance.

### Solution: Module Docking
1. Extract structure from prompt A: composition, outfit, accessories
2. Extract structure from prompt B: scene, lighting, typography
3. Apply personal fixed vocabulary: aesthetic, style identity
4. Dock modules by visual function, not by text blending

### Checking Modules
Identify what each section controls before deciding what to replace:
```
Which block controls visual texture?
Which block controls subject aesthetic?
Which block controls wardrobe material?
Which block controls pose/action?
Which block controls lens/angle?
Which block controls scene mood?
Which block controls layout/typography?
Which block controls boundaries?
```

For iterative work, generate controlled variants. Change one module at a time.

Variant axes:

```text
pose
lighting
wardrobe material
face direction
scene
camera distance
color palette
expression
```

Output format:

```text
Base prompt:
[prompt]

Variant A - pose change:
[same prompt, changed pose only]

Variant B - lighting change:
[same prompt, changed light only]

Variant C - expression change:
[same prompt, changed expression only]
```

This helps the user learn what changes the image instead of rewriting everything.
