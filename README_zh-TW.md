<div align="center">

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2 提示詞" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-874_cases-111111)](README_zh-TW.md#menu)
[![Try GPT Image 2 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2-on_APIKO-4F46E5)](https://apiko.app/zh-tw/models/gpt-image-2?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=model_try)
[![GPT Image 2 API docs](https://img.shields.io/badge/GPT_Image_2-API_docs-111111)](https://apiko.app/zh-tw/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-Current-111111)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2 提示詞

<a id="introduction"></a>
## 🌟 簡介

**GPT Image 2 提示詞：874 條可直接複製的免費提示詞，附成圖，涵蓋廣告、角色、電商、人像、海報與 UI。**

附成圖的 GPT Image 2 提示詞，分成七大類。複製一條，或直接送到模型頁執行。

線上搜尋與篩選： [apiko.app/gpt-image-2-prompts](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2-prompts&utm_content=intro).

> [!NOTE]
> 提示詞保持作者發布時的原文，所以大多是英文；標題與簡介由我們撰寫。每則都署名作者並連結原帖。

<a id="quick-start"></a>
## 🚀 快速開始

**網頁上用：** 每則都有「在 APIKO 執行」連結，會在 [apiko.app](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=browser) 開啟這則範例；點「使用」，提示詞就會填進 GPT Image 2 試用台。

**用 API：** 先建立 [APIKO API 金鑰](https://apiko.app/zh-tw/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=api_key)，再建立非同步任務並輪詢，直到圖片生成完成。

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

介面: `POST https://api.apiko.app/v1/images/generations` (建立任務) · `GET https://api.apiko.app/v1/tasks/{id}` (查詢狀態與結果)

<a id="how-to-write"></a>
## ✍️ 如何寫 GPT Image 2 提示詞

下面這些卡片裡反覆出現的四種寫法。

- **先定版面** · `畫面類型 + 版面 + 主體 + 原文文字` — 先說這是什麼圖（2x2 橫幅、九格分鏡、海報）、怎麼分區，再逐格寫主體和上面的文字。有些提示詞直接寫成 JSON，帶有 layout、text_labels 之類的欄位。
- **鏡頭與光線** · `景別 + 鏡頭或光線 + 材質 + 氛圍` — 寫實人像會點明景別、鏡頭或底片質感（35mm 閃光燈、窗光、逆光）和表面質地，最後用一句話收住氛圍。給出具體風格，比寫「好看」有用。
- **參考、保留、修改** · `參考圖 + 保留 + 修改` — 上傳照片時，先說哪些要維持不變（臉、服裝、產品外型），再說哪些要改（風格、背景、文字）。需要參考圖的卡片會在提示詞裡寫明。
- **範本欄位** · `固定提示詞 + {欄位}` — 可重複使用的提示詞會把變數放進大括號，例如 {argument name="brand" default="…"}。把預設值換成你的品牌、城市或產品，其餘不用動。

**這些 GPT Image 2 提示詞範例透露了什麼**

- **文字加引號。** 要出現在圖裡的字放進引號，常常還會寫明位置（「左上角：……」）。海報和廣告卡片都是一行一行這樣寫的。
- **寫清格數。** 宮格與分鏡會直接說要幾格，例如 4、9、16，再依序描述每一格。
- **比例那行只是說明。** 不少提示詞開頭有一行「Aspect Ratio: 9:16」。在 APIKO 上，輸出比例由 size 參數決定，所以參數裡也要設定。
- **結尾寫不要什麼。** 常見結尾是一小串排除項：不要浮水印、不要模糊、不要五官變形、不要塑膠皮膚。
- **長提示詞很正常。** 很多卡片超過 1,000 個字元，少數超過 1,500。API 最多接受 8,000 個字元。

<a id="menu"></a>
## 📑 目錄

- [⭐ 精選](#featured) (6)
- [📣 廣告](prompts/ad-creative_zh-TW.md) (52) — 行銷海報、產品廣告與品牌板，標題、標語和價格文字直接寫進提示詞。
- [🧩 角色](prompts/character_zh-TW.md) (29) — 角色設定表、遊戲主視覺與動漫卡牌，讓同一個造型在不同姿勢和畫格裡維持一致。
- [🛍️ 電商](prompts/ecommerce_zh-TW.md) (33) — 商品主圖、棚拍圖與詳情資訊圖，也有同一件商品的廣告分鏡。
- [📷 人像](prompts/portrait_zh-TW.md) (243) — 雜誌大片、自拍、底片質感、偶像九宮格與二次元頭像，多數寫明了相機或光線風格。
- [🪧 海報](prompts/poster_zh-TW.md) (323) — 旅遊、電影、美食與星座海報，以及資訊圖和拼貼，版面和字體就是設計本身。
- [🖥️ UI](prompts/ui_zh-TW.md) (116) — 介面截圖、品牌板、分鏡與資訊圖，都由附標註的分區拼成。
- [🆚 對比測試](prompts/comparison_zh-TW.md) (78) — 並排的提示詞測試與細節展示，另有分鏡表和截圖仿製。
- [❓ 常見問題](#faq)
- [🔗 相關連結](#related)

<a id="featured"></a>
## ⭐ 精選

<a id="ad-creative-08"></a>
### 8. 奢華計時腕錶廣告

作者 [@AlwaveNazca](https://x.com/AlwaveNazca) · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08)** · [原帖](https://x.com/AlwaveNazca/status/2048147643809865950)

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-08.webp" width="480" alt="奢華計時腕錶廣告 – GPT Image 2"></a>

**提示詞:**

```text
A dramatic luxury product advertising image for a motorsport-inspired chronograph wristwatch in a dark studio. Center-left foreground, show a single stainless steel chronograph watch standing upright at a slight three-quarter angle, with a black dial, two red-accent subdials, slim silver hour markers, a tachymeter bezel, and visible crown and pushers on the right side. The watch has a black leather strap with bold red stitching along both edges and a sporty premium finish. To the right of the watch, place one black square presentation box slightly behind it, textured like leather, with red stitching around the lid and a silver embossed eye-shaped logo above the text “NESS STUDIO” and smaller red text “TRACK SURFACE.” At the top center of the composition, add the same silver eye logo with the words “NESS STUDIO” and smaller “BY NICOLAS.” Across the background, place one oversized blurred word, {argument name="headline text" default="PRECISION"}, in large gray capital letters spanning nearly the full width. The scene is set against a deep black background with cinematic red and white horizontal light streaks crossing behind the products from left to right, suggesting speed and racetrack energy. Use a glossy wet ground plane with reflective texture, catching red highlights and mirrorlike reflections beneath the watch and box. At the bottom center, add the text “CHRONOGRAPH SERIES” in clean white spaced capitals with thin red horizontal lines extending on both sides, and below it smaller red capitals reading {argument name="tagline text" default="ALSACE MADE"}. Color palette: black, charcoal gray, silver steel, vivid racing red, and a touch of white. Lighting should be high-contrast and premium, with crisp specular highlights on the metal case, subtle soft fill on the box, and moody shadows. Overall style: ultra-polished commercial product photography, luxury watch campaign, sharp focus on the products, sleek branding, high-end automotive aesthetic.
```

<a id="ad-creative-14"></a>
### 14. 奢華杜拜微縮城市模型

作者 [@silentempiredev](https://x.com/silentempiredev) · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14)** · [原帖](https://x.com/silentempiredev/status/2048086378383384773)

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-14.webp" width="480" alt="奢華杜拜微縮城市模型 – GPT Image 2"></a>

**提示詞:**

```text
A hyper-detailed cinematic isometric miniature city model of {argument name="landmark tower" default="Burj Khalifa"} rising dramatically from the center of a square architectural master-plan board, presented like a luxury urban planning maquette on a black background. The composition shows one dominant ultra-tall silver skyscraper in the exact center, surrounded by a dense ring of modern high-rise towers, illuminated roads, bridges, and glowing warm city lights. Curving turquoise-blue water features and artificial lakes wrap around the central district in multiple connected pools and canals, with one large circular fountain-like feature near the tower base and several small island shapes visible in the water. In the lower right quadrant, include a large low-rise complex with rounded geometric roofs and subtle green-lit sections, connected by multilane roads and looping interchanges. The entire city sits on one square beige map board engraved with faint street grids and planning lines, with the board edges clearly visible and slightly raised. Viewpoint is a high three-quarter isometric angle, centered and symmetrical, with the tower extending far upward into negative space. Lighting is dramatic and luxurious: warm golden edge lights on buildings and roads, cool reflections in the water, crisp metallic highlights on the central tower, and a deep black void surrounding the model. Style should feel like a photorealistic architectural visualization mixed with a premium collectible scale model, extremely intricate, sharp, polished, and elegant.
```

<a id="poster-95"></a>
### 443. 跨越兩個世紀的紐約電影海報

作者 [@Shinning1010](https://x.com/Shinning1010) · 3:4 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95)** · [原帖](https://x.com/Shinning1010/status/2049460661109879022)

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-95.webp" width="320" alt="跨越兩個世紀的紐約電影海報 – GPT Image 2"></a>

**提示詞:**

```text
Create a cinematic 3:4 vertical poster of New York City that feels truly epic and unconventional, showing the passage from the 20th century to the 21st century in one seamless image. Place a lone figure at the center of the composition, standing in the middle of the street and looking forward as if witnessing New York across time. The left side should depict 20th-century New York with warm sepia atmosphere, vintage taxis, old newsstands, retro lamps, and landmarks like the Chrysler Building and Empire State Building. The right side should depict 21st-century New York with glass skyscrapers, One World Trade Center, digital billboards, and modern urban energy. Make the transition natural rather than split-screen, with coherent perspective, wet reflective pavement, realistic textures, atmospheric depth, and no text.
```

<a id="poster-176"></a>
### 521. 古文明微縮立體場景

作者 [@Naiknelofar788](https://x.com/Naiknelofar788) · 2:3 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176)** · [原帖](https://x.com/Naiknelofar788/status/2054221110372405534)

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-176.webp" width="320" alt="古文明微縮立體場景 – GPT Image 2"></a>

**提示詞:**

```text
A highly detailed miniature diorama of an ancient civilization under construction, displayed directly on top of large rolled-out architectural blueprints spread across a realistic wooden drafting table. The scene features iconic historical architecture from [CIVILIZATION OR LOCATION], including partially completed monuments, temples, towers, walls, palaces, streets, or ceremonial structures at different stages of construction. Tiny craftsmen, builders, engineers, and workers interact naturally throughout the scene using historically accurate tools, scaffolding, ramps, cranes, carts, stone blocks, timber frameworks, and construction platforms.
The miniature terrain blends seamlessly into the printed engineering drawings beneath, combining realistic sand, stone, earth, marble, vegetation, or desert textures with visible architectural floor plans, elevation sketches, measurements, annotations, and cross-sections. Surrounding the workspace are drafting instruments, compasses, rolled parchment plans, books, rulers, brass weights, candles, maps, carving tools, and historical reference materials that enhance the workshop atmosphere.
Soft cinematic lighting with warm natural sunlight from a nearby window, shallow depth of field, ultra realistic textures, handcrafted museum-quality scale model aesthetic, intricate miniature detailing, photoreal materials, atmospheric realism, editorial architectural photography style, clean composition, immersive world-building, vertical composition, extremely high detail, realistic shadows, authentic historical mood.
```

<a id="ui-73"></a>
### 738. 博物館爆炸組裝圖

作者 [@Gdgtify](https://x.com/Gdgtify) · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73)** · [原帖](https://x.com/Gdgtify/status/2052498708521259162)

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ui-73.webp" width="480" alt="博物館爆炸組裝圖 – GPT Image 2"></a>

**提示詞:**

```text
16:9 2x2 grid, do this for cybertruck, reaper drone, james webb telescope, and another complex machine: do this for cybertruck: { "exhibit_type": "physical exploded assembly", "subject": "$complex_invention", // e.g., "an enigma machine", "a mechanical chronometer" "physical_constraints": { "state": "the machine is pulled apart into its 50 primary components along a horizontal axis.", "support_system": "no magical floating. every single floating gear and casing is physically held in the air by taut, thin, steel suspension wires and heavy brass museum clamps.", "background": "a flat, neutral-grey museum wall." }, "lighting_and_shadows": { "setup": "hard spotlighting from the top left.", "shadow_effect": "critical: the floating, separated components and their suspension wires must cast a highly complex, overlapping, beautiful shadow pattern directly onto the grey wall behind them." } }
```

<a id="character-16"></a>
### 67. 風格化 3D 滑板角色

作者 [@iamaiistudio](https://x.com/iamaiistudio) · 4:5 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16)** · [原帖](https://x.com/iamaiistudio/status/2062038112398954712)

<a href="https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/character-16.webp" width="320" alt="風格化 3D 滑板角色 – GPT Image 2"></a>

**提示詞:**

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

- **[📣 查看「廣告」全部 52 則](prompts/ad-creative_zh-TW.md)**
- **[🧩 查看「角色」全部 29 則](prompts/character_zh-TW.md)**
- **[🛍️ 查看「電商」全部 33 則](prompts/ecommerce_zh-TW.md)**
- **[📷 查看「人像」全部 243 則](prompts/portrait_zh-TW.md)**
- **[🪧 查看「海報」全部 323 則](prompts/poster_zh-TW.md)**
- **[🖥️ 查看「UI」全部 116 則](prompts/ui_zh-TW.md)**
- **[🆚 查看「對比測試」全部 78 則](prompts/comparison_zh-TW.md)**

<a id="faq"></a>
## ❓ 常見問題

<details>
<summary><b>這些 GPT Image 2 提示詞可以免費使用嗎？圖片歸誰？</b></summary>

整個合集已以 CC0 貢獻到公眾領域，提示詞可以自由複製、修改和執行。範例圖片歸每張卡片署名的創作者；你自己生成的圖，要確認提示詞裡用到的品牌、標誌與真人肖像是否有權使用。

</details>

<details>
<summary><b>GPT Image 2 提示詞該用中文還是英文寫？</b></summary>

這裡的提示詞照作者原文呈現，以英文為主，也有中文，不做翻譯。GPT Image 2 支援中文與英文，用你寫得最順的那種就好。

</details>

<details>
<summary><b>怎麼用 API 執行一條 GPT Image 2 提示詞？</b></summary>

呼叫 POST /v1/images/generations，帶上 model 為 gpt-image-2、你的 prompt、size（例如 16:9）、resolution（1k、2k 或 4k）以及 "async": true，再輪詢 GET /v1/tasks/{id}。完整參數請看 API 文件。

</details>

<details>
<summary><b>GPT Image 2 支援哪些比例與尺寸？</b></summary>

比例有 1:1、16:9、9:16、3:2、2:3、4:3、3:4、5:4、4:5 和 21:9，解析度為 1k、2k、4k。每個比例與檔位對應固定的像素尺寸，也可以直接傳入其中一個尺寸（WIDTHxHEIGHT）。不支援 auto。

</details>

<details>
<summary><b>需要參考圖的卡片要怎麼在 GPT Image 2 上使用？</b></summary>

先把圖片上傳到 POST /v1/uploads/images，再把回傳的公開 HTTPS 網址放進 images，呼叫 POST /v1/images/edits。GPT Image 2 支援 0 到 16 張參考圖；帶參考圖時，輸出尺寸不保證與請求一致。

</details>

<details>
<summary><b>為什麼我的 GPT Image 2 結果和卡片上的圖不一樣？</b></summary>

圖像模型不是確定性的，同一條提示詞每次的結果都不同。作者也可能用了別的工具、設定或參考圖。

</details>

<details>
<summary><b>在 ChatGPT 裡用的 GPT Image 2 提示詞，API 也能用嗎？</b></summary>

提示詞是純文字，原樣貼上即可。有些作者說自己是在 ChatGPT 裡跑的，那邊的設定不同，所以結果會相近，但不會一模一樣。

</details>

<details>
<summary><b>有適合海報、電商與角色的 GPT Image 2 提示詞嗎？</b></summary>

有。海報、電商、角色和廣告各有獨立分區，點上方的分類名稱就能跳過去。「對比測試」分區收了一批提示詞測試，可以看出改幾個字會怎麼改變結果。

</details>

<details>
<summary><b>GPT Image 2 海報上的文字要怎麼寫才會對？</b></summary>

每個詞都放進引號，說明擺在哪裡，每行盡量短。字很小的時候選較大的解析度檔位，文字能分到更多像素。

</details>


<a id="related"></a>
## 🔗 相關連結

- [GPT Image 2 提示詞 · apiko.app](https://apiko.app/zh-tw/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [執行 GPT Image 2](https://apiko.app/zh-tw/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2 API 文件](https://apiko.app/zh-tw/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/zh-tw/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 提示詞](https://apiko.app/zh-tw/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [AI 圖像生成器](https://apiko.app/zh-tw/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [APIKO API 程式碼範例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示詞合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-TW.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-TW.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-TW.md)

<a id="license"></a>
## 📄 授權與出處

提示詞與圖片歸每張卡片上署名的創作者所有，卡片連結到原貼文；整個合集以 CC0 貢獻到公眾領域。標題、簡介、譯文與生成腳本採用 [CC BY 4.0](LICENSE) 授權。

如果這份合集幫你省了時間，按個 ⭐ 能讓更多人看到。
