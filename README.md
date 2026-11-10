<div align="center">

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2 Prompts" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-874_cases-111111)](README.md#menu)
[![Try GPT Image 2 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2-on_APIKO-4F46E5)](https://apiko.app/models/gpt-image-2?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=model_try)
[![GPT Image 2 API docs](https://img.shields.io/badge/GPT_Image_2-API_docs-111111)](https://apiko.app/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Current-111111)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome GPT Image 2 Prompts

<a id="introduction"></a>
## 🌟 Introduction

**GPT Image 2 prompts: 874 free, copy-ready prompts with their result images for ads, characters, e-commerce, portraits, posters and UI.**

Copy-ready GPT Image 2 prompts with the images they produced, sorted into seven categories. Copy one, or send it to the model page.

Search and filter them on [apiko.app/gpt-image-2-prompts](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2-prompts&utm_content=intro).

> [!NOTE]
> Each prompt is kept exactly as its author posted it, so most are in English; titles and descriptions are ours. Every case credits the author and links to the original post.

<a id="quick-start"></a>
## 🚀 Quick start

**In the browser:** every case has a **Run on APIKO** link. It opens the example on [apiko.app](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=browser); press **Use** there to load the prompt into the GPT Image 2 playground.

**With the API:** create an [APIKO API key](https://apiko.app/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=api_key), then create an async task and poll it until the image is ready.

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

Endpoints: `POST https://api.apiko.app/v1/images/generations` (create a task) · `GET https://api.apiko.app/v1/tasks/{id}` (read the status and result)

<a id="how-to-write"></a>
## ✍️ How to write a GPT Image 2 prompt

Four patterns that recur across the cards below.

- **Layout first** · `Format + layout + subject + exact text` — Start with what the image is (a 2x2 banner grid, a nine-panel storyboard, a poster) and how it is divided. Then list each panel's subject and the words on it. Several prompts are written as JSON with fields such as layout and text_labels.
- **Camera and light** · `Shot + lens or light + material + mood` — Photo prompts name the shot size, a lens or film look (35mm flash, window light, backlight) and the surface finish, then close with one mood line. A named look gives the model more to work with than "beautiful".
- **Reference, keep, change** · `Reference + keep + change` — When a photo is uploaded, say what must stay (face, outfit, product shape) and what changes (style, background, text). Cards that rely on a reference photo say so in the prompt.
- **Template slots** · `Fixed prompt + {slots}` — Reusable prompts leave variables in curly braces, such as {argument name="brand" default="…"}. Replace the default with your own brand, city or product and leave the rest alone.

**What these GPT Image 2 prompt examples show**

- **Quote the words.** Text that must appear in the image sits in quotation marks, often with its position ("top left: …"). Poster and ad cards do this line by line.
- **State the panel count.** Grids and storyboards say how many cells they want, such as 4, 9 or 16, and describe each one in order.
- **Ratio lines are context.** Many prompts open with a line like "Aspect Ratio: 9:16". On APIKO the output ratio comes from the size parameter, so set it there too.
- **Finish with what to avoid.** Common endings are short exclusion lists: no watermark, no blur, no distorted features, no plastic skin.
- **Long prompts are normal.** Many cards run past 1,000 characters and a few past 1,500. The API accepts up to 8,000 characters.

<a id="menu"></a>
## 📑 Menu

- [⭐ Featured](#featured) (6)
- [📣 Ads](prompts/ad-creative.md) (52) — Campaign posters, product ads and brand boards, with the headline, tagline and price text written into the prompt.
- [🧩 Characters](prompts/character.md) (29) — Character sheets, game key art and anime cards that keep one design consistent across poses and panels.
- [🛍️ E-commerce](prompts/ecommerce.md) (33) — Product main images, studio shots and detail infographics for listings, with ad storyboards for the same product.
- [📷 Portraits](prompts/portrait.md) (243) — Editorial shots, selfies, film looks, idol grids and anime avatars, most of them tied to a named camera or lighting style.
- [🪧 Posters](prompts/poster.md) (323) — Travel, movie, food and zodiac posters, infographics and collages where layout and lettering carry the design.
- [🖥️ UI](prompts/ui.md) (116) — Interface screenshots, brand boards, storyboards and information graphics built from labelled panels.
- [🆚 Comparisons](prompts/comparison.md) (78) — Side-by-side prompt tests and detail showcases, plus storyboard sheets and screenshot imitations.
- [❓ FAQ](#faq)
- [🔗 Related](#related)

<a id="featured"></a>
## ⭐ Featured

<a id="ad-creative-08"></a>
### 8. Luxury Chronograph Watch Ad

by [@AlwaveNazca](https://x.com/AlwaveNazca) · 1:1 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08)** · [Original post](https://x.com/AlwaveNazca/status/2048147643809865950)

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-08.webp" width="480" alt="Luxury Chronograph Watch Ad – GPT Image 2"></a>

**Prompt:**

```text
A dramatic luxury product advertising image for a motorsport-inspired chronograph wristwatch in a dark studio. Center-left foreground, show a single stainless steel chronograph watch standing upright at a slight three-quarter angle, with a black dial, two red-accent subdials, slim silver hour markers, a tachymeter bezel, and visible crown and pushers on the right side. The watch has a black leather strap with bold red stitching along both edges and a sporty premium finish. To the right of the watch, place one black square presentation box slightly behind it, textured like leather, with red stitching around the lid and a silver embossed eye-shaped logo above the text “NESS STUDIO” and smaller red text “TRACK SURFACE.” At the top center of the composition, add the same silver eye logo with the words “NESS STUDIO” and smaller “BY NICOLAS.” Across the background, place one oversized blurred word, {argument name="headline text" default="PRECISION"}, in large gray capital letters spanning nearly the full width. The scene is set against a deep black background with cinematic red and white horizontal light streaks crossing behind the products from left to right, suggesting speed and racetrack energy. Use a glossy wet ground plane with reflective texture, catching red highlights and mirrorlike reflections beneath the watch and box. At the bottom center, add the text “CHRONOGRAPH SERIES” in clean white spaced capitals with thin red horizontal lines extending on both sides, and below it smaller red capitals reading {argument name="tagline text" default="ALSACE MADE"}. Color palette: black, charcoal gray, silver steel, vivid racing red, and a touch of white. Lighting should be high-contrast and premium, with crisp specular highlights on the metal case, subtle soft fill on the box, and moody shadows. Overall style: ultra-polished commercial product photography, luxury watch campaign, sharp focus on the products, sleek branding, high-end automotive aesthetic.
```

<a id="ad-creative-14"></a>
### 14. Luxury Miniature Dubai City Model

by [@silentempiredev](https://x.com/silentempiredev) · 16:9 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14)** · [Original post](https://x.com/silentempiredev/status/2048086378383384773)

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-14.webp" width="480" alt="Luxury Miniature Dubai City Model – GPT Image 2"></a>

**Prompt:**

```text
A hyper-detailed cinematic isometric miniature city model of {argument name="landmark tower" default="Burj Khalifa"} rising dramatically from the center of a square architectural master-plan board, presented like a luxury urban planning maquette on a black background. The composition shows one dominant ultra-tall silver skyscraper in the exact center, surrounded by a dense ring of modern high-rise towers, illuminated roads, bridges, and glowing warm city lights. Curving turquoise-blue water features and artificial lakes wrap around the central district in multiple connected pools and canals, with one large circular fountain-like feature near the tower base and several small island shapes visible in the water. In the lower right quadrant, include a large low-rise complex with rounded geometric roofs and subtle green-lit sections, connected by multilane roads and looping interchanges. The entire city sits on one square beige map board engraved with faint street grids and planning lines, with the board edges clearly visible and slightly raised. Viewpoint is a high three-quarter isometric angle, centered and symmetrical, with the tower extending far upward into negative space. Lighting is dramatic and luxurious: warm golden edge lights on buildings and roads, cool reflections in the water, crisp metallic highlights on the central tower, and a deep black void surrounding the model. Style should feel like a photorealistic architectural visualization mixed with a premium collectible scale model, extremely intricate, sharp, polished, and elegant.
```

<a id="poster-95"></a>
### 443. New York across two centuries cinematic poster

by [@Shinning1010](https://x.com/Shinning1010) · 3:4 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95)** · [Original post](https://x.com/Shinning1010/status/2049460661109879022)

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-95.webp" width="320" alt="New York across two centuries cinematic poster – GPT Image 2"></a>

**Prompt:**

```text
Create a cinematic 3:4 vertical poster of New York City that feels truly epic and unconventional, showing the passage from the 20th century to the 21st century in one seamless image. Place a lone figure at the center of the composition, standing in the middle of the street and looking forward as if witnessing New York across time. The left side should depict 20th-century New York with warm sepia atmosphere, vintage taxis, old newsstands, retro lamps, and landmarks like the Chrysler Building and Empire State Building. The right side should depict 21st-century New York with glass skyscrapers, One World Trade Center, digital billboards, and modern urban energy. Make the transition natural rather than split-screen, with coherent perspective, wet reflective pavement, realistic textures, atmospheric depth, and no text.
```

<a id="poster-176"></a>
### 521. Ancient Civilization Miniature Diorama

by [@Naiknelofar788](https://x.com/Naiknelofar788) · 2:3 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176)** · [Original post](https://x.com/Naiknelofar788/status/2054221110372405534)

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-176.webp" width="320" alt="Ancient Civilization Miniature Diorama – GPT Image 2"></a>

**Prompt:**

```text
A highly detailed miniature diorama of an ancient civilization under construction, displayed directly on top of large rolled-out architectural blueprints spread across a realistic wooden drafting table. The scene features iconic historical architecture from [CIVILIZATION OR LOCATION], including partially completed monuments, temples, towers, walls, palaces, streets, or ceremonial structures at different stages of construction. Tiny craftsmen, builders, engineers, and workers interact naturally throughout the scene using historically accurate tools, scaffolding, ramps, cranes, carts, stone blocks, timber frameworks, and construction platforms.
The miniature terrain blends seamlessly into the printed engineering drawings beneath, combining realistic sand, stone, earth, marble, vegetation, or desert textures with visible architectural floor plans, elevation sketches, measurements, annotations, and cross-sections. Surrounding the workspace are drafting instruments, compasses, rolled parchment plans, books, rulers, brass weights, candles, maps, carving tools, and historical reference materials that enhance the workshop atmosphere.
Soft cinematic lighting with warm natural sunlight from a nearby window, shallow depth of field, ultra realistic textures, handcrafted museum-quality scale model aesthetic, intricate miniature detailing, photoreal materials, atmospheric realism, editorial architectural photography style, clean composition, immersive world-building, vertical composition, extremely high detail, realistic shadows, authentic historical mood.
```

<a id="ui-73"></a>
### 738. Exploded Museum Assembly Diagram

by [@Gdgtify](https://x.com/Gdgtify) · 16:9 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73)** · [Original post](https://x.com/Gdgtify/status/2052498708521259162)

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ui-73.webp" width="480" alt="Exploded Museum Assembly Diagram – GPT Image 2"></a>

**Prompt:**

```text
16:9 2x2 grid, do this for cybertruck, reaper drone, james webb telescope, and another complex machine: do this for cybertruck: { "exhibit_type": "physical exploded assembly", "subject": "$complex_invention", // e.g., "an enigma machine", "a mechanical chronometer" "physical_constraints": { "state": "the machine is pulled apart into its 50 primary components along a horizontal axis.", "support_system": "no magical floating. every single floating gear and casing is physically held in the air by taut, thin, steel suspension wires and heavy brass museum clamps.", "background": "a flat, neutral-grey museum wall." }, "lighting_and_shadows": { "setup": "hard spotlighting from the top left.", "shadow_effect": "critical: the floating, separated components and their suspension wires must cast a highly complex, overlapping, beautiful shadow pattern directly onto the grey wall behind them." } }
```

<a id="character-16"></a>
### 67. Stylized 3D Skater Character

by [@iamaiistudio](https://x.com/iamaiistudio) · 4:5 · **[▶ Run on APIKO](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16)** · [Original post](https://x.com/iamaiistudio/status/2062038112398954712)

<a href="https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/character-16.webp" width="320" alt="Stylized 3D Skater Character – GPT Image 2"></a>

**Prompt:**

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

- **[📣 All 52 Ads cases](prompts/ad-creative.md)**
- **[🧩 All 29 Characters cases](prompts/character.md)**
- **[🛍️ All 33 E-commerce cases](prompts/ecommerce.md)**
- **[📷 All 243 Portraits cases](prompts/portrait.md)**
- **[🪧 All 323 Posters cases](prompts/poster.md)**
- **[🖥️ All 116 UI cases](prompts/ui.md)**
- **[🆚 All 78 Comparisons cases](prompts/comparison.md)**

<a id="faq"></a>
## ❓ FAQ

<details>
<summary><b>Are these GPT Image 2 prompts free to use, and who owns the images?</b></summary>

The collection is dedicated to the public domain (CC0), so you can copy, edit and run the prompts. The example images belong to the creators credited on each card; for images you generate, check that you may use any brand, logo or person's likeness you put in the prompt.

</details>

<details>
<summary><b>Which language should I write a gpt image prompt in?</b></summary>

Prompts here are shown in the author's original language, mostly English with some Chinese, and are not translated. GPT Image 2 takes English and Chinese, so use whichever you write best.

</details>

<details>
<summary><b>How do I run a GPT Image 2 prompt through the API?</b></summary>

Send POST /v1/images/generations with model gpt-image-2, your prompt, a size such as 16:9, a resolution of 1k, 2k or 4k, and "async": true, then poll GET /v1/tasks/{id}. The API docs have the full parameter list.

</details>

<details>
<summary><b>Which aspect ratios and sizes does GPT Image 2 support?</b></summary>

Ratios are 1:1, 16:9, 9:16, 3:2, 2:3, 4:3, 3:4, 5:4, 4:5 and 21:9, at 1k, 2k or 4k. Each ratio and tier returns a fixed pixel size, and you can also pass one of those sizes as WIDTHxHEIGHT. The value auto is not supported.

</details>

<details>
<summary><b>How do I use a card that needs a reference photo with GPT Image 2?</b></summary>

Upload your image to POST /v1/uploads/images, then send the returned public HTTPS URL in images to POST /v1/images/edits. GPT Image 2 takes 0 to 16 reference images, and with references the output size is not guaranteed to match the request.

</details>

<details>
<summary><b>Why does my GPT Image 2 result look different from the card?</b></summary>

Image models are not deterministic, so the same prompt gives different results on each run. The authors may also have used other tools, settings or reference images.

</details>

<details>
<summary><b>Do GPT Image 2 prompts written for ChatGPT work in the API?</b></summary>

They are plain text, so you can paste them in unchanged. Some authors say they ran theirs inside ChatGPT, where settings differ, so expect similar results rather than identical ones.

</details>

<details>
<summary><b>Are there GPT Image 2 prompts for posters, e-commerce and characters?</b></summary>

Yes. Posters, E-commerce, Characters and Ads each have their own section, and the category names above jump straight to them. The Comparisons section collects prompt tests that show how small wording changes alter a result.

</details>

<details>
<summary><b>How do I keep the text correct in a GPT Image 2 poster?</b></summary>

Put every word in quotation marks, say where it goes, and keep each line short. Set a large resolution when the lettering is small, since a larger tier gives the text more pixels.

</details>


<a id="related"></a>
## 🔗 Related

- [GPT Image 2 Prompts · apiko.app](https://apiko.app/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [Run GPT Image 2](https://apiko.app/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2 API docs](https://apiko.app/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 prompts](https://apiko.app/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [AI image generator](https://apiko.app/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [Code examples for the APIKO API](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**More prompt collections**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts)
- [Awesome Claude Fable 5.2 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-fable-5.2-video-prompts)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts)

<a id="license"></a>
## 📄 License and credits

Prompts and images belong to the creators credited on each card, which links to the original post; the collection is dedicated to the public domain (CC0). Titles, descriptions, translations and the build scripts are released under [CC BY 4.0](LICENSE).

If this list saves you time, a ⭐ helps others find it.
