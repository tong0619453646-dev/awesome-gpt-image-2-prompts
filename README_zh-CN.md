<div align="center">

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2 提示词" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-874_cases-111111)](README_zh-CN.md#menu)
[![Try GPT Image 2 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2-on_APIKO-4F46E5)](https://apiko.app/zh/models/gpt-image-2?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=model_try)
[![GPT Image 2 API docs](https://img.shields.io/badge/GPT_Image_2-API_docs-111111)](https://apiko.app/zh/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-Current-111111)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2 提示词

<a id="introduction"></a>
## 🌟 简介

**GPT Image 2 提示词：874 条可直接复制的免费提示词，附成图，涵盖广告、角色、电商、人像、海报和 UI。**

附成图的 GPT Image 2 提示词，分成七大类。复制一条，或一键送到模型页运行。

在线搜索和筛选： [apiko.app/gpt-image-2-prompts](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2-prompts&utm_content=intro).

> [!NOTE]
> 提示词保持作者发布时的原文，所以大多是英文；标题和简介是我们写的。每条都署名作者并链接原帖。

<a id="quick-start"></a>
## 🚀 快速开始

**网页上用：** 每条都有「在 APIKO 运行」链接，会在 [apiko.app](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=browser) 打开这条示例；点「使用」，提示词就会填进 GPT Image 2 试用台。

**用 API：** 先创建 [APIKO API Key](https://apiko.app/zh/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=api_key)，再创建异步任务并轮询，直到图片生成完成。

```bash
export APIKO_API_KEY="your_key_here"

TASK_ID=$(curl -s https://api.apiko.app/v1/images/generations \
  -H "Authorization: Bearer $APIKO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "gpt-image-2",
  "prompt": "A minimalist poster of a paper boat on a calm lake at sunrise, the title \"Morning\" in bold serif type.",
  "size": "16:9",
  "resolution": "1k",
  "quality": "medium",
  "async": true
}' | python3 -c 'import json,sys; print(json.load(sys.stdin)["id"])')

# When status is "completed", the image is at data[0].url (kept for 24 hours).
while :; do
  TASK=$(curl -s https://api.apiko.app/v1/tasks/$TASK_ID \
    -H "Authorization: Bearer $APIKO_API_KEY")
  printf '%s\n' "$TASK"
  printf '%s' "$TASK" | grep -qE '"status": *"(completed|failed)"|"error": *\{' && break
  sleep 5
done
```

接口: `POST https://api.apiko.app/v1/images/generations` (创建任务) · `GET https://api.apiko.app/v1/tasks/{id}` (查询状态和结果)

<a id="how-to-write"></a>
## ✍️ 怎么写 GPT Image 2 提示词

下面这些卡片里反复出现的四种写法。

- **先定版式** · `画面类型 + 版式 + 主体 + 原文文字` — 先说这是什么图（2x2 横幅、九格分镜、海报）、怎么分区，再逐格写主体和上面的文字。有些提示词直接写成 JSON，带 layout、text_labels 之类的字段。
- **镜头与光线** · `景别 + 镜头或光线 + 材质 + 氛围` — 写实人像会点明景别、镜头或胶片质感（35mm 闪光灯、窗光、逆光）和表面质地，最后用一句话收住氛围。给出具体风格，比写“好看”管用。
- **参考、保留、修改** · `参考图 + 保留 + 修改` — 上传照片时，先说哪些要保持不变（脸、服装、产品形状），再说哪些要改（风格、背景、文字）。依赖参考图的卡片会在提示词里写明。
- **模板槽位** · `固定提示词 + {槽位}` — 可复用的提示词把变量放进花括号，比如 {argument name="brand" default="…"}。把默认值换成你的品牌、城市或产品，其余不动。

**这些 GPT Image 2 提示词示例说明了什么**

- **文字加引号。** 要出现在图里的字放进引号，常常还写明位置（“左上角：……”）。海报和广告卡片都是逐行这样写的。
- **写清格数。** 宫格和分镜会直接说要几格，比如 4、9、16，再按顺序描述每一格。
- **比例行只是说明。** 不少提示词开头有一行“Aspect Ratio: 9:16”。在 APIKO 上，输出比例由 size 参数决定，所以也要在参数里设置。
- **结尾写不要什么。** 常见结尾是一小串排除项：不要水印、不要模糊、不要五官变形、不要塑料皮肤。
- **长提示词很正常。** 很多卡片超过 1,000 个字符，少数超过 1,500。API 最多接受 8,000 个字符。

<a id="menu"></a>
## 📑 目录

- [⭐ 精选](#featured) (6)
- [📣 广告](prompts/ad-creative_zh-CN.md) (52) — 营销海报、产品广告和品牌板，标题、标语和价格文字直接写进提示词。
- [🧩 角色](prompts/character_zh-CN.md) (29) — 角色设定表、游戏主视觉和动漫卡牌，让同一个形象在不同姿势和画格里保持一致。
- [🛍️ 电商](prompts/ecommerce_zh-CN.md) (33) — 商品主图、棚拍图和详情信息图，也有同一商品的广告分镜。
- [📷 人像](prompts/portrait_zh-CN.md) (243) — 杂志大片、自拍、胶片质感、爱豆九宫格和二次元头像，多数写明了相机或光线风格。
- [🪧 海报](prompts/poster_zh-CN.md) (323) — 旅行、电影、美食和星座海报，以及信息图与拼贴，版式和字体就是设计本身。
- [🖥️ UI](prompts/ui_zh-CN.md) (116) — 界面截图、品牌板、分镜和信息图，都由带标注的分区拼成。
- [🆚 对比测试](prompts/comparison_zh-CN.md) (78) — 并排的提示词测试和细节展示，另有分镜表和截图仿制。
- [❓ 常见问题](#faq)
- [🔗 相关链接](#related)

<a id="featured"></a>
## ⭐ 精选

<a id="ad-creative-08"></a>
### 8. 奢华计时腕表广告

作者 [@AlwaveNazca](https://x.com/AlwaveNazca) · 1:1 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08)** · [原帖](https://x.com/AlwaveNazca/status/2048147643809865950)

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-08.webp" width="480" alt="奢华计时腕表广告 – GPT Image 2"></a>

**提示词:**

```text
A dramatic luxury product advertising image for a motorsport-inspired chronograph wristwatch in a dark studio. Center-left foreground, show a single stainless steel chronograph watch standing upright at a slight three-quarter angle, with a black dial, two red-accent subdials, slim silver hour markers, a tachymeter bezel, and visible crown and pushers on the right side. The watch has a black leather strap with bold red stitching along both edges and a sporty premium finish. To the right of the watch, place one black square presentation box slightly behind it, textured like leather, with red stitching around the lid and a silver embossed eye-shaped logo above the text “NESS STUDIO” and smaller red text “TRACK SURFACE.” At the top center of the composition, add the same silver eye logo with the words “NESS STUDIO” and smaller “BY NICOLAS.” Across the background, place one oversized blurred word, {argument name="headline text" default="PRECISION"}, in large gray capital letters spanning nearly the full width. The scene is set against a deep black background with cinematic red and white horizontal light streaks crossing behind the products from left to right, suggesting speed and racetrack energy. Use a glossy wet ground plane with reflective texture, catching red highlights and mirrorlike reflections beneath the watch and box. At the bottom center, add the text “CHRONOGRAPH SERIES” in clean white spaced capitals with thin red horizontal lines extending on both sides, and below it smaller red capitals reading {argument name="tagline text" default="ALSACE MADE"}. Color palette: black, charcoal gray, silver steel, vivid racing red, and a touch of white. Lighting should be high-contrast and premium, with crisp specular highlights on the metal case, subtle soft fill on the box, and moody shadows. Overall style: ultra-polished commercial product photography, luxury watch campaign, sharp focus on the products, sleek branding, high-end automotive aesthetic.
```

<a id="ad-creative-14"></a>
### 14. 奢华迪拜微缩城市模型

作者 [@silentempiredev](https://x.com/silentempiredev) · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14)** · [原帖](https://x.com/silentempiredev/status/2048086378383384773)

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-14.webp" width="480" alt="奢华迪拜微缩城市模型 – GPT Image 2"></a>

**提示词:**

```text
A hyper-detailed cinematic isometric miniature city model of {argument name="landmark tower" default="Burj Khalifa"} rising dramatically from the center of a square architectural master-plan board, presented like a luxury urban planning maquette on a black background. The composition shows one dominant ultra-tall silver skyscraper in the exact center, surrounded by a dense ring of modern high-rise towers, illuminated roads, bridges, and glowing warm city lights. Curving turquoise-blue water features and artificial lakes wrap around the central district in multiple connected pools and canals, with one large circular fountain-like feature near the tower base and several small island shapes visible in the water. In the lower right quadrant, include a large low-rise complex with rounded geometric roofs and subtle green-lit sections, connected by multilane roads and looping interchanges. The entire city sits on one square beige map board engraved with faint street grids and planning lines, with the board edges clearly visible and slightly raised. Viewpoint is a high three-quarter isometric angle, centered and symmetrical, with the tower extending far upward into negative space. Lighting is dramatic and luxurious: warm golden edge lights on buildings and roads, cool reflections in the water, crisp metallic highlights on the central tower, and a deep black void surrounding the model. Style should feel like a photorealistic architectural visualization mixed with a premium collectible scale model, extremely intricate, sharp, polished, and elegant.
```

<a id="poster-95"></a>
### 443. 跨越两个世纪的纽约电影海报

作者 [@Shinning1010](https://x.com/Shinning1010) · 3:4 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95)** · [原帖](https://x.com/Shinning1010/status/2049460661109879022)

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-95.webp" width="320" alt="跨越两个世纪的纽约电影海报 – GPT Image 2"></a>

**提示词:**

```text
Create a cinematic 3:4 vertical poster of New York City that feels truly epic and unconventional, showing the passage from the 20th century to the 21st century in one seamless image. Place a lone figure at the center of the composition, standing in the middle of the street and looking forward as if witnessing New York across time. The left side should depict 20th-century New York with warm sepia atmosphere, vintage taxis, old newsstands, retro lamps, and landmarks like the Chrysler Building and Empire State Building. The right side should depict 21st-century New York with glass skyscrapers, One World Trade Center, digital billboards, and modern urban energy. Make the transition natural rather than split-screen, with coherent perspective, wet reflective pavement, realistic textures, atmospheric depth, and no text.
```

<a id="poster-176"></a>
### 521. 古文明微缩立体场景

作者 [@Naiknelofar788](https://x.com/Naiknelofar788) · 2:3 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176)** · [原帖](https://x.com/Naiknelofar788/status/2054221110372405534)

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-176.webp" width="320" alt="古文明微缩立体场景 – GPT Image 2"></a>

**提示词:**

```text
A highly detailed miniature diorama of an ancient civilization under construction, displayed directly on top of large rolled-out architectural blueprints spread across a realistic wooden drafting table. The scene features iconic historical architecture from [CIVILIZATION OR LOCATION], including partially completed monuments, temples, towers, walls, palaces, streets, or ceremonial structures at different stages of construction. Tiny craftsmen, builders, engineers, and workers interact naturally throughout the scene using historically accurate tools, scaffolding, ramps, cranes, carts, stone blocks, timber frameworks, and construction platforms.
The miniature terrain blends seamlessly into the printed engineering drawings beneath, combining realistic sand, stone, earth, marble, vegetation, or desert textures with visible architectural floor plans, elevation sketches, measurements, annotations, and cross-sections. Surrounding the workspace are drafting instruments, compasses, rolled parchment plans, books, rulers, brass weights, candles, maps, carving tools, and historical reference materials that enhance the workshop atmosphere.
Soft cinematic lighting with warm natural sunlight from a nearby window, shallow depth of field, ultra realistic textures, handcrafted museum-quality scale model aesthetic, intricate miniature detailing, photoreal materials, atmospheric realism, editorial architectural photography style, clean composition, immersive world-building, vertical composition, extremely high detail, realistic shadows, authentic historical mood.
```

<a id="ui-73"></a>
### 738. 博物馆爆炸组装图

作者 [@Gdgtify](https://x.com/Gdgtify) · 16:9 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73)** · [原帖](https://x.com/Gdgtify/status/2052498708521259162)

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ui-73.webp" width="480" alt="博物馆爆炸组装图 – GPT Image 2"></a>

**提示词:**

```text
16:9 2x2 grid, do this for cybertruck, reaper drone, james webb telescope, and another complex machine: do this for cybertruck: { "exhibit_type": "physical exploded assembly", "subject": "$complex_invention", // e.g., "an enigma machine", "a mechanical chronometer" "physical_constraints": { "state": "the machine is pulled apart into its 50 primary components along a horizontal axis.", "support_system": "no magical floating. every single floating gear and casing is physically held in the air by taut, thin, steel suspension wires and heavy brass museum clamps.", "background": "a flat, neutral-grey museum wall." }, "lighting_and_shadows": { "setup": "hard spotlighting from the top left.", "shadow_effect": "critical: the floating, separated components and their suspension wires must cast a highly complex, overlapping, beautiful shadow pattern directly onto the grey wall behind them." } }
```

<a id="character-16"></a>
### 67. 风格化 3D 滑板角色

作者 [@iamaiistudio](https://x.com/iamaiistudio) · 4:5 · **[▶ 在 APIKO 运行](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16)** · [原帖](https://x.com/iamaiistudio/status/2062038112398954712)

<a href="https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/character-16.webp" width="320" alt="风格化 3D 滑板角色 – GPT Image 2"></a>

**提示词:**

```text
Design a stylized 3D cartoon skater character with a premium animated-film look, mixing Pixar-like polish, Spider-Verse energy, and indie street-art attitude.

Character details:
- exaggerated proportions with long, skinny limbs
- oversized hoodie in customizable pink
- baggy ripped denim jeans
- chunky sneakers
- expressive tired-but-confident face
- messy stylized hair
- large headphones
- backpack covered with pins and patches
- standing naturally on a skateboard

Visual style:
Clean cinematic 3D render with soft global illumination, subtle chromatic aberration, ultra-detailed textures, smooth shading, playful but believable anatomy, high-end character design, stylized streetwear fashion, and urban youth energy.

Pose:
Slightly slouched posture, one hand relaxed, cool bored expression, looking sideways.

Background:
Minimal clean studio background with soft shadows and a centered composition.

Extra details:
Add stickers, embroidered patches, smiley pins, doodles, skate-culture details, early-2000s urban energy, cinematic render quality, and a polished animation-studio finish.

Aspect ratio: 4:5 vertical.
```

- **[📣 查看「广告」全部 52 条](prompts/ad-creative_zh-CN.md)**
- **[🧩 查看「角色」全部 29 条](prompts/character_zh-CN.md)**
- **[🛍️ 查看「电商」全部 33 条](prompts/ecommerce_zh-CN.md)**
- **[📷 查看「人像」全部 243 条](prompts/portrait_zh-CN.md)**
- **[🪧 查看「海报」全部 323 条](prompts/poster_zh-CN.md)**
- **[🖥️ 查看「UI」全部 116 条](prompts/ui_zh-CN.md)**
- **[🆚 查看「对比测试」全部 78 条](prompts/comparison_zh-CN.md)**

<a id="faq"></a>
## ❓ 常见问题

<details>
<summary><b>这些 GPT Image 2 提示词可以免费用吗？图片归谁？</b></summary>

整个合集已以 CC0 贡献到公有领域，提示词可以随意复制、修改和运行。示例图片归每张卡片署名的创作者；你自己生成的图，要确认提示词里用到的品牌、标志和真人形象是否有权使用。

</details>

<details>
<summary><b>GPT Image 2 提示词该用中文还是英文写？</b></summary>

这里的提示词按作者原文展示，以英文为主，也有中文，不做翻译。GPT Image 2 支持中文和英文，用你写得最顺的那种即可。

</details>

<details>
<summary><b>怎么用 API 运行一条 GPT Image 2 提示词？</b></summary>

调用 POST /v1/images/generations，传 model 为 gpt-image-2、你的 prompt、size（如 16:9）、resolution（1k、2k 或 4k）和 "async": true，再轮询 GET /v1/tasks/{id}。完整参数见 API 文档。

</details>

<details>
<summary><b>GPT Image 2 支持哪些比例和尺寸？</b></summary>

比例有 1:1、16:9、9:16、3:2、2:3、4:3、3:4、5:4、4:5 和 21:9，分辨率 1k、2k、4k。每个比例和档位对应固定像素尺寸，也可以直接传这些尺寸中的某一个（WIDTHxHEIGHT）。不支持 auto。

</details>

<details>
<summary><b>需要参考图的卡片怎么在 GPT Image 2 上用？</b></summary>

先把图片上传到 POST /v1/uploads/images，再把返回的公开 HTTPS 链接放进 images，调用 POST /v1/images/edits。GPT Image 2 支持 0 到 16 张参考图；带参考图时，输出尺寸不保证与请求一致。

</details>

<details>
<summary><b>为什么我的 GPT Image 2 结果和卡片上的图不一样？</b></summary>

图像模型不是确定性的，同一条提示词每次的结果都会不同。作者也可能用了别的工具、设置或参考图。

</details>

<details>
<summary><b>在 ChatGPT 里用的 GPT Image 2 提示词，API 里能用吗？</b></summary>

提示词是纯文本，原样粘贴即可。有些作者说自己是在 ChatGPT 里跑的，那里的设置不同，所以结果会接近，但不会完全一样。

</details>

<details>
<summary><b>有适合海报、电商和角色的 GPT Image 2 提示词吗？</b></summary>

有。海报、电商、角色和广告各有独立分区，点上方的分类名即可跳转。“对比测试”分区收集了一批提示词测试，能看出改几个词会怎样改变结果。

</details>

<details>
<summary><b>GPT Image 2 海报上的文字怎么才能写对？</b></summary>

每个词都放进引号，说明放在哪里，每行尽量短。字很小时选更大的分辨率档位，文字能分到更多像素。

</details>


<a id="related"></a>
## 🔗 相关链接

- [GPT Image 2 提示词 · apiko.app](https://apiko.app/zh/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [运行 GPT Image 2](https://apiko.app/zh/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2 API 文档](https://apiko.app/zh/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/zh/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 提示词](https://apiko.app/zh/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [AI 图像生成器](https://apiko.app/zh/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [APIKO API 代码示例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示词合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts/blob/main/README_zh-CN.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-CN.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-CN.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-CN.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-CN.md)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts/blob/main/README_zh-CN.md)
- [Awesome Seedream 5.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedream-5.5-prompts/blob/main/README_zh-CN.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-CN.md)

<a id="license"></a>
## 📄 许可与出处

提示词和图片归每张卡片上署名的创作者所有，卡片链接到原帖；整个合集以 CC0 贡献到公有领域。标题、简介、译文和生成脚本采用 [CC BY 4.0](LICENSE) 许可。

如果这份合集帮你省了时间，点个 ⭐ 能让更多人看到。
