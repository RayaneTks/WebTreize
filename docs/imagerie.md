# WebTreize — Système visuel photographique

> Document de direction artistique image. Il applique `docs/charte-graphique.md` au site tel qu’il
> est codé aujourd’hui. En cas de conflit, **la charte gagne**.
> Les prompts sont en anglais : c’est la langue dans laquelle les modèles d’image obéissent.

---

## A · Principes

1. On photographie un **métier**, jamais un logiciel. Un écran allumé dans le cadre, c’est déjà raté.
2. Le sujet occupe **un tiers du cadre au plus**. Le reste est du vide tenu — c’est lui qui donne le prix.
3. La lumière vient **de côté**, fin de matinée ou fin d’après-midi. Aucune source artificielle visible.
4. **Une seule tache terre cuite par image**, et jamais plus de trois sur un écran une fois le site assemblé.
5. Les matières sont **mates** : bois clair, lin, papier épais, plâtre, céramique, laiton. Aucun chrome, aucun verre brillant.
6. Marseille se lit à la **lumière et aux matières**, pas à un monument ni à une plaque de rue.
7. **Aucun visage tourné vers l’objectif**, aucun sourire commercial. Des mains, des gestes, des lieux.
8. **Aucun texte dans l’image** : ni enseigne lisible, ni étiquette, ni interface. Les mots du site sont posés par-dessus, en Plus Jakarta Sans.
9. **Une idée par visuel.** Si le cadre est chargé, on retire un objet — jamais de l’espace.
10. **Deux options générées, une seule retenue.** Une image « acceptable » n’entre pas sur le site.

---

## B · Inventaire des emplacements

Six images à générer, plus une ligne d’icônes qui **ne se génère jamais par IA** (§ 4 de la charte).
Le tableau est en deux moitiés pour rester lisible : cadrage d’abord, livraison ensuite.

> **Les cinq cartes de partage ne sont plus des photographies.** Le cahier des charges § 6.8 les
> fait produire par le code : `app/opengraph-image.tsx` et un fichier par route composent l’image
> en 1200 × 630 avec `ImageResponse` de `next/og`, à partir de `lib/og.tsx` — fond ivoire,
> logotype « webtreize. », titre de la page en display, ligne d’appui en `ink-muted`, filet terre
> cuite. Aucune image générée par un modèle n’entre dans une carte de partage, et le texte y est
> du vrai texte. Les lignes `og-*` des tableaux ci-dessous et les prompts C.7 à C.11 restent à
> titre d’archive, **barrés** : ne rien produire à partir d’eux.

### B.1 · Cadrage et rôle éditorial

| Identifiant | Page · composant · fichier | Rôle éditorial | Ratio | Source à générer | Servi (largeur max) |
| --- | --- | --- | --- | --- | --- |
| `hero-atelier` | Accueil · `HeroSection` · `components/sections/HeroSection.tsx` | Plaque d’ouverture, sous le titre. **C’est le LCP du site** : la première preuve de sérieux. | 16/9 | 2400 × 1350 | 1224 px (2448 px en DPR 2) |
| `craft-site` | Accueil · `CraftSection` bloc « Le site » · `components/sections/CraftSection.tsx` | Rendre tangible « un site fait pour votre métier » : le commerce, pas l’écran. | 4/3 | 1600 × 1200 | 520 px (1040 px en DPR 2) |
| `craft-visibilite` | Accueil · `CraftSection` bloc « La visibilité » · idem | Être trouvé à deux rues d’ici : la rue, la devanture, le passage. | 4/3 | 1600 × 1200 | 520 px (1040 px en DPR 2) |
| `craft-outils` | Accueil · `CraftSection` bloc « Les outils » · idem | Le quotidien remis en ordre : l’établi rangé, pas le tableau de bord. | 4/3 | 1600 × 1200 | 520 px (1040 px en DPR 2) |
| `about-atelier` | À propos · après le bloc citation · `app/about/page.tsx` | Donner un lieu au studio sans inventer de personne : le plan de travail, aucun visage. | 3/4 | 1200 × 1600 | 420 px (840 px en DPR 2) |
| `fond-aplat` | Réserve · sections neutres (`PromisesSection`, `ProcessSection`, `PageShell`) | Aplat graphique réutilisable quand une section a besoin de matière sans sujet. | 16/9 | 2400 × 1350 | 1440 px |
| ~~`og-defaut`~~ | *Produit par le code* · `app/opengraph-image.tsx` | Carte de partage par défaut : `/legal/*`, `404`, toute page sans image propre. | 1,91/1 | — | 1200 × 630, servi tel quel |
| ~~`og-accueil`~~ | *Produit par le code* · `app/opengraph-image.tsx` | Ce qu’on voit quand le lien du site tombe dans une conversation WhatsApp. | 1,91/1 | — | 1200 × 630, servi tel quel |
| ~~`og-services`~~ | *Produit par le code* · `app/services/opengraph-image.tsx` | Le devis et le métier, pas la liste de prestations. | 1,91/1 | — | 1200 × 630, servi tel quel |
| ~~`og-about`~~ | *Produit par le code* · `app/about/opengraph-image.tsx` | Le studio comme lieu : une table, une chaise, la lumière. | 1,91/1 | — | 1200 × 630, servi tel quel |
| ~~`og-contact`~~ | *Produit par le code* · `app/contact/opengraph-image.tsx` | L’invitation à écrire : papier, stylo, lin. | 1,91/1 | — | 1200 × 630, servi tel quel |
| `icones` | `app/icon.svg`, `app/apple-icon.png`, `app/manifest.ts`, `public/icons/` | Favicon et icônes PWA. **Aucun prompt : le logotype ne se génère jamais par IA.** | 1/1 | 512 × 512 (export du SVG) | 512 / 192 / 180 px |

### B.2 · Livraison technique

`priority` n’est vrai que pour le LCP : une seule ligne du tableau. Les colonnes `sizes` et `alt`
se recopient **telles quelles** dans le code.

| Identifiant | Format cible | Poids max | `priority` | `sizes` | `alt` (à coller) |
| --- | --- | --- | --- | --- | --- |
| `hero-atelier` | AVIF + WebP générés par `next/image` · JPEG source de repli | source ≤ 500 ko · servi ≤ 160 ko | **`true`** | `(min-width: 1280px) 1224px, 100vw` | Un artisan pose ses outils sur un comptoir de bois clair, dans la lumière de fin de matinée d’une boutique marseillaise. |
| `craft-site` | AVIF + WebP générés par `next/image` · JPEG source de repli | source ≤ 250 ko · servi ≤ 70 ko | `false` | `(min-width: 1120px) 520px, (min-width: 700px) 46vw, 100vw` | Un téléphone posé à plat sur le comptoir en bois clair d’un commerce, à côté d’un carnet de commandes ouvert. |
| `craft-visibilite` | idem | source ≤ 250 ko · servi ≤ 70 ko | `false` | `(min-width: 1120px) 520px, (min-width: 700px) 46vw, 100vw` | Devanture d’un petit commerce marseillais en fin d’après-midi, vue depuis le trottoir d’en face. |
| `craft-outils` | idem | source ≤ 250 ko · servi ≤ 70 ko | `false` | `(min-width: 1120px) 520px, (min-width: 700px) 46vw, 100vw` | Établi d’artisan rangé : un carnet de notes, un mètre pliant et une tablette posés côte à côte sur du bois clair. |
| `about-atelier` | idem | source ≤ 250 ko · servi ≤ 70 ko | `false` | `(min-width: 1120px) 420px, (min-width: 700px) 40vw, 100vw` | Le plan de travail du studio : un carnet ouvert, un crayon et une tasse en céramique, éclairés par la fenêtre. |
| `fond-aplat` | idem | source ≤ 200 ko · servi ≤ 60 ko | `false` | `100vw` | *(décoratif)* `alt=""` |
| ~~`og-defaut`~~ | **PNG produit par `lib/og.tsx`** | — | — | — | Fond ivoire clair traversé par un filet terre cuite et l’ombre douce d’une fenêtre. |
| ~~`og-accueil`~~ | **PNG produit par `lib/og.tsx`** | — | — | — | Comptoir en bois clair d’une boutique marseillaise, éclairé par la lumière du matin. |
| ~~`og-services`~~ | **PNG produit par `lib/og.tsx`** | — | — | — | Un dossier en papier épais et un crayon en laiton mat posés sur une table en bois clair. |
| ~~`og-about`~~ | **PNG produit par `lib/og.tsx`** | — | — | — | Coin de table de travail du studio, avec un carnet et une chaise en bois, à la lumière du matin. |
| ~~`og-contact`~~ | **PNG produit par `lib/og.tsx`** | — | — | — | Une feuille de papier épais, un stylo en laiton mat et un téléphone posés sur du lin sable. |
| `icones` | SVG + PNG | ≤ 20 ko | — | — | *(décoratif, `aria-hidden`)* |

> **Pourquoi les cartes de partage ne sont ni en AVIF ni photographiées.** WhatsApp, LinkedIn et
> Slack ne lisent pas l’AVIF de façon
> fiable et ne passent pas par l’optimiseur de Next : le fichier servi est celui qui part. `next/og`
> rend un PNG, lu partout — et un titre composé en Plus Jakarta Sans, là où un modèle d’image
> n’écrit que des lettres fausses.

> **Pourquoi une seule `priority`.** `hero-atelier` est le plus grand élément visible au chargement
> de l’accueil : c’est lui le LCP. Toute autre image marquée `priority` entre en concurrence avec lui
> et dégrade la mesure.

---

## C · Prompts prêts à l’emploi

Chaque prompt est autonome : le style de base est développé en entier, il n’y a rien à préfixer.
On copie le bloc dans ChatGPT, puis le bloc `Negative prompt` juste en dessous. On génère **les deux
variantes**, on choisit avec la grille du § D, on jette l’autre.

### C.1 · `hero-atelier` — 16/9

Le titre et les boutons sont **au-dessus** de la plaque, pas dessus. Le vide doit donc tomber sur le
**bord haut** de l’image, pour prolonger la respiration du titre ; le poids visuel descend dans les
deux tiers bas.

**Variante A — l’intérieur, juste avant l’ouverture**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural materials
only: light wood, linen, thick paper, plaster, ceramic, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: the interior of a small independent shop in Marseille just before opening, empty of
customers. A light wood counter runs across the lower right of the frame. On it, a few objects of a
real working day: a thick paper order book, a folded linen cloth, a matte brass measuring tool. A
single small burnt terracotta ceramic cup is the only colour accent in the whole picture. Behind
the counter, a sun-lit plaster wall and, further back, the softly blurred shopfront window.

Composition: wide 16:9, camera at counter height, eye level, slightly off-centre. All visual weight
sits in the lower two thirds and to the right. The upper third of the frame must stay almost empty:
plain sun-lit ivory plaster wall crossed only by one long soft window shadow, no objects, no
detail, no clutter — this calm band joins the white space of the headline printed above the image.
Keep a wide empty foreground on the left.

Light and rendering: warm natural side light entering from the left, late morning, no flash, no
blue cast, no midday hardness. 50mm lens, aperture around f/2.2, background gently out of focus.
16:9 aspect ratio, largest available resolution, target 2400 x 1350 px. Subtle film grain, creamy
highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, faces looking at the camera,
smiling models, crowds, cars, cash register screen, lit computer monitor, price labels, hanging
signs, midday sun, hard black shadows, wide-angle distortion, busy upper third
```

**Variante B — le coin de rue, fin d’après-midi**

```text
Editorial photography in a warm minimalist style. Natural side light, late afternoon, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: painted plaster, light wood, linen awning, worn stone. Generous empty space,
off-centre composition, shallow depth of field, 35mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: a quiet street corner in an old Marseille neighbourhood, one small shopfront with a light
wood frame and a plain linen awning, shot slightly from the side, from across the street. No people,
no cars, no readable sign. A single burnt terracotta pot beside the door is the only colour accent.
The rest of the facade is warm ivory plaster, sun-lit, slightly worn and well kept.

Composition: wide 16:9, camera at eye level on the opposite pavement, subject pushed to the right
third. The upper third and the left half are plain sun-lit plaster wall — empty, flat, with one long
diagonal shadow. That calm zone must stay free of any detail so it continues the white space of the
headline placed above the image.

Light and rendering: low warm side light from the left, late afternoon, long soft shadows across
the pavement, no flash, no blue cast. 35mm lens, aperture around f/4, gentle background falloff.
16:9 aspect ratio, largest available resolution, target 2400 x 1350 px. Subtle film grain, creamy
highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, shop signs, menu boards, street
name plates, licence plates, parked cars, scooters, crowds, tourists, graffiti, overhead cables,
postcard landmark, harbour cliché, blue sky saturation
```

### C.2 · `craft-site` — 4/3

Le bloc « Le site » place le texte **à gauche** et la plaque **à droite**. Le vide doit donc tomber
sur le **bord gauche** de l’image, celui qui touche la colonne de texte. Le bord haut reste calme
lui aussi : sur téléphone, la plaque passe sous le texte en pleine largeur.

**Variante A — les mains et le téléphone sur le comptoir**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: the hands of a shopkeeper, seen from just above the counter, holding a modern smartphone
flat over a light wood counter. The phone screen is completely off, dark and matte, reflecting
nothing. Beside it, a thick paper order book lies open and a matte brass pen rests across it. Only
the hands and forearms are visible, sleeves rolled up, no face, no body. One small burnt terracotta
ceramic cup at the edge of the counter is the single colour accent.

Composition: 4:3, the hands and phone grouped in the lower right, camera at eye level and slightly
angled. The entire left third of the frame is bare, sun-lit light wood counter with one soft
diagonal shadow — empty, no objects at all, because the text column of the page sits directly
against that edge. Keep the top strip of the frame calm too: plain out-of-focus wall, no shelves,
no clutter.

Light and rendering: warm natural side light from the left, late morning, no flash, no blue cast.
50mm lens, aperture around f/2.5, background softly out of focus. 4:3 aspect ratio, largest
available resolution, target 1600 x 1200 px. Subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, glowing phone screen, user
interface, app icons, notifications, extra fingers, deformed hands, six fingers, merged fingers,
face, portrait, wristwatch branding, glossy phone case, busy left edge
```

**Variante B — sans mains, à plat**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens. Subtle film grain, gentle contrast,
creamy highlights. Calm, confident, artisanal.

Subject: a still life seen from directly above. A modern smartphone lying flat, screen completely
off and matte, on a soft sand beige linen cloth spread over a light wood table. Next to it, a thick
paper notebook closed with a linen band and a matte brass pen. One small burnt terracotta ceramic
saucer is the only colour accent. No hands, no people.

Composition: 4:3, top-down flat lay, objects grouped tight in the lower right quadrant. The left
third and the top strip of the frame are empty light wood and linen, lit and free of any object,
because the text column of the page sits against the left edge and the plate stacks under the text
on mobile. One long soft window shadow crosses the empty area diagonally.

Light and rendering: warm natural side light from the upper left, late morning, no flash, no blue
cast. 50mm lens, aperture around f/4, everything gently sharp with a soft falloff at the edges.
4:3 aspect ratio, largest available resolution, target 1600 x 1200 px. Subtle film grain, creamy
highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, glowing screen, user interface
mockup, app icons, brand logos on devices, marble surface, dark moody flat lay, symmetrical
centred layout, props filling every corner
```

### C.3 · `craft-visibilite` — 4/3

Le bloc « La visibilité » est inversé : la plaque est **à gauche**, le texte **à droite**. Le vide
doit donc tomber sur le **bord droit** de l’image. Bord haut calme également, pour l’empilement
mobile.

**Variante A — la devanture depuis le trottoir d’en face**

```text
Editorial photography in a warm minimalist style. Natural side light, late afternoon, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: painted plaster, light wood, linen awning, worn stone. Generous empty space,
off-centre composition, shallow depth of field, 35mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: the front of a small neighbourhood shop in Marseille, photographed from the opposite
pavement in late afternoon. A light wood shopfront frame, a plain unmarked linen awning, a glass
door with warm reflections but nothing readable behind it. No people in the frame, no cars. A single
burnt terracotta planter beside the entrance is the only colour accent.

Composition: 4:3, camera at eye level, the shopfront pushed into the left two thirds of the frame.
The right third is plain sun-lit ivory plaster wall, empty and flat, crossed by one long soft shadow
— that side of the image touches the text column of the page and must carry nothing at all. Keep
the top strip of the frame free of cables, balconies and shutters.

Light and rendering: low warm side light coming from the right, late afternoon, long soft shadows on
the pavement, no flash, no blue cast. 35mm lens, aperture around f/4, gentle depth falloff. 4:3
aspect ratio, largest available resolution, target 1600 x 1200 px. Subtle film grain, creamy
highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, shop signs, opening hours
stickers, menu boards, street name plates, price posters, licence plates, parked cars, scooters,
crowds, overhead cables, graffiti tags, harbour postcard, saturated blue sky
```

**Variante B — la porte qu’on pousse, de l’intérieur**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: light wood, plaster, linen, worn stone, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 35mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: the inside of a small Marseille shop looking out through the open doorway onto the sun-lit
street. The wooden door frame and a matte brass handle occupy the left of the frame, sharp and
close. Beyond, the street is bright, warm and softly out of focus, with no readable detail. A single
burnt terracotta doormat tile is the only colour accent. No people, no vehicles.

Composition: 4:3, camera at eye level just inside the shop, the doorway opening into the left two
thirds. The right third is a plain interior plaster wall in warm shade, completely empty, because
the text column of the page sits against that edge. The top strip of the frame stays calm: plain
wall and ceiling, no shelves, no hanging objects.

Light and rendering: strong warm daylight coming from the doorway on the left, deep but soft
interior shade on the right, no flash, no blue cast. 35mm lens, aperture around f/2.8, street
rendered as a soft luminous blur. 4:3 aspect ratio, largest available resolution, target
1600 x 1200 px. Subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, blown-out white doorway, HDR
halo, shop signage, window stickers, price tags, silhouetted people, passers-by, cars, cluttered
shelves, hanging lamps, busy right edge
```

### C.4 · `craft-outils` — 4/3

Le bloc « Les outils » remet la plaque **à droite** et le texte **à gauche** : vide sur le **bord
gauche**, bord haut calme.

**Variante A — l’établi vu de dessus**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens. Subtle film grain, gentle contrast,
creamy highlights. Calm, confident, artisanal.

Subject: a craftsman's workbench seen from directly above, tidy and well used. On the light wood
surface: a thick paper notebook open on blank ruled pages, a wooden folding ruler half unfolded, a
matte brass pencil, and a tablet lying face down with its matte back visible. Nothing is switched
on. One small burnt terracotta ceramic mug is the only colour accent. No hands, no people.

Composition: 4:3, top-down, the objects arranged in a loose diagonal group in the right half of the
frame. The left third is bare, sun-lit light wood with visible grain and one long soft shadow —
completely empty, because the text column of the page sits against that edge. The top strip stays
empty too, so the frame still breathes when it stacks under the text on mobile.

Light and rendering: warm natural side light from the upper left, late morning, no flash, no blue
cast. 50mm lens, aperture around f/4, sharp on the objects with a gentle falloff towards the edges.
4:3 aspect ratio, largest available resolution, target 1600 x 1200 px. Subtle film grain, creamy
highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, glowing tablet screen, dashboard
mockup, charts, spreadsheets, sticky notes with writing, printed pages, tool wall, messy workshop,
sawdust everywhere, dark industrial mood, centred symmetrical layout
```

**Variante B — les mains qui écrivent**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: the hands of a craftsman writing in a thick paper notebook laid on a light wood workbench,
seen from a low three-quarter angle at eye level. Only the hands and forearms are in frame, sleeves
rolled, no face, no body. A wooden folding ruler and a matte brass pencil rest beside the notebook.
The notebook pages are blank and unmarked. One small burnt terracotta ceramic mug in the background
is the only colour accent.

Composition: 4:3, the hands and notebook grouped in the lower right, camera close and slightly
above the bench. The left third of the frame is bare sun-lit workbench, empty of objects, because
the text column of the page sits directly against that edge. The top strip of the frame is a plain
out-of-focus plaster wall, no shelves and no tools hanging.

Light and rendering: warm natural side light from the left, late morning, no flash, no blue cast.
50mm lens, aperture around f/2.5, background softly out of focus. 4:3 aspect ratio, largest
available resolution, target 1600 x 1200 px. Subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, extra fingers, six fingers,
deformed hands, merged fingers, broken pencil geometry, handwriting on the page, sketched diagrams,
face, portrait, smiling model, cluttered tool wall, busy left edge
```

### C.5 · `about-atelier` — 3/4

Image verticale de la page **À propos**, posée après le bloc citation. Le texte est **au-dessus**,
jamais dessus : le vide tombe sur le **tiers haut** de l’image. Aucun visage — on ne fabrique pas de
personne qui n’existe pas.

**Variante A — le plan de travail près de la fenêtre**

```text
Editorial photography in a warm minimalist style. Natural side light, late morning, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: light wood, linen, thick paper, plaster, ceramic, matte brass. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: a corner of a small studio work table beside a window, in a plain plaster-walled room in
Marseille. On the light wood table: a thick paper notebook open on blank pages, a matte brass
pencil, a linen cloth folded, and a burnt terracotta ceramic cup as the single colour accent. A
simple wooden chair is partly visible. No people, no faces, no screens.

Composition: vertical 3:4, camera at eye level, the table occupying the lower two thirds and pushed
slightly to the right. The upper third is bare sun-lit plaster wall with one long soft window
shadow — empty, no frames, no shelves, no objects, because the paragraph text of the page sits
directly above the image and the two must share the same silence.

Light and rendering: warm natural side light entering from the left window, late morning, no flash,
no blue cast. 50mm lens, aperture around f/2.5, background softly out of focus. Vertical 3:4 aspect
ratio, largest available resolution, target 1200 x 1600 px. Subtle film grain, creamy highlights,
gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, face, portrait, person, team
photo, office chairs, computer monitors, keyboards, cable management, framed posters, wall art,
motivational quotes, bookshelves full, plants everywhere, busy upper third
```

**Variante B — la fenêtre et l’ombre, cadre presque vide**

```text
Editorial photography in a warm minimalist style. Natural side light, late afternoon, soft long
shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige #EAE3D8), deep warm
brown-black accents (#17130F), one single burnt terracotta accent (#C4552B). Matte natural
materials only: plaster, light wood, linen, ceramic. Generous empty space, off-centre composition,
shallow depth of field, 35mm lens at eye level. Subtle film grain, gentle contrast, creamy
highlights. Calm, confident, artisanal.

Subject: an almost empty room in a Marseille apartment used as a studio. A tall old window on the
right casts a long geometric shadow across a bare warm ivory plaster wall and a light wood floor.
Against the wall, low and small in the frame, a single wooden stool holds one burnt terracotta
ceramic bowl — the only colour accent. Nothing else. No people, no furniture clutter.

Composition: vertical 3:4, camera at eye level, everything of interest kept in the lower third. The
upper two thirds are plain sun-lit wall and shadow only, with no object at all, so the image reads
as breathing room under the paragraph printed above it.

Light and rendering: low warm side light through the window on the right, late afternoon, long soft
shadow shapes, no flash, no blue cast. 35mm lens, aperture around f/4, everything gently sharp.
Vertical 3:4 aspect ratio, largest available resolution, target 1200 x 1600 px. Subtle film grain,
creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, face, portrait, person,
silhouette, furniture set, rug patterns, wall art, curtains with pattern, radiator, power sockets,
visible light fixtures, hard black shadows, vignetting
```

### C.6 · `fond-aplat` — 16/9, sans photo

Aplat graphique de réserve, pour une section qui a besoin de matière sans sujet. Il n’y a pas de
zone de vide à réserver : **tout est zone de vide**. La seule règle est que le tiers central reste
lisible sous un texte.

**Variante A — papier et ombre de fenêtre**

```text
Minimal editorial background, no photography of objects. A flat sheet of warm ivory paper
(#F6F3EE) filling the whole frame, with a very subtle visible fibre texture and a barely perceptible
paper edge. One large soft shadow of a window frame falls diagonally from the upper left across the
surface, warm grey and completely blurred at the edges. One single thin burnt terracotta hairline
(#C4552B), one pixel wide, crosses the lower third horizontally from edge to edge. Nothing else in
the frame.

Composition: wide 16:9. The central horizontal band must stay flat, even and free of any texture
accident, so that a headline can be laid over it later. No object, no prop, no vignette, no border.

Rendering: 16:9 aspect ratio, largest available resolution, target 2400 x 1350 px. Very gentle
contrast, creamy highlights, subtle film grain, matte finish.

No text, no logo, no signage lettering, no gradient, no 3D.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, marble texture, concrete
texture, crumpled paper, torn edges, decorative patterns, geometric shapes, abstract blobs,
vignette, border frame, multiple coloured lines
```

**Variante B — lin sable et pli unique**

```text
Minimal editorial background, no photography of objects. A soft sand beige linen cloth (#EAE3D8)
stretched flat and filling the whole frame, shot straight from above. The weave is visible but very
fine. A single soft fold runs diagonally across the lower right, catching warm side light and
casting one long gentle shadow. One single thin burnt terracotta thread (#C4552B) is woven into the
lower third and is the only colour accent. Nothing else in the frame.

Composition: wide 16:9, top-down, perfectly parallel to the surface. The upper half and the central
band must stay flat, even and quiet, ready to carry a headline. No object, no prop, no border.

Rendering: 16:9 aspect ratio, largest available resolution, target 2400 x 1350 px. Warm natural side
light from the left, gentle contrast, creamy highlights, subtle film grain, fully matte.

No text, no logo, no signage lettering, no gradient, no 3D.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, embroidery, printed pattern,
tartan, stripes, heavy wrinkles, crumpled fabric, shiny satin, velvet sheen, dark shadows, vignette,
border frame
```

### C.7 · ~~`og-defaut`~~ — archive, ne plus produire

> Cette carte est composée par le code depuis la passe « studio » (§ B). Le prompt ci-dessous
> n’est conservé que comme trace de la recherche visuelle.

Carte de partage générique. Le logotype et le titre seront **incrustés par-dessus dans Figma ou
Canva**, jamais générés : le vide doit donc tomber sur la **moitié gauche**, du bord haut au bord
bas. Les réseaux recadrent : on garde 60 px de marge de sécurité sur les quatre bords.

**Variante A — papier et ombre de fenêtre**

```text
Minimal editorial background for a social share card, no photography of objects. A flat sheet of
warm ivory paper (#F6F3EE) filling the whole frame, with a very subtle fibre texture. One large soft
shadow of a window frame falls diagonally from the upper right, warm grey and fully blurred at the
edges, staying entirely inside the right half of the picture. One single thin burnt terracotta
hairline (#C4552B) crosses the lower right corner. Nothing else.

Composition: wide 1.91:1 banner. The left 45 percent of the frame is completely flat, even ivory
paper with no shadow and no texture accident — the logotype and the headline will be laid over that
area afterwards. Keep a 60 pixel empty safety margin on all four edges, because social networks crop
this image. No object, no prop, no border.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Very gentle contrast, creamy highlights, subtle film
grain, matte finish.

No text, no logo, no signage lettering, no gradient, no 3D.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, dark blue, circuit
pattern, tech motif, badge shapes, decorative frame, centred composition, busy left half, detail
touching the edges
```

**Variante B — l’angle d’une table de bois**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, ceramic. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens. Subtle film grain, gentle contrast,
creamy highlights. Calm, confident, artisanal.

Subject: the bare corner of a light wood table seen from above, with a folded sand beige linen cloth
and one small burnt terracotta ceramic dish resting on it. Nothing else. No people, no hands, no
devices.

Composition: wide 1.91:1 banner. Every object sits inside the right 45 percent of the frame. The
left 55 percent is bare, sun-lit light wood, flat and empty, crossed by one long soft shadow — the
logotype and the headline will be laid over that area afterwards. Keep a 60 pixel empty safety
margin on all four edges, because social networks crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the upper left, no
flash, no blue cast, subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, dark blue, laptops,
phones, coffee cup cliché, latte art, notebooks stacked, props filling the left half, centred
composition, detail touching the edges
```

### C.8 · ~~`og-accueil`~~ — archive, ne plus produire

> Cette carte est composée par le code depuis la passe « studio » (§ B). Le prompt ci-dessous
> n’est conservé que comme trace de la recherche visuelle.

Le lien de l’accueil dans une conversation. Même contrainte : **moitié gauche vide** pour le
logotype et l’accroche ajoutés ensuite, 60 px de marge de sécurité.

**Variante A — le comptoir au matin**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, plaster, ceramic, matte brass.
Generous empty space, off-centre composition, shallow depth of field, 50mm lens at eye level. Subtle
film grain, gentle contrast, creamy highlights. Calm, confident, artisanal.

Subject: the light wood counter of a small independent shop in Marseille before opening, empty of
customers. On the counter, a thick paper order book, a folded linen cloth and a matte brass tool.
One small burnt terracotta ceramic cup is the only colour accent. Behind, a sun-lit plaster wall,
softly out of focus.

Composition: wide 1.91:1 banner, camera at counter height. All subject detail is contained inside
the right 45 percent of the frame. The left 55 percent is a plain sun-lit ivory plaster wall,
completely empty and free of detail, crossed by one long soft window shadow — the logotype and the
headline will be laid over that area afterwards. Keep a 60 pixel empty safety margin on all four
edges, because social networks crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the left, no flash, no
blue cast. 50mm lens, aperture around f/2.8. Subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, faces, smiling models,
crowds, cash register, lit screens, price labels, hanging signs, shelves full of products, props
filling the left half, centred composition, detail touching the edges
```

**Variante B — la rue, très ouverte**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
afternoon, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand
beige #EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent
(#C4552B). Matte natural materials only: painted plaster, light wood, linen awning, worn stone.
Generous empty space, off-centre composition, shallow depth of field, 35mm lens at eye level. Subtle
film grain, gentle contrast, creamy highlights. Calm, confident, artisanal.

Subject: a quiet Marseille street corner with one small shopfront, light wood frame, plain unmarked
linen awning, seen slightly from the side from the opposite pavement. No people, no cars, nothing
readable. One burnt terracotta pot beside the door is the only colour accent.

Composition: wide 1.91:1 banner. The shopfront sits entirely inside the right 45 percent of the
frame. The left 55 percent is a plain sun-lit ivory plaster wall, flat and empty, with one long
diagonal shadow — the logotype and the headline will be laid over that area afterwards. Keep a 60
pixel empty safety margin on all four edges, because social networks crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Low warm side light from the left, late afternoon, no
flash, no blue cast. 35mm lens, aperture around f/4. Subtle film grain, creamy highlights, gentle
contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, shop signs, menu
boards, street plates, licence plates, parked cars, scooters, crowds, overhead cables, graffiti,
harbour postcard, saturated blue sky, props filling the left half
```

### C.9 · ~~`og-services`~~ — archive, ne plus produire

> Cette carte est composée par le code depuis la passe « studio » (§ B). Le prompt ci-dessous
> n’est conservé que comme trace de la recherche visuelle.

La page Services parle de chantiers datés et de devis lisibles. On montre du **papier**, pas une
liste de prestations. **Moitié gauche vide**, 60 px de marge de sécurité.

**Variante A — le dossier posé**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty
space, off-centre composition, shallow depth of field, 50mm lens. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: a thick paper folder, closed, cream coloured and slightly textured, lying on a light wood
table, with a matte brass pen resting across it and a folded sand beige linen cloth beside. The
folder is completely blank, with no printing and no label. One small burnt terracotta ceramic dish
is the only colour accent. No people, no hands, no devices.

Composition: wide 1.91:1 banner, camera slightly above the table. All objects are contained inside
the right 45 percent of the frame. The left 55 percent is bare, sun-lit light wood, flat and empty,
crossed by one long soft shadow — the logotype and the headline will be laid over that area
afterwards. Keep a 60 pixel empty safety margin on all four edges, because social networks crop this
image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the upper left, no
flash, no blue cast. 50mm lens, aperture around f/3.5. Subtle film grain, creamy highlights, gentle
contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, printed documents,
invoices, contracts with visible lines, spreadsheets, charts, laptops, screens, ring binders, office
supplies clutter, props filling the left half, centred composition
```

**Variante B — les quatre outils alignés**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty
space, off-centre composition, shallow depth of field, 50mm lens. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: four simple hand tools laid side by side in a neat row on a soft sand beige linen cloth,
seen from directly above: a wooden folding ruler, a matte brass pencil, a small flat brush and a
folded thick paper sheet. Each object is separated by a clear gap. One burnt terracotta ceramic
button-sized detail is the only colour accent. No people, no hands.

Composition: wide 1.91:1 banner, top-down. The row of tools occupies the right 45 percent of the
frame and runs vertically, not horizontally. The left 55 percent is bare linen, flat and empty, with
one long soft shadow — the logotype and the headline will be laid over that area afterwards. Keep a
60 pixel empty safety margin on all four edges, because social networks crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the left, no flash, no
blue cast. 50mm lens, aperture around f/5.6, all four objects evenly sharp. Subtle film grain,
creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, knolling grid, dozens
of objects, symmetrical centred layout, measuring marks on the ruler, engraved brand names, shiny
metal, dark background, props filling the left half
```

### C.10 · ~~`og-about`~~ — archive, ne plus produire

> Cette carte est composée par le code depuis la passe « studio » (§ B). Le prompt ci-dessous
> n’est conservé que comme trace de la recherche visuelle.

Le studio comme lieu, sans personne. **Moitié gauche vide**, 60 px de marge de sécurité.

**Variante A — la table et la chaise**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, plaster, ceramic. Generous empty
space, off-centre composition, shallow depth of field, 35mm lens at eye level. Subtle film grain,
gentle contrast, creamy highlights. Calm, confident, artisanal.

Subject: a corner of a small studio in a plain plaster-walled Marseille room: a light wood table
against the wall, one simple wooden chair pushed slightly back, a thick paper notebook closed on the
table. One burnt terracotta ceramic cup is the only colour accent. Empty of people, no screens, no
cables.

Composition: wide 1.91:1 banner, camera at eye level. The table and chair are contained inside the
right 45 percent of the frame. The left 55 percent is bare sun-lit plaster wall, flat and empty,
crossed by one long soft window shadow — the logotype and the headline will be laid over that area
afterwards. Keep a 60 pixel empty safety margin on all four edges, because social networks crop this
image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the left, no flash, no
blue cast. 35mm lens, aperture around f/3.5. Subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, people, team photo,
faces, office chairs, monitors, keyboards, cables, framed posters, wall art, motivational quotes,
open-space background, props filling the left half
```

**Variante B — l’ombre de la fenêtre sur le mur nu**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
afternoon, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: plaster, light wood, ceramic. Generous empty space, off-centre
composition, shallow depth of field, 35mm lens at eye level. Subtle film grain, gentle contrast,
creamy highlights. Calm, confident, artisanal.

Subject: an almost empty room used as a studio. A tall old window on the far right throws a long
geometric shadow across a bare warm ivory plaster wall and a light wood floor. Low in the frame,
against the wall, a single wooden stool carries one burnt terracotta ceramic bowl — the only colour
accent. Nothing else, no people.

Composition: wide 1.91:1 banner, camera at eye level. The window, stool and bowl sit inside the
right 45 percent of the frame. The left 55 percent is bare wall and floor, flat and empty apart from
the tail of one soft shadow — the logotype and the headline will be laid over that area afterwards.
Keep a 60 pixel empty safety margin on all four edges, because social networks crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Low warm side light from the right, late afternoon,
no flash, no blue cast. 35mm lens, aperture around f/4. Subtle film grain, creamy highlights, gentle
contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, people, silhouettes,
furniture sets, patterned rug, curtains, radiator, power sockets, visible light fixtures, hard black
shadows, vignetting, props filling the left half
```

### C.11 · ~~`og-contact`~~ — archive, ne plus produire

> Cette carte est composée par le code depuis la passe « studio » (§ B). Le prompt ci-dessous
> n’est conservé que comme trace de la recherche visuelle.

L’invitation à écrire. **Moitié gauche vide**, 60 px de marge de sécurité.

**Variante A — le papier, le stylo, le lin**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, ceramic, matte brass. Generous empty
space, off-centre composition, shallow depth of field, 50mm lens. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: a single sheet of thick cream paper, completely blank, lying on a soft sand beige linen
cloth over a light wood table, seen from directly above. A matte brass pen rests beside it and a
modern smartphone lies face down with its screen off. One small burnt terracotta ceramic dish is the
only colour accent. No people, no hands.

Composition: wide 1.91:1 banner, top-down. Every object is contained inside the right 45 percent of
the frame. The left 55 percent is bare linen and wood, flat and empty, crossed by one long soft
shadow — the logotype and the headline will be laid over that area afterwards. Keep a 60 pixel empty
safety margin on all four edges, because social networks crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the upper left, no
flash, no blue cast. 50mm lens, aperture around f/4. Subtle film grain, creamy highlights, gentle
contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, handwriting, printed
lines, envelope stamps, mail icons, glowing phone screen, notification badges, coffee cup cliché,
props filling the left half, centred composition
```

**Variante B — la main qui tend la feuille**

```text
Editorial photography in a warm minimalist style, for a social share card. Natural side light, late
morning, soft long shadows. Warm ivory and sand beige palette (warm ivory #F6F3EE, soft sand beige
#EAE3D8), deep warm brown-black accents (#17130F), one single burnt terracotta accent (#C4552B).
Matte natural materials only: light wood, linen, thick paper, ceramic. Generous empty space,
off-centre composition, shallow depth of field, 50mm lens at eye level. Subtle film grain, gentle
contrast, creamy highlights. Calm, confident, artisanal.

Subject: one hand, seen from the wrist only, laying a blank sheet of thick cream paper down on a
light wood table. No face, no body, no second person. The sheet is completely blank. A folded sand
beige linen cloth and one small burnt terracotta ceramic dish are the only other elements, the dish
being the single colour accent.

Composition: wide 1.91:1 banner, camera slightly above the table. The hand and the sheet are
contained inside the right 45 percent of the frame. The left 55 percent is bare, sun-lit light wood,
flat and empty, crossed by one long soft shadow — the logotype and the headline will be laid over
that area afterwards. Keep a 60 pixel empty safety margin on all four edges, because social networks
crop this image.

Rendering: 1.91:1 aspect ratio, 1200 x 630 px. Warm natural side light from the left, no flash, no
blue cast. 50mm lens, aperture around f/2.8. Subtle film grain, creamy highlights, gentle contrast.

No text, no logo, no signage lettering.
```

```text
Negative prompt: neon, blue tech glow, circuit board, futuristic city, hologram, gradient
background, lens flare, glass morphism, 3D render, stock-photo businessmen, handshake in suits,
rising bar chart, cluttered layout, drop shadows, chrome, glossy plastic, saturated filter, teal and
orange grade, emoji, watermark, distorted text, gibberish letters, navy blue, extra fingers, six
fingers, deformed hand, merged fingers, two hands shaking, face, portrait, sleeve of a business
suit, wristwatch branding, handwriting on the sheet, props filling the left half
```

### C.12 · `icones` — aucun prompt

Le favicon et les icônes PWA sont **le logotype**. Le § 4 de la charte est sans appel : on ne demande
jamais le logo à un modèle d’image. Les icônes se produisent à partir du fichier existant
`app/icon.svg` (monogramme `13`, carré arrondi, encre `#17130F` sur ivoire) :

```bash
node -e "require('sharp')('app/icon.svg',{density:600}).resize(512,512).png().toFile('public/icons/icon-512.png')"
node -e "require('sharp')('app/icon.svg',{density:600}).resize(192,192).png().toFile('public/icons/icon-192.png')"
node -e "require('sharp')('app/icon.svg',{density:600}).resize(512,512).png().toFile('public/icons/icon-maskable-512.png')"
node -e "require('sharp')('app/icon.svg',{density:600}).resize(180,180).png().toFile('app/apple-icon.png')"
```

> Ces quatre PNG sont livrés et versionnés : la règle `*.png` du `.gitignore` a été ancrée en
> `/*.png`, elle ne vise plus que les captures déposées à la racine du dépôt.
>
> `app/apple-icon.png` et `app/icon.svg` sont des conventions de fichier de Next : il pose
> lui-même les balises `<link>` correspondantes. Les trois PNG de `public/icons/` sont déclarés
> par `app/manifest.ts`, et `icon-512.png` sert aussi de `logo` au nœud JSON-LD `Organization`.

---

## D · Contrôle qualité

Huit vérifications avant qu’une image entre dans `public/images/`. Une seule qui échoue et on
régénère — on ne retouche pas, on recommence.

| # | Point | Comment on tranche |
| --- | --- | --- |
| 1 | **Dominante colorimétrique** | Pipette sur trois zones claires : on doit lire de l’ivoire ou du sable (proches de `#F6F3EE` / `#EAE3D8`). Un gris bleuté ou un virage bleu-orange = refus. |
| 2 | **Règle des trois terres cuites** | Une seule tache `#C4552B` dans l’image. Puis on regarde l’écran assemblé : au-delà de trois occurrences avec le bouton et le point du logo, on en retire une. |
| 3 | **Texte parasite** | Zoom 200 % sur les enseignes, étiquettes, dos de carnet, écrans. Une seule lettre inventée = refus, ce sont toujours des lettres fausses. |
| 4 | **Anatomie et géométrie** | Doigts comptés un par un, articulations, manches. Puis les objets : un mètre pliant qui se replie mal ou un pied de table impossible se voient autant qu’une main à six doigts. |
| 5 | **Netteté de la zone de vide** | La zone calme annoncée dans le prompt doit être vraiment vide et vraiment propre : pas d’objet fantôme, pas de bavure, pas d’ombre sale. C’est là que le titre viendra. |
| 6 | **Grain et bruit** | Grain argentique fin et régulier, hautes lumières crémeuses. Un bruit numérique en damier dans les ombres, ou une peau/matière lissée en plastique = refus. |
| 7 | **Poids et dimensions** | Conformes au tableau B.2 après conversion. Au-dessus du plafond, on baisse la qualité JPEG de 82 à 78 — jamais les dimensions. |
| 8 | **Le test de la charte** | *Est-ce que ce visuel pourrait être l’affiche d’un bon restaurant ?* Si oui, c’est du WebTreize. S’il ressemble à une publicité de logiciel, on recommence. |

---

## E · Intégration technique

### E.1 · Où déposer

Un seul dossier : `public/images/`. Un fichier par identifiant du tableau B, en minuscules, sans
accent ni espace, mots séparés par un tiret, extension `.jpg`.

```
public/images/hero-atelier.jpg
public/images/craft-site.jpg
public/images/craft-visibilite.jpg
public/images/craft-outils.jpg
public/images/about-atelier.jpg
public/images/fond-aplat.jpg
```

Les fichiers d’origine sortis de ChatGPT restent sur le disque du client, hors du dépôt : ils sont
trop lourds et n’ont aucune raison d’être versionnés.

### E.2 · Convertir

`sharp` est déjà une dépendance du projet : aucune installation. Depuis la racine du dépôt.

```bash
# Plaque héro — 2400 px de large
node -e "require('sharp')('C:/masters/hero-atelier.png').resize(2400).jpeg({quality:82,mozjpeg:true,chromaSubsampling:'4:4:4'}).toFile('public/images/hero-atelier.jpg')"

# Plaques 4/3 et 3/4 — 1600 px sur le grand côté
node -e "require('sharp')('C:/masters/craft-site.png').resize(1600).jpeg({quality:82,mozjpeg:true}).toFile('public/images/craft-site.jpg')"

# Contrôle du poids
node -e "const fs=require('fs');fs.readdirSync('public/images').filter(f=>/\.(jpg|avif|webp)$/.test(f)).forEach(f=>console.log((fs.statSync('public/images/'+f).size/1024).toFixed(0).padStart(5)+' ko  '+f))"
```

Sans Node, l’équivalent ffmpeg :

```bash
ffmpeg -i hero-atelier.png -vf scale=2400:-1 -q:v 3 public/images/hero-atelier.jpg
```

### E.3 · Le composant est déjà prêt

`components/ui/Plate.tsx` remplace l’ancienne classe CSS `.plate`, supprimée depuis. Sans `src`, il
affiche un cadrage de studio en attente ; avec `src`, il sert la photo via `next/image` (`fill`,
`sizes`, `priority` à la demande). Le ratio est posé en `aspect-ratio` : aucun décalage de mise en
page.

Le fondu de chargement n’est pas écrit dans le composant : il est décrit en CSS sous `html.js`
(`app/globals.css`, sélecteur `[data-plate-image]`) et neutralisé sous `prefers-reduced-motion`.
Sans JavaScript, aucun voile n’est posé — un `opacity-0` levé par `onLoad` laissait sinon les photos
invisibles pour toujours dans le HTML servi.

```tsx
type PlateProps =
  | (PlateCommonProps & { src: string; alt: string })
  | (PlateCommonProps & { src?: undefined; alt?: never });

type PlateCommonProps = {
  ratio?: '16/9' | '4/3' | '1/1' | '3/4';   // défaut '4/3'
  priority?: boolean;                        // défaut false — réservé au LCP
  sizes?: string;                            // défaut '100vw'
  caption?: string;                          // libellé du cadrage en attente
  className?: string;
};
```

Le type est discriminé : `<Plate src="…" />` sans `alt` **ne compile pas**. Une image décorative
passe `alt=""` explicitement.

**Les trois plaques de l’accueil** sont posées, et se branchent uniquement par la donnée, dans
`lib/data/site.ts` :

```ts
{
  id: 'site',
  // …
  imageSrc: '/images/craft-site.jpg',
  imageAlt: 'Un téléphone posé à plat sur le comptoir en bois clair d’un commerce, à côté d’un carnet de commandes ouvert.',
}
```

Tant que `imageSrc` est absent, `CraftSection` affiche le cadrage en attente. Dès qu’il est
renseigné, la photo prend sa place, avec le bon `sizes`. Aucune autre modification.

**La plaque héro** est montée dans `components/sections/HeroSection.tsx`, seule plaque du site à
porter `priority`. **`about-atelier`** est montée dans `app/about/page.tsx`.

**`fond-aplat`** n’est montée nulle part. Le jour où on la pose :

```tsx
<Plate
  src="/images/fond-aplat.jpg"
  alt=""
  ratio="16/9"
  sizes="100vw"
/>
```

### E.4 · Ce qui a été repris ailleurs

Ces cinq points étaient en attente chez d’autres intervenants au moment où ce document a été écrit.
Ils sont tous traités ; ils restent listés pour que personne ne les rouvre.

1. **`public/og-image.jpg` a disparu.** Fond bleu marine, monogramme « W13 » tracé en pistes de
   circuit imprimé, flèche qui monte : trois des interdits nommés au § 1 de la charte réunis sur une
   seule image. Les cartes de partage sont désormais composées par le code (§ B), et le JSON-LD
   `Organization.logo` pointe `public/icons/icon-512.png`.
2. **`public/logo.svg`, `public/logo.png` et `public/manifest.json` ont été supprimés.** Le manifeste
   est un fichier typé, `app/manifest.ts`, aux couleurs de la charte — `theme_color` et
   `background_color` en ivoire `#f6f3ee`, alignés sur le `viewport.themeColor` du layout racine. Le
   monogramme à jour est `app/icon.svg`, en tracés et non en texte.
3. **`next.config.ts` sert l’AVIF.** `images.formats: ['image/avif', 'image/webp']` est en place.
4. **`.gitignore` n’ignore plus que la racine.** La règle est ancrée en `/*.png` et `/*.jpg` : elle
   ne vise plus que les captures d’audit déposées à la racine du dépôt, et laisse passer les actifs
   de marque de `public/` et de `app/`.
5. **La classe `.plate` a été supprimée de `app/globals.css`.** `components/ui/Plate.tsx` est la
   source unique de la figure. `.plate-container` reste, employée par `HeroSection`.

### E.5 · Garder la constance

Le § 8 de la charte le dit : la façon la plus fiable de rester constant est de **réinjecter une
image validée en référence** dans la conversation suivante. Dès qu’une image passe les huit points
du § D, on la garde comme image de style pour toutes les suivantes. C’est ce qui fait qu’onze
images générées séparément finissent par ressembler à une seule série.
