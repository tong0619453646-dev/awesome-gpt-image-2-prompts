<div align="center">

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-gpt-image-2-prompts"><img src="assets/banner.jpg" alt="Awesome GPT Image 2 프롬프트" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-874_cases-111111)](README_ko.md#menu)
[![Try GPT Image 2 on APIKO](https://img.shields.io/badge/Try_GPT_Image_2-on_APIKO-4F46E5)](https://apiko.app/ko/models/gpt-image-2?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=model_try)
[![GPT Image 2 API docs](https://img.shields.io/badge/GPT_Image_2-API_docs-111111)](https://apiko.app/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=badge&utm_campaign=awesome-gpt-image-2-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-Current-111111)](README_ko.md)

</div>

# Awesome GPT Image 2 프롬프트

<a id="introduction"></a>
## 🌟 소개

**GPT Image 2 프롬프트 874개를 결과 이미지와 함께 무료로 복사해 쓰세요. 광고, 캐릭터, 이커머스, 포스터, UI를 담았습니다.**

결과 이미지가 붙은 GPT Image 2 프롬프트를 일곱 가지 분류로 모았습니다. 복사하거나 모델 페이지로 바로 보내 보세요.

검색과 필터는 [apiko.app/gpt-image-2-prompts](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-gpt-image-2-prompts&utm_content=intro).

> [!NOTE]
> 프롬프트는 작성자가 올린 원문 그대로라 대부분 영어입니다. 제목과 설명은 저희가 썼습니다. 모든 예시에 작성자와 원본 게시물 링크를 달았습니다.

<a id="quick-start"></a>
## 🚀 빠른 시작

**브라우저에서:** 모든 예시에 **APIKO에서 실행** 링크가 있습니다. [apiko.app](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=browser)에서 해당 예시가 열리며, **사용**을 누르면 프롬프트가 GPT Image 2 플레이그라운드에 채워집니다.

**API로:** [APIKO API 키](https://apiko.app/ko/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-gpt-image-2-prompts&utm_content=api_key)를 만든 뒤 비동기 작업을 생성하고, 이미지가 완성될 때까지 상태를 조회합니다.

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

엔드포인트: `POST https://api.apiko.app/v1/images/generations` (작업 생성) · `GET https://api.apiko.app/v1/tasks/{id}` (상태와 결과 조회)

<a id="how-to-write"></a>
## ✍️ GPT Image 2 프롬프트 쓰는 법

아래 카드에서 반복해서 나타나는 네 가지 패턴입니다.

- **레이아웃 먼저** · `형식 + 레이아웃 + 피사체 + 들어갈 글자` — 먼저 어떤 이미지인지(2x2 배너, 9컷 스토리보드, 포스터)와 구획을 적고, 칸마다 피사체와 글자를 나열합니다. layout, text_labels 같은 필드를 쓴 JSON 형식 프롬프트도 있습니다.
- **카메라와 빛** · `샷 + 렌즈 또는 조명 + 질감 + 분위기` — 사진 프롬프트는 샷 크기, 렌즈나 필름 느낌(35mm 플래시, 창가 빛, 역광), 표면 질감을 짚고 분위기 한 줄로 마무리합니다. '예쁘게'보다 구체적인 룩이 더 잘 먹힙니다.
- **참조, 유지, 변경** · `참조 + 유지 + 변경` — 사진을 올릴 때는 그대로 둘 것(얼굴, 의상, 제품 형태)과 바꿀 것(스타일, 배경, 글자)을 나눠 적습니다. 참조 사진이 필요한 카드는 프롬프트에 그렇게 적혀 있습니다.
- **템플릿 슬롯** · `고정 프롬프트 + {슬롯}` — 재사용용 프롬프트는 {argument name="brand" default="…"}처럼 변수를 중괄호에 둡니다. 기본값만 내 브랜드, 도시, 제품으로 바꾸고 나머지는 그대로 두면 됩니다.

**이 GPT Image 2 프롬프트 예시가 보여 주는 것**

- **글자는 따옴표로.** 이미지에 들어갈 글자는 따옴표 안에 넣고, 위치("왼쪽 위: …")를 함께 적는 경우가 많습니다. 포스터와 광고 카드가 이렇게 한 줄씩 씁니다.
- **컷 수를 밝히기.** 그리드와 스토리보드는 4, 9, 16처럼 칸 수를 직접 말하고 칸마다 순서대로 설명합니다.
- **비율 줄은 참고용.** 'Aspect Ratio: 9:16' 같은 줄로 시작하는 프롬프트가 많습니다. APIKO에서는 출력 비율이 size 파라미터로 정해지므로 거기서도 설정하세요.
- **빼 달라는 말로 마무리.** 끝에 제외 목록을 짧게 붙이는 경우가 흔합니다. 워터마크 금지, 흐림 금지, 얼굴 왜곡 금지, 플라스틱 피부 금지 같은 식입니다.
- **긴 프롬프트도 괜찮다.** 1,000자를 넘는 카드가 많고 1,500자를 넘는 것도 있습니다. API는 최대 8,000자까지 받습니다.

<a id="menu"></a>
## 📑 목차

- [⭐ 추천](#featured) (6)
- [📣 광고](prompts/ad-creative_ko.md) (52) — 캠페인 포스터, 제품 광고, 브랜드 보드. 헤드라인과 슬로건, 가격 문구까지 프롬프트에 적습니다.
- [🧩 캐릭터](prompts/character_ko.md) (29) — 캐릭터 시트, 게임 키 아트, 애니 카드. 포즈와 컷이 달라도 하나의 디자인을 유지합니다.
- [🛍️ 이커머스](prompts/ecommerce_ko.md) (33) — 상품 메인 이미지, 스튜디오 컷, 상세 인포그래픽과 같은 제품의 광고 스토리보드입니다.
- [📷 인물](prompts/portrait_ko.md) (243) — 에디토리얼 컷, 셀카, 필름 감성, 아이돌 그리드, 애니 프로필. 대부분 카메라나 조명 스타일을 지정합니다.
- [🪧 포스터](prompts/poster_ko.md) (323) — 여행, 영화, 음식, 별자리 포스터와 인포그래픽, 콜라주. 레이아웃과 글자가 곧 디자인입니다.
- [🖥️ UI](prompts/ui_ko.md) (116) — 화면 캡처, 브랜드 보드, 스토리보드, 인포그래픽. 이름 붙인 패널을 이어 붙여 구성합니다.
- [🆚 비교 테스트](prompts/comparison_ko.md) (78) — 나란히 비교한 프롬프트 테스트와 디테일 쇼케이스, 스토리보드 시트, 화면 모사를 모았습니다.
- [❓ 자주 묻는 질문](#faq)
- [🔗 관련 링크](#related)

<a id="featured"></a>
## ⭐ 추천

<a id="ad-creative-08"></a>
### 8. 럭셔리 크로노그래프 시계 광고

작성자 [@AlwaveNazca](https://x.com/AlwaveNazca) · 1:1 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08)** · [원본 게시물](https://x.com/AlwaveNazca/status/2048147643809865950)

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-08#ad-creative-08"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-08.webp" width="480" alt="럭셔리 크로노그래프 시계 광고 – GPT Image 2"></a>

**프롬프트:**

```text
A dramatic luxury product advertising image for a motorsport-inspired chronograph wristwatch in a dark studio. Center-left foreground, show a single stainless steel chronograph watch standing upright at a slight three-quarter angle, with a black dial, two red-accent subdials, slim silver hour markers, a tachymeter bezel, and visible crown and pushers on the right side. The watch has a black leather strap with bold red stitching along both edges and a sporty premium finish. To the right of the watch, place one black square presentation box slightly behind it, textured like leather, with red stitching around the lid and a silver embossed eye-shaped logo above the text “NESS STUDIO” and smaller red text “TRACK SURFACE.” At the top center of the composition, add the same silver eye logo with the words “NESS STUDIO” and smaller “BY NICOLAS.” Across the background, place one oversized blurred word, {argument name="headline text" default="PRECISION"}, in large gray capital letters spanning nearly the full width. The scene is set against a deep black background with cinematic red and white horizontal light streaks crossing behind the products from left to right, suggesting speed and racetrack energy. Use a glossy wet ground plane with reflective texture, catching red highlights and mirrorlike reflections beneath the watch and box. At the bottom center, add the text “CHRONOGRAPH SERIES” in clean white spaced capitals with thin red horizontal lines extending on both sides, and below it smaller red capitals reading {argument name="tagline text" default="ALSACE MADE"}. Color palette: black, charcoal gray, silver steel, vivid racing red, and a touch of white. Lighting should be high-contrast and premium, with crisp specular highlights on the metal case, subtle soft fill on the box, and moody shadows. Overall style: ultra-polished commercial product photography, luxury watch campaign, sharp focus on the products, sleek branding, high-end automotive aesthetic.
```

<a id="ad-creative-14"></a>
### 14. 럭셔리 두바이 미니어처 도시 모형

작성자 [@silentempiredev](https://x.com/silentempiredev) · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14)** · [원본 게시물](https://x.com/silentempiredev/status/2048086378383384773)

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ad-creative-14#ad-creative-14"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ad-creative-14.webp" width="480" alt="럭셔리 두바이 미니어처 도시 모형 – GPT Image 2"></a>

**프롬프트:**

```text
A hyper-detailed cinematic isometric miniature city model of {argument name="landmark tower" default="Burj Khalifa"} rising dramatically from the center of a square architectural master-plan board, presented like a luxury urban planning maquette on a black background. The composition shows one dominant ultra-tall silver skyscraper in the exact center, surrounded by a dense ring of modern high-rise towers, illuminated roads, bridges, and glowing warm city lights. Curving turquoise-blue water features and artificial lakes wrap around the central district in multiple connected pools and canals, with one large circular fountain-like feature near the tower base and several small island shapes visible in the water. In the lower right quadrant, include a large low-rise complex with rounded geometric roofs and subtle green-lit sections, connected by multilane roads and looping interchanges. The entire city sits on one square beige map board engraved with faint street grids and planning lines, with the board edges clearly visible and slightly raised. Viewpoint is a high three-quarter isometric angle, centered and symmetrical, with the tower extending far upward into negative space. Lighting is dramatic and luxurious: warm golden edge lights on buildings and roads, cool reflections in the water, crisp metallic highlights on the central tower, and a deep black void surrounding the model. Style should feel like a photorealistic architectural visualization mixed with a premium collectible scale model, extremely intricate, sharp, polished, and elegant.
```

<a id="poster-95"></a>
### 443. 두 세기를 넘나드는 뉴욕 시네마틱 포스터

작성자 [@Shinning1010](https://x.com/Shinning1010) · 3:4 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95)** · [원본 게시물](https://x.com/Shinning1010/status/2049460661109879022)

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-95#poster-95"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-95.webp" width="320" alt="두 세기를 넘나드는 뉴욕 시네마틱 포스터 – GPT Image 2"></a>

**프롬프트:**

```text
Create a cinematic 3:4 vertical poster of New York City that feels truly epic and unconventional, showing the passage from the 20th century to the 21st century in one seamless image. Place a lone figure at the center of the composition, standing in the middle of the street and looking forward as if witnessing New York across time. The left side should depict 20th-century New York with warm sepia atmosphere, vintage taxis, old newsstands, retro lamps, and landmarks like the Chrysler Building and Empire State Building. The right side should depict 21st-century New York with glass skyscrapers, One World Trade Center, digital billboards, and modern urban energy. Make the transition natural rather than split-screen, with coherent perspective, wet reflective pavement, realistic textures, atmospheric depth, and no text.
```

<a id="poster-176"></a>
### 521. 고대 문명 미니어처 디오라마

작성자 [@Naiknelofar788](https://x.com/Naiknelofar788) · 2:3 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176)** · [원본 게시물](https://x.com/Naiknelofar788/status/2054221110372405534)

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=poster-176#poster-176"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/poster-176.webp" width="320" alt="고대 문명 미니어처 디오라마 – GPT Image 2"></a>

**프롬프트:**

```text
A highly detailed miniature diorama of an ancient civilization under construction, displayed directly on top of large rolled-out architectural blueprints spread across a realistic wooden drafting table. The scene features iconic historical architecture from [CIVILIZATION OR LOCATION], including partially completed monuments, temples, towers, walls, palaces, streets, or ceremonial structures at different stages of construction. Tiny craftsmen, builders, engineers, and workers interact naturally throughout the scene using historically accurate tools, scaffolding, ramps, cranes, carts, stone blocks, timber frameworks, and construction platforms.
The miniature terrain blends seamlessly into the printed engineering drawings beneath, combining realistic sand, stone, earth, marble, vegetation, or desert textures with visible architectural floor plans, elevation sketches, measurements, annotations, and cross-sections. Surrounding the workspace are drafting instruments, compasses, rolled parchment plans, books, rulers, brass weights, candles, maps, carving tools, and historical reference materials that enhance the workshop atmosphere.
Soft cinematic lighting with warm natural sunlight from a nearby window, shallow depth of field, ultra realistic textures, handcrafted museum-quality scale model aesthetic, intricate miniature detailing, photoreal materials, atmospheric realism, editorial architectural photography style, clean composition, immersive world-building, vertical composition, extremely high detail, realistic shadows, authentic historical mood.
```

<a id="ui-73"></a>
### 738. 박물관식 분해 조립도

작성자 [@Gdgtify](https://x.com/Gdgtify) · 16:9 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73)** · [원본 게시물](https://x.com/Gdgtify/status/2052498708521259162)

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=ui-73#ui-73"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/ui-73.webp" width="480" alt="박물관식 분해 조립도 – GPT Image 2"></a>

**프롬프트:**

```text
16:9 2x2 grid, do this for cybertruck, reaper drone, james webb telescope, and another complex machine: do this for cybertruck: { "exhibit_type": "physical exploded assembly", "subject": "$complex_invention", // e.g., "an enigma machine", "a mechanical chronometer" "physical_constraints": { "state": "the machine is pulled apart into its 50 primary components along a horizontal axis.", "support_system": "no magical floating. every single floating gear and casing is physically held in the air by taut, thin, steel suspension wires and heavy brass museum clamps.", "background": "a flat, neutral-grey museum wall." }, "lighting_and_shadows": { "setup": "hard spotlighting from the top left.", "shadow_effect": "critical: the floating, separated components and their suspension wires must cast a highly complex, overlapping, beautiful shadow pattern directly onto the grey wall behind them." } }
```

<a id="character-16"></a>
### 67. 스타일화 3D 스케이터 캐릭터

작성자 [@iamaiistudio](https://x.com/iamaiistudio) · 4:5 · **[▶ APIKO에서 실행](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16)** · [원본 게시물](https://x.com/iamaiistudio/status/2062038112398954712)

<a href="https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-gpt-image-2-prompts&utm_content=character-16#character-16"><img src="https://media.apiko.app/prompts/gpt-image-2-prompts/character-16.webp" width="320" alt="스타일화 3D 스케이터 캐릭터 – GPT Image 2"></a>

**프롬프트:**

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

- **[📣 광고 전체 52개 보기](prompts/ad-creative_ko.md)**
- **[🧩 캐릭터 전체 29개 보기](prompts/character_ko.md)**
- **[🛍️ 이커머스 전체 33개 보기](prompts/ecommerce_ko.md)**
- **[📷 인물 전체 243개 보기](prompts/portrait_ko.md)**
- **[🪧 포스터 전체 323개 보기](prompts/poster_ko.md)**
- **[🖥️ UI 전체 116개 보기](prompts/ui_ko.md)**
- **[🆚 비교 테스트 전체 78개 보기](prompts/comparison_ko.md)**

<a id="faq"></a>
## ❓ 자주 묻는 질문

<details>
<summary><b>GPT Image 2 프롬프트는 무료로 쓸 수 있나요? 이미지 권리는 누구에게 있나요?</b></summary>

이 모음집은 CC0로 퍼블릭 도메인에 공개되어 프롬프트를 자유롭게 복사하고 고쳐서 실행할 수 있습니다. 예시 이미지는 카드에 표시된 제작자의 것입니다. 직접 만든 이미지는 프롬프트에 넣은 브랜드, 로고, 실존 인물의 모습을 쓸 권리가 있는지 확인하세요.

</details>

<details>
<summary><b>GPT Image 2 프롬프트는 한국어로 써도 되나요?</b></summary>

여기 프롬프트는 작성자의 원문 그대로이며 대부분 영어이고 일부는 중국어입니다. GPT Image 2는 영어와 중국어를 받으니 가장 편한 언어로 쓰면 됩니다.

</details>

<details>
<summary><b>API로 GPT Image 2 프롬프트를 실행하려면 어떻게 하나요?</b></summary>

POST /v1/images/generations에 model을 gpt-image-2로, prompt와 size(예: 16:9), resolution(1k, 2k, 4k), "async": true를 담아 보낸 뒤 GET /v1/tasks/{id}를 폴링합니다. 전체 파라미터는 API 문서에 있습니다.

</details>

<details>
<summary><b>GPT Image 2는 어떤 비율과 크기를 지원하나요?</b></summary>

비율은 1:1, 16:9, 9:16, 3:2, 2:3, 4:3, 3:4, 5:4, 4:5, 21:9이고 해상도는 1k, 2k, 4k입니다. 비율과 단계마다 픽셀 크기가 고정되어 있고, 그 표의 크기 중 하나를 WIDTHxHEIGHT로 넘길 수도 있습니다. auto는 지원하지 않습니다.

</details>

<details>
<summary><b>참조 사진이 필요한 카드는 GPT Image 2에서 어떻게 쓰나요?</b></summary>

POST /v1/uploads/images로 이미지를 올린 뒤 돌려받은 공개 HTTPS 주소를 images에 넣어 POST /v1/images/edits를 호출합니다. GPT Image 2는 참조 이미지를 0~16장 받으며, 참조를 쓰면 출력 크기가 요청과 같다는 보장은 없습니다.

</details>

<details>
<summary><b>내 GPT Image 2 결과가 카드 이미지와 다른 이유는 무엇인가요?</b></summary>

이미지 모델은 결정적이지 않아 같은 프롬프트도 실행할 때마다 결과가 다릅니다. 작성자가 다른 도구나 설정, 참조 이미지를 썼을 수도 있습니다.

</details>

<details>
<summary><b>ChatGPT용으로 쓴 GPT Image 2 프롬프트를 API에서도 쓸 수 있나요?</b></summary>

일반 텍스트라서 그대로 붙여 넣으면 됩니다. 일부 작성자는 ChatGPT에서 실행했다고 밝히는데, 설정이 달라 결과는 비슷할 뿐 똑같지는 않습니다.

</details>

<details>
<summary><b>포스터, 이커머스, 캐릭터용 GPT Image 2 프롬프트도 있나요?</b></summary>

네. 포스터, 이커머스, 캐릭터, 광고가 각각 따로 있고 위의 분류 이름을 누르면 바로 이동합니다. '비교 테스트'에는 단어 몇 개만 바꿔도 결과가 달라지는 것을 보여 주는 테스트가 모여 있습니다.

</details>

<details>
<summary><b>GPT Image 2 포스터의 글자를 정확하게 넣으려면 어떻게 하나요?</b></summary>

단어마다 따옴표로 감싸고 들어갈 위치를 적으며, 한 줄은 짧게 둡니다. 글자가 작다면 더 큰 해상도 단계를 골라 글자에 픽셀을 더 배분하세요.

</details>


<a id="related"></a>
## 🔗 관련 링크

- [GPT Image 2 프롬프트 · apiko.app](https://apiko.app/ko/gpt-image-2-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2 실행](https://apiko.app/ko/models/gpt-image-2?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2 API 문서](https://apiko.app/docs/api-manual/image-series/gpt-image-2/gpt-image-2-image-generation?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 Flare](https://apiko.app/ko/models/gpt-image-2.5-flare?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [GPT Image 2.5 프롬프트](https://apiko.app/ko/gpt-image-2-5-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [AI 이미지 생성기](https://apiko.app/ko/image-generator?utm_source=github&utm_medium=related&utm_campaign=awesome-gpt-image-2-prompts)
- [APIKO API 코드 예시](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**다른 프롬프트 모음**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_ko.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_ko.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_ko.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_ko.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_ko.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_ko.md)

<a id="license"></a>
## 📄 라이선스와 출처

프롬프트와 이미지의 권리는 각 카드에 표시된 제작자에게 있고, 카드는 원본 게시물로 연결됩니다. 이 모음집은 CC0로 퍼블릭 도메인에 공개되었습니다. 제목, 설명, 번역, 빌드 스크립트는 [CC BY 4.0](LICENSE)으로 배포합니다.

이 목록이 도움이 됐다면 ⭐ 를 눌러 다른 사람도 찾을 수 있게 해 주세요.
