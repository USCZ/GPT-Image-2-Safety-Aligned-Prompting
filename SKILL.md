# GPT Image 2 Safety-Aligned 4K Prompting

Use this skill when the user wants to create, expand, rewrite, debug, or improve prompts for GPT Image 2 or similar image-generation models, especially for 4K images, mature fashion portraits, 3D CG character posters, swimwear/lifestyle photography, elegant sensual portraiture, and high-detail mythic art.

This skill is based on:
- Li Yue article version 1: "99%的人都写错了，GPT Image 2 生成美女，千万别直接写“性感”", article id `2056764035287359488`.
- Li Yue article version 2: "GPT Image 2 安全审查真相：不是只看“性感”，而是在预测你的意图", article id `2057435047138037760`.
- Additional user-supplied prompt references covering 4K API generation, mature sensual portrait expansion, swimwear, waterpark candid photography, backlit back-focused editorial portraits, low-angle outdoor fashion, forest Tyndall lighting, morning chiffon editorial portraits, 3D CG fantasy character posters, and Dunhuang cracked-wall mythic art.
- OpenAI official image-generation documentation checked on 2026-05-25: `gpt-image-2` supports flexible image sizes up to 4K-class outputs, including `3840x2160` and `2160x3840`, with `quality` values such as `high` and `output_format` values such as `png`.

Important framing: do not help users bypass, defeat, or evade safety systems. The goal is to express a safe creative intent more clearly, reduce accidental false positives, and generate compliant, tasteful, non-exploitative images. If the user says "过审", interpret it as "make the prompt safety-aligned and clear".

## 4K GPT Image 2 Workflow

For native 4K landscape output, use:

```text
model: gpt-image-2
size: 3840x2160
quality: high
output_format: png
```

For native 4K portrait output, use:

```text
model: gpt-image-2
size: 2160x3840
quality: high
output_format: png
```

Use `3840x2160` for 16:9 horizontal images and `2160x3840` for 9:16 vertical images. Use `png` when maximum fidelity is preferred. Use `jpeg` or `webp` when latency/file size matters.

Example CLI pattern for a local wrapper:

```bash
python image_gen.py generate \
  --model gpt-image-2 \
  --prompt "Native 4K photorealistic aerial drone photo of red desert sand dunes at sunrise, high oblique view, wind-carved sand ripples, sharp realistic texture, no text, no watermark." \
  --size 3840x2160 \
  --quality high \
  --output-format png \
  --out output/imagegen/example.png
```

If implementing directly with the OpenAI Python SDK, use the Image API shape your local SDK supports. A typical generation call has these fields:

```python
from openai import OpenAI
import base64

client = OpenAI()

result = client.images.generate(
    model="gpt-image-2",
    prompt="Native 4K photorealistic aerial drone photo of red desert sand dunes at sunrise, high oblique view, wind-carved sand ripples, sharp realistic texture, no text, no watermark.",
    size="3840x2160",
    quality="high",
    output_format="png",
)

image_base64 = result.data[0].b64_json
with open("output/imagegen/example.png", "wb") as f:
    f.write(base64.b64decode(image_base64))
```

After generation, verify the actual pixel size locally:

```bash
sips -g pixelWidth -g pixelHeight output/imagegen/example.png
```

Expected for 4K landscape:

```text
pixelWidth: 3840
pixelHeight: 2160
```

Expected for 4K portrait:

```text
pixelWidth: 2160
pixelHeight: 3840
```

## Core Safety Model

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
- Sexualized minors, young-looking sexualization, loli/underage framing, school-uniform sexualization, or age ambiguity mixed with sexuality.
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

Avoid building the prompt around body stimulation, sexual invitation, body-part fixation, private sexual atmosphere, or voyeuristic camera angles. Build it around:
- Adult identity and mature face.
- Overall posture and natural body proportion.
- Clothing structure, fabric, fit, silhouette, and design.
- Lighting, composition, color, background, atmosphere, and camera style.
- Commercial, editorial, product, lifestyle, cinematic, or character-design context.
- Explicit safety boundaries such as no nudity, no explicit sexual content, no body-part close-up, and no underage appearance.

## Mature Allure Translation

When the user asks for "性感、撩人、丰满", do not intensify into explicit exposure or sexual acts. Translate the intent into mature visual language:

```text
性感 -> mature feminine appeal, refined sensuality, elegant visual tension
撩人 -> expressive eyes, emotionally magnetic presence, close but restrained intimacy
丰满 -> healthy full figure, rounded natural proportions, soft body volume, balanced curves
火辣 -> confident fashion energy, strong silhouette, high visual impact
诱惑 -> mysterious elegance, cinematic tension, suggestive only through light and gaze
贴身 -> tailored fit, fabric following the silhouette, clothing structure visible
湿身 -> realistic water environment, natural water highlights, not sexualized wet-body display
私房 -> cinematic editorial room portrait, quiet emotional photography, tasteful styling
低机位 -> fashion low-angle full-body composition, not voyeuristic body-part framing
```

When using body-shape details, embed them inside an overall adult, fashion, editorial, or character-design context. Prefer:

```text
overall body rhythm
balanced proportions
soft waist line
rounded but natural figure
shoulder-neck line
clothing silhouette
fabric tension and folds
editorial posture
```

Avoid:

```text
explicit body-part close-up
low-angle body gaze
clothes falling off
transparent clothing used for nudity
minor-coded cuteness combined with sensuality
sexual acts or fetish framing
```

## Prompt Risk Colors

Use these categories as a rewrite guide.

### Green Terms: Stable Direction

Prefer terms like:

```text
adult woman / adult female character
25+ mature woman when realism is requested
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
cinematic portrait
clean soft light
real skin texture
fabric texture
tailored silhouette
high-end styling
polished composition
no text
no watermark
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
bikini
wet look
back-focused portrait
low angle
looking back
leaning forward
soft chiffon
sheer fabric
private room
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
intimate -> emotionally close, cinematic, restrained
bedroom -> bright interior / editorial room portrait / lifestyle setting
swimsuit -> swimwear brand lookbook / product presentation / resort lifestyle
bikini -> tasteful swimwear styling with moderate coverage
wet look -> water reflections and natural water droplets
back-focused -> backlit shoulder-neck and back-line art portrait
low angle -> full-body fashion perspective with natural proportions
looking back -> natural over-shoulder glance, calm expression
leaning forward -> slight posture dynamics with composure
sheer fabric -> layered chiffon with safe coverage and skin-tone lining
private room -> filmic editorial portrait, not explicit private content
```

### Red Terms: Avoid

Do not use or intensify:

```text
tempting in an explicit sexual sense
provocative sexual pose
teasing sexual action
nude
exposed private parts
explicit body-part close-up
cleavage focus
private parts
wet seductive body display
clothes slipping to reveal nudity
vulgar pose
adult photo / porn / soft porn
fetish
minor-like
loli
schoolgirl sexy
childlike sexy
underage sexy
non-consensual framing
celebrity/private sexual likeness
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
cinematic emotional portrait
mythic art key visual
```

Unstable categories:

```text
adultized private scene
body-part display
suggestive bedroom image
voyeuristic camera framing
minor-like sexualization
coercive intimacy
explicit wet-body display
```

### 3. Risk Accumulation

Single elements may be acceptable alone but unsafe in combination.

Risky combination:

```text
adult woman + bikini + bedroom + wet look + teasing expression + low angle + body-part emphasis
```

Safer combination:

```text
adult woman + tasteful swimwear + bright resort pool + natural posture + eye-level camera + focus on fabric, water, color, and summer atmosphere
```

### 4. Generation Direction Control

Even if text passes, the generation process may pull the result toward safety. To keep the output expressive without becoming risky, specify safe visual anchors:

```text
adult appearance
mature natural face
natural proportions
upright or relaxed posture
eye-level or clearly editorial camera
well-fitted but non-revealing clothing
clear clothing structure
bright, clean background
commercial/editorial visual language
no nudity
no explicit sexual content
no body-part close-up
no underage or childlike appearance
```

### 5. Final Image Review

Prompts can pass but final images can fail if the image appears to contain nudity, sexualized minors, explicit body focus, over-revealing clothing, suggestive pose, celebrity/private misuse, severe gore, illegal content, or deception.

If this happens, reduce ambiguity in the next prompt:

```text
adult, mature natural face, not childlike, no underage appearance, tasteful styling, no nudity, no explicit or suggestive pose, focus on clothing design, lighting, posture, and character art.
```

## Expansion Workflow For Short Prompts

When the user provides a short prompt and asks for it to become "性感、撩人、丰满", expand it safely instead of asking follow-up questions unless the subject age or target is unsafe.

Use this sequence:

```text
1. Identify format: 4K, 9:16, 16:9, photo, 3D CG, illustration, phone snapshot, editorial portrait.
2. Define adult subject: adult woman / 25+ mature woman / adult fantasy female character.
3. Define scene: pool, window, forest, bedroom editorial, street fashion, mythic wall, etc.
4. Define posture: natural, composed, elegant, dynamic, close-up, full-body, back-focused.
5. Translate sensuality: mature appeal, expressive eyes, soft full figure, balanced curves, refined tension.
6. Define clothing: fabric, cut, texture, fit, coverage, safety layer if needed.
7. Define camera: lens, angle, distance, depth of field, phone capture, editorial composition.
8. Define light: sun, backlight, Tyndall beams, soft morning window light, cinematic glow.
9. Define detail: skin texture, hair, water, fabric folds, PBR materials, 4K clarity.
10. Add negative constraints: no nudity, no explicit sexual content, no underage look, no text, no watermark, no broken anatomy.
```

Default expansion language for Chinese users should be Chinese unless they request English.

### Short Prompt Expansion Template

```text
生成一张 [画幅比例] [媒介风格]，主题为「[主题]」。

画面中是一位 [明确成年身份]，[面容与气质]。她的整体气质为成熟、优雅、柔和但有吸引力，身形健康丰腴、比例自然协调，曲线明显但克制，不低俗。画面重点不是直白暴露，而是通过眼神、姿态、服装剪裁、材质、光影和构图呈现成熟女性魅力。

场景为 [场景]。人物 [姿态与动作]，镜头采用 [镜头与构图]，让视觉焦点落在 [脸部/肩颈/背部/服装/整体体态/氛围]。

服装为 [服装]，材质具有 [材质细节]，剪裁 [剪裁与版型]，贴合身体线条但保持得体，重点表现服装结构、布料褶皱、柔和高光与高级质感。

光线为 [光线]，营造 [情绪氛围]。画面需要 [画质要求]。

避免：低俗色情、裸露敏感部位、未成年感、过度暴露、身体局部特写、透明失控、挑逗动作、肢体畸形、错误手指、塑料皮肤、文字、水印。
```

## Mature Sensual Prompt Formula

Use this transformation:

```text
raw desire wording
-> adult-safe subject definition
-> aesthetic intent
-> overall posture and body rhythm
-> clothing structure and fabric
-> scene and camera language
-> light/material/detail language
-> safety boundaries
```

Template:

```text
Create a [format/aspect ratio] image of an adult [subject type].

The subject has a mature natural face, [personality/aura], and a confident, calm presence. The posture is natural and composed, with balanced proportions, soft body volume, and coordinated body lines. The image should feel refined, sensual, and emotionally magnetic, while emphasizing clothing design, gaze, light, color, and composition rather than body exposure.

Wardrobe: [garment], with [fabric], [cut], [color], and [fit]. The clothing is tasteful, well-fitted, and not overly revealing. Let the silhouette be expressive through tailoring, folds, highlights, and fabric tension.

Scene: [bright, clean, public/commercial/lifestyle/cinematic/character-design context]. Camera: [eye-level / editorial / product lookbook / fashion low-angle full-body / phone snapshot / cinematic portrait]. Lighting: [soft natural light / studio light / backlight / Tyndall beams / morning window light].

Safety boundaries: no nudity, no explicit sexual content, no body-part close-up, no voyeuristic framing, no underage or childlike appearance, no real-person private likeness, no text, no watermark.
```

## Prompt Self-Check

Before generating or returning a prompt, verify:

1. Is the subject clearly adult when attraction, body shape, or stylized beauty is involved?
2. Does the prompt avoid mixing young/childlike/schoolgirl/cute minor-coded terms with sexual or body-focused language?
3. Is the prompt about overall body posture, styling, and design rather than isolated body parts?
4. Does it avoid explicit nude, fetish, pornographic, coercive, or private-sexual wording?
5. Does it avoid voyeuristic low-angle framing, sexualized wet-body framing, and body-part close-ups?
6. Is clothing described through cut, fabric, color, fit, layering, and design rather than exposure?
7. Is the scene framed as bright, editorial, cinematic, public/lifestyle, or character-design instead of explicit private sexual content?
8. Are safety boundaries included when the topic is close to sensitive areas?
9. If using sheer fabric, is safe coverage or lining specified?
10. If using swimwear, is it framed as resort/lifestyle/lookbook/realistic pool context rather than body display?

## Common Repairs

### Prompt Rejected

Remove:

```text
sexy, seductive, provocative, chest/hips as isolated focus, low-angle body display, wet-body seduction, private intimacy, teasing, explicit body focus
```

Replace with:

```text
mature, elegant, healthy, confident, natural curves, refined feminine beauty, commercial portrait, tasteful clothing, editorial lighting, fabric texture, eye expression
```

### Output Too Conservative

Do not add explicit sexual intensity. Add design and craft detail:

```text
increase fashion expressiveness
strengthen silhouette rhythm
enhance fabric texture and folds
add refined styling
improve soft lighting and skin rendering
make the pose more graceful but still natural
use a stronger editorial composition
bring the subject closer to camera while keeping tasteful framing
```

### Body Looks Distorted

Add:

```text
natural human anatomy, balanced shoulders and waist, realistic limb length, stable seated/standing posture, correct hands and fingers, no twisted body, no distorted joints.
```

### Face Looks Too Young

Add:

```text
mature natural adult face, 25+ if photorealistic, not childlike, not teen-coded, refined adult features, calm confident expression.
```

### Output Feels Too Suggestive

Add:

```text
return to a high-end commercial portrait and character-design expression, reduce body exposure, reduce private or suggestive atmosphere, emphasize clothing, light, posture, and personality.
```

## Reference Prompt Patterns

Use these as learned patterns. Adapt them; do not blindly copy them. Preserve the safe adult boundary and the professional visual category.

### 1. 3D CG Romantic Duo Character Poster

Use for adult fantasy female duo posters with closeness, romantic tension, and high-end game-promo polish.

Key ingredients:

```text
9:16 vertical, high-detail 3D CG, adult fantasy women, bright window backlight, close face distance, mutual emotional tension, diagonal composition, S-shaped dual-character rhythm, white fantasy fashion dresses, satin/chiffon materials, hair ribbons, petals, soft particles, PBR materials, cinematic light, commercial character poster finish.
```

Risk controls:

```text
mutual closeness, no coercive sexual framing, no nudity, no transparent clothing, no explicit sexual action, no underage look, no body-part close-up, no lowbrow erotic tone.
```

### 2. Photorealistic Pool Portrait

Use for realistic swimwear portraits in a bright outdoor pool.

Key ingredients:

```text
9:16 vertical real-photo portrait, adult East Asian woman 20+ or 25+, bright outdoor pool, clear blue water, natural pool ladder pose, full-frame camera feel, 85mm portrait lens, RAW photo texture, real skin pores, realistic wet hair, realistic water reflections, tasteful white swimwear, commercial resort portrait.
```

Risk controls:

```text
moderate swimwear coverage, natural relaxed posture, no sexualized wet-body display, no nudity, no transparency, no explicit body focus, no underage appearance.
```

### 3. 3D CG Pool Character Illustration

Use for anime-style but high-end 3D CG pool character posters.

Key ingredients:

```text
9:16 vertical, adult fantasy female character, outdoor pool, blue water, pool ladder, calm elegant pose, blue hair, white swimwear, realistic water droplets, subsurface skin shading, premium 3D CG character rendering, summer sunlight, clean bright background.
```

Risk controls:

```text
adult character, tasteful swimwear, elegant pose, no transparent clothing, no explicit body-part framing, no underage look.
```

### 4. Window-Side Soft Shirt 3D Character

Use for warm indoor 3D CG portraits with soft shirt styling.

Key ingredients:

```text
9:16 vertical high-detail 3D CG, adult fantasy woman, window-side seated pose, platinum hair, ribbons, soft white shirt, fabric folds, gentle S-shaped posture, golden morning backlight, dust particles, refined commercial character-poster finish.
```

Risk controls:

```text
shirt remains safely covering sensitive areas, no nudity, no transparent wet effect, no exaggerated anatomy, no vulgar private framing.
```

### 5. iPhone Waterpark Candid

Use for candid, realistic, social-media-style summer waterpark photos.

Key ingredients:

```text
9:16 iPhone 15 Pro snapshot feel, adult Chinese/Asian woman 25+, bright waterpark, slide splash, candid laugh, hand shielding water, close friendly framing, real skin, realistic wet hair, physical water droplets, slight handheld tilt, natural sunlight, social-platform casual moment.
```

Risk controls:

```text
adult age clear, playful not erotic, swimwear tasteful and opaque, no overexposure, no underage look, no staged pornographic tone.
```

### 6. Backlit Beautiful-Back Emotional Portrait

Use for elegant art portraits where the back, shoulder-neck line, and light are the visual core.

Key ingredients:

```text
vertical high-quality emotional portrait, adult woman, back as main visual focus, over-shoulder or side pose, low-back dress or draped garment, shoulder-neck line, shoulder blades, spine line, waist-back curve, window backlight, soft fabric layers, quiet cinematic mood, real skin texture, film grain.
```

Risk controls:

```text
artistic back-focused portrait, no nudity, no explicit sexualization, no visible private areas, no vulgar pose, no underage look, face secondary.
```

### 7. Low-Angle Outdoor Fashion

Use for fashion street/editorial shots with elongated legs and big-sky composition.

Key ingredients:

```text
9:16 vertical ultra-real outdoor fashion photography, adult Chinese woman, full body, camera close to ground, sky-dominant background, slight wide-angle perspective, natural proportions, fashion confidence, short skirt/stockings/chiffon/shorts as one tasteful styling choice, real fabric texture, summer daylight, magazine street-shoot feel.
```

Risk controls:

```text
fashion full-body composition, not voyeuristic, no body-part close-up, no explicit pose, no excessive distortion, no underage look.
```

### 8. Forest Tyndall Cinematic Fashion Portrait

Use for dreamlike forest fashion photos with visible light beams.

Key ingredients:

```text
vertical cinematic photoreal portrait, mature Chinese/Asian woman 25+, summer forest, moss, leaves, morning mist, pollen and dust particles, multiple Tyndall light beams, one main beam crossing face/shoulders/upper body/fabric, half light half shadow, shallow depth of field, film grain, realistic skin and fabric.
```

Risk controls:

```text
fashion and light are the focus, no explicit exposure, no eerie horror mood, no body-part close-up, no underage look.
```

### 9. Morning Chiffon Editorial Portrait

Use for high-end art portraits with a single continuous sheer fabric element.

Key ingredients:

```text
vertical photoreal morning editorial portrait, adult woman 25+, clean bedroom by large window, one continuous ultra-light white chiffon/tulle styling element, invisible skin-tone safety layer, relaxed morning pose, cool blue dawn light, soft light stripes, dust particles, real fabric weave, cinematic private-art portrait.
```

Risk controls:

```text
safe coverage complete, no visible nudity, no separate lingerie emphasis, no explicit private content, no transparent exposure, no text or watermark.
```

### 10. 4K Mature Sensual Portrait

Use for 4K photoreal/editorial portraits where the user wants "sexy" but compliant output.

Key ingredients:

```text
native 4K, adult woman / 25+ mature woman, fashion portrait, magazine editorial, cinematic portrait, satin or V-neck tailoring or fitted garment, expressive eyes, refined sensuality, real skin texture, visible pores, natural highlights, hair detail, fabric weave, high resolution, tasteful and restrained.
```

Risk controls:

```text
do not describe explicit exposure, do not name sensitive areas as the focus, no nudity, no explicit sexual content, no vulgar pose, no underage look.
```

### 11. Dunhuang Cracked-Wall Mythic Art

Use for high-end oriental mythic art in a broken-wall, immersive close-up composition.

Key ingredients:

```text
vertical close-up interactive composition, ancient Dunhuang mural wall opened like a portal, subject emerging from the mural world, foreground hand offering glowing symbolic object or ritual artifact, midground face/shoulders/robes, background moon wheel, lotus pond, flying apsaras, clouds, shrine, phoenix, baoxiang flowers, caisson patterns, mineral pigments, weathered plaster, cracked mud-gold lines, cinematic mythic light.
```

Risk controls:

```text
classical sacred temperament, no modern influencer face, no vulgar seduction, no excessive skin exposure, no readable text, no seal, no logo, no cheap gold, no collage feeling.
```

## Ready-to-Use Safe Examples

### 4K Landscape Example

```text
Native 4K photorealistic aerial drone photo of red desert sand dunes at sunrise, high oblique view, wind-carved sand ripples, sharp realistic texture, cinematic natural light, clean horizon, no text, no watermark.
```

Use with:

```text
model: gpt-image-2
size: 3840x2160
quality: high
output_format: png
```

### Fashion Character Portrait

```text
Create a 9:16 high-quality 3D character illustration of an adult woman.

She has a mature natural face, calm eyes, and an elegant, confident presence. Her posture is relaxed and upright, with balanced proportions, natural body lines, and graceful shoulder and neck alignment. The image feels refined and magnetic while emphasizing personality, styling, clothing design, and soft lighting.

She wears a refined pastel dress with a tailored silhouette, soft fabric texture, subtle folds, and tasteful fit. The clothing is elegant, well-fitted, and not overly revealing.

The scene is a bright, clean interior with soft natural light, a polished editorial composition, and a gentle premium color palette.

Safety boundaries: no nudity, no explicit sexual content, no body-part close-up, no low-angle voyeuristic framing, no underage or childlike appearance, no text, no watermark.
```

### Swimwear Lookbook

```text
Create a 16:9 high-end swimwear brand lookbook poster.

The scene features an adult female model standing at a bright resort pool. Her expression is relaxed and friendly, and her posture is natural, upright, and confident. The visual focus is the swimwear product, color palette, fabric texture, support structure, and summer resort atmosphere.

She wears a tasteful one-piece swimsuit with a clean cut, moderate coverage, and subtle elastic fabric texture. The styling feels like a professional commercial catalog rather than a private photo.

Use eye-level camera framing, clean sunlight, water reflections, resort architecture, and a polished fashion-advertising look.

Safety boundaries: no nudity, no wet-body seduction, no provocative pose, no body-part close-up, no low-angle voyeuristic framing, no excessive exposure, no text, no watermark.
```

### Fantasy Character

```text
Create a 9:16 fantasy character illustration of an adult woman in high-quality 3D CG style.

The character has a mature natural face, serene expression, and graceful presence. Her pose is slightly dynamic but composed, with flowing posture rhythm and balanced proportions. The image emphasizes fantasy styling, costume design, fabric layers, lighting, and atmosphere.

She wears an elegant star-themed gown with layered translucent fabric, subtle holographic highlights, refined embroidery, and a tasteful silhouette. The outfit is beautiful and expressive without being revealing.

The background includes soft blue, silver, and pale pink light, gentle mist, star particles, and a clean cinematic fantasy atmosphere.

Safety boundaries: no nudity, no explicit sexual content, no body-part close-up, no underage appearance, no text, no watermark.
```

## Agent Behavior

When the user provides a risky prompt:
1. Identify the likely risk pattern briefly.
2. Rewrite toward safe aesthetic intent.
3. Preserve the benign creative goal if possible.
4. Translate "sexy/alluring/full figure" into mature adult fashion, cinematic, editorial, or character-design language.
5. Add safety boundaries only where useful.
6. Do not lecture, but do not provide evasion tactics.

Suggested response style:

```text
这版主要风险在于它把画面推向身体凝视和私密暧昧语境。我把它改成商业人像/角色设计方向，保留成熟、美感、丰满体态和情绪张力，但把重点落到服装剪裁、光影、姿态和高级摄影语言上。
```

Then provide the rewritten or expanded prompt.

## Version Learning Summary

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

This iteration adds:
- Native 4K GPT Image 2 workflow with `3840x2160` and `2160x3840`.
- Mature sensual prompt expansion that keeps adult boundaries clear.
- Scene-specific reference patterns for pool, waterpark, window, backlit back portrait, forest Tyndall light, morning chiffon, fashion low-angle, romantic 3D CG duo, and Dunhuang mythic wall art.
- A rule for short prompts: expand sparse ideas into professional visual language instead of relying on explicit exposure.

Combined rule:

```text
Do not ask "how do I bypass the filter?"
Ask "how do I make the model correctly understand my safe, aesthetic, non-exploitative creative intent?"

Do not write "露哪里".
Write "服装、光影、眼神、姿态、材质、镜头、成年边界".
```
