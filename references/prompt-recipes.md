# Prompt Recipes

Use this file for reusable output formats, parameter systems, negative banks, 4K settings, and rewrite procedures.

## Compact High-Signal Portrait Recipe

Use this first for normal portraits, lifestyle photos, simple fashion portraits, or any request where the user has not asked for a complex scene. GPT Image 2 often produces cleaner portraits when the prompt gives a clear direction instead of many stacked details.

Structure:

```text
[style anchor] + [adult subject] + [mood/pose] + [scene or outfit anchor] + [lighting] + [clean photo quality]
```

Chinese template:

```text
[商业杂志风格/专业人像写真/自然生活剧照/电影感编辑肖像]，一位[成年主体]，[气质与表情]，[服装或场景核心]，[自然柔和光线/窗边光/雨夜霓虹/直闪]，干净专业摄影质感，真实皮肤质感，无文字，无水印。
```

English template:

```text
Commercial magazine editorial portrait of [adult subject], [mood/pose], [scene or outfit anchor], natural soft lighting, clean professional photography style, realistic skin texture, no text, no watermark.
```

Good compact examples:

```text
商业杂志风格专业人像写真，一位优雅自信的成年东方女性，安静看向镜头，浅色衬衫与窗边自然光，干净真实摄影质感，真实皮肤质感，无文字，无水印。
```

```text
电影感雨夜时尚人像，一位 22 岁以上成年东亚女性，透明雨伞下安静看向镜头，黑色时尚泳装与霓虹雨滴背景，自然湿发质感，干净专业摄影风格，无文字，无水印。
```

When the first output is close but imperfect, add one targeted fix at a time:

```text
脸太假 -> realistic skin texture
光太硬 -> natural soft lighting
背景太乱 -> minimal clean background
网红感太重 -> commercial editorial style, natural face, not over-retouched
AI感太强 -> clean professional photography style, no over-sharpening, no plastic skin
```

## Low-Intersection Modular Prompt Recipe

Use this when the user's prompt involves guofeng, cosplay, roleplay, couple/interaction composition, mood tension, thin or ornate wardrobe, strong body-line focus, or any scene where prose creates too much semantic binding.

Core idea:

```text
Do not let the model read a plot paragraph.
Let the model read independent visual modules.
```

Block order:

```text
画面质感 + 人物审美 + 服饰材质
动作姿态
视觉重点
光线方式
互动对象或道具
人物状态
场景氛围
限制与负面词
```

Safe modular template:

```text
[画面质感] + [明确成年人物审美] + [服饰材质与安全遮挡]
[动作姿态，保持自然稳定]
[视觉重点，落在脸、眼神、服装剪裁、光影或整体轮廓]
[光线方式]
[互动对象或道具，保持空间关系，不写性升级]
[人物状态，克制、自然、非失控]
[场景氛围]
无文字，无水印，不低俗，不透明暴露，不身体局部特写，肢体自然
```

Detailed conversion:

```text
Original prose intent: [one sentence]
Risky binding: [wardrobe/body/relationship/state/camera words that became too fused]
Modular rewrite:
[block prompt]
```

Use block mode for fast testing. Convert to full prose only when the user asks for a polished paragraph prompt.

## Expression-Controlled Portrait Recipe

Use when the user gives an expression, emoji, kaomoji, meme face, or asks for a specific emotional reaction.

Translate symbols into face mechanics:

```text
嫌弃 / tsk -> furrowed brows, narrowed side glance, wrinkled nose, slightly pursed lips, head slightly tilted away
冷淡 -> relaxed mouth, low-intensity gaze, minimal smile, still posture
委屈 -> moist eyes, slightly lowered brows, soft mouth, restrained sadness
轻蔑 -> raised brow, asymmetric half-smile, sideways glance
惊讶 -> widened eyes, parted lips, lifted brows, paused gesture
疲惫 -> half-lidded eyes, relaxed shoulders, muted mouth, soft under-eye shadows
温柔 -> softened eyes, slight smile, relaxed cheek muscles, open posture
自信 -> direct gaze, lifted chin, stable shoulders, controlled mouth shape
```

Prompt shape:

```text
[style anchor] portrait of [adult subject], [primary expression mechanics], [secondary emotional nuance], [pose/crop], [light], clean professional photography style, no text, no watermark.
```

Rules:

```text
Do not generate floating emoji unless the user explicitly asks for visible emoji.
Use one primary expression and at most one secondary nuance.
Strong expressions need clear eyebrows, eyes, mouth, head angle, and posture.
```

## Image-To-Prompt Distillation Recipe

Use when the user uploads an image or asks to learn a picture's style.

Output:

```text
1. 视觉识别
- 图像类型:
- 构图:
- 第一眼吸睛点:

2. 可复用方法
- 主体:
- 姿态:
- 服饰/材质:
- 光线:
- 色彩:
- 背景:
- 负面边界:

3. 生成提示词
[fresh prompt]
```

Rules:

```text
Extract the visual system, not the source.
Do not mention the source in final skill output.
If a real person reference is uploaded by the user, preserve identity only when the user asks; otherwise describe general visual traits.
```

## Fast Final Prompt Recipe

Use this when the user asks for a complete detailed prompt, gives a complex scene, asks for strict outfit coverage, or provides locked parameters.

```text
生成一张 [画幅比例] [媒介/摄影/渲染风格]，主题为「[主题]」。

画面主体是一位 [年龄明确的成年身份]，[脸型/五官/发型/气质]。她的整体气质 [气质标签]，漂亮、有吸引力但保持高级克制。身形为 [身形]，比例自然协调，[肩颈/锁骨/腰线/腿部/整体曲线] 清晰，但画面重点不是身体局部，而是 [眼神/姿态/服装剪裁/材质/光影/镜头语言]。

她穿着 [服装]，材质为 [材质]，剪裁 [剪裁]，有 [细节]。服装贴合身体线条但保持得体；如有深领、露背、薄纱、开衩或泳装，写明 [安全遮挡/内衬/布料交叠/不透明/无走光]。

场景为 [场景]，人物 [姿态动作]。镜头采用 [镜头/构图]，光线为 [光线]，色彩为 [色调]。画面要求 [皮肤/发丝/布料/水面/道具/空间] 真实细腻，高完成度，干净构图。

负面提示：[按场景选择负面词]。
```

## Director Parameter System

Use when the user wants a reusable generator, gives style fields, or expects the agent to "像摄影导演一样补全".

Required loop:

```text
1. Lock every filled user field.
2. Route the request to one style family.
3. Fill only blank/自动 fields.
4. Build modules: subject, face, body, wardrobe, pose, scene, camera, light, filter, negative.
5. Merge into one finished prompt; do not expose rough modules unless the user asks.
```

Recommended user fields:

```text
写真风格: 自动 / 清纯生活照 / 纯欲曲线生活照 / 都市时尚写真 / 古风仙侠美人图 / 电商服装模特图 / 男性魅力人像 / 品牌KV海报 / 城市情绪海报
场景方向: 自动 / 卧室 / 窗边 / 咖啡馆 / 城市街头 / 海边 / 宫殿回廊 / 摄影棚 / 品牌场景 / 城市主场景
服装方向: 自动 / 白衬衫 / 针织 / 吊带外搭 / 修身裙装 / 唐风大袖 / 新中式 / 商务西装 / 产品主视觉服装
气质标签: 自动 / 温柔 / 清冷 / 松弛 / 明艳 / 故事感 / 自信 / 仙气 / 商业感
五官方向: 自动 / 初恋感淡颜 / 邻家清秀脸 / 温柔圆脸 / 清冷淡颜 / 电影故事脸 / 古典东方美人脸 / 稳重男性脸
身形方向: 自动 / 轻盈纤细 / 匀称柔美 / 丰腴自然曲线 / 男性匀称成熟
线条重点: 自动 / 肩颈 / 锁骨 / 腰线 / 小腹 / 大腿 / 全身服装版型 / 面部轮廓
镜头方向: 自动 / 半身近景 / 半身到大腿 / 全身 / 轻侧身 / 回眸 / 行走抓拍 / 低机位 / 正面商品展示
光线氛围: 自动 / 窗边柔光 / 冷白低反差 / 奶油暖白 / 直闪 / 金色侧逆光 / 夜景霓虹 / 棚拍柔光
滤镜效果: 自动 / 生活剧照 / 冷白纯欲 / 奶油暖白 / 日系胶片 / 高级商业精修 / 古风仙气
画幅比例: 9:16 / 3:4 / 4:5 / 1:1 / 16:9
平台用途: 自动 / 社交平台发布 / 头像 / 个人品牌形象 / 电商主图 / 海报KV / 角色写真
```

Route defaults:

```text
清纯生活照 -> natural face, clean outfit, simple stable pose, bright soft light
纯欲曲线生活照 -> clean face, restrained body-line emphasis, cool/soft film-still filter
都市时尚写真 -> confident expression, stronger styling, city depth, editorial light
古风仙侠美人图 -> classical face, ornate hair/accessories, hanfu/tang silhouette, palace or misty landscape
电商服装模特图 -> complete outfit, accurate garment structure, neutral commercial light, no mood overtake
男性魅力人像 -> identity retention, mature gaze, clothing/status/scene translate personality
品牌KV海报 -> visual DNA, product hierarchy, brand color, slogan tone, clean layout
城市情绪海报 -> city recognition, emotional hook, unified scene, controlled typography
```

## Parameter-Locked Output

Use when the user provides fields like 写真风格、场景方向、服装方向、气质标签、身形方向、线条强调、镜头方向、画幅比例.

Output:

```text
1. 参数锁定复核
- 写真风格：...
- 五官方向：...
- 场景方向：...
- 服装方向：...
- 气质标签：...
- 身形方向：...
- 线条强调：...
- 镜头方向：...
- 画幅比例：...

2. 完整生成提示词
[one polished prompt]

3. 本次自动补全部分
[list only fields inferred from 自动/blank]

4. 主要吸睛点
[3-5 bullets]

5. 负面限制词
[compact negative bank]
```

Rules:

```text
Never replace a locked field.
If user says "自动", choose the best match and disclose it.
If style and face conflict, keep both; harmonize through makeup, expression, lighting, pose, clothing color, and scene.
If body direction is fixed as 丰腴曲线, do not slim it down. Keep it proportional and tasteful.
```

## Cinematic Clean-Curvy Lifestyle Recipe

Use for "电影生活剧照感", "纯欲曲线", "冷白滤镜", "清纯脸 + 有吸引力身形".

Definition:

```text
清纯感五官 + 自然吸引力身形 + 克制欲感 + 写实生活照 + 电影生活剧照滤镜
```

Not definition:

```text
lowbrow erotic pose, lingerie ad, exaggerated bust, hard seduction, heavy retouching, cheap bedroom fantasy
```

Build order:

```text
1. 明确年轻成年东方女性, usually 20-28.
2. Choose face: 初恋感淡颜 / 邻家清秀脸 / 温柔圆脸 / 清冷淡颜 / 电影故事脸.
3. Choose body direction: 自然吸引力曲线 / 腰臀曲线感 / 胸腰腿线条感 / 丰腴自然曲线 / 轻熟曲线感.
4. Set line emphasis: 锁骨、肩颈、腰线、小腹、大腿; show through clothing, pose, crop, and light.
5. Use stable poses: 坐在床边, 靠窗坐姿, 轻侧身站姿, 半身到大腿, 行走抓拍.
6. Use one filter: 冷白低反差, 柔白生活剧照, 奶油暖白, dusk beach, street-corner candid.
7. Add boundaries: no minor-coded styling, no explicit exposure, no cheap studio, no over-retouch.
```

Compact template:

```text
9:16 写实电影生活剧照感人像，一位 20-28 岁年轻成年东方女性，[五官方向]，[身形方向]，穿着[克制贴身但得体的生活感服装]，在[生活化场景]中[稳定自然姿态]，重点通过锁骨、腰线、发丝、眼神和冷白柔光呈现自然吸引力，真实皮肤质感，轻微生活滤镜，干净高级，不低俗，无文字无水印。
```

Negative bank:

```text
未成年感，幼态娃娃脸，低俗色情，刻意挑逗，廉价情趣风，夸张爆乳，透明暴露，身体局部特写，影楼感，网红重修图，塑料皮肤，过度磨皮，肢体扭曲，错误手指，背景杂乱，文字，水印。
```

## 3D CG To Realistic Bridge

Use when direct realistic output is unstable, too conservative, or loses beauty, but the target is still safe and non-explicit.

Step 1 prompt should be a clean 3D CG anchor:

```text
成年主体 + clear composition + safe wardrobe coverage + material physics + scene + lighting + restrained beauty
```

Step 2 rewrite should preserve:

```text
same composition, pose, outfit structure, hairstyle, scene, lighting, subject age, garment coverage
```

Step 2 must remove:

```text
二次元, 3D CG, Unreal, Octane, PBR, 渲染, 次表面散射, 角色插画, anime/cg/render words
```

Step 2 should add:

```text
真实摄影, natural skin texture, real wet/dry hair, believable fabric, real room/pool/street space, camera snapshot/editorial language
```

Bridge example:

```text
把上一步的 3D CG 泳池角色转写为真实摄影版本：保留 9:16 竖版、人物在泳池扶梯旁半身到大腿构图、蓝发、白色得体泳装、清澈池水、夏日自然光和安全遮挡；去掉二次元、CG、渲染词，改成真实相机拍摄、真实皮肤、真实湿发、水面反射和度假写真质感。
```

## Brand KV And City Poster Recipe

Use for brand advertising, drink/coffee/cosmetics KV posters, city confession posters, and city terrain-outline posters.

Brand KV compiler:

```text
1. Input: brand name, product category, target mood, output ratio.
2. Infer brand visual DNA: color, consumer emotion, product hierarchy, scene language, slogan tone.
3. Build one clean key visual, not a logo pile.
4. Make the product or brand experience the protagonist.
5. Add typography only when the user wants poster output; keep text short and readable.
```

Brand KV template:

```text
生成一张 [画幅] 高级品牌 KV 海报，品牌为「[品牌名称]」，品类为 [品类]。请先根据品牌名称和品类自动推断视觉气质、核心颜色、目标人群、产品主次关系和广告语气质。画面不是简单堆 logo，而是用产品、场景、光线、色彩和版式表达品牌性格。主视觉为 [产品/人物/场景]，背景为 [品牌场景]，文字层级克制清晰，整体适合社交平台发布和品牌视觉提案。无乱码文字，无廉价大 logo，无杂乱元素。
```

City emotion poster compiler:

```text
1. Input: city name + emotion theme.
2. Recognize landmarks, skyline, river/sea/mountain/street/night mood.
3. Build a unified emotional scene; do not make a tourist collage.
4. Typography should feel like a poster title, not a travel brochure.
5. Romance can come from rain, dusk, lights, river reflections, negative space; avoid cheap hearts and wedding props.
```

City terrain-outline compiler:

```text
1. The city boundary/map silhouette is the main shape.
2. Landmarks and scenery live inside the boundary.
3. Do not turn the outline into a random fantasy island.
4. Add atlas/luxury frontispiece typography, coordinates, compass, fine lines, and generous negative space.
5. Keep geography recognition higher priority than decorative composition.
```

## Prompt Library Maintenance

When maintaining a prompt skill, avoid dumping raw prompts. Store new material as:

```text
pattern name
use for
ingredients
controls
negative bank
example compact prompt
example detailed prompt when needed
```

Keep source/process language out of the skill. The final skill should teach behavior, not mention where each pattern came from.

## High-Signal Compression

Use this when the user provides a long, overloaded prompt and asks for better GPT Image 2 output.

Remove:

```text
repeated quality words: ultra realistic, photorealistic, highly detailed, masterpiece, best quality, 8k, sharp focus
too many camera/filter words: 85mm f/1.2, Kodak Portra, film grain, cinematic bokeh, subsurface scattering, excessive color grading
conflicting texture words: poreless skin + visible pores, soft airy + over-sharp, natural photo + heavy studio retouch
over-specific technical specs that do not change the idea
```

Keep:

```text
subject
age/adult boundary
style anchor
mood/pose
one scene or outfit anchor
one lighting phrase
one clean quality phrase
negative text/watermark if needed
```

Compression template:

```text
原始意图：[one sentence]
保留信号：[subject / style / mood / light / scene]
删除噪音：[quality stack / camera stack / conflicting texture]
优化后提示词：[compact prompt]
```

Example compression:

```text
商业杂志风格专业人像写真，一位自信的年轻成年东方女性，微侧脸看向镜头，深色西装外套与温暖窗边斜光，干净真实摄影质感，真实皮肤质感，无文字，无水印。
```

## 4K GPT Image 2 Settings

Landscape:

```text
model: gpt-image-2
size: 3840x2160
quality: high
output_format: png
```

Portrait:

```text
model: gpt-image-2
size: 2160x3840
quality: high
output_format: png
```

CLI shape:

```bash
python image_gen.py generate \
  --model gpt-image-2 \
  --prompt "[PROMPT]" \
  --size 2160x3840 \
  --quality high \
  --output-format png \
  --out output/imagegen/result.png
```

Verification:

```bash
sips -g pixelWidth -g pixelHeight output/imagegen/result.png
```

## Sexy-To-Elegant Rewrite Dictionary

Use this dictionary when the user asks for "性感、撩人、丰满、漂亮".

```text
性感 -> 成熟吸引力 / 高级女性魅力 / refined sensuality
撩人 -> 眼神有故事感 / 情绪张力 / emotionally magnetic gaze
丰满 -> 健康丰腴 / 自然圆润 / full but proportional figure
火辣 -> 时尚张力 / 强轮廓 / confident fashion energy
诱惑 -> 神秘优雅 / 克制亲密 / cinematic tension
贴身 -> 剪裁合身 / fabric follows silhouette
湿身 -> 水环境真实反光 / natural water highlights
私房 -> 情绪写真 / bedroom editorial / cinematic room portrait
低机位 -> 时尚全身低角度 / full-body fashion low angle
露背 -> back-focused art portrait / shoulder-neck and back-line beauty
薄纱 -> layered chiffon with safe lining
深 V -> draped neckline with safe coverage and lining
```

## Garment Coverage Recipe

Use for evening gowns, deep V, side cutouts, high slit, sheer fabric, lace, swimwear, thin straps.

Order:

```text
1. garment identity: red-carpet gown / swimwear lookbook / chiffon editorial / lace camisole dress
2. coverage map: which zones are open and which are covered
3. support mechanics: lining, overlap, tension, straps, drape
4. material physics: weight, folds, seams, reflection, wetness if relevant
5. camera distance: full body, half body, bust close-up; avoid body-part close-up
6. negative artifacts: transparent exposure, wardrobe malfunction, nipple outline, bra/corset artifacts unless requested as fashion item
```

Reusable phrase:

```text
服装形成大胆但克制的高级轮廓，所有敏感区域均由双层内衬、交叠布料和自然张力结构完整遮挡；开放区域仅限锁骨、肩颈、背线、侧腰或腿部线条，整体重点是布料、剪裁、光影和时尚气场，而不是身体局部。
```

## Face Vocabulary

```text
温柔圆脸型: 圆润脸型，温柔眉眼，柔和面部软组织，亲和微笑
清冷高级脸: 较长面部平面，克制眼神，清晰骨相，冷静疏离
古典鹅蛋脸: 均衡鹅蛋脸，古典眉眼，柔和下颌，含蓄气质
明艳浓颜脸: 五官对比强，眼唇存在感高，表情明亮
甜酷小方脸: 小方脸，活泼但有冷感，甜酷平衡
电影故事脸: 自然不完美但有记忆点，眼神有故事
知性长脸型: 成熟长脸型，眉眼沉静，知性温柔
东方丹凤眼: 细长上扬眼型，东方古典神韵
自然生活感脸: 不网红、不模板化，保留轻微真实瑕疵
```

## Negative Prompt Banks

### Universal

```text
未成年感，幼态化，低俗色情，裸露敏感部位，身体局部特写，夸张比例，畸形身体，错误手指，多余肢体，五官错位，塑料皮肤，过度磨皮，低清晰度，背景杂乱，文字，水印，logo
```

### Realistic Photo

```text
假脸，AI塑料感，过度美颜，蜡像皮肤，假发片感，棚拍廉价感，不真实光线，过度HDR，过度锐化，脏灰背景，模糊脸部
```

### 3D CG

```text
廉价二次元，低模，塑料材质，头发糊成一片，布料贴图平，肢体穿模，过曝炫光，背景杂乱
```

### Clothing And Coverage

```text
透明暴露，走光，衣服滑落，painted-on clothes，unnatural fabric folds，floating fabric，nipple outline，bra cup lines，molded bra shape，visible lingerie support，corset cups，hard underwire outline
```

### Product Infographic

```text
零件排成死板直线，标签过密，文字乱码，黑色厚重背景，产品遮挡严重，不真实结构，廉价3D，过度反光
```

## Rejection Repair

If a prompt is rejected:

```text
1. Remove explicit body/sex words.
2. Keep adult identity.
3. Reframe as fashion/editorial/product/lifestyle/character art.
4. Add clothing coverage mechanics.
5. Replace private sexual mood with cinematic, emotional, or commercial mood.
6. Add negative boundaries.
```

If the image looks too AI or over-processed:

```text
1. Shorten the prompt.
2. Remove repeated quality words.
3. Remove excessive lens/film/grain/camera simulation.
4. Keep one style anchor and one lighting direction.
5. Add "clean professional photography style" or "natural soft lighting" if needed.
```

Example:

```text
Before: 性感私房，胸部突出，挑逗姿势，湿身。
After: 成年女性情绪写真，电影感室内光，剪裁合身的缎面服装，肩颈和整体姿态优雅，真实皮肤与布料高光，情绪克制，不低俗，无裸露、无身体局部特写、无透明暴露。
```
