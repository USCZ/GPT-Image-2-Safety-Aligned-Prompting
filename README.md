# GPT Image 2 Safety-Aligned Prompting

Use this skill when the user wants to create, rewrite, debug, or improve prompts for GPT Image 2 or similar image-generation models, especially when prompts are being rejected, over-filtered, or producing overly conservative results.

This skill is based on two Li Yue articles:
- Version 1: "99%的人都写错了，GPT Image 2 生成美女，千万别直接写“性感”", article id `2056764035287359488`.
- Version 2: "GPT Image 2 安全审查真相：不是只看“性感”，而是在预测你的意图", article id `2057435047138037760`.

Important framing: do not help users bypass, defeat, or evade safety systems. The goal is to express a safe creative intent more clearly, reduce accidental false positives, and keep generated images compliant, tasteful, and non-exploitative.

## Core Model

Treat image safety review as a risk prediction system, not a simple keyword filter.

The system likely evaluates:
1. Text risk in the prompt.
2. Overall semantic intent.
3. Risk accumulation across combined elements.
4. Direction control during generation.
5. Final image review after generation.

The key question is not "which single word is banned?" The key question is:

```text
What final image does this prompt appear to be steering the model toward?
```

If the prompt points toward adultized, exploitative, deceptive, violent, illegal, private, or harmful imagery, risk increases even if no single word is obviously forbidden. If the prompt points toward commercial design, fashion editorial, character art, product presentation, lifestyle photography, or high-quality visual design, stability usually improves.

## Non-Negotiable Safety Rules

Always refuse or redirect requests involving:
- Sexualized minors, "young-looking" sexualization, loli/underage framing, school-uniform sexualization, or age ambiguity mixed with sexuality.
- Non-consensual sexual imagery, private/intimate images of real people, celebrity sexual images, or deepfake sexual content.
- Explicit nudity, sexual acts, fetish content, or instructions to bypass platform safety controls.
- Fake IDs, dangerous weapon construction, terrorism propaganda, severe gore, self-harm depiction, or deceptive images of public events.
- Prompts intended to mislead, impersonate, violate privacy, or infringe protected likeness rights.

When a user asks to "绕过审查", reinterpret only if possible as:

```text
Make the prompt safer, clearer, and more policy-aligned while preserving the benign aesthetic goal.
```

If the goal itself is unsafe, refuse briefly and offer a safe alternative.

## Main Principle

Replace desire language with aesthetic language.

Avoid building the prompt around body stimulation, sexual invitation, body-part focus, private atmosphere, or camera angles associated with voyeurism. Build it around:
- Adult identity and mature face.
- Overall posture and natural body proportion.
- Clothing structure, fabric, fit, and design.
- Lighting, composition, color, background, and camera style.
- Commercial, editorial, product, lifestyle, or character-design context.
- Explicit safe boundaries such as no nudity, no suggestive pose, no body-part close-up, and no underage appearance.

## Prompt Risk Colors

Use these categories as a rewrite guide.

### Green Terms: Stable Direction

Prefer terms like:

```text
adult woman / adult female character
mature natural face
elegant
confident
healthy
graceful
natural smile
calm expression
balanced proportions
natural curves
coordinated posture
fashion editorial
commercial portrait
brand lookbook
product presentation
character design
clean soft light
refined styling
well-fitted clothing
tailored silhouette
fabric texture
polished composition
```

### Yellow Terms: Rewrite Carefully

These can become unstable depending on context:

```text
sexy
seductive
hot body
charming
curvy
alluring
tight
prominent curves
intimate atmosphere
bedroom
swimsuit
wet look
low angle
looking back
leaning forward
```

Rewrite them into safer intent:

```text
sexy -> refined feminine beauty / mature appeal
seductive -> mysterious elegance / expressive eyes
hot body -> balanced, healthy proportions
charming -> warm, confident presence
curvy -> natural, coordinated body lines
alluring -> visually engaging but restrained
tight -> well-fitted / tailored
intimate -> soft, calm, emotionally warm
bedroom -> bright interior / lifestyle setting
swimsuit -> swimwear brand lookbook / product presentation / vacation outfit
low angle -> eye-level editorial composition
looking back -> natural slight turn with relaxed shoulders
leaning forward -> upright or gently dynamic posture
```

### Red Terms: Avoid

Do not use or intensify:

```text
tempting
provocative
teasing
nude
exposed
explicit body-part close-up
cleavage focus
private parts
wet seductive
clothes slipping
vulgar pose
adult photo
soft porn
fetish
minor-like
loli
childlike sexy
underage sexy
```

## Five-Layer Safety Diagnosis

When a prompt fails or is over-filtered, diagnose it with these five layers.

### 1. Text Review

Look for explicit high-risk terms. Remove or neutralize words that directly imply nudity, explicit sex, minors, non-consent, body-part fixation, illegal behavior, violent harm, deception, or real-person misuse.

Example:

```text
Risky: emphasize chest, body-part close-up, low-angle display.
Safer: upper-body clothing structure is natural, waist and shoulder proportions are balanced, the dress is tailored and well fitted.
```

### 2. Semantic Intent

Ask what category the full prompt implies.

Stable categories:

```text
fashion editorial
commercial portrait
brand advertisement
character art
lifestyle photography
product lookbook
high-end illustration
```

Unstable categories:

```text
adultized private scene
body-part display
suggestive bedroom image
voyeuristic camera framing
minor-like sexualization
```

### 3. Risk Accumulation

Single elements may be acceptable alone but unsafe in combination.

Risky combination:

```text
adult woman + swimsuit + bedroom + wet look + teasing expression + low angle + body-part emphasis
```

Safer combination:

```text
adult woman + swimwear product lookbook + bright resort pool + natural posture + eye-level camera + focus on fabric, cut, color, and summer atmosphere
```

### 4. Generation Direction Control

Even if text passes, the generation process may pull the result toward safety. To keep the output expressive without becoming risky, specify safe visual anchors:

```text
adult appearance
natural proportions
upright or relaxed posture
eye-level camera
well-fitted but non-revealing clothing
clear clothing structure
bright, clean background
commercial/editorial visual language
no nudity
no suggestive pose
no body-part close-up
```

### 5. Final Image Review

Prompts can pass but final images can fail if the image appears to contain nudity, sexualized minors, explicit body focus, over-revealing clothing, suggestive pose, celebrity/private misuse, severe gore, illegal content, or deception.

If this happens, reduce ambiguity in the next prompt:

```text
adult, mature natural face, not childlike, no underage appearance, modest styling, no nudity, no explicit or suggestive pose, focus on clothing design, lighting, and character art.
```

## Rewrite Formula

Use this transformation:

```text
raw desire wording
-> aesthetic intent
-> adult-safe subject definition
-> full-body or overall posture description
-> clothing structure and fabric
-> bright or commercial scene
-> eye-level/editorial camera
-> explicit safety boundaries
```

Template:

```text
Create a [format/aspect ratio] image of an adult [subject type].

The subject has a mature natural face, [personality/aura], and a confident, calm presence. The posture is natural and composed, with balanced proportions and coordinated body lines. The image should emphasize overall elegance, clothing design, light, color, and composition rather than body exposure.

Wardrobe: [garment], with [fabric], [cut], [color], and [fit]. The clothing is tasteful, well-fitted, and not overly revealing.

Scene: [bright, clean, public/commercial/lifestyle/character-design context]. Camera: [eye-level / editorial / product lookbook / commercial portrait]. Lighting: [soft natural light / studio light / cinematic but clean].

Safety boundaries: no nudity, no explicit sexual content, no suggestive pose, no body-part close-up, no low-angle voyeuristic framing, no underage or childlike appearance, no real-person private likeness.
```

## Prompt Self-Check

Before generating or returning a prompt, verify:

1. Is the subject clearly adult when attraction, body shape, or stylized beauty is involved?
2. Does the prompt avoid mixing "young/childlike/schoolgirl/cute minor-coded" with sexual or body-focused language?
3. Is the prompt about overall body posture, styling, and design rather than isolated body parts?
4. Does it avoid provocative, tempting, explicit, nude, fetish, or private-sexual wording?
5. Does it avoid low-angle voyeurism, wet-body framing, and body-part close-ups?
6. Is clothing described through cut, fabric, color, fit, and design rather than exposure?
7. Is the scene bright, public, commercial, editorial, or lifestyle instead of private and suggestive?
8. Are safety boundaries included when the topic is close to sensitive areas?

## Common Repairs

### Prompt Rejected

Remove:

```text
sexy, seductive, provocative, chest, hips, low angle, wet look, intimate, teasing, explicit body focus
```

Replace with:

```text
mature, elegant, healthy, confident, natural curves, refined feminine beauty, commercial portrait, tasteful clothing, editorial lighting
```

### Output Too Conservative

Do not add more sexual intensity. Add design and craft detail:

```text
increase fashion expressiveness
improve silhouette rhythm
enhance fabric texture
add refined styling
improve soft lighting and skin rendering
make the pose more graceful but still natural
use a stronger editorial composition
```

### Body Looks Distorted

Add:

```text
natural human anatomy, balanced shoulders and waist, realistic limb length, stable seated/standing posture, correct hands and fingers, no twisted body, no distorted joints.
```

### Face Looks Too Young

Add:

```text
mature natural adult face, not childlike, not teen-coded, refined adult features, calm confident expression.
```

### Output Feels Too Suggestive

Add:

```text
return to a high-end commercial portrait and character-design expression, reduce body exposure, reduce private or suggestive atmosphere, emphasize clothing, light, posture, and personality.
```

## Safe Example: Fashion Character Portrait

```text
Create a 9:16 high-quality 3D character illustration of an adult woman.

She has a mature natural face, calm eyes, and an elegant, confident presence. Her posture is relaxed and upright, with balanced proportions, natural body lines, and graceful shoulder and neck alignment. The image emphasizes personality, styling, clothing design, and soft lighting.

She wears a refined pastel dress with a tailored silhouette, soft fabric texture, subtle folds, and tasteful fit. The clothing is elegant, well-fitted, and not overly revealing.

The scene is a bright, clean interior with soft natural light, a polished editorial composition, and a gentle premium color palette.

Safety boundaries: no nudity, no explicit sexual content, no suggestive pose, no body-part close-up, no low-angle voyeuristic framing, and no underage or childlike appearance.
```

## Safe Example: Swimwear Lookbook

```text
Create a 16:9 high-end swimwear brand lookbook poster.

The scene features an adult female model standing at a bright resort pool. Her expression is relaxed and friendly, and her posture is natural, upright, and confident. The visual focus is the swimwear product, color palette, fabric texture, support structure, and summer resort atmosphere.

She wears a tasteful one-piece swimsuit with a clean cut, moderate coverage, and subtle elastic fabric texture. The styling feels like a professional commercial catalog rather than a private photo.

Use eye-level camera framing, clean sunlight, water reflections, resort architecture, and a polished fashion-advertising look.

Safety boundaries: no nudity, no wet-body seduction, no provocative pose, no body-part close-up, no low-angle voyeuristic framing, and no excessive exposure.
```

## Safe Example: Fantasy Character

```text
Create a 9:16 fantasy character illustration of an adult woman in high-quality 3D CG style.

The character has a mature natural face, serene expression, and graceful presence. Her pose is slightly dynamic but composed, with flowing posture rhythm and balanced proportions. The image emphasizes fantasy styling, costume design, fabric layers, lighting, and atmosphere.

She wears an elegant star-themed gown with layered translucent fabric, subtle holographic highlights, refined embroidery, and a tasteful silhouette. The outfit is beautiful and expressive without being revealing.

The background includes soft blue, silver, and pale pink light, gentle mist, star particles, and a clean cinematic fantasy atmosphere.

Safety boundaries: no nudity, no explicit sexual content, no suggestive pose, no body-part close-up, no underage appearance.
```

## Agent Behavior

When the user provides a risky prompt:
1. Identify the likely risk pattern briefly.
2. Rewrite toward safe aesthetic intent.
3. Preserve the benign creative goal if possible.
4. Add safety boundaries only where useful.
5. Do not lecture, but do not provide evasion tactics.

Suggested response style:

```text
这版主要风险在于它把画面指向了身体凝视和私密暧昧语境。我把它改成商业人像/角色设计方向，保留成熟、美感和造型表现，但移除挑逗、低机位和身体局部强调。
```

Then provide the rewritten prompt.

## Version 1 vs Version 2 Learning Summary

Version 1 teaches practical rewriting:
- Use a red/yellow/green vocabulary system.
- Replace direct desire words with aesthetic and commercial-design words.
- Define adult subject and mature face when needed.
- Prefer whole-body posture and clothing texture over body-part emphasis.
- Use bright, editorial, product, lifestyle, or character-design context.
- Add short negative/safety boundaries when prompts are repeatedly rejected.

Version 2 teaches the mechanism:
- Safety review is semantic and contextual, not just keyword-based.
- Risk accumulates when multiple borderline elements point in the same unsafe direction.
- The generation process itself may become conservative if the prompt steers toward unsafe imagery.
- Final image review can still block an output if the model visually drifts into unsafe territory.
- The same prompt can behave differently because multiple classifiers and policy systems may be involved.

Combined rule:

```text
Do not ask "how do I bypass the filter?"
Ask "how do I make the model correctly understand my safe, aesthetic, non-exploitative creative intent?"
```
