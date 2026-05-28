# GPT Image 2 Safety-Aligned 4K Prompting

Use this skill when the user wants to create, expand, rewrite, debug, or improve prompts for GPT Image 2 or similar image-generation models, especially for 4K images, mature fashion portraits, 3D CG character posters, swimwear/lifestyle photography, elegant sensual portraiture, and high-detail mythic art.

This skill is based on:
- Li Yue article version 1: "99%的人都写错了，GPT Image 2 生成美女，千万别直接写“性感”", article id `2056764035287359488`.
- Li Yue article version 2: "GPT Image 2 安全审查真相：不是只看“性感”，而是在预测你的意图", article id `2057435047138037760`.
- Additional user-supplied prompt references covering 4K API generation, mature sensual portrait expansion, swimwear, waterpark candid photography, backlit back-focused editorial portraits, low-angle outdoor fashion, forest Tyndall lighting, morning chiffon editorial portraits, 3D CG fantasy character posters, and Dunhuang cracked-wall mythic art.
- Additional user-supplied prompt references covering elegant roleplay fashion, fantasy elf portraits, nurse-themed studio portraits, xianxia action posters, ice fantasy cosplay, soft guofeng portraits, Japanese cinematic flower close-ups, rainy neon fashion portraits, Xiaohongshu lifestyle stills, pure portrait parameter systems, 3D CG bedroom characters, bridal couture magazine covers, product exploded-structure infographics, new-Chinese guofeng half portraits, oriental scroll breakout posters, White Snake character archive posters, reference-photo mural portraits, overhead flash bedroom editorials, and waterpark candid snapshots.
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

## Image Type Recognition Router

When the user provides a short prompt, first infer the likely image type, then expand with the matching pattern library. Do this silently unless the user asks for analysis.

Use keyword-to-route recognition:

```text
格纹制服 / 眼罩 / 托盘 / 胸牌 / 包厢 -> adult roleplay fashion portrait
护士帽 / 听诊器 / 白色制服 / wink -> light nurse-themed studio fashion portrait
精灵 / 尖耳 / 森林 / 银白长发 / 宝石额饰 -> realistic fantasy elf portrait
剑修 / 持剑 / 云海 / 古松 / 超广角 -> xianxia action concept poster
冰蓝假发 / 冰雪 / 宝石肩饰 / Cos -> ice fantasy cosplay portrait
古风走廊 / 木柱 / 纱裙 / 花饰 -> soft guofeng cosplay portrait
花海 / 日系 / 逆光 / Komorebi / 胶片 -> Japanese cinematic flower close-up
雨夜 / 霓虹 / 雨伞 / 比基尼 -> rainy neon fashion portrait
小红书 / 生活剧照 / 卧室 / 窗边 / 真实日常 -> Xiaohongshu natural lifestyle still
清纯写真 / 参数选择 -> pure youthful adult portrait generator
丰腴曲线 / 参数锁定 -> locked-parameter curvy portrait generator
床边 / 3D CG / 黑色缎面 / 月光 -> 3D CG bedroom character poster
婚纱 / 杂志封面 / 双人 / VOGUE -> bridal couture magazine cover
产品爆炸结构 / 信息板 / 部件标签 -> product exploded-structure infographic
新中式 / 琴棋书画 / 半身人像 -> new-Chinese guofeng half portrait
画卷 / 破卷而出 / 画中美人 -> oriental scroll breakout poster
白蛇传 / 立像档案 / 剧情切片 -> White Snake character archive poster
上传肖像 / 自己画自己 / 白墙壁画 -> reference-photo mural portrait concept
俯拍 / 白床 / 直闪 / 冷甜 -> overhead flash bedroom editorial
水上乐园 / iPhone 抓拍 / 滑水道 -> waterpark candid snapshot
```

After routing:

```text
1. Preserve locked user parameters exactly.
2. Add adult boundary if the image contains beauty, sensuality, cosplay, swimwear, bedroom, or intimate styling.
3. Expand with the route's scene, wardrobe, pose, lens, light, texture, and negative constraints.
4. Translate "性感/漂亮/撩人/丰满" into professional visual language: fashion styling, gaze, silhouette, fabric, light, skin texture, composition.
5. Remove or redirect explicit sexual acts, sexualized minor cues, non-consensual framing, and body-part close-ups.
```

## Parameter Locking

When the user provides a parameter template, obey locked values exactly. Do not replace them with a more convenient style.

Rules:

```text
User-filled value -> must preserve and expand only.
"自动" or blank -> agent may choose the most coherent option.
Style controls scene, clothing, light, lens, pose, and mood.
Face direction controls face shape, eye type, nose, lips, bone structure, soft tissue, expression, and recognizability.
Body direction controls silhouette and proportion; do not let style overwrite body direction.
If style and face direction conflict, keep both and harmonize through makeup, expression, color temperature, pose tension, and scene atmosphere.
```

For parameter-driven requests, output this structure unless the user asks only for the final prompt:

```text
1. 参数锁定复核
2. 完整生成提示词
3. 本次自动补全部分
4. 主要吸睛点
5. 负面限制词
```

## Face And Beauty Diversity

Do not generate the same default AI face for every woman. Apply "not average but harmonious" facial design:

```text
温柔圆脸型: soft round face, warm eyes, gentle cheek volume, friendly expression
清冷高级脸: longer facial plane, refined cheekbones, calm narrow eyes, restrained expression
古典鹅蛋脸: balanced oval face, soft jawline, classical brows, elegant lips
明艳浓颜脸: stronger facial contrast, defined eyes, fuller lips, vivid expression
甜酷小方脸: compact square-soft jaw, bright eyes, playful-cool expression
电影故事脸: natural asymmetry, memorable eyes, subtle imperfections, emotional gaze
知性长脸型: mature long oval face, calm brow-eye relationship, intelligent expression
东方丹凤眼: elongated upward eye shape, subtle classical charm, controlled expression
自然生活感脸: realistic everyday face, not influencer-like, gentle imperfections
```

Always keep adult cues clear; "young" means young adult, not childlike.

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

## High-Priority Garment Occlusion And Scale Control

Use this high-priority module whenever the user asks for a mature, sensual, full-figured fashion image with evening gowns, deep necklines, side cutouts, thin straps, metallic silk, chiffon, sheer fabric, swimwear, or any clothing that could drift into unsafe exposure.

The learned pattern is: create a low-coverage couture impression while explicitly controlling what the garment covers, how the fabric is physically supported, and what visual artifacts must not appear.

### Why This Pattern Works

Strong fashion prompts become more stable when they describe a full garment engineering system instead of only body appeal:

```text
adult age boundary
+ high-fashion / red-carpet / couture context
+ exact garment identity and color
+ clear coverage map
+ inner lining and support logic
+ fabric tension, drape, weight, folds, and reflection
+ full-body editorial framing
+ realistic skin/hair/material response
+ negative prompt against wardrobe artifacts and anatomy errors
= sensual but controlled fashion image
```

### Coverage Map First

For deep V, draped neckline, side cutout, open back, sheer fabric, or high-slit designs, state the safe coverage logic before adding glamour details.

Use:

```text
the garment creates a daring couture silhouette while all sensitive areas remain fully covered by layered fabric and seamless inner lining
the open area is limited to upper chest, shoulder, collarbone, side waist, or back line
the fabric crosses and overlaps exactly where coverage is needed
no visible nipple or areola outline
no wardrobe malfunction
no transparent exposure
```

Avoid:

```text
exposure as the main goal
uncovered private areas
clothing falling away to reveal nudity
transparent fabric used as nudity
body-part close-up as the composition
```

### Couture Support Mechanics

When a garment has a deep neckline, minimal straps, or a sculpted silhouette, add physical support language so the model does not invent lingerie artifacts or impossible cloth.

Use:

```text
seamless couture support structure
double-layer inner lining
wireless dress construction
natural fabric support
soft tension fabric
side-gathered drape
layered fabric overlap
fabric compression that follows the silhouette naturally
thin shoulder straps holding the dress with realistic tension
```

Use negative constraints to prevent accidental bra/corset artifacts:

```text
no bra cup lines
no molded bra shape
no push-up structure
no visible lingerie support
no corset cups
no hard underwire outline
no nipple outline
```

### Material Physics

High-quality sensual fashion prompts should make the clothing feel physically real. Prioritize material response over explicit body description.

Use:

```text
liquid metallic silk
oil-gloss black satin
smooth reflective textile
soft draped fabric with real weight
side-gathered folds
realistic tension lines
subtle fabric compression
seamless luxury evening dress
high side slit with layered overlap
fabric naturally falling with gravity
realistic wrinkles, folds, seams, straps, highlights, and reflections
```

Negative material controls:

```text
no painted-on clothes
no unnatural fabric folds
no floating fabric
no plastic shine
no over-sharpened metallic texture
no muddy fabric reflection
```

### Body Scale Control

When the user asks for a full figure, do not exaggerate into impossible anatomy. Use proportional fashion language:

```text
28-year-old or 25+ adult Chinese woman
mature natural face
healthy full figure
rounded natural upper-body volume
slim waist contrast
long legs with realistic proportions
balanced curve relationship
sculpted red-carpet silhouette
full-length fashion editorial framing
```

Avoid:

```text
impossibly large anatomy
distorted waist
unnatural leg stretch
body-part close-up
overly explicit chest framing
```

### Recommended Garment-Control Template

Use or adapt this template for elegant, sensual evening-gown prompts:

```text
生成一张 9:16 竖版真人写实高级时尚写真。

人物为 28 岁中国成熟女性，五官精致自然，气质自信、优雅、成熟，身形健康丰腴、比例协调，纤细腰身与修长腿部形成明确但真实的曲线对比。画面重点是红毯礼服、布料结构、方向光和高级时尚气场，而不是身体局部特写。

她穿着油光黑色高级晚礼服，整体为 full-length luxury evening gown / couture gala fashion。礼服采用 deep plunging draped neckline 的高级剪裁，但所有敏感区域都由双层内衬、交叠布料和 seamless couture support structure 完整遮挡。开放区域仅限锁骨、肩颈、上胸轮廓和侧腰线条，形成大胆但克制的红毯轮廓。

礼服材质为 oil-gloss black satin / liquid metallic silk，表面有 smooth reflective textile 的真实反光。布料通过 thin shoulder straps、side-gathered drape、soft tension fabric、layered fabric overlap 和 natural fabric support 形成自然支撑；裙身有真实重量感、自然垂坠、褶皱、拉力线、缝线和柔和高光。高侧开衩使用 layered fabric overlap，保持优雅和安全覆盖。

构图为全身或七分身 luxury fashion editorial，禁止背面，姿态自然自信，背景为红毯、酒店大堂、城市夜景、画廊或高级室内空间之一。光线为明确方向光，柔和边缘光勾勒头发、肩线和礼服轮廓，前后景自然分离。皮肤保留真实毛孔、自然油光和细微肤色变化，发丝有重力和飞散细节，服装有真实材质响应。

负面提示：低俗色情，裸露敏感部位，透明暴露，衣服滑落，身体局部特写，未成年感，plastic skin, waxy face, beauty filter, painted-on clothes, unnatural fabric folds, floating fabric, bra cup lines, molded bra shape, push-up structure, visible lingerie support, corset cups, hard underwire outline, nipple outline, bad anatomy, extra fingers, text, watermark.
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

### 12. Oil-Gloss Black Couture Gown

Use for mature red-carpet or luxury evening-gown portraits where the user wants a full figure, deep neckline, side cutouts, metallic/satin fabric, or strong feminine curves without unsafe exposure.

Key ingredients:

```text
9:16 photoreal luxury fashion editorial, 25+ or 28-year-old adult Chinese woman, mature natural face, healthy full figure, sculpted red-carpet silhouette, oil-gloss black satin or liquid metallic silk evening gown, deep draped neckline with safe layered coverage, thin shoulder straps, side-gathered drape, double-layer inner lining, seamless couture support, high side slit with layered fabric overlap, full-length gown, directional lighting, subtle rim light, realistic skin texture, real hair gravity, realistic fabric folds and reflective material response.
```

Risk controls:

```text
all sensitive areas fully covered by fabric and lining, no visible nipple/areola outline, no transparent exposure, no wardrobe malfunction, no lingerie/corset/bra artifacts, no body-part close-up, no vulgar pose, no underage look, no painted-on clothing.
```

### 13. Adult Roleplay Uniform Fashion Portrait

Use for elegant adult roleplay styling with uniform-like garments, eye masks, badges, trays, tablets, or dark interior spaces.

Key ingredients:

```text
9:16 photoreal indoor roleplay fashion portrait, young adult Asian woman, dark corridor or private lounge interior, plaid uniform-inspired fitted mini dress, ruffled trim, high collar, waist structure, badge lanyard, black lace eye mask, white thigh-high socks or garter-inspired styling, holding a tray or tablet, full-body vertical composition, focused moody light, mysterious theatrical mood, clear fabric and prop details.
```

Risk controls:

```text
adult roleplay fashion not schoolgirl, no underage cues, no explicit sexual action, no vulgar pose, no body-part close-up, eye mask correctly shaped, prop not deformed, background clean.
```

### 14. Realistic Fantasy Elf Close-Up

Use for young-adult but non-childlike fantasy elf portraits with forest dawn light.

Key ingredients:

```text
9:16 high-finish realistic fantasy portrait, visually young but clearly adult East Asian elf woman, champagne-silver long wavy hair, pointed ears, crystal earrings, jeweled forehead ornament, pale blue/silver/gold tulle gown, vine embroidery, tiny gemstones, morning forest, ancient trees, warm gold side-backlight, light dust, soft mist, ultra-close bust portrait, face, ears, hair, jewelry, shoulder-neck line, real skin texture, shallow depth of field.
```

Risk controls:

```text
not childlike, no middle-aged heaviness if user asks youthful elegance, no excessive skin exposure, no plastic fantasy skin, no anime-only face when realism is requested.
```

### 15. Light Nurse-Themed Studio Fashion

Use for clean, playful, adult nurse-themed cosplay fashion portraits.

Key ingredients:

```text
9:16 realistic studio role portrait, young adult East Asian woman, white nurse-inspired fitted dress, clean zipper design, small red-cross details, white nurse cap, pink stethoscope, black over-knee stockings, wink or sweet smile, one hand on waist, one hand near collar, simple solid studio background, soft even light, high-end light cosplay fashion shoot.
```

Risk controls:

```text
adult subject, professional light cosplay not medical misinformation, no sexualized patient context, no explicit exposure, no underage look, no fetish framing.
```

### 16. Xianxia Sword Action Poster

Use for dynamic guofeng/xianxia action images with strong perspective.

Key ingredients:

```text
9:16 epic xianxia concept poster, adult East Asian female sword cultivator, black hair high updo, gold classical crown and forehead chain, cold determined eyes, standing or lunging from ancient pine over mountain clouds, one sword thrust toward camera, ultra-wide perspective, long ribbons and sleeves flying in strong wind, white-gold-gray gauze hanfu, blue-white sword glow, waterfalls, cliffs, cloud sea, cold gray-blue palette, cinematic motion and heroic clarity.
```

Risk controls:

```text
no distorted perspective on face/body, no broken sword hand, no excessive cleavage, no game-card clutter if cinematic poster is requested.
```

### 17. Ice Fantasy Cosplay Bust Portrait

Use for high-end cosplay official-promo style portraits with cold blue fantasy styling.

Key ingredients:

```text
9:16 realistic fantasy cosplay bust portrait, adult East Asian cos model, ice-blue long curled wig, side bangs, cool fairy makeup, calm noble gaze, hand touching cheek or chin, blue-silver-white ice fantasy costume, jewel chest ornament, star pendant, translucent tulle sleeves, silver armor motifs, ice-crystal earrings, complex shoulder pieces, blue smoke and ice mist background, soft cold light, precise rim light, high-detail jewelry and fabric.
```

Risk controls:

```text
adult, no plastic cosplay skin, no cheap costume material, no anime face if photoreal, no excessive exposure.
```

### 18. Soft Guofeng Sitting Portrait

Use for gentle guofeng/han-element cosplay portraits in wooden corridors or traditional architecture.

Key ingredients:

```text
9:16 soft guofeng portrait, young adult woman, kneeling or half-kneeling in wooden building corridor, wooden columns, railings, steps, black long hair with soft bangs, pink-white floral hair accessory, shy quiet expression, ivory-white han-element gauze dress, bustier-style inner layer safely covered by translucent outer robe, pale blue ribbon detail, pale gold embroidery, wide flowing sleeves, layered tulle skirt spread on floor, warm wood tone and soft light.
```

Risk controls:

```text
adult, no underage softness, no exposed sensitive areas, no transparent exposure, no awkward kneeling anatomy, no messy background.
```

### 19. Japanese Cinematic Flower Close-Up

Use for airy, romantic, Japanese film-style portraits with flowers and dappled light.

Key ingredients:

```text
9:16 close-up Japanese cinematic portrait, adult East Asian woman surrounded by white flowers, lazy afternoon mood, warm low-saturation vintage film color, cream white and yellow-green palette, backlight or side-backlight through petals, Komorebi dappled light on skin and shoulders, f/1.4-f/2 shallow depth of field, dreamy bokeh foreground and background, clear emotional eyes, airy feel, Iwai Shunji / Rinko Kawauchi-inspired softness.
```

Risk controls:

```text
adult not schoolgirl, no childlike framing, no over-blur on eyes, no overexposed flowers, no text.
```

### 20. Rainy Neon Fashion Portrait

Use for cinematic rainy city fashion portraits, including tasteful swimwear or black styling in a high-fashion context.

Key ingredients:

```text
vertical high-end cinematic fashion portrait, 22+ adult Japanese/East Asian woman, rainy night city street, transparent vinyl umbrella, wet black hair naturally on cheeks and shoulders, tasteful black fashion swimwear or sleek rainwear styling, quiet melancholic eye contact, street lamps and neon bokeh, rain droplets sparkling in HDR light, medium-full shot, RED Monstro 8K VV feel, slight anamorphic blur, emotional commercial fashion atmosphere.
```

Risk controls:

```text
adult, fashion context, no explicit wet-body seduction, no transparency, no body-part close-up, no unsafe street vulnerability framing.
```

### 21. Xiaohongshu Natural Lifestyle Still

Use for realistic, quiet, everyday Chinese social-platform portraits.

Key ingredients:

```text
9:16 realistic cinematic everyday portrait, young adult East Asian woman 20-26, natural East Asian features, not influencer-like, warm bedroom/window/living-room setting, bed linens, cushions, curtains, lamp, book or cup, soft indoor light from bedside lamp or weak window light, light makeup, real pores and slight imperfections, simple stable pose on bed/sofa/window, 35mm or 50mm lens, natural film-still warmth, gentle story feeling.
```

Risk controls:

```text
adult but natural, no over-sexual bedroom framing, no cheap studio look, no excessive retouch, no complex twisted pose.
```

### 22. Pure Young-Adult Portrait Generator

Use when the user asks for "清纯写真" or gives a parameter form for clean youthful adult portraits.

Key ingredients:

```text
young adult East Asian woman 20-26, clean natural beauty, clear skin, bright eyes, shoulder-neck line, collarbone line, soft waist line, coordinated legs, light and relaxed body contour, natural expression, clean outfit, bright light, real scene, high-quality social-platform portrait, not cheap studio, not selfie, not over-retouched.
```

Expansion dimensions:

```text
style, scene, clothing, temperament, body direction, line emphasis, lens direction, aspect ratio, first visual hook.
```

Risk controls:

```text
no underage look, no deliberate childishness, no lowbrow seduction, no excessive exposure.
```

### 23. Locked Curvy Portrait Generator

Use when the user provides the stricter parameter-lock template with fixed "丰腴曲线".

Key ingredients:

```text
lock all filled parameters, young adult East Asian woman 20-26 unless specified older, curvy full figure, natural full bust contour in tasteful clothing, clear waist, waist-hip transition, rounded hip-leg lines, shoulder-neck softness, elegant S-shaped posture, style and face direction both preserved, harmonized through makeup, expression, color, light, posture, and scene.
```

Output structure:

```text
参数锁定复核
完整生成提示词
本次自动补全部分
主要吸睛点
负面限制词
```

Risk controls:

```text
do not override locked user choices, no exaggerated anatomy, no explicit exposure, no underage look.
```

### 24. Moonlit 3D CG Bedroom Character

Use for mature 3D CG anime-realistic bedroom/window scenes with satin/lace styling.

Key ingredients:

```text
9:16 high-detail 3D CG realistic anime-style adult fantasy woman 22-26, silver-gray long wavy hair, blue glass-like eyes, thigh-to-head mid-close framing, sitting on bed or window-side, slight side turn, lazy quiet posture, black satin lace camisole dress with safe coverage, dark blue-gray loose sheer shawl on shoulders and arms, deep blue night bedroom, cold moonlight through window but no visible moon, soft volume light, silk and lace material detail, realistic skin, clean cinematic character poster finish.
```

Risk controls:

```text
adult, no loli look, no nipple show-through, no excessive nudity, no visible moon if user forbids it, no broken fingers or distorted body.
```

### 25. Bridal Couture Magazine Cover Duo

Use for elegant duo bridal covers. If the user requests explicit kissing or tongue contact, redirect to romantic near-kiss or soft kiss without explicit sexual detail.

Key ingredients:

```text
ultra-real luxury bridal magazine cover, two elegant adult Korean/East Asian women, complementary couture bridal looks, ivory duchess satin off-shoulder ball gown with cathedral train and 3D floral appliques, pale pink silk bias-cut slip-style bridal gown with lace tulle shawl, dark soft long curls, diamond and pearl jewelry, warm champagne studio, rose petals, 85mm lens, crisp satin and lace texture, romantic intimate embrace, cheek-to-cheek, forehead touch, near-kiss, or gentle closed-mouth kiss, Vogue-like editorial spacing if text is allowed.
```

Risk controls:

```text
no explicit tongue contact, no sexual act, no pornographic framing, no watermarks, avoid adding readable magazine masthead unless user explicitly wants text.
```

### 26. Product Exploded-Structure Infographic

Use for non-portrait product information boards.

Key ingredients:

```text
vertical 4:5 high-end product exploded-structure information board, light gray-white minimal background, central product in 3/4 perspective, components floating with slight offsets in assembly directions, realistic precise parts, metal reflection, matte plastic, glass highlights, circuit details, heatsink fins, soft contact and floating shadows, Chinese title block, 6-9 numbered component labels, thin blue guide lines, bottom feature bar with 3-4 icon modules.
```

Risk controls:

```text
labels readable but not overcrowded, no black heavy background, no random fake brand marks unless provided, no impossible component geometry.
```

### 27. New-Chinese Guofeng Half Portrait

Use for 4K photoreal new-Chinese half portraits with qin/qi/shu/hua atmosphere.

Key ingredients:

```text
native 4K vertical photoreal new-Chinese guofeng half portrait, adult Chinese woman in her early 20s, clear face, emotional eye contact, long black hair, delicate hair ornament, light summer hanfu or new-Chinese gauze outfit, elegant upper-body line, natural wrist and fingers, soft natural window light, blurred background, qin/qi/shu/hua element as atmosphere only.
```

Element choices:

```text
qin: guqin at lower or side area, clear strings and wood grain, hand resting near instrument
qi: wooden board and black-white stones softly blurred at side, calm intelligent gaze
shu: scroll, xuan paper, brush, inkstone as background atmosphere
hua: ink painting or landscape scroll, figure feels like emerging from painting
```

Risk controls:

```text
no text/watermark, cultural object does not block subject, no over-costume clutter, no excessive exposure.
```

### 28. Oriental Scroll Breakout Poster

Use for "画中美人 · 破卷而出" or any subject emerging from a scroll.

Key ingredients:

```text
9:16 oriental fantasy narrative poster, central vertical long scroll as core structure, beautiful realistic East Asian subject emerging from the scroll, body partly outside and partly still inside, outside face/hands/upper body more realistic and sharp, inside hair/skirt/sleeves still painterly and misty, foreground hand or sleeve creates depth, flower branches, birds, silk ribbons, petals, mist, gold particles, low-information dark teal/gray/gold atmosphere, clear reading path from face to hand to scroll-world relationship.
```

Risk controls:

```text
not a flat painting, not a normal guofeng portrait, no horror/ghost feeling, no unreadable text, no modern logo, no game-card clutter.
```

### 29. White Snake Character Archive Poster

Use for a 3D character archive series based on classic White Snake legend archetypes.

Key ingredients:

```text
3:4 high-finish 3D character archive poster, classic White Snake cinematic feeling, full-body central figure, natural foreground-breaking hand or prop, six to eight light translucent story panels with numbers and short Chinese notes, thin gold borders and connectors, left-side character name and small tags, bottom story index line, background with West Lake, broken bridge, rain mist, willow, Leifeng Pagoda, Jinshan Temple, pharmacy, river fog, or bamboo shadows.
```

Character routes:

```text
白素贞: dignified gentle mature beauty, oil-paper umbrella or water sleeves
小青: agile playful sharp protector, green sword breaking foreground
许仙: gentle scholar physician, prescription scroll, medicine box, or umbrella
法海: stern monk, golden bowl forward, staff as support
```

Risk controls:

```text
classic filmic legend mood, not game card, do not copy real actor face, foreground prop complete and not cropped, no unreadable text clutter.
```

### 30. Reference-Photo Mural Self-Portrait Concept

Use when the user uploads a reference portrait and wants a playful mural scene.

Key ingredients:

```text
use uploaded portrait as identity reference for face shape, hairstyle, hair color, skin texture, and overall temperament; realistic outdoor courtyard or alley with clean white wall; person wearing fluffy yellow animal onesie with cute hood and small ears; side kneeling or crouching pose; holding paintbrush; painting a giant wall mural portrait of themselves; painting tools, palette, paint cans, metal brush bucket, natural colored paint traces; mural has hand-painted realistic oil-paint texture; warm cute healing atmosphere; real camera photography.
```

Risk controls:

```text
preserve reference identity if user asks, do not claim identity if unknown, no plastic skin, no anime style, no duplicate real person except mural representation, no text, no watermark, correct perspective between person and wall.
```

### 31. Overhead Flash Bedroom Editorial

Use for restrained cold-sweet bedroom flash editorials.

Key ingredients:

```text
vertical 4:3 adult female fashion portrait, subject lying on clean white bed, diagonal overhead camera, clear centered face, relaxed body, large white negative space from sheet and pillow, cold-sweet expression, black wavy hair spread naturally, cool nude makeup, black sheer long-sleeve top with tasteful layered coverage, silver earrings or thin bracelet, direct phone/camera flash, hard shadow, bright highlights, black-white-gray palette with low-saturation pink, bedroom flash editorial, slight Y2K soft grunge.
```

Risk controls:

```text
adult, restrained intimate editorial not explicit private content, no pornographic pose, no overexposure through sheer fabric, no exaggerated chest-waist ratio, no messy bed props.
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
- High-priority garment occlusion and scale control for deep-neckline couture, side cutouts, metallic silk/satin, full figures, and red-carpet evening gowns.
- Image-type recognition and routing for roleplay fashion, fantasy elf, nurse-themed studio, xianxia action, ice cosplay, soft guofeng, Japanese flower close-up, rainy neon fashion, Xiaohongshu lifestyle, clean portrait parameter systems, bridal couture, product exploded views, new-Chinese guofeng, oriental scroll breakout, White Snake archive, reference-photo mural concepts, and overhead flash bedroom editorials.
- Parameter-locking behavior: preserve every user-filled value exactly, only auto-complete fields marked "自动" or left blank, and harmonize style/face/body conflicts without replacing locked choices.
- A rule for short prompts: expand sparse ideas into professional visual language instead of relying on explicit exposure.

Combined rule:

```text
Do not ask "how do I bypass the filter?"
Ask "how do I make the model correctly understand my safe, aesthetic, non-exploitative creative intent?"

Do not write "露哪里".
Write "服装、光影、眼神、姿态、材质、镜头、成年边界".
```
