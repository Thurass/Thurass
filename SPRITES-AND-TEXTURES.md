# Sprites & Textures — Asset & Tooling Library

A broad, exhaustively-researched reference library of **where to get** and **how to make, process, and ship** game and graphics assets — 2D sprites, 2D/3D textures, 3D models, fonts & icons, audio, and VFX/shaders.

> **How this was built.** Compiled from thirteen parallel web-research sweeps (June 2026), one per domain below. Every link was checked by the researching agent to resolve to a real, current resource — no invented URLs. Pricing, licenses, and product status change; treat figures as "as of mid-2026" and re-verify license terms before shipping. Nothing here is legal advice (see [§9](#9-curated-lists-cc0-hubs--licensing-guide)).

---

## How to read this library

**License / cost shorthand used throughout:**

| Tag | Meaning |
|---|---|
| **CC0** | Public-domain dedication — use anywhere, commercial OK, no attribution required |
| **CC-BY** | Free, commercial OK, **attribution required** |
| **CC-BY-SA** | As CC-BY, but derivatives must keep the same/compatible license (ShareAlike) |
| **CC-BY-NC** | Attribution + **NonCommercial only** (avoid for revenue projects) |
| **RF** | Royalty-free — usually pay once, reuse without per-use fees, but still licensed (≠ public domain) |
| **EULA** | Proprietary marketplace/store license — you buy a *right to use*, not ownership |
| **OSS** | Free & open source (MIT/Apache/GPL/etc., as noted) |

**Sections:**

1. [2D Sprite & Game-Art Asset Sources](#1-2d-sprite--game-art-asset-sources) — where to download ready-made 2D art
2. [PBR & 3D Texture / Material Libraries](#2-pbr--3d-texture--material-libraries) — seamless textures and PBR map sets
3. [Sprite & Pixel-Art Creation / Editing Software](#3-sprite--pixel-art-creation--editing-software) — draw and animate sprites
4. [Texture & Material Authoring Tools](#4-texture--material-authoring-tools) — author/derive PBR materials
5. [Sprite-Sheet / Atlas Packers & 2D Animation Tools](#5-sprite-sheet--atlas-packers--2d-animation-tools) — pack atlases, rig animation
6. [Programmatic Image & Texture Processing](#6-programmatic-image--texture-processing-libraries-clis-compression) — scripts, libraries, GPU compression
7. [AI-Powered Sprite & Texture Generation](#7-ai-powered-sprite--texture-generation) — generative tools (+ licensing caveats)
8. [Runtime Frameworks & Engines](#8-runtime-frameworks--engines-sprites--textures-in-code) — load/render sprites & textures in code
9. [Curated Lists, CC0 Hubs & Licensing Guide](#9-curated-lists-cc0-hubs--licensing-guide) — meta-resources and how to stay legal

*Extended asset categories:*

10. [3D Models & Meshes](#10-3d-models--meshes) — model sources, formats, and the glTF pipeline
11. [Fonts, Bitmap Fonts & Icon Systems](#11-fonts-bitmap-fonts--icon-systems) — type, bitmap-font/SDF tools, icons, emoji
12. [Game Audio — Sound Effects, Music & Tools](#12-game-audio--sound-effects-music--tools) — SFX/music sources, editors, middleware
13. [VFX, Particles & Shaders](#13-vfx-particles--shaders) — particle/VFX editors, shader tools & learning
- [Appendix: End-to-End Workflow Recipes](#appendix-end-to-end-workflow-recipes)

---

## Recommended starter stacks

Opinionated, mostly-free bundles assembled from the sections below. Section refs in parentheses.

**A — Free 2D web game (TypeScript), pixel-art style**
Draw in **Aseprite** or free **Pixelorama**/**Piskel** (§3) → grab CC0 packs from **Kenney**, **itch.io**, **OpenGameArt** (§1) → pack with **Free Texture Packer** or **TexturePacker** (§5) → render with **Pixi.js** or **Phaser** (both have TexturePacker + Aseprite loaders) (§8) → optimize the build with **sharp** + **oxipng/pngquant** (§6). Prefer CC0; keep attribution strings for any CC-BY (§9).

**B — 3D / PBR material pipeline**
Pull CC0 textures from **Poly Haven** / **ambientCG** (§2) → author custom materials in **Blender** + **Material Maker** (free) or **Substance Designer/Painter**, derive maps with **Materialize**/**AwesomeBump** (§4) → compress to **KTX2 + Basis Universal** via **toktx** (§6) → load with **Three.js** or **Babylon.js** `KTX2Loader` (§8).

**C — 2D skeletal/cutout animation**
Rig and animate in **Spine** (paid) or free **DragonBones** (§5) → play back through official runtimes in **Pixi.js / Phaser / Godot / Unity** (§5, §8).

**D — AI-assisted, leaning commercial-safe**
Sprites from **Scenario** / **PixelLab** / **Retro Diffusion** (paid tiers) → textures from **Adobe Firefly** + **Substance 3D Sampler**, or **Polycam** / **Poly** (§7). ⚠️ Verify each tool's commercial-use + IP terms before shipping (§7, §9).

**E — Headless asset build/optimization (CLI/CI)**
`ImageMagick`/`sharp` (resize/convert) → `pngquant`/`oxipng`/`mozjpeg` (optimize) → `TexturePacker` CLI or `free-tex-packer-cli` (atlas) → `basisu`/`toktx` (GPU compress to KTX2). (§5, §6)

---

## 1. 2D Sprite & Game-Art Asset Sources

Websites and marketplaces where you download ready-made 2D sprites, pixel art, character sprite sheets, tilesets, UI kits, backgrounds, and icon packs.

### Free / CC0 & open-license
- **[Kenney](https://kenney.nl/)** — Huge library of cohesive sprite packs, pixel platformer tiles, UI, top-down kits, and icons by Kenney Vleugels. *CC0 · sprites/tilesets/UI/icons · [browse assets](https://kenney.nl/assets) · also on [itch.io](https://kenney.itch.io/).*
- **[OpenGameArt.org](https://opengameart.org/)** — The largest community archive of free-licensed 2D art: sprites, tilesets, characters, GUI, icons. *Mixed CC0 / CC-BY / CC-BY-SA / GPL / OGA-BY (per asset) · 2D art of all kinds.* **Licensing note:** license varies per submission — check each asset's license box and attribute accordingly (see [§9](#9-curated-lists-cc0-hubs--licensing-guide)).
- **[Reiner's Tilesets](https://www.reinerstilesets.de/)** — Long-running freeware site by Reiner Prokein with 2D sprites, isometric tiles, animated characters, vehicles, and humans. *Freeware incl. commercial use (credit "Reiner 'Tiles' Prokein") · [2D graphics index](https://www.reinerstilesets.de/graphics/2d-grafiken/) · [license](https://www.reinerstilesets.de/graphics/lizenz/).*
- **[Game-icons.net](https://game-icons.net/)** — 4,000+ vector game/RPG icons (weapons, spells, items, UI) in SVG and PNG. *CC-BY 3.0 (attribution required) · icons.* **Licensing note:** credit "Icons made by [author] — game-icons.net".
- **[Liberated Pixel Cup (LPC)](https://opengameart.org/content/liberated-pixel-cup-0)** — Open consistent-style 2D character/tileset art; powers the [Universal LPC Spritesheet Generator](https://liberatedpixelcup.github.io/Universal-LPC-Spritesheet-Character-Generator/). *CC-BY-SA 3.0 + GPLv3 · character sprite sheets/tiles.* **Licensing note:** share-alike; list per-asset authors/licenses for every sprite layer used.
- **[Quaternius](https://quaternius.com/)** — Primarily CC0 low-poly 3D, but includes 2D card kits and platformer assets; one cohesive style. *CC0 · mostly 3D, some 2D kits · also on [itch.io](https://quaternius.itch.io/).*

### Marketplaces (paid + free)
- **[itch.io — Game Assets](https://itch.io/game-assets)** — Massive open marketplace of indie 2D asset packs; per-creator pricing and licensing. *Free + paid, license set by seller (often CC0 or custom EULA) · [2D + Sprites tag](https://itch.io/game-assets/tag-2d/tag-sprites) · [free 2D sprites](https://itch.io/game-assets/free/tag-2d/tag-sprites).*
- **[CraftPix.net](https://craftpix.net/)** — High-volume store of 2D sprites, tilesets, GUI, backgrounds, icons, and game kits; large freebies section. *RF proprietary (unlimited commercial projects) · [freebies](https://craftpix.net/freebies/) · [all assets](https://craftpix.net/all-game-assets/).*
- **[GameArt2D.com](https://www.gameart2d.com/)** — RF 2D character sprites, platformer/top-down tilesets, GUI packs, and backgrounds. *RF proprietary · [freebies](https://www.gameart2d.com/freebies.html) · [license](https://www.gameart2d.com/license.html).*
- **[Game Developer Studio](https://www.gamedeveloperstudio.com/)** — Thousands of hand-drawn animated 2D sprites/characters/props in one consistent style. *Per-asset proprietary · animated 2D sprites/backgrounds/UI.*
- **[GameDev Market](https://www.gamedevmarket.net/)** — Curated indie marketplace for 2D sprites, tilesets, GUI, and audio. *Single "Pro Licence" (commercial, unlimited projects) · [2D category](https://www.gamedevmarket.net/category/2d).*
- **[Unity Asset Store (2D)](https://assetstore.unity.com/2d)** — Engine-integrated store with 2D characters, environments, and pixel-art packs (free + paid). *Unity Asset Store EULA · [2D characters](https://assetstore.unity.com/2d/characters) · [pixel assets](https://assetstore.unity.com/popular-assets/pixel-assets).*
- **[Fab](https://www.fab.com/)** — Epic's unified content marketplace (successor to Unreal Marketplace/Sketchfab/Quixel/ArtStation); 2D assets for Unreal, Unity, and other tools. *Per-product Fab license (commercial) · multi-engine assets.*
- **[Unreal Engine Marketplace (legacy)](https://www.unrealengine.com/marketplace)** — Being replaced by Fab; existing purchases remain in the Unreal vault. *Legacy UE EULA · migrating to [Fab](https://www.fab.com/).*
- **[Envato GraphicRiver](https://graphicriver.net/category/game-assets/sprites)** — 1,900+ game sprite/sheet templates (PNG/EPS/AI/PSD); also via Envato Elements subscription. *Envato per-item or subscription license · sprites/sheets.*
- **[Creative Market](https://creativemarket.com/)** — Independent-designer marketplace including 2D game sprites, pixel art, and graphic kits. *Per-product license (commercial) · sprites/graphics/UI.*
- **[Humble Bundle — gamedev/asset bundles](https://www.humblebundle.com/software)** — Periodic pay-what-you-want bundles of 2D sprite/tileset/SFX packs (often redeemed on itch.io). *Bundle-specific license · time-limited bundles.*

### Notable individual creators
- **[Pixel Frog](https://pixelfrog-assets.itch.io/)** — Polished modular pixel-art packs incl. Pixel Adventure 1/2 and Tiny Swords. *CC0 (free) · platformer/strategy sprites.*
- **[ansimuz / Luis Zuno](https://ansimuz.itch.io/)** — Prolific 16-bit pixel art (Gothicvania, Sunny Land, Warped, Tiny RPG, effects); free starter packs + paid collections. *Mixed — many free packs CC0, paid collections commercial license · [ansimuz.com](https://ansimuz.com/).*
- **[Cainos](https://cainos.itch.io/)** — Clean pixel-art top-down and platformer tilesets, props, and RPG icon packs. *Free + paid; commercial use allowed, no resale · [Pixel Art Top Down – Basic](https://cainos.itch.io/pixel-art-top-down-basic).*
- **[Penzilla](https://penzilla.itch.io/)** — Pixel-art tilesets (terrain, cyberpunk, interiors), GUI bundles, animated characters. *Free + paid, per-pack license.*
- **[0x72](https://0x72.itch.io/)** — Compact 16×16 pixel tilesets incl. the widely used DungeonTileset II and µFantasy. *CC0 (free) · [DungeonTileset II](https://0x72.itch.io/dungeontileset-ii).*
- **[Buch (Michele Bucelli)](https://opengameart.org/users/buch)** — Classic OGA pixel-art tilesets and backgrounds (dungeon, outside, RPG). *CC-BY / CC0 per asset.*
- **[Cup Nooble](https://cupnooble.itch.io/sprout-lands-asset-pack)** — Cozy 16-bit farming pixel art (Sprout Lands asset + UI packs). *Freemium · free pack = non-commercial only; commercial requires paid version (≈$3.99+); no resale.*
- **[pixel-boy (Sébastien Bénard)](https://pixel-boy.itch.io/ninja-adventure-asset-pack)** — Ninja Adventure pack: top-down RPG characters, enemies, tiles, plus sound/music. *CC0 (free).*
- **[chierit](https://chierit.itch.io/)** — Animated boss/monster sprites and pixel VFX (Demon Slime, Frost Guardian…), Aseprite source included. *CC-BY 4.0 (credit required); commercial OK.*
- **[finalbossblues (Time Fantasy)](https://finalbossblues.itch.io/)** — SNES-style "Time Fantasy" RPG character/monster packs and tilesets. *Paid, RF for any engine · battlers by [Tyler Warren](https://tylerjwarren.itch.io/).*
- **[Free Game Assets (CraftPix's itch arm)](https://free-game-assets.itch.io/)** — CraftPix's itch.io storefront for free GUI, sprite, and tileset releases. *Free under CraftPix [file license](https://craftpix.net/file-licenses/).*

### Ripped-sprite archives (reference only — not for commercial use)
- **[The Spriters Resource](https://www.spriters-resource.com/)** — Community archive of sprite sheets ripped from commercial games across all platforms. *Copyright held by original publishers · [Terms of Use](https://www.spriters-resource.com/page/tou/).* **Licensing note:** owned by the original companies — not licensed for commercial use or store publication; reference/study only.
- **[Sprite Database](https://www.spritedatabase.net/)** — Similar archive of ripped sprites organized by console/platform, plus ripping tools. *Copyright held by original publishers · private/non-commercial only.*

> **Note:** For free packs, licensing is per-asset/per-pack — always confirm the license on the specific download page before shipping (especially "free for non-commercial" vs. CC0 vs. attribution-required).

---

## 2. PBR & 3D Texture / Material Libraries

High-quality seamless textures and physically-based-rendering (PBR) material sets — albedo/diffuse, normal, roughness/gloss, metallic, ambient occlusion (AO), and height/displacement maps — for Blender, Unreal, Unity, Godot, 3ds Max, Maya, and offline renderers. Grouped by license model.

### CC0 / fully free (public domain, commercial OK, no attribution)
- **[Poly Haven](https://polyhaven.com/textures)** — Photoscanned seamless materials, no signup or paywall; absorbed the former Texture Haven. *CC0 · up to 8K · albedo, roughness, metalness, normal, displacement · free.*
- **[ambientCG](https://ambientcg.com/)** — 2,800+ PBR materials (plus HDRIs/models), formerly CC0Textures.com; no registration. *CC0 · up to 8K · albedo, normal, roughness, AO, displacement · JPG/PNG · free.*
- **[cgbookcase.com](https://www.cgbookcase.com/textures)** — ~566 free texture sets, multiple resolution tiers per asset. *CC0 1.0 · 1K–8K · base color, normal, height, roughness, AO, metallic · free.*
- **[3dtextures.me](https://3dtextures.me/)** — Large, frequently-updated seamless library; 4K + SBS/SBSAR source via Patreon. *CC0 · 1K free (4K via Patreon) · diffuse, normal, metallic, displacement, roughness, AO · free.*
- **[ShareTextures](https://www.sharetextures.com/)** — Free CC0 textures and 3D models, no signup. *Custom CC0 · up to 4K · diffuse, displacement, normal, specular, AO · TIFF/PNG · free.*
- **[TextureCan](https://www.texturecan.com/)** — 650+ free PBR textures plus CC0 3D models; SBSAR procedural files offered. *CC0 · 4K+ · PBR map sets · free.*
- **[Texture Ninja](https://texture.ninja/)** — 5,000+ public-domain photo textures and cutouts; raw reference more than ready-made PBR. *CC0 · ~5,000px+ wide · raw photo textures (no normal/rough maps) · free.*
- **[Material Maker](https://www.materialmaker.org/)** — Open-source (Godot-based) node tool to *author* procedural materials, with a community library of hundreds of materials/nodes/brushes. *MIT · exports full PBR sets · free.* → full entry in [§4](#4-texture--material-authoring-tools).

### Freemium (free tier + paid/subscription for higher-res or commercial)
- **[Poliigon](https://www.poliigon.com/)** — ~103 free assets; 3,000+ premium via credits or subscription, specular/gloss and metal/rough workflows. *Proprietary (commercial OK) · free 1K–4K, premium up to 8K · diffuse, displacement, normal, AO · PNG · freemium.*
- **[Textures.com](https://www.textures.com/)** — Formerly CGTextures; 140,000+ photo textures plus 2,000+ PBR materials/3D scans. Free account = daily credits; per-asset licenses vary. *Proprietary (per-asset) · up to 16K (scans) · diffuse, normal, roughness, AO, displacement · freemium.*
- **[FreePBR.com](https://freepbr.com/)** — 600+ PBR sets free for non-commercial; one-time ~$16 unlocks commercial + batch download. *Free NC / paid commercial · 2K · normal, albedo, roughness, metallic, AO, sometimes height · PNG · freemium.*
- **[LotPixel](https://www.lotpixel.com/)** — 1,300+ scan-based texture sets free (registration); premium adds higher res, 3D scans, decals. *Proprietary (commercial OK, no resale) · up to 8K free (16K premium) · full PBR set · JPEG · freemium.*
- **[Texture Box](https://texturebox.com/)** — Free CC0 PBR sets plus premium (~$3/mo) for 1,500+ textures and 3D-scan assets (Patreon-exclusive sets not CC0). *CC0 (free) / proprietary (premium) · 1K–8K · full PBR sets · freemium.*
- **[GenPBR](https://genpbr.com/)** — Browser image-to-PBR generator (not a fixed library); free 1K, paid adds 4K–8K, API, commercial license; $299 lifetime option. *Free 1K (commercial via paid) · up to 8K · normal, roughness, metallic, AO, height (+ MaterialX) · freemium.*
- **[Architextures (ARTX)](https://architextures.org/)** — Procedural seamless-texture / bump-map / CAD-hatch web app for architects; Revit & SketchUp plugins. *Proprietary · procedural · color + bump/CAD hatch · freemium.*

### Paid / subscription (professional libraries)
- **[Quixel Megascans (via Fab)](https://www.fab.com/)** — World's largest scanned asset library (surfaces, 3D scans, atlases, decals); free-for-all era ended Dec 2024, now individually priced or in Fab subscription tiers. *Fab Standard license · up to 8K · full scan-based PBR sets · paid (some free rotation).*
- **[Adobe Substance 3D Assets](https://substance3d.adobe.com/assets/)** — ~20,000 parametric materials, models, HDR lights; unmetered for Texturing ($19.99/mo) or Collection ($49.99/mo) subscribers. *Proprietary (subscription) · parametric (resolution on export) · all PBR channels · .sbsar · paid.*
- **[GameTextures.com](https://gametextures.com/)** — 3,000+ customizable PBR/Substance materials; subscription with rollover credits; separate commercial vs. NC (≤$2K/yr) licenses. *Proprietary (subscription) · 4K · paid.*
- **[ScansLibrary](https://www.scanslibrary.com/)** — High-end surface, plant, and 3D-asset photogrammetry scans. *Proprietary (subscription/credits) · up to 8K+ · full scan PBR sets · paid.*
- **[HDRMAPS](https://hdrmaps.com/textures/)** — Photo-based PBR materials, textures, and scanned models (alongside its HDRI library). *Proprietary (free + paid) · up to 8K · diffuse, normal, roughness, AO, displacement · freemium.*
- **[Sketchfab Store (Fab)](https://sketchfab.com/store)** — Marketplace of individually-sold texture/material packs from independent creators; commercial OK, no resale/repackaging. *Per-seller RF · varies (commonly 4K) · paid.*

### Reference / photo textures (graphics & overlays, not full PBR sets)
- **[Wild Textures](https://www.wildtextures.com/free-textures/)** — High-res photographic textures, backgrounds, patterns; no credit required, no redistribution. *Free personal/commercial · high-res JPG · flat textures.*
- **[Textures4Photoshop](https://www.textures4photoshop.com/)** — Large collection of Photoshop textures/overlays. *CC-BY (attribution) · flat textures.*
- **[Free Stock Textures](https://freestocktextures.com/)** — RF photographic stock textures for design and 3D reference. *RF (no redistribution) · high-res JPG · flat textures.*

> **Note:** `cc0textures.com` / `cc0-textures.com` are legacy domains for what is now **ambientCG** — historical mirrors, not a separate library.

**Top sources at a glance:**

| Source | License | Max Res | Maps | Free? |
|---|---|---|---|---|
| Poly Haven | CC0 | 8K | albedo, rough, metal, normal, displ | Yes |
| ambientCG | CC0 | 8K | albedo, normal, rough, AO, displ | Yes |
| cgbookcase | CC0 1.0 | 8K | base color, normal, height, rough, AO, metal | Yes |
| 3dtextures.me | CC0 | 1K (4K Patreon) | diffuse, normal, metal, displ, rough, AO | Yes |
| Poliigon | Proprietary | 4K free / 8K paid | diffuse, displ, normal, AO | Freemium |
| Textures.com | Proprietary | up to 16K | diffuse, normal, rough, AO, displ | Freemium |
| Quixel/Fab | Fab Standard | 8K | full scan PBR set | Paid |
| Substance 3D Assets | Subscription | parametric | all PBR channels (.sbsar) | Paid |

---

## 3. Sprite & Pixel-Art Creation / Editing Software

Applications to draw, animate, and export sprites, pixel art, tilesets, and sprite sheets.

### Dedicated pixel-art & sprite editors
- **[Aseprite](https://www.aseprite.org/)** — The de-facto standard pixel-art and animation tool, built around frames, layers, and tags. *Win/Mac/Linux · paid (~$19.99; source on GitHub under EULA) · onion-skinning, palette/alpha management, custom brushes, pixel-perfect strokes, RotSprite, tiled mode, PNG+JSON sheet export, full Lua scripting API + CLI · [docs](https://www.aseprite.org/docs/).*
- **[LibreSprite](https://libresprite.github.io/)** — Free/open fork of the last GPLv2 Aseprite release. *Win/Mac/Linux/Android · OSS (GPLv2) · animation preview, onion-skinning, layers+frames, palettes, tiled mode · [docs](https://github.com/LibreSprite/LibreSprite/wiki).*
- **[Pixelorama](https://www.pixelorama.org/)** — Powerful open-source pixel-art multitool built on Godot. *Win/Mac/Linux/Web · OSS (MIT) · timeline layers/frames, onion-skinning, cel linking, non-destructive layer effects, 3D layers, isometric/hex tilemap layers, pixel-art rotation/scaling, PNG/spritesheet/GIF/APNG export, extensions · [docs](https://www.oramainteractive.com/Pixelorama-Docs/).*
- **[Pyxel Edit](https://pyxeledit.com/)** — Pixel-art editor focused on tileset creation and level design. *Win/Mac (older free beta + paid ~$9) · tile references (edit one tile, all update), tileset auto-detection, onion-skinning, animation, sheet/GIF export, tilemap XML/JSON/text · [docs](https://pyxeledit.com/learn.php).*
- **[Pro Motion NG](https://www.cosmigo.com/pixel_animation_software)** — Long-running professional pixel-art/animation studio (Deluxe Paint lineage). *Win (Mac/Linux via Wine) · free edition + full ~$19 · animation timeline, onion-skinning, tile/map editor, color-cycling, dithering, tileset/sheet export · [docs](https://www.cosmigo.com/pixel_animation_software/manual).*
- **[GraphicsGale](https://graphicsgale.com/us/)** — Veteran Windows spriting/animation editor (since 1997), now freeware. *Windows · free · real-time animation preview, robust onion-skinning, layers, palette control, export to sheet/per-frame/GIF/AVI, TWAIN import · [docs](https://graphicsgale.com/us/faq.html).*
- **[GrafX2](http://grafx2.chez.com/)** — Open-source 256-color bitmap paint program inspired by Deluxe Paint/Brilliance. *Win/Linux/Haiku + ports · OSS (GPL) · indexed-palette painting, airbrush/splines/gradients, custom brushes, dual-view, RGB/HSL palette editor, color-cycling · [docs](http://grafx2.chez.com/index.php?static3/documentation).*
- **[mtPaint](https://mtpaint.sourceforge.net/)** — Lightweight open-source raster editor for icons/pixel art/photos; runs on low-spec hardware. *Win/Linux · OSS (GPL) · 1000 undo steps, zoom 10%–8000%, up to 100 layers, palette/layer-move animation, PNG/GIF/TIFF/WEBP · [docs](https://mtpaint.sourceforge.net/handbook/).*
- **[PikoPixel](https://twilightedge.com/mac/pikopixel/)** — Free open-source pixel-art drawing app for Apple/Unix. *Mac/Linux/BSD (GNUstep) · OSS · unlimited undo, layers, customizable canvas bg, hotkey panels, gamma-correct (linear) blending · [docs](https://twilightedge.com/mac/pikopixel/documentation.html).*
- **[Pixen](https://pixenapp.com/)** — Native pixel-art and animation editor for Apple platforms. *Mac/iPhone/iPad · paid (App Store) · layers, palettes, animation, high zoom, iCloud sync, Apple Pencil, Dark Mode.*
- **[Pixaki](https://pixaki.com/)** — Polished iPad-first pixel-art studio designed around Apple Pencil. *iPad (free "Intro" + paid "Pro") · up to 50 layers, frame animation, palettes, reference layers, sheet export · [docs](https://pixaki.com/help/).*
- **[PixiEditor](https://pixieditor.net/)** — Open-source universal 2D editor mixing pixel art, vector, painting, and node-based procedural graphics. *Win/Mac/Linux (Avalonia) · OSS (MIT) · frame animation, node-graph non-destructive workflow, photo adjustments, vector editing, PNG/JPG/SVG/GIF/MP4 export · [docs](https://pixieditor.net/docs/introduction/).*

### Web-based pixel-art editors
- **[Piskel](https://www.piskelapp.com/)** — Easy in-browser sprite editor with free offline desktop builds. *Web + Win/Mac/Linux · OSS · live animation preview, unlimited layers, mirror pen, GIF + spritesheet PNG/ZIP export (with frame coords for Unity/Phaser/Godot) · [docs](https://github.com/piskelapp/piskel/wiki).*
- **[Lospec Pixel Editor](https://lospec.com/pixel-editor/)** — Free, minimal browser pixel-art tool from the Lospec community (now open source). *Web (installable PWA) · OSS · pencil/eraser/fill/shape, palette picker, animation frames, layers, PNG/GIF export · [source](https://github.com/lospec/pixel-editor).*
- **[Pixilart](https://www.pixilart.com/)** — Free online drawing tool plus a large pixel-art community. *Web + Android/iOS · free · layers, animation frames/GIF, autosave, adjustable export, gallery/contests · [articles](https://www.pixilart.com/articles).*

### General raster editors (capable of pixel art)
- **[Krita](https://krita.org/)** — Free open-source digital-painting suite with a dedicated pixel engine and full animation workspace. *Win/Mac/Linux/Android · OSS (GPL) · 12+ brush engines, rich layer/mask stack, frame-by-frame animation timeline with audio import + video export · [docs](https://docs.krita.org/).*
- **[GIMP](https://www.gimp.org/)** — Long-established free open-source raster editor; pixel art via zoom/grid/indexed modes and GIF-layer animation. *Win/Mac/Linux · OSS (GPL) · layers, indexed palettes, animation plug-in (GIF/MNG), Script-Fu/Python-Fu · [docs](https://docs.gimp.org/).*
- **[Adobe Photoshop](https://www.adobe.com/products/photoshop.html)** — Industry-standard raster editor; pixel art via Pencil tool, nearest-neighbor scaling, frame/timeline animation. *Win/Mac/iPad · paid (Creative Cloud) · layers, frame animation, sheet export, scripting, huge plug-in ecosystem · [docs](https://helpx.adobe.com/photoshop/user-guide.html).*
- **[Affinity (Photo)](https://www.affinity.studio/)** — Professional photo/vector/layout app (former Affinity Photo, reimagined as "Affinity by Canva" v3, Oct 2025). *Win/Mac/iPad · now free (freemium; Canva AI behind Canva Pro) · Pixel/Vector/Layout studios, layers, masks, non-destructive adjustments · [docs](https://affinity.help/).*

### Tilemap / level editors
- **[Tiled](https://www.mapeditor.org/)** — Flexible, general-purpose open-source tile-map and level editor. *Win/Mac/Linux · OSS (GPL; donation) · orthogonal/isometric/hex maps, unlimited layers, object layers, tile animation + per-tile collision, custom properties, TMX/JSON, JS extensions & plugin formats · [docs](https://doc.mapeditor.org/).*
- **[LDtk](https://ldtk.io/)** — Modern, friendly 2D level editor from the director of Dead Cells. *Win/Mac/Linux · OSS (MIT) · rule-based auto-tiling, world layouts, typed entities, crash backup, "Super Simple Export" (PNG+JSON) + Tiled (TMX) export, engine API loaders · [docs](https://ldtk.io/docs/).*
- **[Tilesetter](https://www.tilesetter.org/)** — Tileset generator + map editor that builds smart auto-tilesets from a base tile. *Win/Mac/Linux · paid (~$12.99) · auto-tile/Wang generation, live compositing, export to Godot/Unity/GameMaker 2/Defold · [docs](https://www.tilesetter.org/docs).*
- **[Sprite Fusion](https://www.spritefusion.com/)** — Free browser-based 2D tilemap/level editor; no account or install. *Web (also itch.io) · free (incl. commercial) · drag-drop tilesets, auto-tiling, layers, export to Unity/Godot/Defold + UVTT for VTTs · [blog/docs](https://www.spritefusion.com/blog).*
- **[Tile Studio](https://tilestudio.sourceforge.net/)** — Classic all-in-one tile/sprite bitmap editor + map editor with programmable output. *Windows · OSS · bitmap editor, animation sequences, map editor, fully customizable code/data generator · [docs](https://tilestudio.sourceforge.net/tutor.html).*

### Sprite normal-map & lighting tools
- **[Laigter](https://azagaya.itch.io/laigter)** — Open-source automatic normal-map generator for sprites. *Win/Mac/Linux · OSS (GPL-3.0, pay-what-you-want) · generates normal/specular/parallax/AO maps with real-time multi-light preview (also usable on textures) · [docs](https://laigter.readthedocs.io/).*
- **[SpriteIlluminator](https://www.codeandweb.com/spriteilluminator)** — Dedicated normal-map editor for 2D dynamic lighting by CodeAndWeb. *Win/Mac · paid (~$40 perpetual) · algorithmic + hand-painted normals, Bevel/Emboss/Corner-Brush, lasso/magic-wand, Unity/GameMaker/Cocos2d integration · [docs](https://www.codeandweb.com/spriteilluminator/documentation).*
- **[Sprite Lamp](https://www.snakehillgames.com/spritelamp/)** — Turns hand-drawn shading profiles into normal/depth maps that preserve 2D art style. *Win/Mac/Linux · paid · normal/depth from line art, shaders for Unity etc., works with skeletal animation (e.g. Spine) · [docs](https://www.snakehillgames.com/using-sprite-lamp-with-engines/).*
- **[Sprite DLight](https://www.kickstarter.com/projects/2dee/sprite-dlight-instant-normal-maps-for-2d-graphics)** — One-click "instant" normal-map generator for 2D sprites/pixel art. *Win/Mac/Linux · paid · volumetric normal/depth/AO/specular in one click, day/night re-render, Unity integration.*

> **Note:** Affinity Photo's status changed materially in Oct 2025 (now free/freemium, merged into a single "Affinity by Canva" app); Affinity V2 perpetual licenses via Serif remain valid but won't get future updates.

---

## 4. Texture & Material Authoring Tools

Software to *create* PBR materials/textures — procedurally (node graphs), by painting, or by deriving maps (normal/AO/height) from images. **Strong free/open picks are flagged.**

### Procedural / node-based
- **[Adobe Substance 3D Designer](https://www.adobe.com/products/substance3d/apps/designer.html)** — Industry-standard procedural material authoring; fully parametric, resolution-independent PBR in a non-destructive node graph (400+ nodes), output reusable `.sbsar`. *Win/Mac/Linux · subscription (Texturing $24.99/mo or $249.99/yr) or $199.99 perpetual · [docs](https://helpx.adobe.com/substance-3d-designer.html).*
- **[Material Maker](https://www.materialmaker.org/)** — Free, open-source Substance Designer alternative built on Godot; ~250 nodes, SDF shapes, custom GLSL nodes, plus 3D painting, with export presets for Godot/Unity/Unreal/Blender. *Win/Mac/Linux · OSS (MIT) · [docs](https://github.com/RodZill4/material-maker).* **★ Strong free/open pick.**
- **[Filter Forge](https://filterforge.com/)** — Node-based filter/texture editor generating seamless procedural textures (up to 65000² px) with randomized variations; standalone or Photoshop/Affinity plugin, big community filter library. *Win/Mac · commercial (editions from ~$29; trial) · [docs](https://www.filterforge.com/more/help/index.html).*
- **[MaPZone](https://www.gamedeveloper.com/pc/allegorithmic-releases-free-mapzone-2-6-texture-tool)** — Legacy free node-based texturing tool from Allegorithmic (predecessor to Substance), FXMaps tech, auto-tiling diffuse/specular/normal. *Win · free (legacy).*

### Painting (3D & 2D)
- **[Adobe Substance 3D Painter](https://www.adobe.com/products/substance3d/apps/painter.html)** — The reference 3D texture-painting app (AAA games/film/VFX); paint on 3D models with smart materials/masks, non-destructive layer stack, integrated baking. *Win/Mac/Linux · subscription ($24.99/mo or $249.99/yr) or $199.99 perpetual · [docs](https://helpx.adobe.com/substance-3d-painter/get-started.html).*
- **[Foundry Mari](https://www.foundry.com/products/mari)** — High-end 3D painting for film/VFX-scale assets; hundreds of high-res UDIM textures, full Node Graph + layer workflows. *Win/Linux/Mac · subscription ~$86/mo or $689/yr; **free non-commercial edition** · [docs](https://learn.foundry.com/mari).*
- **[3DCoat / 3DCoatTextura](https://pilgway.com/product/3dcoattextura)** — Texturing-focused 3DCoat build for hand-painted + PBR textures (up to 16K); full 3DCoat adds sculpt/retopo/UV. *Win/Mac/Linux · Textura subscription ~€9.85/mo; perpetual available · [docs](https://3dcoat.com/manual/).*
- **[ArmorPaint](https://armorpaint.org/)** — Open-source, GPU-accelerated PBR 3D texture painter with node-based layers/masks, real-time raytraced preview, baking (up to 16K). *Win/Mac/Linux (exp. iPad/Android) · source free (zlib); prebuilt binaries ~$19 · [docs](https://armorpaint.org/manual).* **★ Strong free/open pick (compile-from-source is free).**
- **[Blender](https://www.blender.org/)** — Free 3D suite whose Texture Paint mode paints maps on models, while the Shader Editor (Principled BSDF + procedural nodes) builds materials node-by-node; the bundled **Node Wrangler** add-on auto-loads/wires PBR sets. *Win/Mac/Linux · OSS (GPL) · [docs](https://docs.blender.org/manual/en/latest/sculpt_paint/texture_paint/index.html).* **★ Strong free/open pick.**
- **[Laigter](https://azagaya.itch.io/laigter)** — Open-source tool that auto-generates normal/specular/parallax/occlusion maps for 2D sprites with real-time lighting (also usable on textures). *Win/Mac/Linux · OSS (GPL-3.0).* **★** → full entry in [§3](#3-sprite--pixel-art-creation--editing-software).

### Image-to-material & map generators (normal / AO / height)
- **[Adobe Substance 3D Sampler](https://www.adobe.com/products/substance3d/apps/sampler.html)** — Turns photos/scans into tileable PBR materials via AI Image-to-Material (de-lights and derives base color, roughness, normal, height, metallic, AO); also multi-angle + photogrammetry capture. *Win/Mac · subscription · [docs](https://helpx.adobe.com/substance-3d-sampler/get-started.html).* (Its Firefly **Text-to-Texture** AI feature is covered in [§7](#7-ai-powered-sprite--texture-generation).)
- **[Substance B2M (Bitmap2Material)](https://helpx.adobe.com/substance-3d-b2m/get-started.html)** — Legacy single-image-to-material engine generating seamlessly tiling base color, normal, height, roughness, metallic, AO; now a legacy `.sbsar` filter in the Substance ecosystem. *Win/Mac (legacy).*
- **[Quixel Mixer](https://quixel.com/mixer)** — Layer-based texturing/material-mixing tool with photo-to-material and Megascans integration. *Win/Mac · discontinued (final free offline build 2023.1).*
- **[Materialize](https://www.boundingboxsoftware.com/materialize/)** — Free standalone tool converting a single image into a full PBR set (height, normal, AO, edge, metallic, smoothness) with real-time 3D preview; used on the Uncharted Collection. *Win · OSS (GPL v3) · [tutorials](https://www.boundingboxsoftware.com/materialize/tutorials.php).* **★ Strong free/open pick.**
- **[ArmorLab](https://armorlab.org/)** — Stand-alone **AI** texture-authoring app (sibling to ArmorPaint) generating PBR maps from a dropped photo or text prompt via a node editor + pre-trained net. *Win/Mac/Linux · source free (zlib); prebuilt binaries paid.* → see AI context in [§7](#7-ai-powered-sprite--texture-generation).
- **[AwesomeBump](https://github.com/kmkolasinski/AwesomeBump)** — Free, open-source GPU tool generating normal/height/specular/AO/metallic/roughness from a single image in real time; a CrazyBump alternative. *Win/Mac/Linux (Qt) · OSS (GPL) · [wiki](https://github.com/kmkolasinski/AwesomeBump/wiki).* **★ Strong free/open pick.**
- **[ShaderMap](https://shadermap.com/home/)** — Node-based map generator deriving normal/displacement/height/AO/curvature/color-ID from an image, and baking those from 3D geometry. *Win · free version + Pro ~$49 · [docs](https://shadermap.com/docs/).*
- **[CrazyBump](http://www.crazybump.com/)** — Classic desktop app for displacement/normal/specular/fake-occlusion maps from 2D images, with interactive controls. *Win/Mac · commercial (~$99–$299; trial).*
- **[NormalMap-Online](https://cpetry.github.io/NormalMap-Online/)** — Free, fully client-side (WebGL) browser tool converting a color image into normal/displacement/AO/specular maps with PNG/JPG export — no upload, no install. *Any browser · OSS · [source](https://github.com/cpetry/NormalMap-Online).* **★ Strong free/open pick (web).**
- **[DeepBump](https://hugotini.github.io/deepbump)** — Machine-learning (U-Net/MobileNetV2) generator inferring normal maps from a single photo, plus height/curvature from the normal map; Blender add-on + CLI. *Win/Mac/Linux · OSS (GPL-3.0) · [GitHub](https://github.com/HugoTini/DeepBump).* **★ Strong free/open pick.**
- **[xNormal](https://xnormal.net/)** — Long-standing free utility for baking normal/AO/height/curvature maps from high-poly meshes onto low-poly game models, plus image-based conversion. *Win · free.* **★ Strong free pick.**
- **[InsaneBump (GIMP plugin)](https://github.com/RobertBeckebans/gimp-plugin-insanebump)** — Open-source GIMP plug-in generating normal (and related) maps from a single image inside GIMP. *Win/Mac/Linux (via GIMP) · OSS (GPLv3).*
- **[Quixel Suite (legacy NDO/DDO)](https://support.quixel.se/hc/en-us/articles/207439035)** — Legacy Photoshop-based toolset: NDO (normal maps) + DDO (PBR texture sets) with 3DO viewer; unmaintained but legacy installers remain. *Win (legacy).*

**Free / open-source highlights:** Blender (paint + shader nodes + Node Wrangler), Material Maker (procedural), ArmorPaint (3D paint, free from source), Materialize & AwesomeBump (image-to-PBR), NormalMap-Online (zero-install web), DeepBump (AI maps), Laigter (2D sprite maps), and xNormal (free baking).

---

## 5. Sprite-Sheet / Atlas Packers & 2D Animation Tools

Tools that pack many sprites into atlases (and emit metadata), plus tools for authoring 2D animation (frame-based and skeletal/cutout).

### Atlas / sprite-sheet packers
- **[TexturePacker](https://www.codeandweb.com/texturepacker)** — Industry-standard sprite-sheet packer supporting 48+ engines out of the box, with trimming, rotation, polygon/mesh packing, and multipack. *GUI + CLI (Docker/CI) · JSON (hash/array), plist (Cocos2D/Cocos2d-x/Axmol), XML, libGDX, Sparrow, Phaser, Unity, Godot + custom exporters · free "Essential" tier; Pro $49.99 one-time; subscription CI license · [docs](https://www.codeandweb.com/texturepacker/documentation).*
- **[Free Texture Packer](https://free-tex-packer.com/)** — Free, open-source cross-platform packer (Win/Mac/Linux/Web) with trimming, rotation, multipack. *GUI + Web + CLI (`free-tex-packer-cli`, gulp/grunt/webpack plugins) · JSON, XML, CSS, Pixi.js, Godot, Phaser, Cocos2d · OSS (MIT) · [docs](https://github.com/odrick/free-tex-packer).*
- **[CodeAndWeb Free Sprite Sheet Packer](https://www.codeandweb.com/free-sprite-sheet-packer)** — Free browser drag-and-drop packer; a lightweight TexturePacker alternative (a.k.a. TexturePacker Online). *Web/GUI · JSON, Phaser, CSS, LESS · free · [docs](https://www.codeandweb.com/tp-online).*
- **[libGDX Texture Packer (gdx-tools)](https://libgdx.com/wiki/tools/texture-packer)** — Built-in libGDX packer that outputs page images + a `.atlas` descriptor; runnable class or standalone JAR. *Library / CLI · libGDX `.atlas` (compact + legacy) · OSS (Apache-2.0) · [docs](https://libgdx.com/wiki/tools/texture-packer).*
- **[GDX Texture Packer GUI](https://github.com/crashinvaders/gdx-texture-packer-gui)** — Visual wrapper over the libGDX packer with extra features and a headless batch mode. *GUI + headless · libGDX `.atlas` · OSS (Apache-2.0) · [docs](https://github.com/crashinvaders/gdx-texture-packer-gui/blob/master/CHANGES.md).*
- **[ShoeBox](https://renderhjs.net/shoebox/)** — Free Adobe AIR toolbox for packing images/SWF/GIF into atlases, plus sprite extraction, animation sheets, bitmap fonts. *GUI · PNG + coordinate text/XML · freeware (last ~2016) · [docs](https://renderhjs.net/shoebox/packSprites.htm).*
- **[Sprite Sheet Packer (amakaseev)](https://amakaseev.github.io/sprite-sheet-packer/)** — Qt-based open-source packer with GUI + CLI and multiple pixel formats. *GUI + CLI · JSON, Pixi.js, Cocos2d-x · OSS (MIT) · [docs](https://github.com/amakaseev/sprite-sheet-packer).*
- **[Leshy SpriteSheet Tool](https://www.leshylabs.com/apps/sstool/)** — Client-side HTML5 tool to pack/edit/auto-detect/convert sprite sheets; can emit ImageMagick rebuild scripts. *Web/GUI · JSON, XML, CSS, ImageMagick scripts · free · [docs](https://www.leshylabs.com/blog/posts/2013-12-03-Leshy_SpriteSheet_Tool.html).*
- **[spritesheet.js](https://github.com/krzysztof-o/spritesheet.js/)** — Node.js CLI texture-atlas generator (requires ImageMagick) with whitespace trimming. *CLI / npm (`spritesheet-js`) · JSON, Starling/Sparrow, Pixi.js, Easel.js, Cocos2d · OSS (MIT) · [docs](https://github.com/krzysztof-o/spritesheet.js/blob/master/README.md).*
- **[Cheetah Texture Packer](https://github.com/scriptum/Cheetah-Texture-Packer)** — Fast C++/Qt 2D bin-packer using MaxRects, with cropping/rotation/extrude/square options. *GUI · OSS (GPL) · [docs](https://github.com/scriptum/Cheetah-Texture-Packer/blob/master/README.md).*
- **[atlasc](https://github.com/septag/atlasc)** — Minimal dependency-free C tool/library building a PNG atlas with alpha trimming and mesh-sprite support. *CLI + C library · PNG + JSON · OSS (BSD-2-Clause) · [docs](https://github.com/septag/atlasc).*
- **[Unity Sprite Atlas](https://docs.unity3d.com/6000.3/Documentation/Manual/sprite/atlas/atlas-landing.html)** — Built-in Unity asset (Sprite Atlas V2, `.spriteatlasv2`) consolidating sprites/textures/folders into one atlas to cut draw calls. *Engine-integrated · bundled with Unity · [docs](https://docs.unity3d.com/6000.3/Documentation/Manual/sprite/atlas/create-sprite-atlas.html).*
- **[msdf-atlas-gen](https://github.com/Chlumsky/msdf-atlas-gen)** — Generator for compact multi-channel signed-distance-field **font** atlases from TTF/OTF, for crisp scalable text. *CLI + C++ library · PNG/image, JSON, CSV, Artery Font · OSS (MIT) · [docs](https://github.com/Chlumsky/msdf-atlas-gen/blob/master/README.md).*

### 2D animation (frame & skeletal)
- **[Spine](https://esotericsoftware.com/)** — Leading 2D skeletal animation editor with mesh deformation, IK, skins, and physics-based secondary motion; runtimes for nearly every engine/language. *JSON/binary skeleton data (+GIF/PNG/video export); runtimes for Unity, Unreal, libGDX, Godot, web… · Essential $69, Professional $379, Enterprise $2499+ · [docs](https://esotericsoftware.com/spine-in-depth).*
- **[DragonBones](https://dragonbones.github.io/en/)** — Free, open-source 2D skeletal/cutout animation suite with IK, constraints, skinning; imports layered PS files and Spine/Cocos data. *DragonBones JSON, Egret MovieClip, image sequences; HTML5/Unity/Cocos runtimes · OSS · [docs](https://dragonbones.github.io/en/animation.html).*
- **[Spriter Pro](https://brashmonkey.com/spriter-pro/)** — BrashMonkey's modular 2D character animation tool (bone-based cutout, swappable parts); Spriter 2 in development. *SCML/SCON (+PNG parts); community runtimes (Java, Lua, Phaser…) · $59 one-time · [docs](https://brashmonkey.com/spriter_manual/texturepacker%20support.htm).*
- **[Creature](https://www.kestrelmoon.com/creature/)** — Automated 2D mesh-deformation tool with cloth, soft-body, and procedural motion. *Custom JSON, sheets, image sequences, FBX, video; runtimes for Unity, UE4, Godot, WebGL (Pixi/Phaser/Three/Babylon/Cocos) · paid (trial) · [docs](https://www.kestrelmoon.com/creaturedocs/Game_Engine_Runtimes_And_Integration/Runtimes_Introduction.html).*
- **[Live2D Cubism](https://www.live2d.com/en/)** — Animates layered 2D illustrations into expressive moving models (mesh deform/morph), widely used for VTubers and games. *Cubism model formats, Cubism SDK runtimes · permanent **free** tier (small-scale commercial OK) + paid Pro; SDK revenue-tiered licensing · [docs](https://www.live2d.com/en/cubism/comparison/).*
- **[COA Tools](https://github.com/ndee85/coa_tools)** — Free Blender add-on bringing a Spine/Spriter-like 2D cutout rigging + IK workflow into Blender, with PS/GIMP exporters and a Godot importer. *OSS (GPL); maintained fork [coa_tools2](https://github.com/Aodaruma/coa_tools2) for Blender 3.4+ · [docs](https://github.com/ndee85/coa_tools/blob/master/README.md).*
- **[OpenToonz](https://opentoonz.github.io/e/)** — Full-featured open-source 2D animation software (Toonz, customized by Studio Ghibli) supporting hand-drawn, cutout, and effects. *Image sequences, video, raster formats · OSS (New BSD; commercial OK) · [source](https://github.com/opentoonz/opentoonz).*
- **[Synfig Studio](https://www.synfig.org/)** — Free, open-source vector-and-bitmap animation studio with automatic tweening, a bone system, and parameter linking. *PNG/BMP/OpenEXR sequences, GIF/MNG, AVI/Theora/MPEG · OSS (GPLv3) · [docs](https://wiki.synfig.org/Doc:Overview).*
- **[Pencil2D](https://www.pencil2d.org/)** — Lightweight, beginner-friendly hand-drawn animation tool with a clutter-free UI and raster/vector workflow. *Image sequences, GIF, video · OSS (GPL; commercial OK); Win/Mac/Linux/FreeBSD · [docs](https://www.pencil2d.org/doc/).*
- **[Krita (animation)](https://docs.krita.org/en/user_manual/animation.html)** — Frame-by-frame raster animation with onion skinning and frame tagging; sprite-sheet export via [plugin](https://github.com/Falano/kritaSpritesheetManager). *OSS (GPLv3).* → also a painting app; see [§3](#3-sprite--pixel-art-creation--editing-software).
- **[Aseprite](https://www.aseprite.org/)** — Frame-based pixel animation with onion skinning, frame tags, and PNG+JSON sheet/GIF export. *Paid (~$20).* → full entry in [§3](#3-sprite--pixel-art-creation--editing-software); [sheet-export docs](https://www.aseprite.org/docs/sprite-sheet/).
- **[Pyxel Edit](https://pyxeledit.com/)** — Pixel animation timeline + tileset tools; sheet/GIF and tilemap export. *Paid (~$9).* → full entry in [§3](#3-sprite--pixel-art-creation--editing-software).

---

## 6. Programmatic Image & Texture Processing (Libraries, CLIs, Compression)

For scripting asset pipelines: resize, convert, optimize, generate mips, and compress to GPU formats.

### General image libraries & CLIs
- **[ImageMagick](https://imagemagick.org/)** — Create/convert/resize/edit raster images via the `magick`/`convert` CLI and many language bindings. *C, CLI + bindings · ImageMagick License (Apache-2.0-like) · [docs](https://imagemagick.org/script/command-line-processing.php).*
- **[GraphicsMagick](http://www.graphicsmagick.org/)** — Fork of ImageMagick 5.5.2 focused on stability/performance for batch work; `gm` CLI + C/C++ APIs. *C/C++ · MIT/X11 · [docs](http://www.graphicsmagick.org/).*
- **[libvips](https://github.com/libvips/libvips)** — Fast, low-memory demand-driven image-processing library (used by sharp, imgproxy, MediaWiki). *C/C++ core + bindings · LGPL-2.1+ · [docs](https://www.libvips.org/).*
- **[sharp](https://github.com/lovell/sharp)** — High-performance Node.js module on libvips; resize/convert/composite JPEG/PNG/WebP/AVIF/TIFF (often 4–5× faster than ImageMagick). *Node.js · Apache-2.0 · [docs](https://sharp.pixelplumbing.com/).*
- **[Pillow (PIL fork)](https://github.com/python-pillow/Pillow)** — The de-facto Python imaging library; broad format support, resize/convert/draw/filter. *Python · MIT-CMU · [docs](https://pillow.readthedocs.io/).*
- **[scikit-image](https://github.com/scikit-image/scikit-image)** — Image-processing algorithms (filters, transforms, segmentation) for the SciPy stack. *Python · BSD-3-Clause · [docs](https://scikit-image.org/).*
- **[Wand](https://github.com/emcconville/wand)** — ctypes-based ImageMagick (MagickWand) binding for Python. *Python · MIT · [docs](https://docs.wand-py.org/).*
- **[OpenCV](https://github.com/opencv/opencv)** — Large computer-vision/image-processing library (2500+ algorithms) with image I/O, resize, color, codecs. *C++ + Python/Java · Apache-2.0 · [docs](https://docs.opencv.org/).*
- **[stb_image / stb_image_write](https://github.com/nothings/stb)** — Single-header C libraries to decode (PNG/JPEG/GIF…) and write (PNG/BMP/TGA/JPEG/HDR) images; trivial to embed. *C/C++ single-header · Public Domain / MIT · [source](https://github.com/nothings/stb/blob/master/stb_image.h).*
- **[SOIL2](https://github.com/SpartanJ/SOIL2)** — Tiny C library to upload textures to OpenGL; extends stb_image with DDS support + load helpers. *C · MIT/zlib-style · [docs](https://github.com/SpartanJ/SOIL2).*
- **[FreeImage](https://freeimage.sourceforge.io/)** — Cross-platform image-loading library with very wide format support (PNG/BMP/JPEG/TIFF/OpenEXR/HDR…). *C/C++ + bindings · dual GPLv2/v3 or FreeImage Public License · [docs](https://freeimage.sourceforge.io/documentation.html).*
- **[DevIL (OpenIL)](https://openil.sourceforge.net/)** — Full-featured cross-platform image library (read/write many formats + processing like scaling, histogram equalization). *C + C/.NET bindings · LGPL-2.1 · [docs](https://openil.sourceforge.net/docs.php).*
- **[GLI (OpenGL Image)](https://github.com/g-truc/gli)** — Header-only C++ library to load/save KTX and DDS, create GPU textures, sample texels, generate mipmaps. *C++11 header-only · MIT/Modified MIT · [docs](https://gli.g-truc.net/).*

### Image optimizers
- **[pngquant](https://github.com/kornelski/pngquant)** — Lossy PNG compressor (palette quantization) via libimagequant; big savings with alpha. *C/Rust, CLI + lib · GPLv3+ or commercial · [docs](https://pngquant.org/).*
- **[oxipng](https://github.com/oxipng/oxipng)** — Multithreaded lossless PNG optimizer (recompresses IDAT, strips metadata). *Rust, CLI + lib · MIT · [docs](https://github.com/oxipng/oxipng#readme).*
- **[zopflipng](https://github.com/google/zopfli)** — Lossless PNG optimizer using Zopfli deflate for maximum compression. *C/C++ · Apache-2.0 · [docs](https://github.com/google/zopfli#readme).*
- **[mozjpeg](https://github.com/mozilla/mozjpeg)** — Improved JPEG encoder (drop-in libjpeg-turbo fork) for higher quality at smaller sizes. *C, CLI + lib · BSD-3-Clause (IJG) · [docs](https://github.com/mozilla/mozjpeg#readme).*
- **[jpegoptim](https://github.com/tjko/jpegoptim)** — Optimize/compress JPEGs (lossless + optional target quality), strip metadata. *C, CLI · GPLv3 · [docs](https://github.com/tjko/jpegoptim#readme).*
- **[Squoosh + @squoosh/cli](https://github.com/GoogleChromeLabs/squoosh)** — Browser app + CLI to compress images locally with best-in-class codecs (MozJPEG, OxiPNG, WebP, AVIF); CLI auto-optimizes to a Butteraugli target. *Web / Node.js (WASM) · Apache-2.0 · [docs](https://github.com/GoogleChromeLabs/squoosh/blob/dev/cli/README.md).*

### GPU texture compression & transcoding
- **[Basis Universal](https://github.com/BinomialLLC/basis_universal)** — Supercompressed LDR/HDR GPU texture interchange (`.basis`/`.KTX2`) with a `basisu` CLI + transcoder that converts to virtually any GPU format (BCn, ETC, ASTC, PVRTC) at runtime. *C++ (+WASM/JS) · Apache-2.0 · [wiki](https://github.com/BinomialLLC/basis_universal/wiki).*
- **[Khronos KTX-Software](https://github.com/KhronosGroup/KTX-Software)** — Reference `libktx` + `ktx`/`toktx` CLIs to create KTX/KTX2, generate mipmaps, encode to Basis (ETC1S/UASTC), apply Zstd supercompression. *C/C++ (+JS/Java/Python) · Apache-2.0 (mixed) · [docs](https://github.khronos.org/KTX-Software/).*
- **[Microsoft DirectXTex / texconv](https://github.com/microsoft/DirectXTex)** — Texture library + `texconv`/`texassemble` CLIs to resize/convert/mip/block-compress (BC1–BC7) to DDS for D3D. *C++ · MIT · [wiki](https://github.com/microsoft/DirectXTex/wiki).*
- **[NVIDIA Texture Tools (nvtt)](https://github.com/castano/nvidia-texture-tools)** — Open-source texture processing/compression library + tools with D3D 10/11 format support. *C++ · MIT · [docs](https://github.com/castano/nvidia-texture-tools#readme).*
- **[NVIDIA Texture Tools Exporter](https://developer.nvidia.com/texture-tools-exporter)** — Free standalone app + Photoshop plugin + CLI with CUDA/GPU-accelerated compression to 130+ DXGI and ASTC formats (BC7, BC6H, ASTC). *Freeware (closed) · [docs](https://docs.nvidia.com/texture-tools/index.html).*
- **[AMD Compressonator](https://github.com/GPUOpen-Tools/compressonator)** — GUI + CLI + SDK for texture/3D-model compression and quality analysis; BC1–BC7/DXTC, ETC1/2, ASTC, ATC, ATI1N/2N. *C++ · MIT · [docs](https://compressonator.readthedocs.io/).*
- **[Arm astcenc](https://github.com/ARM-software/astc-encoder)** — Reference ASTC compressor/decompressor, all block sizes (0.89–8 bpp), LDR/HDR. *C++, CLI + lib · Apache-2.0 · [docs](https://github.com/ARM-software/astc-encoder/blob/main/Docs/README.md).*
- **[Imagination PVRTexTool](https://developer.imaginationtech.com/solutions/pvrtextool/)** — Library/CLI/GUI to encode/transcode textures; outputs PVR, KTX, KTX2, ASTC, DDS; targets PVRTC + core Vulkan/GLES/D3D formats. *Proprietary EULA (free) · [docs](https://docs.imgtec.com/tools-manuals/pvrtextool-manual/html/).*
- **[crunch / crnlib](https://github.com/BinomialLLC/crunch)** — Advanced DXTc compression library + tool producing the highly compressed `.crn` format (and DDS) that transcodes quickly to DXT1/5/N. *C++ · Public Domain · [docs](https://github.com/BinomialLLC/crunch#readme).*
- **[crunch (Unity fork)](https://github.com/Unity-Technologies/crunch)** — Unity's maintained fork: ~2.5× faster compression, ~10% better ratio; basis of Unity's Crunch support. *C++ · Public Domain/Zlib · [docs](https://github.com/Unity-Technologies/crunch/tree/unity).*
- **[ISPC Texture Compressor](https://github.com/GameTechDev/ISPCTextureCompressor)** — Fast SIMD (ISPC) compressor for BC1/3/4/5/6H/7, ASTC (LDR), ETC1 (archived 2024). *C++/ISPC · MIT · [docs](https://github.com/GameTechDev/ISPCTextureCompressor#readme).*
- **[Google etc2comp](https://github.com/google/etc2comp)** — Fast CLI/library ETC2 encoder built for encode-speed on asset-heavy builds. *C++ · Apache-2.0 · [docs](https://github.com/google/etc2comp#readme).*
- **[Ericsson ETCPACK](https://github.com/Ericsson/ETCPACK)** — Reference compressor/decompressor for ETC1, ETC2, EAC. *C++ · custom Ericsson license (free) · [docs](https://github.com/Ericsson/ETCPACK/blob/master/README.md).*
- **[etcpak](https://github.com/wolfpld/etcpak)** — Extremely fast ETC1/ETC2 and BC1/BC3/BC7 compressor (+decompressor). *C++ · BSD-3-Clause · [docs](https://github.com/wolfpld/etcpak#readme).*
- **[kram](https://github.com/alecazam/kram)** — Cross-platform wrapper to encode/decode/analyze KTX, KTX2, DDS with BC1/3/4/5/7, ASTC, ETC2 (LDR/HDR); CLI, macOS viewer, batch scripts. *C++11 · MIT · [docs](https://github.com/alecazam/kram#readme).*

### Texture formats — quick reference

| Format | Type | Typical use | Container |
|---|---|---|---|
| BC1 (DXT1) | Block (4 bpp, RGB/1-bit A) | PC/console opaque base color | DDS, KTX2 |
| BC3 (DXT5) | Block (8 bpp, RGBA) | PC/console color + smooth alpha | DDS, KTX2 |
| BC4 / BC5 | Block (1/2-channel) | Grayscale, normal maps (XY) | DDS, KTX2 |
| BC6H | Block (HDR RGB) | HDR/environment maps | DDS, KTX2 |
| BC7 | Block (8 bpp, high-quality RGBA) | High-quality PC/console RGBA | DDS, KTX2 |
| ETC1 | Block (4 bpp, RGB) | Legacy Android / OpenGL ES 2 | KTX, PKM, KTX2 |
| ETC2 / EAC | Block (RGB/RGBA + R/RG) | Android / OpenGL ES 3 standard | KTX, KTX2 |
| ASTC | Block (variable 0.89–8 bpp, 4×4–12×12) | Modern mobile/desktop, LDR/HDR | KTX, KTX2, ASTC, DDS |
| PVRTC | Block (2/4 bpp) | iOS / PowerVR GPUs | PVR, KTX, KTX2 |
| Basis Universal | Transcodable intermediate (ETC1S/UASTC) | Ship once, transcode to any GPU format | .basis, KTX2 |
| Crunch (.crn) | Compressed DXTn intermediate | Small distributables, transcode to DXTn | .crn (+ DDS) |
| DDS | Container | Direct3D textures, mips, cubemaps, arrays | — (holds BCn) |
| KTX / KTX2 | Container | Khronos GL/Vulkan textures; KTX2 adds Basis + Zstd supercompression | — (holds BCn/ETC/ASTC/Basis) |

---

## 7. AI-Powered Sprite & Texture Generation

Tools that generate game-ready 2D art, sprite sheets, seamless tiles, and PBR materials via generative AI. Split by primary output, plus the general models/local pipelines artists build on. **Commercial-use stances vary sharply — most hosted tools grant ownership only on *paid* tiers, while free tiers are often public/non-commercial.** Read the [licensing caveat](#-licensing-caveat) at the end.

### Sprite & pixel-art generators
- **[Scenario](https://www.scenario.com/)** — Train custom models on your own art style, then generate consistent 2D assets (characters, props, environments, UI), plus video/3D. *Hosted · free tier (50 credits, personal/eval only) + paid ~$20–200/mo; paid plans grant a full commercial license and output ownership · [pricing](https://www.scenario.com/pricing) · [FAQ](https://help.scenario.com/en/articles/frequently-asked-questions-faq/).*
- **[Layer.ai](https://www.layer.ai/)** — Production "AI OS" for studios: unified canvas over 149+ models with custom style training for sprites, concept sheets, UI, marketing art; image-to-sprite tooling. *Hosted (SOC 2 Type 2, private generation), Unity/Unreal/Adobe/Figma integrations · subscription/enterprise (verify tiers) · [sprite use case](https://www.layer.ai/use-cases/sprite-generation).*
- **[PixelLab](https://www.pixellab.ai/)** — Purpose-built pixel-art generator: animated characters, skeleton/text-driven animation, directional rotations, tilesets/maps, UI, with reference-based style consistency + inpainting. *Hosted (browser, Aseprite extension, API) · freemium (verify rates/license) · [docs](https://www.pixellab.ai/docs/ways-to-use-pixellab) · [API](https://www.pixellab.ai/pixellab-api).*
- **[Retro Diffusion](https://retrodiffusion.ai/)** — Pixel-art-specialized diffusion models (grid-aligned, multi-style) by Astropulse; trained on the creator's own + consenting artists' work. *Hosted web (pay-as-you-go, ~<$0.01/image, 50 free credits) + Aseprite extension ($65 full / $20 Lite, no subscription); you own + may use outputs commercially · also on [Replicate](https://replicate.com/retro-diffusion/rd-plus).*
- **[Rosebud AI / PixelVibe](https://lab.rosebud.ai/ai-game-assets)** — ~15 pre-trained models for production 2D assets: full-body sprites, portraits, items/icons, isometric tiles, 360° skyboxes; background removal, variations, bulk generation. *Hosted · free trial (~10/day) + Standard/Pro (verify ownership terms) · [overview](https://lab.rosebud.ai/blog/ai-game-assets-generator-pixelvibe).*
- **[Leonardo.ai](https://leonardo.ai/)** — General image model with strong game-asset workflows (sprites, tiles, UI, asset suites) and fine-tuned/community models. *Hosted · free tier (outputs public, Leonardo-owned, but royalty-free commercial license) + paid (private, you retain full ownership, no training) · [pricing](https://leonardo.ai/pricing) · [commercial usage](https://intercom.help/leonardo-ai/en/articles/8044018-commercial-usage).*
- **[Recraft](https://www.recraft.ai/)** — Generates true editable vector SVGs (+PNG/JPG/PDF/TIFF/Lottie) with style lock — great for crisp icons/UI/flat art rather than pixel-grid sprites. *Hosted · free plan (images public, Recraft-owned, limited commercial) · paid + API grant full commercial rights + ownership · [pricing](https://www.recraft.ai/pricing) · [ownership FAQ](https://www.recraft.ai/blog/ownership-and-commercial-use-faq).*
- **[OpenArt](https://openart.ai/)** — Multi-model platform with dedicated pixel-art/sprite/game-asset generators (e.g., Pixel Art XL); general-purpose, so sprites often need cleanup and lack native sheet export. *Hosted · generous free tier · commercial use with attribution/back-link (verify current terms) · [pixel-art generator](https://openart.ai/generator/pixel-art).*

### Texture & material generators
- **[Adobe Substance 3D Sampler](https://helpx.adobe.com/substance-3d-sampler/release-notes/version-4-4---substance-3d-sampler.html)** — Firefly-powered Text-to-Texture, Image-to-Texture, Text-to-Pattern produce square tileable images that convert into parametric PBR via Image-to-Material. *Desktop (Creative Cloud); AI features in beta, subscribers only · Firefly positioned as commercially safe (licensed/public-domain training) · [announcement](https://blog.adobe.com/en/publish/2024/03/18/adobe-announces-firefly-powered-features-substance-3d-apps).* (Base app in [§4](#4-texture--material-authoring-tools).)
- **[Poly (withpoly.com)](https://withpoly.com/)** — Browser tool generating customizable, seamlessly tileable PBR textures (Color, Normal, Height, AO, Roughness, Metalness) from text and/or image prompts, with AI upscaling to 8K/32-bit. *Hosted · free up to 2K but non-commercial; "Poly Infinity" ~$20/mo unlocks 8K/32-bit + commercial (verify availability).*
- **[Polycam AI Texture Generator](https://poly.cam/tools/material-generator)** — Text-to-PBR generating up to four seamlessly tileable material sets (albedo, displacement, normal, roughness) as ZIPs for Blender/Unreal/Unity/SketchUp; integrates with Polycam scans. *Hosted · unlimited for Polycam Pro · royalty-free, watermark-free, no attribution · [docs](https://learn.poly.cam/hc/en-us/articles/27426153753364).*
- **[Meshy.ai](https://www.meshy.ai/)** — Text/image-to-3D plus an AI texture generator producing PBR textures (and text-to-texture re-skinning) for 3D models. *Hosted · free tier (100 credits/mo, assets CC BY 4.0 — attribution) · paid from ~$20/mo grant private, owned assets + API · [commercial-use help](https://help.meshy.ai/en/articles/9992001).*
- **[NVIDIA Edify / Shutterstock 3D & materials](https://blogs.nvidia.com/blog/edify-3d-generative-ai-custom-fine-tuning/)** — Edify (trained exclusively on licensed Shutterstock content) powers text-to-3D with up-to-4K PBR plus standalone 4K PBR material sets and a 360 HDRi generator. *Hosted API via Shutterstock/Getty; enterprise + credit packs from ~$25 · marketed as "ethical"/licensed-data for commercial use · [Shutterstock generative 3D](https://www.shutterstock.com/discover/generative-ai-3d).*
- **[Dream Textures](https://github.com/carson-katri/dream-textures)** — Open-source Blender add-on embedding Stable Diffusion: text-to-texture with a Seamless option, inpaint-to-seamless, outpainting, projection onto meshes, node system, 4× upscaling. *Local/OSS (GPL), your GPU (~4GB+ VRAM) · free · output rights follow the SD model you load · also on [Superhive/Blender Market](https://superhivemarket.com/products/dream-textures).*
- **[StableMaterials](https://gvecchio.com/stablematerials/)** — Research diffusion model generating high-res tileable PBR maps (Basecolor, Roughness, Metallic, Height, Normal) from text/image (SDXL distillation; fast 4-step variant). *Local/OSS weights on [Hugging Face](https://huggingface.co/gvecchio/StableMaterials) · free · check repo license · [paper](https://arxiv.org/abs/2406.09293).*
- **[ArmorLab](https://armorlab.org/download)** — Open-source AI-assisted PBR texture authoring (Armory/ArmorPaint family) for generating/editing material maps. *Local/OSS (source free; prebuilt binaries paid to fund the project) · output is yours; verify model/data licensing for AI features · [GitHub](https://github.com/armory3d/armortools).* (Also in [§4](#4-texture--material-authoring-tools).)
- **ControlNet Tile + seamless/tiling LoRA workflows** — Not a product but a common pipeline: deterministic upscaler (Real-ESRGAN/Swin2SR) → SD/FLUX with the ControlNet **Tile** model (denoise ~0.3–0.45) to reconstruct detail, plus the Tiling setting + detail LoRAs to force seamless, repeatable textures. *Local/OSS (A1111/ComfyUI) · free · rights follow your base model · ref: [Stable Diffusion Art](https://stable-diffusion-art.com/controlnet-upscale/).*

### General image models & local pipelines
- **[Stable Diffusion (SDXL)](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0)** — Open-weights foundation model behind most local pipelines; tens of thousands of fine-tunes/LoRAs (incl. pixel-art and texture LoRAs on Civitai). *Local/OSS · free · CreativeML Open RAIL++-M permits commercial use of model + outputs (use-based restrictions) · [license](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/blob/main/LICENSE.md).*
- **[AUTOMATIC1111 WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)** — The most common local SD interface; has a **Tiling** toggle for seamless textures + the Seamless Tile Inpainting extension to convert any image into a perfect tile. *Local/OSS · free · rights follow your model · [tiling discussion](https://github.com/AUTOMATIC1111/stable-diffusion-webui/discussions/12091).*
- **[ComfyUI](https://github.com/comfyanonymous/ComfyUI)** — Node-based local SD/Flux UI ideal for repeatable texture pipelines; **ComfyUI-seamless-tiling** nodes replicate A1111 tiling for SD/SDXL. *Local/OSS · free · rights follow your model · [seamless-tiling nodes](https://github.com/spinagon/ComfyUI-seamless-tiling).*
- **[Flux.1 (Black Forest Labs)](https://bfl.ai/)** — High-quality open-weights image models popular for textures/concept art; FLUX.1 [schnell] is Apache-2.0 (fully commercial), while [dev] **weights** are non-commercial — *but generated outputs are explicitly not "derivatives" and may be used commercially.* *Local/OSS weights · [model license](https://bfl.ai/legal/non-commercial-license-terms) · [licensing/pricing](https://bfl.ai/licensing).*
- **[Midjourney](https://www.midjourney.com/)** — Hosted high-quality generator; game assets allowed on paid plans, and `--tile` creates seamless repeating textures/patterns. *Hosted · paid for commercial; subscribers own images, but businesses >$1M/yr need Pro/Mega · [commercial-use docs](https://docs.midjourney.com/hc/en-us/articles/27870375276557) · [Tile docs](https://docs.midjourney.com/hc/en-us/articles/32197978340109-Tile).*
- **[DALL·E 3 / OpenAI Images](https://openai.com/index/dall-e-3/)** — Hosted text-to-image (ChatGPT/API); good for concept art + reference textures (no native pixel-grid/seamless mode). *Hosted · OpenAI assigns output ownership to the user, commercial OK; Business/Team/API don't train on your content · content restrictions · [terms](https://openai.com/policies/row-terms-of-use/).*
- **[Adobe Firefly](https://www.adobe.com/products/firefly.html)** — Hosted generator (embedded across Creative Cloud) marketed as "commercially safe": trained on licensed Adobe Stock + public-domain/expired content. *Hosted · free + paid; non-beta outputs usable commercially, enterprise/Premium add IP indemnification · [FAQ](https://helpx.adobe.com/firefly/web/get-started/learn-the-basics/adobe-firefly-faq.html).*
- **Upscalers — [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) / [Upscayl](https://upscayl.org/) / [Topaz Gigapixel](https://www.topazlabs.com/topaz-gigapixel)** — Super-resolution to clean up/enlarge generated sprites/textures; ESRGAN variants power most free upscalers, Upscayl is a free OSS desktop GUI (local GPU), Topaz is the paid standard (up to 16×). *Mix of OSS (free) + paid · note: generic upscalers blur pixel art unless using pixel-aware/nearest settings.*

### ⚠️ Licensing caveat
Treat every "commercial-use OK" claim as **plan- and time-specific**, and re-read the live terms before shipping. Three distinct layers can each bite you:

1. **Tool/model license** — many hosted tools (Recraft, Leonardo, Midjourney, Meshy, Poly) grant ownership/commercial rights only on *paid* tiers while free outputs are public, vendor-owned, or NC/CC-BY; and open weights like FLUX.1 [dev] forbid *commercial use of the weights* even when outputs are permitted, whereas SDXL (OpenRAIL++) and FLUX.1 [schnell] (Apache-2.0) are broadly commercial.
2. **Training-data / IP-infringement risk** — models trained by scraping the web can reproduce copyrighted characters, logos, or trademarked styles; "commercially safe" offerings (Adobe Firefly, NVIDIA Edify/Shutterstock) and consent-trained pixel models (Retro Diffusion) reduce but don't eliminate this, and only some vendors (Adobe enterprise/Premium) offer IP indemnification.
3. **Copyrightability of the output** — under current U.S. guidance (e.g. the *Thaler v. Perlmutter* line), purely AI-generated images may not qualify for copyright protection, so even where you're licensed to *use* an asset, you may be unable to stop others from copying it.

For commercial game/asset work, prefer paid/private tiers, keep records of prompts and tool terms, lean on commercially-safe or consent-trained models for shippable art, and consult counsel for anything high-stakes.

---

## 8. Runtime Frameworks & Engines (Sprites & Textures in Code)

The libraries and engines used in code to load, batch, atlas, and render sprites and textures. The **Web/JS/TS** subsection is intentionally the richest (relevant to TypeScript projects); native engines follow.

### Web / JavaScript / TypeScript
- **[Pixi.js](https://pixijs.com/)** — WebGL/WebGPU 2D renderer. Core primitives are `Sprite` (a view) and `Texture`; load images + TexturePacker JSON atlases via the `Assets` API (`Assets.load()`), which builds a `Spritesheet` exposing `sheet.textures` and `sheet.animations`. Supports TexturePacker **multipack** and compressed textures (.dds/.ktx/.ktx2/.basis) by importing `pixi.js/ktx2`, `pixi.js/basis`, etc. before load. *[Spritesheet API](https://pixijs.download/dev/docs/assets.Spritesheet.html) · [Compressed Textures guide](https://pixijs.com/8.x/guides/components/assets/compressed-textures).*
- **[Phaser](https://phaser.io/)** — Mature 2D HTML5 framework (Canvas/WebGL). `Loader` distinguishes fixed-grid `load.spritesheet()` from packed `load.atlas()` / `load.unityAtlas()` (TexturePacker/Shoebox JSON Hash or Array). Native **Aseprite** support: `load.aseprite()` + `anims.createFromAseprite()`; `TextureManager` manages loaded textures. *[Textures concept docs](https://docs.phaser.io/phaser/concepts/textures) · [Aseprite loader](https://newdocs.phaser.io/docs/3.55.0/focus/Phaser.Loader.LoaderPlugin-spritesheet).*
- **[Three.js](https://threejs.org/)** — WebGL/WebGPU 3D library. `TextureLoader` for standard images; for GPU-compressed textures use `KTX2Loader` (KTX 2.0 / Basis Universal → ASTC/DXT/ETC2 after `detectSupport(renderer)`), `KTXLoader`, and `DDSLoader` (all subclasses of `CompressedTextureLoader`). The older `BasisTextureLoader` is superseded by `KTX2Loader`. *[KTX2Loader docs](https://threejs.org/docs/pages/KTX2Loader.html) (see also [DDSLoader](https://threejs.org/docs/pages/DDSLoader.html), [KTXLoader](https://threejs.org/docs/pages/KTXLoader.html)).*
- **[Babylon.js](https://www.babylonjs.com/)** — Full WebGL/WebGPU 3D engine (TS-first). `Texture` loads any image incl. `.ktx2` directly via the external KTX2 decoder. 2D sprites via `SpriteManager` (fixed-cell) and `SpritePackedManager` for variable-size **packed** sheets driven by TexturePacker JSON(Hash) (addressed by `cellIndex`/`cellRef`). *[Introduction To Sprites](https://doc.babylonjs.com/features/featuresDeepDive/sprites/sprites_introduction/) · [Sprite Packed Manager](https://doc.babylonjs.com/features/featuresDeepDive/sprites/packed_manager/) · [KTX2 textures](https://doc.babylonjs.com/features/featuresDeepDive/materials/using/ktx2Compression).*
- **[Konva.js](https://konvajs.org/)** — 2D Canvas scene-graph library (with React/Vue bindings). `Konva.Image` draws an image; `Konva.Sprite` plays sprite-sheet animations from an `animations` map of `[x, y, w, h]` frame arrays with `frameRate`/`frameIndex` (no built-in TexturePacker importer — you supply the frame map). *[Sprite API](https://konvajs.org/api/Konva.Sprite.html) · [Sprite tutorial](https://konvajs.org/docs/shapes/Sprite.html).*
- **[melonJS](https://melonjs.org/)** — Open-source 2D HTML5 engine. First-class **TexturePacker** support: load the atlas JSON + image, build a `TextureAtlas`, then `createAnimationFromName()`; trimming/rotation metadata honored. Single-texture atlasing cuts draw calls + VRAM. *[TextureAtlas / TexturePacker guide](https://github.com/melonjs/melonJS/wiki/How-to-use-Texture-Atlas-with-TexturePacker).*
- **[Excalibur.js](https://excaliburjs.com/)** — TypeScript-native 2D engine. Built-in `SpriteSheet` (from grid or sublists) + `ImageSource`; official **Aseprite** plugin (`@excaliburjs/plugin-aseprite`) imports `.aseprite`/JSON with tags, layers, opacity. *[Spritesheets docs](https://excaliburjs.com/docs/spritesheets/) · [Aseprite plugin](https://excaliburjs.com/docs/aseprite-plugin/).*
- **[Kontra.js](https://straker.github.io/kontra/)** — Tiny (~12 KB) JS/TS library for size-restricted (js13k) games. `SpriteSheet` slices a grid image and defines named animations via range notation (e.g. `'2..6'`) with `frameRate`; `Sprite` consumes the animations. *[SpriteSheet API](https://straker.github.io/kontra/api/spriteSheet) · [Sprite API](https://straker.github.io/kontra/api/sprite).*
- **[Cocos Creator](https://www.cocos.com/en/creator)** — Cross-platform 2D/3D engine with TS scripting (Web/native). `Sprite` + `SpriteFrame` (region over a `Texture2D`); **Auto Atlas** at build time + third-party `.plist`+`.png` `SpriteAtlas` (`atlas.getSpriteFrame(name)`). Compressed textures (ASTC/ETC/PVR) per-image. *[Atlas assets](https://docs.cocos.com/creator/3.8/manual/en/asset/atlas.html) · [SpriteFrame](https://docs.cocos.com/creator/3.8/manual/en/asset/sprite-frame.html) · [Compressed Textures](https://docs.cocos.com/creator/3.8/manual/en/asset/compress-texture.html).*
- **[PlayCanvas](https://playcanvas.com/)** — WebGL/WebGPU engine with editor + JS/TS API. 2D pipeline: `Texture` → **Texture Atlas** → `Sprite` asset (TexturePacker import). **Basis** supercompression in-editor transcodes to ASTC/DXT/ETC2/PVR at runtime (up to ~6× VRAM reduction). *[Sprite asset](https://developer.playcanvas.com/user-manual/assets/types/sprite/) · [Texture Atlas](https://developer.playcanvas.com/user-manual/editor/assets/inspectors/texture-atlas/) · [Texture Compression](https://developer.playcanvas.com/user-manual/optimization/texture-compression/).*
- **[CreateJS / EaselJS](https://createjs.com/easeljs)** — Classic HTML5 Canvas display-list library. `Bitmap` draws an image; `SpriteSheet` defines `images` + `frames` + named `animations`, played by `Sprite`. `SpriteSheetBuilder` rasterizes vector art into a runtime sheet. *[SpriteSheet API](https://createjs.com/docs/easeljs/classes/SpriteSheet.html) · [Sprite API](https://createjs.com/docs/easeljs/classes/Sprite.html).*
- **[p5.js + p5play](https://p5js.org/)** — Creative-coding library; `loadImage()` + `image()`. The companion **p5play** adds a `Sprite` class with image/animation support and image caching. *[p5.js loadImage](https://p5js.org/reference/p5/loadImage/) · [p5play Sprite](https://p5play.org/learn/sprite).*

### Native engines & frameworks
- **[Godot Engine](https://godotengine.org/)** — Open-source 2D/3D engine (GDScript/C#/C++). `Sprite2D` draws a `Texture2D`; `AtlasTexture` defines a sub-`region` of a larger atlas; imported images become `CompressedTexture2D` (`.ctex`, VRAM-compressed S3TC/ETC2/BPTC/ASTC), with `PortableCompressedTexture2D` for runtime-portable data. *[AtlasTexture](https://docs.godotengine.org/en/stable/classes/class_atlastexture.html) · [Sprite2D](https://docs.godotengine.org/en/stable/classes/class_sprite2d.html) · [CompressedTexture2D](https://docs.godotengine.org/en/stable/classes/class_compressedtexture2d.html).*
- **[Unity](https://unity.com/)** — Industry 2D/3D engine (C#). Images import as `Sprite`/`Texture2D`; the **Sprite Atlas** asset (`.spriteatlasv2`) consolidates many textures into one so all sprites draw in a single draw call. *[Packing sprites into atlases](https://docs.unity3d.com/6000.4/Documentation/Manual/sprite/atlas/atlas-landing.html) · [Sprite Atlas V2](https://docs.unity3d.com/2022.3/Documentation//Manual/SpriteAtlasV2.html).*
- **[Unreal Engine / Paper2D](https://www.unrealengine.com/)** — AAA engine (C++/Blueprints); **Paper2D** provides `PaperSprite` (region of a source texture/sheet) + `PaperFlipbook` (keyframe sprite animation at set FPS), with auto-flipbook creation from numerically-named sprites. *[Paper 2D Flipbooks](https://dev.epicgames.com/documentation/unreal-engine/paper-2d-flipbooks-in-unreal-engine) · [Paper 2D Sprites](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprites).*
- **[Bevy](https://bevyengine.org/)** — Data-driven ECS engine (Rust). 2D sprites use the `Sprite` component + a `TextureAtlas` (handle to a `TextureAtlasLayout` + section index); build layouts from a grid (`from_grid`) or pack at load time with `TextureAtlasBuilder`. *[TextureAtlas](https://docs.rs/bevy/latest/bevy/prelude/struct.TextureAtlas.html) · [TextureAtlasLayout](https://docs.rs/bevy/latest/bevy/image/struct.TextureAtlasLayout.html).*
- **[libGDX](https://libgdx.com/)** — Cross-platform Java framework. `SpriteBatch` batches `TextureRegion`/`Sprite` draws; the bundled `TexturePacker` packs into pages, and `TextureAtlas` reads `.atlas` to fetch `AtlasRegion`s by name, with index-suffixed filenames auto-grouped into animation frames. *[SpriteBatch, TextureRegions, and Sprites](https://libgdx.com/wiki/graphics/2d/spritebatch-textureregions-and-sprites) · [Texture packer](https://libgdx.com/wiki/tools/texture-packer).*
- **[MonoGame](https://monogame.net/)** — Open-source XNA-compatible framework (C#). Load images as `Texture2D` (Content Pipeline `Content.Load<Texture2D>` or `Texture2D.FromStream`) and render with `SpriteBatch`, incl. source-rectangle draws for sheet/atlas frames; `MonoGame.Extended` adds `Sprite`/`Texture2DRegion`/atlas helpers. *[Working with Textures](https://docs.monogame.net/articles/tutorials/building_2d_games/06_working_with_textures/index.html) · [Optimizing Texture Rendering (atlases)](https://docs.monogame.net/articles/tutorials/building_2d_games/07_optimizing_texture_rendering/index.html).*
- **[raylib](https://www.raylib.com/)** — Simple C library (many bindings). `LoadTexture()` → `Texture2D`; draw whole textures with `DrawTexture()`/`DrawTextureEx()` or sub-regions for sheets/atlases with `DrawTextureRec()`/`DrawTexturePro()`. *[raylib cheatsheet (textures)](https://www.raylib.com/cheatsheet/cheatsheet.html).*
- **[SDL3 + SDL_image](https://www.libsdl.org/)** — Low-level cross-platform multimedia layer (C). `IMG_LoadTexture()` loads PNG/JPG/etc. straight into a GPU `SDL_Texture`; render whole/partial with `SDL_RenderTexture(renderer, texture, srcrect, dstrect)`. Atlasing is manual via source rects. *[IMG_LoadTexture](https://wiki.libsdl.org/SDL3_image/IMG_LoadTexture) · [SDL_RenderTexture](https://wiki.libsdl.org/SDL3/SDL_RenderTexture).*
- **[LÖVE (Love2D)](https://love2d.org/)** — Lightweight 2D framework scripted in Lua. `love.graphics.newImage()` loads a texture; `newQuad(x,y,w,h,sw,sh)` selects a sheet/atlas frame; `newSpriteBatch()` batches many quads from one atlas into a single draw call. *[SpriteBatch](https://love2d.org/wiki/SpriteBatch) · [love.graphics.newQuad](https://love2d.org/wiki/love.graphics.newQuad).*
- **[Heaps.io](https://heaps.io/)** — High-performance Haxe 2D/3D engine (HL/JS/C++). 2D uses `h2d.Tile` (region of a `Texture`) + `h2d.Bitmap`; for many sprites use batched `h2d.SpriteBatch`/`h2d.TileGroup`, and load packed atlases from libGDX/TexturePacker via `hxd.res.Atlas`. *[h2d.Tile API](https://heaps.io/api/h2d/Tile.html) · [H2D documentation](https://heaps.io/documentation/h2d.html).*
- **[Defold](https://defold.com/)** — Lightweight cross-platform engine (Lua). A `Sprite` component sources from an **Atlas** (separate images auto-combined) or a **Tile Source** (uniform-grid sheet with inner-padding/extrude-border); animations come from the first atlas/tilesource on the sprite. *[Atlas manual](https://defold.com/manuals/atlas/) · [Tile source manual](https://defold.com/manuals/tilesource/) · [Sprite manual](https://defold.com/manuals/sprite/).*
- **[GameMaker](https://gamemaker.io/)** — Popular 2D engine (GML / visual). Imported sprites auto-pack onto power-of-two **Texture Pages** (up to 4096²), organized via **Texture Groups**; Dynamic Texture Groups defer loading to runtime via `texturegroup_*` to manage VRAM. *[Texture Groups](https://manual.gamemaker.io/monthly/en/Settings/Texture_Groups.htm) · [Texture Pages](https://manual.gamemaker.io/lts/en/Settings/Texture_Information/Texture_Pages.htm).*
- **[Construct 3](https://www.construct.net/)** — Browser-based, largely no-code 2D engine (with JS scripting). The `Sprite` plugin is an animatable image object; import frames from a strip via **Import Frames > From Strip**; the engine spritesheets project images at export. *[Sprite plugin reference](https://www.construct.net/en/make-games/manuals/construct-3/plugin-reference/sprite) · [Sprite script interface](https://www.construct.net/en/make-games/manuals/construct-3/scripting/scripting-reference/plugin-interfaces/sprite).*

> **For TypeScript/web projects specifically:** Pixi.js, Three.js, Babylon.js, and PlayCanvas have first-class KTX2/Basis/DDS compressed-texture support, while Pixi.js, Phaser, melonJS, and Excalibur.js have the strongest TexturePacker/Aseprite atlas pipelines.

---

## 9. Curated Lists, CC0 Hubs & Licensing Guide

Meta-resources that aggregate everything, plus a practical licensing primer so you use assets legally.

### Curated aggregator lists
- **[Calinou/awesome-gamedev](https://github.com/Calinou/awesome-gamedev)** — The canonical free-culture/free-software gamedev list (CC BY-SA 4.0). Dedicated **Graphics** subsections (Sprites, Icons, Collections, UI glyphs) + Graphics Tools — every asset link is free-licensed.
- **[skywind3000/awesome-gamedev](https://github.com/skywind3000/awesome-gamedev)** — Broad, popular gamedev list; aggregates engines, art/sprite packs, audio, tooling.
- **[FronkonGames/Awesome-Gamedev](https://github.com/FronkonGames/Awesome-Gamedev)** — Large curated collection spanning art, audio, engines, tutorials, asset sites.
- **[Siilwyn/awesome-pixel-art](https://github.com/Siilwyn/awesome-pixel-art)** — The go-to pixel-art list: tutorials, editors, palettes, artists, inspiration.
- **[madjin/awesome-cc0](https://github.com/madjin/awesome-cc0)** — "Awesome list of free-to-use public-domain CC0 assets," categorized into 3D models, PBR textures, sound, and game assets. Best single CC0 jump-off point (lightly maintained).
- **[johnjago/awesome-uncopyright](https://github.com/johnjago/awesome-uncopyright)** — Curated public-domain / CC0-equivalent works: 3D models, fonts, game assets, HDRs, images, music, SFX, books.
- **[shime/creative-commons-media](https://github.com/shime/creative-commons-media)** — Curated image/audio/video resources under Creative Commons or public domain (verify it loads before relying on it).
- **[ripienaar/free-for-dev](https://github.com/ripienaar/free-for-dev)** — Massive "free tier" catalog. Scoped to as-a-Service dev/infra (CDN, image hosting), **not** an art-asset hub — useful for adjacent tooling.
- **[ericjang/awesome-graphics](https://github.com/ericjang/awesome-graphics)** — Computer-graphics tutorials/resources (rendering, math, techniques) — learning, not ready-made assets.
- **[Kavex/GameDev-Resources](https://github.com/Kavex/GameDev-Resources)** — Long-running general gamedev list including royalty-free art, icons, 3D model sources.

### CC0 / public-domain hubs
- **[Kenney](https://kenney.nl/)** — Thousands of cohesive 2D sprites, low-poly 3D, UI, audio, fonts. **CC0.** (Detailed in [§1](#1-2d-sprite--game-art-asset-sources).)
- **[ambientCG](https://ambientcg.com/)** — 2,800+ PBR materials, HDRIs, scanned models. **CC0.** (Detailed in [§2](#2-pbr--3d-texture--material-libraries).)
- **[Poly Haven](https://polyhaven.com/)** — HDRIs, PBR textures, 3D models, all original/donated. **CC0** ([license](https://polyhaven.com/license)). (Detailed in [§2](#2-pbr--3d-texture--material-libraries).)
- **[OpenGameArt (CC0 filter)](https://opengameart.org/)** — Community archive; filter the [CC0 collection](https://opengameart.org/content/cc0-resources). **Per-asset / multi-license** — always check each submission.
- **[Public Domain Vectors](https://publicdomainvectors.org/)** — Copyright-waived vector clip art (SVG/EPS/AI). Effectively **public domain / CC0**, commercial OK.
- **[Sketchfab (CC filter)](https://sketchfab.com/features/free-3d-models)** — 700k+ downloadable models. **Various Creative Commons** (mostly CC-BY; ~2k+ CC0) — check and credit per model.
- **[Wikimedia Commons](https://commons.wikimedia.org/)** — 140M+ media files. **Free CC (CC-BY / CC-BY-SA) or public domain only** (no -NC/-ND) — verify each file's tag and attribute.
- **[Unsplash](https://unsplash.com/license)** / **[Pexels](https://www.pexels.com/license/)** — Photos for reference & textures. Custom **free license** (commercial OK, no attribution required; don't resell unaltered copies or imply endorsement — watch trademarks/people).
- **[Reiner's Tilesets](https://www.reinerstilesets.de/)** — Classic free 2D/3D sprites, tiles, textures, meshes. **Freeware, commercial OK with credit** ([license](https://www.reinerstilesets.de/graphics/lizenz/)).

### Asset licensing — practical primer

**Creative Commons family.** Every CC license except CC0 requires **attribution (BY)**. Optional modules: **NC** (NonCommercial — no commercial use), **SA** (ShareAlike — derivatives must carry the same/compatible license), **ND** (NoDerivatives — no modified versions may be shared). CC0 is a public-domain **dedication**, not a license.

| License | Attribution? | Commercial OK? | ShareAlike? | Derivatives? |
|---|---|---|---|---|
| [CC0](https://creativecommons.org/publicdomain/zero/1.0/) | No | Yes | No | Yes (any use) |
| [CC BY](https://creativecommons.org/licenses/by/4.0/) | Yes | Yes | No | Yes |
| [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/) | Yes | Yes | **Yes** | Yes |
| [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/) | Yes | **No** | No | Yes |
| [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/) | Yes | Yes | n/a | **No** |
| [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) | Yes | **No** | **Yes** | Yes |
| [CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/) | Yes | **No** | n/a | **No** |

(Full list: [creativecommons.org/share-your-work/cclicenses](https://creativecommons.org/share-your-work/cclicenses/).) For commercial games, **avoid any -NC license** and treat -ND assets as "use as-is, no edits."

**Public domain vs royalty-free vs "free."**
- *Public domain / CC0* — no copyright restrictions; use for anything, forever, no payment, no attribution. The purest free.
- *Royalty-free (RF)* — usually pay **once**, then reuse without per-use royalties, **but still licensed and rule-bound** (NOT public domain). Most paid marketplace assets are RF.
- *"Free" / "copyright-free"* — ambiguous marketing. "Free" can mean zero-cost-but-restricted (attribution required, or NC). Always read the actual license — free-to-download ≠ free-to-use-commercially.

**Game-engine / marketplace EULAs — what "buying" grants.** You buy a **license to use**, not ownership.
- **[Unity Asset Store EULA](https://unity.com/legal/as-terms)** — Standard assets grant **Single-Entity** use (one company/individual; unlimited machines you own); **Multi-Entity** extends to affiliates/contractors. "Editor Extension/Scripting/Services" assets are **per-seat**. Commercial use permitted. ([tiers explained](https://support.unity.com/hc/en-us/articles/208601846))
- **[Epic Fab](https://www.fab.com/eula)** — Free assets may carry **Creative Commons**; paid/free assets use the **Fab Standard License** (Personal and Professional tiers grant the **same usage rights**; tiers differ by buyer revenue, not scope). ([licenses & pricing](https://dev.epicgames.com/documentation/en-us/fab/licenses-and-pricing-in-fab))
- **[Envato Elements](https://elements.envato.com/license-terms)** — Subscription with **unlimited downloads**; each download is licensed **per single project** (register a new license to reuse elsewhere). Items used during the subscription stay covered after it lapses. Envato Market sells per-use Regular/Extended licenses instead.

**OpenGameArt's multi-license model.** Many OGA submissions list **several licenses at once** (e.g. CC-BY 3.0 + CC-BY-SA 3.0 + GPL). You may pick **any one** and use the whole submission under just those terms — it does **not** mean different files carry different licenses. Licenses are set per-submission (bundles can mix authors), so **check the license on every asset** and keep attribution/author info; CC0 items can be relicensed freely, BY/SA items cannot.

### Commercial-use checklist
- **Confirm commercial use is allowed** — reject any **-NC** asset for revenue projects; treat **-ND** as no-edits.
- **Keep attribution.** For any **BY/SA** asset, store the required credit string (author, title, source URL, license name + link) and surface it in-game/credits; CC0 needs none but crediting is courteous.
- **Save the license file/page** alongside each asset (copy the license text + download date) to prove provenance later.
- **Honor ShareAlike (SA):** if you modify and distribute an SA asset, license your derivative under the same/compatible license.
- **Verify the uploader actually owns it.** Watch for **ripped/copyrighted** content (game rips, brand logos, recognizable people) re-uploaded to "free" sites — re-upload doesn't make it legal.
- **Read marketplace EULAs** for seat/entity limits (Unity Single vs Multi-Entity; Envato per-project) and don't redistribute raw source files.
- **Check AI-generated asset terms** — confirm the tool's output license/commercial grant and any IP indemnity before shipping (see [§7](#7-ai-powered-sprite--texture-generation)).
- **When in doubt, prefer CC0 hubs** (Kenney, Poly Haven, ambientCG) — the lowest-risk path for commercial use.

---

## 10. 3D Models & Meshes

Ready-made 3D assets, the interchange formats that move them between tools, and the open-source pipeline that converts, validates, and optimizes them. (Texturing tools and texture libraries are in [§2](#2-pbr--3d-texture--material-libraries) and [§4](#4-texture--material-authoring-tools).)

### CC0 / free model sources
- **[Poly Haven](https://polyhaven.com/models)** — Community-funded scanned/modeled assets as Blender, FBX, glTF, and USD with up to 8K textures; no login or paywall. *CC0 · models/HDRIs/textures · [license](https://polyhaven.com/license).*
- **[Quaternius](https://quaternius.com/)** — Thousands of stylized low-poly packs (characters, nature, vehicles) + a Universal Animation Library; FBX/OBJ/glTF. *CC0 · game-ready packs · also on [itch.io](https://quaternius.itch.io/).*
- **[Kenney](https://kenney.nl/assets/category:3D)** — 40k+ assets incl. modular 3D kits (city, platformer, nature, prototyping); excellent placeholders. *CC0 · 3D kits/sprites/audio · commercial OK.*
- **[Poly Pizza](https://poly.pizza/)** — Independent successor to the defunct Google Poly (shut June 30 2021); thousands of hand-picked low-poly models + a free real-time API. *Mix of CC0 and CC-BY (filterable) · low-poly · [press](https://poly.pizza/docs/press).*
- **[Sketchfab — Free models](https://sketchfab.com/features/free-3d-models)** — 1M+ downloadable Creative Commons models (incl. 2,000+ CC0); most are CC-BY (attribution), not CC0. *CC-BY / CC0 (per-model) · all categories · [CC guide](https://sketchfab.com/blogs/community/an-introduction-to-creative-commons-licenses/).*
- **[BlenderKit](https://www.blenderkit.com/)** — 130k+ assets browsable from inside Blender via the official add-on; ~47% free (17k+ models). *CC0 & RF (free tier) · models/materials/HDRIs · [licenses](https://www.blenderkit.com/docs/licenses/).*
- **[Free3D](https://free3d.com/)** — 15k+ user-uploaded free models (plus premium) in .blend/.obj/.c4d/.3ds/.max/.ma. *Per-model Personal Use / RF (read each listing) · free + paid.*
- **[Clara.io Library](https://clara.io/library)** — 100k+ free models in OBJ/Blend/STL/FBX/DAE/Three.js (cloud editor shut Dec 31 2022; library remains). *Per-model flexible licenses · legacy service.*

### Marketplaces & rigged-character sources
- **[Fab](https://www.fab.com/)** — Epic's unified marketplace (successor to Unreal Marketplace + Sketchfab Store) and the new home of **Quixel Megascans**. Free assets rotate weekly; Megascans became paid in 2025 (from $0.99). *Fab Standard License (engine-agnostic) · free + paid · [purchasing docs](https://dev.epicgames.com/documentation/en-us/fab/purchasing-and-downloading-assets-in-fab).*
- **[Adobe Mixamo](https://www.mixamo.com/)** — Free auto-rigger + huge mocap animation library; upload a humanoid mesh and get rigged animations in-browser (bipedal humanoids only). *RF for any project · rigged characters + mocap · [FAQ](https://helpx.adobe.com/creative-cloud/faq/mixamo-faq.html).*
- **[Ready Player Me](https://readyplayer.me/)** — Cross-app avatar system built on glTF/GLB; every avatar is a unique GLB URL with optional Draco/meshopt compression. *Proprietary platform terms · GLB avatars · [docs](https://docs.readyplayer.me/).*
- **[TurboSquid](https://www.turbosquid.com/)** — Long-running premium marketplace for film/games/AR-VR/product viz. *RF EULA (no ongoing royalties) · free + paid, all formats.*
- **[CGTrader](https://www.cgtrader.com/)** — 2M+ models with flexible RF/Editorial licensing and 150k+ free models. *RF/Editorial (per listing) · free + paid · [free models](https://www.cgtrader.com/free-3d-models).*

### Research / cultural open datasets
- **[Objaverse / Objaverse-XL](https://objaverse.allenai.org/)** — AI2's research corpus of 10M+ 3D objects (XL ~100× larger than prior datasets) for generative-3D / reconstruction training. *Dataset ODC-By v1.0; objects keep own licenses · ML research · [repo](https://github.com/allenai/objaverse-xl).*
- **[Smithsonian Open Access 3D](https://3d.si.edu/cc0)** — 2,000+ scanned museum objects (OBJ, glTF); part of the 5.1M-item Open Access release. *CC0 (items marked CC0) · cultural-heritage scans · [Open Access](https://www.si.edu/openaccess).*
- **[NASA 3D Resources](https://science.nasa.gov/3d-resources/)** — Spacecraft, rovers, satellites, and textures from NASA missions. *Free / no copyright (see NASA media guidelines) · [GitHub](https://github.com/nasa/NASA-3D-Resources).*
- **[Thingiverse](https://www.thingiverse.com/)** — 4M+ community designs, primarily STL, print-oriented (acquired by MyMiniFactory 2026; existing free models stay free). *Mostly Creative Commons (many NC) · print STL.*
- **[Printables](https://www.printables.com/)** — Prusa Research's clean print-model repository with high-quality free STL/3MF. *Creative Commons (per listing) · print-oriented · free.*

### 3D interchange formats — quick reference

| Format | Ext | Strengths | Typical use |
|---|---|---|---|
| **glTF / GLB** | `.gltf` / `.glb` | Open Khronos standard, compact, PBR + skinning + animation; the "JPEG of 3D" | Runtime delivery: web/WebGL, AR/VR, engines |
| **FBX** | `.fbx` | Rich: meshes, skeletal anim, blendshapes, cameras, lights; ubiquitous | DCC ↔ engine transfer; proprietary (Autodesk) |
| **OBJ + MTL** | `.obj` / `.mtl` | Dead-simple, human-readable, universal | Static single meshes; no animation/rig |
| **USD / USDZ** | `.usd` / `.usdz` | Composable scene graph, layering, huge-scene scale; USDZ = AR-ready zip | Film/VFX (Pixar), Apple AR, e-commerce |
| **COLLADA** | `.dae` | XML interchange (Khronos); geometry, materials, animation | Legacy DCC interchange; SketchUp |
| **STL** | `.stl` | Surface triangles only — no color/material | 3D printing, CAD prototyping |
| **PLY** | `.ply` | Vertices + faces + per-vertex color/attributes | 3D scans, point clouds, photogrammetry |
| **Alembic** | `.abc` | Baked per-frame geometry cache (deformation without the rig) | VFX/animation interchange |
| **VRM** | `.vrm` | glTF 2.0 ext with a standardized humanoid rig + expressions | VTubing, VR/metaverse avatars |

### Model pipeline tools (convert, validate, optimize, compress)
- **[Blender](https://www.blender.org/)** — Free import/export hub: reads/writes glTF, FBX, OBJ, USD, DAE, STL, PLY, Alembic — doubles as a universal converter and cleanup tool. *OSS (GPL) · [glTF I/O manual](https://docs.blender.org/manual/en/latest/addons/import_export/scene_gltf2.html).*
- **[glTF-Transform](https://gltf-transform.dev/)** — The go-to glTF 2.0 SDK + CLI for JS/TS: prune, dedup, weld, resample animations, resize/compress textures (KTX2/WebP), apply Draco/meshopt. *OSS (MIT) · [repo](https://github.com/donmccurdy/glTF-Transform).*
- **[meshoptimizer + gltfpack](https://meshoptimizer.org/)** — zeux's mesh-optimization library; `gltfpack` shrinks glTF via meshopt vertex/index compression (a Draco alternative), LOD simplification, and KTX2/WebP texture compression. *OSS (MIT) · [gltfpack docs](https://meshoptimizer.org/gltf/).*
- **[Draco](https://github.com/google/draco)** — Google's mesh/point-cloud geometry compression, standardized in glTF as `KHR_draco_mesh_compression`; supported in three.js/Babylon/Cesium. *OSS (Apache-2.0) · [project](https://google.github.io/draco/).*
- **[assimp (Open Asset Import Library)](https://github.com/assimp/assimp)** — C/C++ library loading 50+ formats into one clean data structure, with export + post-processing (triangulate, gen normals/tangents). Bindings for C#, Python, Java. *OSS (BSD-3-Clause) · [site](https://www.assimp.org/).*
- **[FBX2glTF](https://github.com/facebookincubator/FBX2glTF)** — Meta's CLI FBX→glTF converter (also on npm); optional Draco compression (Godot maintains an active [fork](https://github.com/godotengine/FBX2glTF)). *OSS (BSD-3-Clause).*
- **[Khronos glTF Validator](https://github.khronos.org/glTF-Validator/)** — Drag-and-drop browser tool (validates locally, nothing uploaded) + `gltf-validator` npm package; checks assets against the glTF 2.0 spec. *OSS (Apache-2.0) · [repo](https://github.com/KhronosGroup/glTF-Validator).*

> **Licensing caveat:** "Free" on Sketchfab, Free3D, CGTrader, and the print sites is per-listing — many models are CC-BY (attribution) or non-commercial, so check each download. Only Poly Haven, Quaternius, Kenney, and CC0-flagged Smithsonian items are blanket public-domain. Quixel Megascans on Fab is no longer free (since 2025). Clara.io's editor and Google Poly are defunct (Poly Pizza is the live successor). See [§9](#9-curated-lists-cc0-hubs--licensing-guide).

---

## 11. Fonts, Bitmap Fonts & Icon Systems

Pixel/game fonts, the tools that turn fonts into sprite-sheet "bitmap fonts" and SDF/MSDF atlases for crisp real-time text, and icon libraries for game UI. (Bitmap fonts are literally sprite sheets; icons are core UI sprites.) The MSDF atlas generators here pair with [§5](#5-sprite-sheet--atlas-packers--2d-animation-tools).

> **SIL Open Font License (OFL):** lets you use, embed, modify, and redistribute fonts freely — including in commercial products and games — but you may not sell the font *by itself*, and any "Reserved Font Name" can't be used by your modified versions without permission.

### Font sources (incl. pixel/game fonts)
- **[Google Fonts](https://fonts.google.com/)** — ~1,900+ open-licensed font families (web + downloadable TTF/variable fonts), incl. many pixel/game faces. *Mostly SIL OFL, some Apache 2.0 · free · [GitHub](https://github.com/google/fonts) · [docs](https://developers.google.com/fonts/faq).*
- **[DaFont — Bitmap/Pixel](https://www.dafont.com/bitmap.php)** — Large browsable catalog of bitmap/pixel/screen fonts for retro/8-bit looks. *Per-font licenses (100% Free, Public Domain, GPL, OFL — check each) · mostly free · TTF.*
- **[1001 Fonts — Pixel fonts](https://www.1001fonts.com/pixel-fonts.html)** — 500+ pixel fonts with clear per-font license badges; a [free-for-commercial filter](https://www.1001fonts.com/free-for-commercial-use-fonts.html) is available. *Per-font (many free-for-commercial / Public Domain) · TTF/OTF.*
- **[FontStruct](https://fontstruct.com/)** — Free browser grid/tile editor to build bitmap-style fonts from blocks; exports ready-to-use TrueType. *Per-creator license (often CC) · free (ad-supported) · TTF.*
- **[Lospec — pixel-font tutorials](https://lospec.com/pixel-art-tutorials/tags/fonts)** — Pixel-art hub with tutorials on making pixel fonts (rather than a hosted font list). *Free · tutorials/tools.*
- **[itch.io — pixel-font assets](https://itch.io/game-assets/tag-pixel-font)** — Hundreds of indie pixel/bitmap fonts (monogram, Public Pixel, GB Studio packs); [free filter](https://itch.io/game-assets/free/tag-pixel-font). *Per-asset license · free & paid · TTF/PNG/bitmap.*
- **[Press Start 2P](https://fonts.google.com/specimen/Press+Start+2P)** — Classic 8px arcade bitmap font (by CodeMan38) based on 1980s Namco games. *SIL OFL · free · best at multiples of 8px.*
- **[Pixel Operator](https://www.dafont.com/pixel-operator.font)** — Versatile libre pixel family (proportional + mono, many weights/sizes) by Jayvee Enaguas. *CC0 · free · TTF · [source](https://notabug.org/HarvettFox96/ttf-pixeloperator).*
- **[m5x7](https://managore.itch.io/m5x7)** — Popular thin 5×7 pixel font by Daniel Linssen (accents/symbols); best at multiples of 16px. *Free to use (attribution appreciated) · TTF.*
- **[m3x6](https://managore.itch.io/m3x6)** — Tiny 3×6 companion pixel font by Daniel Linssen for ultra-compact UI/dialogue. *Free to use (attribution appreciated) · TTF.*
- **[Kenney Fonts](https://kenney.nl/assets/kenney-fonts)** — Pixel/game font pack from the CC0 game-asset maker Kenney. *CC0 · free · TTF.*

### Bitmap-font & SDF/MSDF generation tools
- **[AngelCode BMFont](https://www.angelcode.com/products/bmfont/)** — The original Windows bitmap-font generator; rasterizes TTF/OTF to sprite-sheet pages + a `.fnt` descriptor; Unicode, 8/32-bit output (TGA/PNG/DDS), and SDF export. *Freeware · Windows · defines the de-facto BMFont format · [docs](https://www.angelcode.com/products/bmfont/documentation.html).*
- **[Hiero](https://libgdx.com/wiki/tools/hiero)** — libGDX's cross-platform bitmap-font packer; rasterizes TTFs with shadow/outline/glow effects and exports the AngelCode `.fnt` format. *OSS (Apache 2.0) · JVM.*
- **[fontbm](https://github.com/vladimirgamalyan/fontbm)** — BMFont-compatible, cross-platform command-line generator built on FreeType2; great for build pipelines/CI. *OSS (MIT) · outputs `.fnt` + PNG.*
- **[msdf-bmfont-xml](https://github.com/soimy/msdf-bmfont-xml)** — Node CLI converting TTF to multi-channel SDFs + AngelCode `.fnt` (XML/txt/JSON) via msdfgen. *OSS (MIT) · [npm](https://www.npmjs.com/package/msdf-bmfont-xml) · [web tool](https://github.com/donmccurdy/msdf-bmfont-web).*
- **[msdfgen](https://github.com/Chlumsky/msdfgen)** — Viktor Chlumský's foundational multi-channel SDF generator (library/CLI) that preserves sharp corners for scalable real-time text. *OSS (MIT) · C++.*
- **[msdf-atlas-gen](https://github.com/Chlumsky/msdf-atlas-gen)** — Builds compact MSDF font atlases from TTF/OTF subsets + layout metadata (Artery Font/CSV/JSON). *OSS (MIT) · CLI.* (Also in [§5](#5-sprite-sheet--atlas-packers--2d-animation-tools).)
- **[Glyph Designer](https://www.71squared.com/glyphdesigner)** — Polished commercial bitmap-font editor with rich effects, custom glyph images, and 15+ export presets; macOS + a [Windows GDX edition](https://www.71squared.com/gdx). *Paid · AngelCode-compatible output.*
- **[ShoeBox — bitmap-font mode](https://renderhjs.net/shoebox/bitmapFont.htm)** — Free Adobe AIR toolbox producing AngelCode `.fnt` with Photoshop styling (also a sprite packer — see [§5](#5-sprite-sheet--atlas-packers--2d-animation-tools)). *Freeware · cross-platform.*
- **[Littera](https://kvazars.com/littera/)** — Web-based bitmap-font generator (AngelCode format) with glow/shadow/outline + distance-field. *Free · web · note: built in Flash/AS3, so it may not run in modern browsers.*
- **[SnowB Bitmap Font](https://snowb.org/)** — Modern free in-browser generator (TTF/OTF/WOFF → bitmap) with gradients/effects; exports Text/XML/Binary/JSON/C-header and MSDF-atlas JSON (SDF/PSDF/MSDF/MTSDF via msdfgen WASM). *Free, runs locally · [docs](https://snowb.org/en/docs/) · [source](https://github.com/SilenceLeo/snowb-bmf).*

### Icon libraries & systems
- **[game-icons.net](https://game-icons.net/)** — 4,000+ monochrome SVG/PNG icons purpose-built for games/RPGs (weapons, spells, creatures, dungeon, cards); recolorable in-browser. *CC-BY 3.0 (attribution) · free · [about/license](https://game-icons.net/about.html).* (Also in [§1](#1-2d-sprite--game-art-asset-sources).)
- **[Iconify](https://iconify.design/)** — Universal icon framework + aggregator unifying 200+ open sets (~300k icons) behind one API with React/Vue/Svelte/web components. *MIT framework (sets keep own licenses) · [search](https://icon-sets.iconify.design/) · [docs](https://iconify.design/docs/icons/).*
- **[Font Awesome](https://fontawesome.com/)** — The iconic SVG/font/CSS toolkit; Free tier has 2,000+ icons (Pro is paid). *Free: CC-BY 4.0 (SVG), SIL OFL (fonts), MIT (code) · [GitHub](https://github.com/FortAwesome/Font-Awesome).*
- **[Material Symbols / Icons](https://fonts.google.com/icons)** — Google's huge UI icon system; Symbols ship as variable fonts (fill/weight/grade/optical-size) + SVGs. *Apache 2.0 · [guide](https://developers.google.com/fonts/docs/material_symbols) · [GitHub](https://github.com/google/material-design-icons).*
- **[Lucide](https://lucide.dev/)** — Community-maintained 1,600+ stroke-based icons (a modern Feather fork) with React/Vue/Svelte packages. *ISC · [GitHub](https://github.com/lucide-icons/lucide).*
- **[Tabler Icons](https://tabler.io/icons)** — 6,000+ consistent 24×24 / 2px-stroke icons; SVG, icon font, and framework packages. *MIT (no attribution) · [GitHub](https://github.com/tabler/tabler-icons).*
- **[Feather](https://feathericons.com/)** — Minimal 280+ icons on a 24×24 grid by Cole Bemis (the original behind Lucide). *MIT · [GitHub](https://github.com/feathericons/feather).*
- **[Phosphor Icons](https://phosphoricons.com/)** — Flexible 1,200+ family in six weights (thin→fill + duotone) with many framework packages. *MIT · [GitHub](https://github.com/phosphor-icons).*
- **[Heroicons](https://heroicons.com/)** — Hand-crafted icons by the Tailwind CSS team (outline/solid/mini) with React/Vue libs. *MIT · [GitHub](https://github.com/tailwindlabs/heroicons).*
- **[Boxicons](https://boxicons.com/)** — 3,000+ web-friendly icons in regular/solid/logo styles. *CC-BY 4.0 · SVG/PNG/web font.*
- **[Remix Icon](https://remixicon.com/)** — 3,200+ neutral system symbols (outlined + filled) on a 24×24 grid. *Apache 2.0 · SVG/font · [GitHub](https://github.com/Remix-Design/RemixIcon).*
- **[The Noun Project](https://thenounproject.com/)** — Massive crowd-sourced icon marketplace; free under CC-BY (attribution) or royalty-free via paid plan. *CC-BY or RF (paid) · [license info](https://help.thenounproject.com/hc/en-us/articles/200509798).*

### Open emoji sets
- **[Twemoji](https://github.com/jdecked/twemoji)** — Twitter's open emoji set, community-maintained (jdecked fork); flat colorful SVG/PNG, full Unicode. *Graphics CC-BY 4.0, code MIT · [demo](https://jdecked.github.io/twemoji/).*
- **[OpenMoji](https://openmoji.org/)** — 4,000+ community-designed emoji in one style, with colored + outlined variants and skin tones. *Graphics CC-BY-SA 4.0, code LGPL-3.0 · [GitHub](https://github.com/hfg-gmuend/openmoji).*
- **[Noto Emoji](https://github.com/googlefonts/noto-emoji)** — Google's Noto emoji fonts (color + monochrome) for broad Unicode coverage and cross-platform consistency. *Fonts SIL OFL 1.1, tools/images Apache 2.0.*

---

## 12. Game Audio — Sound Effects, Music & Tools

Sound-effect and music sources, the editors and trackers to make audio, and the middleware/libraries to play it in-engine. **Audio licensing is often per-asset and attribution-heavy — read each "Licensing note".**

### Sound-effect & music libraries
- **[Freesound](https://freesound.org/)** — Massive collaborative database of user-uploaded sounds and field recordings. *Free · per-sound license varies (CC0, CC-BY, CC-BY-NC); free account required · [license help](https://freesound.org/help/faq/).*
  - **Licensing note:** each sound carries its own CC license — check every file. CC-BY/CC-BY-NC require crediting the uploader; CC-BY-NC bars commercial use.
- **[Sonniss GDC Game Audio Bundle](https://sonniss.com/gameaudiogdc/)** — Annual multi-gigabyte bundles of pro SFX, released for GDC; 200GB+ across years in the [community archive](https://gdc.sonniss.com/). *Free · royalty-free, no attribution, unlimited lifetime/commercial use · AI/ML training prohibited.*
- **[BBC Sound Effects](https://sound-effects.bbcrewind.co.uk/)** — 16,000+ archival sound effects in WAV from the BBC's library. *Free · RemArc License · [terms](https://sound-effects.bbcrewind.co.uk/licensing).*
  - **Licensing note:** RemArc is personal/educational/research (non-commercial) by default — commercial projects need separate BBC permission.
- **[OpenGameArt — Audio](https://opengameart.org/art-search-advanced?field_art_type_tid%5B%5D=13)** — Community game-asset site with music and SFX packs. *Free · per-asset license (CC0, CC-BY, CC-BY-SA, GPL).*
  - **Licensing note:** mixed licenses; CC-BY/SA require credit and GPL/SA carry copyleft/share-alike obligations.
- **[Kenney — Audio](https://kenney.nl/assets/category:Audio)** — Polished, game-ready SFX packs (UI, impact, RPG, sci-fi, digital, jingles, voiceover) in WAV/OGG/M4A. *Free · CC0, no attribution.*
- **[Pixabay (audio)](https://pixabay.com/sound-effects/)** — 120,000+ SFX plus a large royalty-free [music library](https://pixabay.com/music/). *Free · Pixabay Content License, no attribution, commercial OK · [license](https://pixabay.com/service/license-summary/).*
- **[Zapsplat](https://www.zapsplat.com/)** — 150,000+ SFX and music; MP3 on free tier, WAV + no-credit on paid. *Free w/ account (attribution) or paid · [standard license](https://www.zapsplat.com/license-type/standard-license/).*
  - **Licensing note:** free members must credit "ZapSplat"; only a small CC0 subset is attribution-free.
- **[Mixkit](https://mixkit.co/free-sound-effects/)** — Curated free SFX and music by Envato; no sign-up. *Free · Mixkit License, no attribution · [license](https://mixkit.co/license/).*
  - **Licensing note:** ⚠️ music may NOT be used in video games (or CDs/DVDs, TV/radio) — a key restriction for game devs.
- **[Free To Use Sounds](https://www.freetousesounds.com/)** — Large field-recording SFX libraries from world travel. *Free (paid bulk packs) · attribution (website link) for free downloads · [license](https://www.freetousesounds.com/license-agreement).*
- **[Soundsnap](https://www.soundsnap.com/)** — 500,000+ professional SFX with unlimited downloads. *Paid subscription · perpetual royalty-free, no credit · [license](https://www.soundsnap.com/license).*
- **[Free Music Archive](https://freemusicarchive.org/)** — Long-running royalty-free music repository (WFMU origins). *Free · per-track CC license · [license guide](https://freemusicarchive.org/License_Guide).*
  - **Licensing note:** most tracks are CC-BY/-NC/-SA/-ND — verify each; attribution generally required.
- **[ccMixter](https://ccmixter.org/)** — Community remix/sample library (loops, acapellas, stems); see the [commercial-use section](http://dig.ccmixter.org/free). *Free · per-track CC (many NC) · attribution usually required.*
- **[Incompetech (Kevin MacLeod)](https://incompetech.com/music/royalty-free/)** — 2,000+ royalty-free library tracks across genres. *Free under CC-BY 4.0, or paid no-attribution license (~$30) · [FAQ](https://incompetech.com/music/royalty-free/faq.html).*
  - **Licensing note:** free use REQUIRES crediting Kevin MacLeod, e.g. "Title — Kevin MacLeod (incompetech.com), Licensed under Creative Commons: By Attribution 4.0."
- **[Bensound](https://www.bensound.com/)** — Royalty-free music for video/games. *Free tier (attribution) or paid per-track / All-Access · [pricing](https://www.bensound.com/pricing).*
- **[Patrick de Arteaga](https://patrickdearteaga.com/)** — Royalty-free game/chiptune music. *Free under CC-BY 4.0, or Pro/Broadcast licenses · [licensing](https://patrickdearteaga.com/en/licensing/).*
- **[Soundimage.org (Eric Matyas)](https://soundimage.org/)** — 2,500+ original music tracks plus SFX in many genres. *Free with attribution, or non-attribution license ($30/track, $5/SFX) · [attribution info](https://soundimage.org/attribution-info/).*
- **[Uppbeat](https://uppbeat.io/)** — Creator-focused royalty-free music + SFX with YouTube-safe licensing. *Free tier (3 dl/month, credit) or paid · [how licenses work](https://uppbeat.io/blog/royalty-free-and-copyright-free-music/uppbeats-music-licenses).*
- **[itch.io — game audio](https://itch.io/game-assets/tag-audio)** — Huge marketplace of indie music/SFX packs ([music](https://itch.io/game-assets/tag-music), [sound-effects](https://itch.io/game-assets/tag-sound-effects)). *Free + paid · per-asset license (many CC0/RF) — check each.*
- **[Tabletop Audio](https://tabletopaudio.com/)** — Original 10-minute ambiences and music for tabletop RPGs. *Free (donation-supported) · personal/tabletop use; contact for other licensing.*
- **[GameSounds.xyz](https://gamesounds.xyz/)** — Curated directory of royalty-free / public-domain game music and sounds (incl. BBC and Sonniss mirrors). *Free · per-folder license file — read each.*

### SFX generators (retro/procedural)
- **[Bfxr](https://www.bfxr.net/)** — Browser/desktop generator for retro 8-bit SFX (lasers, explosions, pickups), an elaborated remake of sfxr; exports WAV. *Free · OSS · sounds free for any use.*
- **[jsfxr / sfxr.me](https://sfxr.me/)** — HTML5 port of DrPetter's sfxr; coin/laser/explosion/powerup presets, usable as a [JS library](https://github.com/chr15m/jsfxr). *Free · OSS (MIT).*
- **[ChipTone (SFB Games)](https://sfbgames.itch.io/chiptone)** — Advanced free SFX tool by Tom Vian with waveform feedback, envelopes, filters, and modulation. *Free · output is CC0.*
- **[rFXGen](https://raylibtech.itch.io/rfxgen)** — sfxr-based generator by raylib's Ramon Santamaria; exports WAV/RAW and C header arrays, with CLI batch mode ([source](https://github.com/raysan5/rfxgen)). *Free · OSS (zlib).*
- **[as3sfxr](https://www.superflashbros.net/as3sfxr/)** — Thomas Vian's ActionScript port of sfxr (the lineage behind Bfxr/ChipTone); 4 oscillators, 7 generators, WAV export. *Free · OSS.*

### Music & tracker tools
- **[Bosca Ceoil](https://terrycavanagh.itch.io/bosca-ceoil)** — Terry Cavanagh's beginner-friendly loop-based music maker with 100+ MIDI/chiptune presets. *Free · OSS · [source](https://github.com/TerryCavanagh/boscaceoil).*
- **[Bosca Ceoil Blue](https://yurisizov.itch.io/boscaceoil-blue)** — Modern Godot-engine rework (Win/macOS/Linux/web); exports WAV, MIDI, XM. *Free · OSS · [source](https://github.com/YuriSizov/boscaceoil-blue).*
- **[BeepBox](https://www.beepbox.co/)** — Online tool for sketching and sharing instrumental/chiptune music. *Free · OSS (MIT).*
- **[FamiStudio](https://famistudio.org/)** — DAW-style NES/Famicom chiptune editor (piano-roll, no hex), FamiTracker import, many expansions; Win/macOS/Linux/Android. *Free · OSS (MIT) · [source](https://github.com/BleuBleu/FamiStudio).*
- **[OpenMPT](https://openmpt.org/)** — Mature Windows module tracker editing IT/XM/S3M/MOD with VST and ASIO support. *Free · OSS (BSD-3-Clause) · [features](https://openmpt.org/features).*
- **[LMMS](https://lmms.io/)** — Cross-platform DAW with piano-roll, beat/bassline editor, 15+ synths, VST2 + SoundFont2; exports WAV/FLAC/OGG/MP3. *Free · OSS (GPL-2.0+) · [source](https://github.com/LMMS/lmms).*

### Audio editors (DAWs)
- **[Audacity](https://www.audacityteam.org/)** — Ubiquitous multitrack audio editor/recorder (WAV/AIFF/MP3/OGG/FLAC) with effects and LADSPA/VST/Nyquist plug-ins. *Free · OSS (GPLv3) · [source](https://github.com/audacity/audacity).*
- **[Ocenaudio](https://www.ocenaudio.com/)** — Fast, lightweight cross-platform editor with real-time effect preview, VST support, and spectrogram editing. *Free (freeware, closed-source) · Win/macOS/Linux.*
- **[REAPER](https://www.reaper.fm/)** — Full-featured pro DAW with a 60-day free evaluation. *Paid · ~$60 discounted (personal / <$20k revenue) or ~$225 commercial · [purchase](https://www.reaper.fm/purchase.php).*
- **[Cakewalk Sonar](https://www.cakewalk.com/sonar/)** — BandLab's revived flagship Windows DAW: unlimited tracks, 64-bit engine, VST3/ARA. *Free basic tier (BandLab account); premium via paid BandLab membership.*
- **[Ardour](https://ardour.org/)** — Professional cross-platform DAW: unlimited tracks, non-destructive editing, mixing, MIDI, LV2/VST/AU. *Free if self-compiled; prebuilt binaries need a one-time payment/donation · OSS (GPL).*
- The major paid commercial DAWs — **FL Studio**, **Ableton Live**, **Apple Logic Pro**, **Steinberg Cubase** — are proprietary industry standards for game-music scoring.

### Audio middleware & engine libraries
- **[FMOD Studio](https://www.fmod.com/studio)** — Leading adaptive game-audio middleware with Unity/Unreal integration. *Free for indies (revenue <$200k & budget <$500k); otherwise ~$2k–$15k per title · [info](https://www.fmod.com/studio).*
- **[Audiokinetic Wwise](https://www.audiokinetic.com/en/wwise/pricing/)** — AAA-grade interactive audio engine (spatial audio, interactive music, dynamic mixing). *Free Indie license (budget ≤$250k) + free non-commercial; tiered Pro/Premium above · [pricing](https://www.audiokinetic.com/en/wwise/pricing/for-games/).*
  - **Licensing note:** a separate Wwise license is required per platform shipped.
- **[CRI ADX / ADX LE](https://game.criware.jp/en/products/adx/)** — Widely used (esp. Japan) game audio middleware supporting Unity/UE/cocos2d-x. *[ADX LE](https://game.criware.jp/en/products/adx-le_en/) free for small studios (company & game revenue each <¥10M); fees apply above.*
- **[miniaudio](https://miniaud.io/)** — Single-file C/C++ playback & capture library, no dependencies, all major platforms; WAV/FLAC/MP3 decoding, mixing, 3D spatialization. *Free · public domain or MIT-0 · [source](https://github.com/mackron/miniaudio).*
- **[SoLoud](https://solhsa.com/soloud/)** — Easy portable C/C++ game audio engine with an sfxr generator, speech synth, MOD/XM playback, and many bindings. *Free · OSS (zlib/libpng) · [source](https://github.com/jarikomppa/soloud).*
- **[OpenAL Soft](https://openal-soft.org/)** — Software implementation of the OpenAL 3D audio API: distance attenuation, Doppler, HRTF, environmental reverb (EFX). *Free · OSS (LGPL) · [source](https://github.com/kcat/openal-soft).*
- **[libsndfile](https://libsndfile.github.io/libsndfile/)** — C library for reading/writing audio formats (WAV, AIFF, FLAC, Ogg/Vorbis…) with conversion. *Free · OSS (LGPL-2.1+) · [source](https://github.com/libsndfile/libsndfile).*

---

## 13. VFX, Particles & Shaders

Tools to author real-time visual effects and particle systems, sources of sprite/VFX asset packs, and shader learning/resource hubs.

### Particle & VFX editors (engine-integrated)
- **[Unity VFX Graph](https://unity.com/features/graphics)** — Node-based GPU particle system for large-scale (millions-of-particles) real-time effects; works with URP/HDRP. *Unity · free with Unity · [docs](https://docs.unity3d.com/Manual/VFXGraph.html).*
- **[Unity Built-in Particle System (Shuriken)](https://docs.unity3d.com/Manual/class-ParticleSystem.html)** — Unity's classic CPU-driven particle module; broad platform support, good for smaller effects. *Unity · free with Unity.*
- **[Unreal Engine Niagara](https://dev.epicgames.com/documentation/en-us/unreal-engine/niagara-visual-effects)** — Modern, highly programmable node/module VFX system in UE4/UE5 (CPU & GPU sims). *Unreal · free with Unreal.*
- **[Unreal Cascade (legacy)](https://dev.epicgames.com/documentation/en-us/unreal-engine/cascade-particle-systems)** — Older UE particle editor, superseded by Niagara (with an official converter plugin). *Unreal · free with Unreal.*
- **[Godot GPUParticles2D / 3D](https://docs.godotengine.org/en/stable/classes/class_gpuparticles3d.html)** — GPU-driven particle nodes configured via `ParticleProcessMaterial` or a custom `ShaderMaterial`; CPUParticles fallbacks exist. *Godot · OSS (MIT) · [process-material docs](https://docs.godotengine.org/en/stable/classes/class_particleprocessmaterial.html).*
- **[Cocos Creator Particle System](https://docs.cocos.com/creator/3.8/manual/en/particle-system/index.html)** — Built-in 2D (`ParticleSystem2D`, plist support) and modular 3D particle systems. *Cocos · OSS (engine) · [2D particles](https://docs.cocos.com/creator/3.8/manual/en/particle-system/2d-particle/2d-particle.html).*
- **[Phaser Particle Emitter](https://docs.phaser.io/phaser/concepts/gameobjects/particles)** — Built-in 2D particle emitter (explode/flow modes, per-particle props, bounds, callbacks). *Phaser / web · OSS (MIT) · [API](https://docs.phaser.io/api-documentation/class/gameobjects-particles-particleemitter).*

### Particle & VFX editors (standalone / web / cross-engine)
- **[Effekseer](https://effekseer.github.io/en/)** — Free standalone editor authoring `.efk` 2D/3D effects with runtimes for Unity, Unreal, Godot, Cocos2d-x, DXLib, and DirectX/OpenGL/Vulkan/Metal/WebGL. *Cross-engine · OSS (MIT) · [docs](https://effekseer.github.io/Help_Tool/en/).*
- **[libGDX Particle Editor (Flame)](https://libgdx.com/wiki/tools/2d-particle-editor)** — Official GUI editor for tuning 2D (and 3D) particle effects in real time for libGDX. *libGDX / JVM · OSS (Apache-2.0) · [repo](https://github.com/libgdx/gdx-particle-editor).*
- **[PixiJS particle-emitter](https://github.com/pixijs-userland/particle-emitter)** — Particle-system library for PixiJS (formerly `pixi-particles`), behavior-based config. *Pixi.js / web · OSS (MIT) · [docs](https://particle-emitter.pixijs.io/docs/).*
- **[PixiJS particle-emitter Editor](https://github.com/pixijs/pixi-particles-editor)** — Interactive web editor to design and preview Pixi particle configs (use `upgradeConfig()` on older output). *Pixi.js / web · OSS · [getting started](https://www.pixiparticles.com/pixijs-particle-emitter/getting-started).*
- **[three.quarks](https://github.com/Alchemist0823/three.quarks)** — General-purpose particle/VFX engine for Three.js (TypeScript) with a WYSIWYG [editor](https://quarks.art/) and JSON export. *Three.js / web · OSS (MIT).*
- **[three-nebula](https://three-nebula.org/)** — WebGL particle-system engine for Three.js with a cross-platform GUI designer and JSON-loadable systems. *Three.js / web · OSS (MIT) · [repo](https://github.com/creativelifeform/three-nebula).*
- **[Pixel FX Designer](https://codemanu.itch.io/particle-fx-designer)** — Standalone slider-driven 2D pixel-art particle tool exporting PNG spritesheets/GIFs; 1000+ particle assets. *Win/Mac (Steam & itch) · paid (~$15) · [Steam](https://store.steampowered.com/app/939360/Pixel_FX_Designer/).*
- **[SpriteMancer](https://spritemancer.com/)** — All-in-one effect tool (particles, fluids, node graph, sprite animation) by CodeManu, successor to Pixel FX Designer. *Win/Mac (Steam & itch) · paid (Early Access) · [Steam](https://store.steampowered.com/app/1858750/SpriteMancer/).*

### Sprite & VFX asset packs
*More 2D-art creators are catalogued in [§1](#1-2d-sprite--game-art-asset-sources); these are a few verified VFX-focused examples.*
- **[CodeManu — Free VFX Asset Pack](https://codemanu.itch.io/vfx-free-pack)** — 22 pixel-art effects (30/60fps). *2D sprite-sheets · CC0 (personal & commercial) · also [Free Pixel Effects Pack](https://codemanu.itch.io/pixelart-effect-pack).*
- **[ansimuz — Magic & VFX packs](https://ansimuz.itch.io/)** — Crispy pixel-art explosion/magic VFX (Free Magic Pack 9 is free; larger collections paid). *2D sprite-sheets · free + paid.*
- **[Pimen](https://pimen.itch.io/)** — Hand-drawn pixel-art spell/elemental VFX (40+ sets: fire, ice, thunder, wind…). *2D sprite-sheets · free + paid.*
- **[JosephSeraph / Seraph Circle](https://seraphcircle.itch.io/)** — Pixel-art elemental/sci-fi VFX packs ("SC: Animation – Essentials" is free). *2D sprite-sheets · free + paid.*

### Shader authoring tools
- **[Unity Shader Graph](https://docs.unity3d.com/Packages/com.unity.shadergraph@latest/)** — Node-based visual shader editor for URP/HDRP. *Unity · free with Unity.*
- **[Unreal Material Editor](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-material-editor-user-guide)** — Node-graph material/shader authoring (expressions compiled to HLSL). *Unreal · free with Unreal · [materials docs](https://dev.epicgames.com/documentation/unreal-engine/unreal-engine-materials).*
- **[Godot Visual Shaders](https://docs.godotengine.org/en/stable/tutorials/shaders/visual_shaders.html)** — Graph-based shader editor (vertex/fragment/light) with live previews and custom nodes. *Godot · OSS (MIT) · [class ref](https://docs.godotengine.org/en/stable/classes/class_visualshader.html).*
- **[SHADERed](https://shadered.org/)** — Full-featured cross-platform shader IDE with a step-through GLSL/HLSL debugger, compute/geometry shaders, render textures, and a plugin API. *Win/Linux/Web · OSS · [repo](https://github.com/dfranx/SHADERed).*
- **[KodeLife](https://hexler.net/kodelife)** — Real-time GPU shader live-coding editor with audio/MIDI/gamepad inputs; GLSL, Metal, HLSL. *Win/Mac/Linux/iOS/Android · paid (free unlimited beta available) · [manual](https://hexler.net/kodelife/manual/introduction).*
- **[Shadron](https://www.arteryengine.com/shadron/)** — GLSL-based procedural graphics editor for generating/processing images, animations, textures, and particles with live parameters. *Win/Mac/Linux (Steam) · paid · [docs](https://www.arteryengine.com/shadron/doc/).*
- **[Synthclipse](https://synthclipse.sourceforge.net/)** — Eclipse-based GLSL prototyping IDE (FS/VS/GS/TS/CS) with Fragmentarium/Shadertoy/GLSL-Sandbox compatibility. *Win/Linux · OSS · [user guide](https://synthclipse.sourceforge.net/user_guide/shadertoy.html).*
- **[ISF (Interactive Shader Format) Editor](https://isf.video/)** — GLSL+JSON shader format and free desktop editor (200+ bundled shaders) for portable, parameterized shaders. *Win/Mac · OSS · [docs](https://docs.isf.video/).*

### Shader learning & resource hubs
- **[Shadertoy](https://www.shadertoy.com/)** — Online community/playground for writing, sharing, and remixing GLSL fragment shaders with multi-pass and audio/video/VR inputs. *Web · free.*
- **[GLSL Sandbox](https://glslsandbox.com/)** — Minimal in-browser fragment-shader editor and fork-and-remix gallery by mrdoob. *Web · OSS (MIT) · [repo](https://github.com/mrdoob/glsl-sandbox).*
- **[The Book of Shaders](https://thebookofshaders.com/)** — Free step-by-step guide to fragment shaders (shaping functions, noise, patterns, raymarching) with live editors. *Web · free.*
- **[Inigo Quilez — Articles](https://iquilezles.org/articles/)** — Deep reference articles on SDFs, raymarching, noise, distance functions, and procedural graphics math. *Web · free.*
- **[Catlike Coding](https://catlikecoding.com/unity/tutorials/)** — In-depth written C#/shader/rendering tutorials for Unity (and Godot). *Free (Patreon-supported).*
- **[Godot Shaders](https://godotshaders.com/)** — Community library of free 3D (spatial) and 2D (canvas-item) shaders plus snippets for Godot. *Godot · free.*

---

## Appendix: End-to-End Workflow Recipes

Concrete pipelines wiring the sections together.

**Recipe 1 — Ship a pixel-art sprite to a TypeScript web game**
1. Draw + animate in **Aseprite** (§3); export a sheet with the `--sheet`/JSON option.
2. (Or skip drawing: pull a CC0 pack from **Kenney**/**itch.io** (§1).)
3. Pack multiple sheets with **TexturePacker** or **Free Texture Packer** CLI → one atlas + JSON (§5).
4. Optimize the PNG with **oxipng**/**pngquant** in CI (§6).
5. Load via **Pixi.js** `Assets.load()` → `Spritesheet.animations`, or **Phaser** `load.aseprite()` (§8).
6. Record the asset's license + attribution (§9).

**Recipe 2 — Author and ship a compressed PBR material for WebGL**
1. Grab a CC0 base from **Poly Haven**/**ambientCG**, or author in **Material Maker**/**Substance Designer** (§2, §4).
2. Derive any missing maps with **Materialize**/**AwesomeBump**/**DeepBump** (§4).
3. Convert to **KTX2 + Basis** with `toktx` (KTX-Software) or `basisu` (§6), generating mips.
4. Load with **Three.js** `KTX2Loader` (call `detectSupport(renderer)`) or **Babylon.js** `.ktx2` (§8).

**Recipe 3 — AI-assisted, commercial-safe sprite + texture set**
1. Generate base sprites in **Scenario**/**PixelLab**/**Retro Diffusion** on a **paid** tier (§7).
2. Generate seamless textures via **Adobe Firefly** + **Substance 3D Sampler**, or **Polycam** (§7).
3. Upscale/clean with pixel-aware settings (**Real-ESRGAN**/**Upscayl**) (§7).
4. Verify each tool's commercial-use + IP terms; archive prompts and the terms (§7, §9).
5. Pack, compress, and load as in Recipes 1–2.

**Recipe 4 — Headless asset-optimization step for CI**
`ImageMagick`/`sharp` (normalize size/format) → `mozjpeg`/`oxipng`/`pngquant` (optimize) → `free-tex-packer-cli`/`TexturePacker` (atlas) → `basisu`/`toktx` (GPU-compress to KTX2). All four stages are scriptable and license-clean for build servers (§5, §6).

**Recipe 5 — Optimize a 3D model for web/runtime**
1. Grab or author a model (§10) — e.g. CC0 from **Poly Haven**/**Quaternius**, or rig a character with **Mixamo**.
2. Export to **glTF/GLB** (the runtime standard) via **Blender** (§10).
3. Validate with the **Khronos glTF Validator**; optimize with **glTF-Transform** or **gltfpack** — Draco/meshopt geometry compression + KTX2/WebP textures (§10, §6).
4. Load in **Three.js**/**Babylon.js** with `GLTFLoader` + `KTX2Loader` (§8).

**Recipe 6 — Royalty-free audio, legally**
1. Pull CC0 SFX from **Kenney**/**Sonniss**; music from **Incompetech**/**Patrick de Arteaga** (§12).
2. Track the per-asset license — **credit Kevin MacLeod** for Incompetech, check each **Freesound** file individually, and don't use **Mixkit** music in games (§12).
3. Integrate via **FMOD**/**Wwise** (free indie tiers) or OSS **miniaudio**/**SoLoud** (§12).

---

*Compiled 2026-06-03 via thirteen parallel web-research streams. Links verified at time of writing; product status, pricing, and licenses change — re-check terms before relying on them. Corrections and additions welcome.*
