# WebTreize — passer au niveau supérieur

> Comparaison levupp.com / webtreize.com et spécification d’améliorations.
> Rédigé le 30 septembre 2026 à partir des deux sites **en ligne**, capturés en 1440 et 390 px.
> **Autorité : `docs/charte-graphique.md`.** Rien de ce qui suit ne la contredit. Quand levupp fait
> quelque chose que la charte interdit, c’est écrit en toutes lettres et ce n’est pas repris.

## Sources

| Quoi | Où |
| --- | --- |
| levupp, écran par écran (défilement réel, animations jouées) | `design/maquettes/_references/levupp/audit/ecrans/{accueil,services,agence,portfolio}-{1440,390}-NN.png` |
| levupp, plan des titres mesuré (taille, graisse, alignement, position) | `design/maquettes/_references/levupp/audit/levupp-structure.json` |
| WebTreize en ligne, écran par écran | `design/maquettes/_references/webtreize/audit/ecrans/{accueil,services,realisations,about,contact}-{1440,390}-NN.png` |
| WebTreize, plan des titres, texte de `main` | `design/maquettes/_references/webtreize/audit/webtreize-structure.json` |
| Pages entières (attention : les titres animés au défilement y apparaissent coupés, ne pas s’y fier pour les titres) | `design/maquettes/_references/{levupp,webtreize}/audit/*-full.png` et `tranches/` |
| Mesures des sections (hauteurs, fonds, nombre de mots) | `design/maquettes/_references/audit-report.json` |

---

## 0 · En une page

**Ce qui sépare les deux sites, ce n’est pas la quantité de texte** : l’accueil de levupp compte 794 mots,
celui de WebTreize 635. Les deux pages ont à peu près la même longueur (7 550 px contre 8 623 px en 1440).
La différence vient de **la façon dont le contenu est présenté** :

1. **Levupp a une grammaire, WebTreize en a quatre.** Chaque section de levupp suit le même schéma :
   un titre court et centré, un objet visuel, un petit bouton en pilule. WebTreize alterne titres
   centrés et titres alignés à gauche, sur trois tailles de H2 différentes (22, 54 et 60 px, plus 76 px
   pour l’audit), avec des titres de 6 à 8 mots.
2. **Chez WebTreize, tout est texte posé sur le fond ; chez levupp, tout est rangé dans des objets.**
   Levupp range tout dans des surfaces arrondies (cartes, bento, grilles d’avis, tarifs). WebTreize
   n’a que des paragraphes et des filets. La charte autorise pourtant les **encarts** (blanc chaud) et
   les **aplats** (sable) : c’est le levier principal, et il n’enfreint rien.
3. **Les preuves arrivent trop tard, ou pas du tout.** Chez levupp, les logos clients sont juste sous
   le héros, suivis des projets, des avis, de l’équipe et des chiffres. Chez WebTreize, la première
   preuve (les réalisations) apparaît à 3 900 px. Pas de visage, pas de nom, aucun chiffre, alors que
   des faits vrais existent (4 projets livrés, 1 seul interlocuteur, le code rendu au client, Marseille).
4. **Navigation et appels à l’action dispersés.** WebTreize a une barre pleine largeur, deux pilules
   en mobile (« Audit gratuit » et « Menu ») et six libellés d’action différents. Levupp a une pilule
   flottante, une action principale, des actions secondaires identiques entre elles, et chaque page
   finit par le même bloc d’appel et la même carte « Un projet ? » dans le pied de page.
   L’accueil de WebTreize finit sur la FAQ, sans appel.
5. **Les pages internes sont des pages de texte.** `/services` aligne quatre blocs de texte, sans
   image, sans projet lié, sans FAQ et sans rien sur le prix. Le formulaire de `/contact` commence
   sous la ligne de flottaison, avec une colonne de gauche vide. `/about` ne montre ni visage ni nom.

**Plan d’accueil cible** (6 sections + 1 conditionnelle, contre 10 blocs aujourd’hui) :

1. Héros : « Votre savoir-faire mérite d’être trouvé. », suivi d’une ligne de preuve (les vrais noms des clients)
2. « Ce que nous faisons. » : 3 encarts
3. « Quelques réalisations. » : 3 cartes (refonte en cours, autre développeur)
4. *(conditionnel)* « Ce qu’ils en disent. » : uniquement s’il existe de vrais avis
5. « Le studio, en vrai. » : bento de faits vrais
6. « Vos questions. » : FAQ
7. « Ce qui vous freine, par écrit. » : bloc sombre d’audit, qui devient l’appel final
8. Pied de page : une carte, avec « Un projet ? »

**P0** : (1) une grammaire de section unique, avec le composant `SectionHead` ; (2) les encarts et un
fond ivoire continu ; (3) la restructuration de l’accueil selon le plan ci-dessus ; (4) la navigation
en pilule flottante et un vocabulaire d’action unifié ; (5) un héros resserré avec la ligne de preuve ;
(6) le pied de page en carte, avec « Un projet ? ».

---

## 1 · Ce qui rend levupp beau, concrètement

### 1.1 Le rythme : une seule phrase musicale, répétée six fois

L’accueil de levupp enchaîne six sections, toutes construites de la même façon :

| Titre (H2, 46 px / 600, centré) | Mots | Objet | Bouton |
| --- | --- | --- | --- |
| Trois services, une offre. | 4 | trois cartes en éventail | — |
| À vous de juger. | 4 | 3 couvertures de projet | « Voir tous les projets » |
| Voilà ce qui se dit. | 5 | mur d’avis en 3 colonnes, fondu en bas | « Voir plus » |
| Enchantés, nous c’est Levupp. | 5 | bento : photo d’équipe, carte de Marseille, outils, 2019, +100 | « Réserver un appel » |
| Des tarifs clairs. | 3 | 3 cartes de prix, celle du centre surélevée | « Choisir cette offre » |
| Le niveau supérieur, ça vous tente ? | 6 | (étiquette « RENCONTRONS-NOUS ») | « Demande de projet » |

- **Titre, objet, bouton.** Aucune section n’ajoute de paragraphe d’introduction sous son titre.
  Le texte se trouve dans les objets (avis, cartes de prix), jamais en vrac.
- **Chaque section occupe à peu près un écran** : 800 à 1 270 px entre deux H2 en 1440. On lit la
  page en ne lisant que les titres.
- **Trois niveaux typographiques seulement** : H1 110 px / 500, H2 46 px / 600, H3 22 à 32 px / 600.
  Pas d’étiquette (eyebrow) sur l’accueil, sauf pour le bloc final.
- **Un fond continu.** Pas de bandes de couleur alternées : la variété vient des objets, pas du fond.

### 1.2 La navigation en pilule

- En haut de page, c’est une barre pleine largeur et transparente : logo à gauche, **3 liens** au
  centre (Services, Portfolio, Agence), **1 bouton** plein à droite (« Se rencontrer »).
- Dès qu’on défile, elle se replie en **pilule centrée d’environ 800 × 74 px**, posée à 20 px du haut,
  avec un filet de 1 px et un fond presque opaque. Le contenu passe dessous.
  (`ecrans/accueil-1440-01.png` et suivants.)
- En mobile, la pilule ne contient que le logo et un bouton menu (`ecrans/accueil-390-03.png`).

### 1.3 Les cartes

Rayon constant (16 à 20 px), marge intérieure constante (environ 30 px), même traitement partout :
couvertures de projet avec un nom en 22 px / 600 et des catégories en gris ; avis en maçonnerie ;
bento de l’agence ; tarifs. C’est cette **répétition d’un même objet** qui donne l’impression d’un
système maîtrisé.

### 1.4 Le mouvement

Mot du héros qui tourne (« en mieux », « plus fluide »), cartes de services en éventail, bande de logos
qui défile, bande d’écrans mobiles sur `/services`, apparitions au défilement, barre qui se replie en
pilule. **Défaut constaté** : le contenu est caché tant qu’il n’a pas été révélé. Sur nos captures
pleine page, des titres et le pied de page entier sont vides (`tranches/accueil-1440-05.png`).
WebTreize ne cache jamais rien sans JavaScript ; il faut garder cette doctrine.

### 1.5 La cohérence des appels à l’action

- **Une** action principale (« Se rencontrer », « Demande de projet », « Planifier un appel » : même
  intention, formulée pour un rendez-vous).
- Toutes les actions secondaires ont **la même forme** : petite pilule d’environ 42 px de haut, contour
  sombre, centrée sous l’objet.
- **Chaque page finit pareil** : le bloc « RENCONTRONS-NOUS / Le niveau supérieur, ça vous tente ? /
  Demande de projet », puis le pied de page.

### 1.6 Le pied de page

Une **carte** arrondie et bordée, en trois colonnes : coordonnées et bureaux ; logo, signature et
réseaux ; « Un projet ? » avec un bouton et un lien texte. En dessous, la lettre d’information, puis
une ligne avec © et les liens. Le pied de page est lui-même un dernier appel.

### 1.7 Les preuves

Logos clients sous le héros (7), au moins 8 avis étoilés, photo des trois associés, carte de Marseille,
chiffres (« 2019 », « +100 projets »), tarifs publics, index du portfolio (« Index des projets 110 »).
Sur `/agence`, chaque fondateur a un portrait et une citation signée.

### 1.8 Le parcours vers le contact

Le bouton de la navigation est toujours visible. Chaque section propose une suite. Les tarifs mènent à
« Choisir cette offre ». Le bloc final et la carte du pied de page se répètent sur toutes les pages.
Où qu’on soit, le prochain pas est à moins d’un écran.

### 1.9 Transposable / non transposable

| Ce que fait levupp | WebTreize | Pourquoi |
| --- | --- | --- |
| Grammaire titre court, objet, bouton | **Oui** | Structure, pas style. |
| Une seule taille de H2, centrée | **Oui** | Plus Jakarta Sans 800 à −0,05em (charte §3). |
| Navigation qui se replie en pilule | **Oui** | En blanc chaud opaque et filet `line`, **sans flou ni verre** (le négatif de la charte range « glass morphism » parmi les interdits). |
| Cartes et bento | **Oui, en « encarts »** | La charte donne le blanc chaud aux « encarts, respiration » et le sable aux « aplats, blocs image ». Pas de bordure, pas d’ombre (charte §5 : « filets fins plutôt que cadres »). |
| Preuves sous le héros | **Oui, avec les vrais noms** | 4 projets publiés. Noms composés en caractères, pas de mur de logos. |
| Chiffres | **Oui, seulement vrais** | En Newsreader 300, la charte réservant Newsreader « aux grands chiffres ». |
| Même bloc d’appel en fin de page, carte « Un projet ? » | **Oui** | C’est du parcours, pas du style. |
| FAQ par service sur `/services`, livrables en étiquettes | **Oui** | Contenu réel à écrire par le studio. |
| Paragraphe en deux tons (première phrase en encre, suite en gris) | **Oui** | `text-ink` puis `text-ink-muted`, deux couleurs de la charte. |
| Thème sombre, vert néon, grille de fond, halos | **Non** | Charte : ivoire dominant, une seule couleur vive (terre cuite), pas de dégradé. |
| Cartes en éventail « 3D », verre, lueurs | **Non** | Négatif de la charte : « 3D render, glass morphism, gradient ». |
| Mur de 7 logos, 8 avis étoilés | **Non, pas en l’état** | WebTreize n’a pas d’avis publiés (`lib/data/temoignages.ts` est vide). Un mur de 4 noms serait maigre, en inventer serait mentir. |
| Tarifs publics chiffrés | **Non, pas en l’état** | Aucun tarif n’est arrêté. On prépare une structure prête à recevoir les vrais montants (voir P1-1). |
| « 2 places pour le printemps » | **Seulement si c’est vrai** | Une disponibilité réelle, saisie par le studio. Sinon rien (P2-5). |
| Photo d’équipe souriante | **Non** | Charte §5 : visages entiers rares, « jamais souriants à la caméra ». |
| Mot qui tourne dans le H1 | **Non** | Le H1 est l’élément LCP, et ce serait un gadget. |
| Contenu caché jusqu’au défilement | **Non** | Voir §1.4. |
| Lettre d’information | **Non** | Il n’y en a pas. |

---

## 2 · Audit de WebTreize en ligne, section par section

Mesures prises en 1440 × 900 sur www.webtreize.com le 30/09/2026 (`audit-report.json`,
`webtreize-structure.json`).

### 2.1 Accueil : 5,5/10

Hauteur : 8 623 px. **10 blocs** (levupp : 6). Alignement des titres, dans l’ordre : centré, centré,
gauche ×3, centré, centré, gauche, centré, gauche. Tailles de H2 : 22, 54, 60 et 76 px.

| Section | Note | Ce qui fait amateur ou lourd par rapport à levupp |
| --- | --- | --- |
| **Header** | 6 | Propre, mais générique : barre pleine largeur avec 4 liens et un bouton. En 390 px, logo, pilule contour « Audit gratuit » et pilule pleine « Menu » se disputent 350 px (`ecrans/accueil-390-00.png`). Le point du logotype se détache du mot (`gap-px` et approche −0,045em), alors que la charte veut qu’il ferme le mot « comme on termine une phrase ». |
| **Héros** | 7 | Le H1 et la photo sont les meilleurs éléments du site. Mais on empile 5 couches : étiquette, H1, chapô de 30 mots, 2 appels, mention. Le lien « Découvrir notre approche » en terre cuite consomme une des 3 terres cuites de l’écran pour un lien secondaire. **Aucune preuve** avant la photo. En 390 px, le H1 se coupe en « savoir– / faire ». |
| **Approche** | 4 | Un H2 de 22 px en `ink-muted` posé au-dessus d’une citation Newsreader de 54 px : deux titres qui se neutralisent, le H2 ressemble à une légende. Puis un paragraphe centré de 38 mots, coupé en « introu-/vables ». 670 px pour un slogan, sans objet. Levupp n’a pas de section slogan. |
| **Ce que nous faisons** (3 blocs en zigzag) | 5 | Le zigzag photo/texte est le motif le plus « gabarit » du web. 3 blocs d’environ 470 px, titres de 7 à 8 mots, étiquettes répétées. Les photos sont des ambiances : elles n’illustrent rien de précis. Le contenu redit `/services`. Environ 1 470 px au total. |
| **Réalisations** | 7 | Refonte en cours (cartes à couverture). Déjà au bon niveau. Le bouton « Voir toutes les réalisations (4) » fait 330 × 52 px, bordé : trop gros pour une action secondaire. |
| **Promesses** | 5 | Titre de 8 mots. 3 colonnes de texte sous filets, puis juste après… |
| **Méthode** | 5 | … 4 colonnes de texte sous filets, avec un titre aligné à gauche après un titre centré. Deux grilles de texte identiques à la suite : c’est le moment le plus monotone de la page. |
| **Audit** (bloc sombre) | 8 | La meilleure section : un objet (la fiche d’audit) et une action. Mais trois lignes de texte suivent le bouton (courriel, zone, horaires), et le bloc arrive **avant** la FAQ : la page ne se termine pas sur la conversion. |
| **FAQ** | 6 | Quatre bonnes questions. Mais la colonne fait 800 px, calée à gauche, la moitié droite de l’écran est vide. Le signe « → » évoque un lien qui emmène ailleurs, pas un dépliant. La page finit ici, sans appel. |
| **Pied de page** | 5 | Complet mais plat : une colonne « L’accueil » d’ancres internes (du bruit), pas de « Un projet ? », Snapchat en réseau principal, et le © seul sur sa ligne. |

### 2.2 Pages internes

| Page | Note | Constat |
| --- | --- | --- |
| **/services** | 4 | En-tête aligné à gauche (l’accueil est centré : ce ne sont pas les mêmes pages). Quatre blocs « titre / paragraphe / liste sous filets », **aucune image, aucun projet lié, aucune FAQ, rien sur le prix**. Il reste du jargon (« Core Web Vitals »). La page finit sur « Commençons simplement. », une invitation sans contenu. Levupp (`ecrans/services-1440-03.png` et `-04.png`) : titre, paragraphe en deux tons, étiquettes de livrables, FAQ par service. |
| **/realisations** | 7 | Déjà refaite (index compté, filtres, couvertures). 6 filtres pour 4 projets, dont 4 filtres à 1 projet : trop de choix pour si peu. Voir P2-3, à transmettre au développeur en charge. |
| **/about** | 5 | Aucun visage, aucun nom, alors que la promesse centrale est « un seul interlocuteur ». La citation « Un petit studio, volontairement. » fonctionne. Trois paragraphes (132 mots) dans « Où nous sommes ». La grille « Trois choses que vous ne verrez jamais ici » reprend la forme des Promesses de l’accueil. La section « Du lundi au vendredi » fait doublon avec /contact et le pied de page. |
| **/contact** | 6 | En 1440, **le formulaire commence à y ≈ 670 px** : un en-tête de 445 px le repousse. La colonne de gauche est vide sous trois lignes. « Trois champs obligatoires. » est une consigne de formulaire, pas un titre. La section des coordonnées reprend celle de /about. |

### 2.3 Défauts transversaux

- **Six libellés d’action** pour deux intentions : « Audit gratuit », « Commencer par un audit »,
  « Demander mon audit », « Découvrir notre approche », « Voir toutes les réalisations (4) »,
  « Envoyer ma demande ».
- **Césure automatique** sur les chapôs centrés : « introu-/vables », « lo-/cal », « écou-/tons »,
  « ré-/pondons » (`p, li { hyphens: auto }` dans `app/globals.css`).
- **Ponctuation finale détachée** dans les grands titres (« trouvé . », « portfolio . »,
  « d’ être ») : l’interlettrage de −0,05em resserre les lettres, pas l’approche du point et de
  l’apostrophe (`audit/zoom-h1.png`).
- **Des bandes de fond alternées** (ivoire, blanc chaud, ivoire…) remplacent les objets : c’est ce
  qui donne à l’accueil son côté « long document ».

---

## 3 · Spécification priorisée

Conventions : classes et jetons existants (`tailwind.config.ts`, `app/globals.css`). Les nouveaux
jetons sont signalés **[nouveau]**. Toute animation passe par les durées `micro/state/reveal/long` et
les courbes `out/swap`. Toute animation pilotée par le défilement est enveloppée dans
`@media (prefers-reduced-motion: no-preference)` (règle déjà écrite en tête de la section
« Mouvement piloté par le défilement » de `globals.css`).

**Règles d’écriture, valables partout :**

| Élément | Longueur maximale |
| --- | --- |
| H2 de section | 6 mots |
| H3 d’encart | 5 mots |
| Chapô de section | 20 mots, ou rien |
| Texte d’encart | 20 mots |
| Chapô du héros | 20 mots |

---

### P0-1 · Une seule grammaire de section : `SectionHead`

**Fichier nouveau** : `components/sections/SectionHead.tsx` (composant serveur).

```tsx
type SectionHeadProps = {
  id: string;            // id du h2, pour aria-labelledby
  title: string;         // ≤ 6 mots
  eyebrow?: string;      // rare : réservé au bloc d’audit et aux pages internes
  lede?: string;         // ≤ 20 mots
  className?: string;
};
```

Rendu :

```html
<Reveal className="mx-auto max-w-[44rem] text-center">
  {eyebrow && <p class="eyebrow">…</p>}
  <h2 id class="sweep mx-auto mt-gap-xs max-w-[18ch] text-display-sm font-extrabold">…</h2>
  {lede && <p class="lede mx-auto mt-gap-sm max-w-[44ch]">…</p>}
</Reveal>
```

- **Une seule taille** de H2 de section sur tout le site : `text-display-sm` (30 → 54 px). Le H1
  garde `text-display-xl` sur l’accueil et `text-display-lg` sur les pages internes.
  `text-display-md` n’est plus utilisé pour les titres de section ; `text-display-lg` reste réservé
  au H2 du bloc d’audit, le point culminant de la page.
- Titre toujours centré. L’objet suit à `mt-gap-lg`. Le bouton secondaire suit l’objet à
  `mt-gap-lg`, centré.
- Mobile : identique, le titre équilibré (`text-wrap: balance` est déjà posé sur `h2`).
- Mouvement : `sweep` (découverte au défilement, déjà en place) et `Reveal` sur le chapô, avec
  `delay={60}`. Avec `prefers-reduced-motion: reduce`, rien ne bouge ; c’est déjà garanti par
  `globals.css`.

### P0-2 · Les encarts, et un fond ivoire continu

**Fichier** : `app/globals.css`, couche `components`.

```css
/* Encart — la surface de la charte (« Blanc chaud : encarts, respiration »).
   Pas de bordure, pas d’ombre : c’est un aplat sur l’ivoire, pas un cadre. */
.encart {
  @apply relative flex flex-col rounded-plate bg-surface p-gap-md;
}
.encart--sable { @apply bg-sand; }        /* aplat, pour un encart image ou un chiffre */
.encart--lien  { @apply transition-colors duration-micro; }
@media (hover: hover) {
  .encart--lien:hover { @apply bg-sand; }  /* le survol change l’aplat, rien ne se soulève */
}
.encart .plate-in {                        /* photo dans un encart */
  @apply -mx-gap-xs -mt-gap-xs mb-gap-sm overflow-hidden rounded-plate;
}
```

- Au survol d’un encart lien : l’image se rapproche (`scale(1.035)` en `--dur-long`, même règle que
  `.work-plate`) sous `@media (hover: hover) and (prefers-reduced-motion: no-preference)`, et la
  flèche glisse de 3 px (comme `Button arrow`). Pas d’ombre, pas de translation verticale.
- Tout l’encart est un seul lien : `<Link>` qui enveloppe l’encart, ou `::after` étendu comme
  `.projet__lien`. Anneau de focus sur l’encart entier.
- Écart entre encarts : `gap-gap-sm` (20 → 28 px). Levupp est à 20–35 px.
- **Fond continu** : sur l’accueil, les sections ne portent plus `bg-surface`. Tout est sur
  `bg-canvas` ; le blanc chaud n’apparaît que dans les encarts. Seul le bloc d’audit reste sur
  l’encre. À retirer : `bg-surface` sur `CraftSection` et `ProcessSection` (qui quittent l’accueil
  de toute façon, voir P0-3).
- **Règle des trois terres cuites** (charte §2) : un encart ne porte jamais de terre cuite.

### P0-3 · Restructurer l’accueil

**Fichier** : `app/page.tsx`. Ordre cible :

```tsx
<HeroSection />          {/* P0-5 */}
<ServicesTeaser />       {/* nouveau — « Ce que nous faisons. » */}
<WorkSection />          {/* autre développeur — voir §4.2 */}
<TestimonialsSection />  {/* rend null tant que TEMOIGNAGES est vide */}
<StudioBento />          {/* nouveau — « Le studio, en vrai. » */}
<FaqSection />           {/* « Vos questions. » */}
<AuditSection />         {/* bloc final */}
```

**Retirés de l’accueil** : `ApproachSection` (sa citation part sur /services, voir P1-1),
`CraftSection` (remplacé par `ServicesTeaser`), `PromisesSection` (repris dans `StudioBento`),
`ProcessSection` (déplacé sur /services).

#### a) `ServicesTeaser` : « Ce que nous faisons. »

Fichier nouveau : `components/sections/ServicesTeaser.tsx`. Section `section-pad`, `id="services"`.

- `SectionHead` : titre « Ce que nous faisons. », sans chapô.
- Grille `mt-gap-lg grid gap-gap-sm md:grid-cols-3`. Trois encarts liens (`.encart .encart--lien`)
  vers `/services#site`, `/services#visibilite`, `/services#outils`.
- Chaque encart contient :
  1. l’image existante (`CRAFT_BLOCKS[i].imageSrc`) dans `.plate-in`, via `Plate` en ratio 4/3,
     avec `sizes="(min-width: 1120px) 352px, (min-width: 768px) 31vw, 100vw"` ;
  2. l’étiquette `eyebrow` (« Le site », « La visibilité », « Les outils ») ;
  3. un H3 en `text-title font-extrabold` ;
  4. une phrase en `text-body text-ink-muted` ;
  5. en bas (`mt-auto pt-gap-sm`), « En savoir plus → » en `text-note font-semibold text-ink`.
- Textes, tous tirés de l’existant (`CRAFT_BLOCKS`), sans nouvelle promesse. Nouveaux champs
  `teaserTitle` et `teaserBody` dans `lib/data/site.ts` :
  | Bloc | H3 | Phrase |
  | --- | --- | --- |
  | site | Un site qui fait appeler. | Rapide sur téléphone, clair en trois secondes, et entièrement à vous. |
  | visibilite | Trouvé près de chez vous. | Fiche Google soignée, référencement local, avis suivis. |
  | outils | Votre quotidien, au même endroit. | Devis, plannings, relances : un outil simple à la place du tableur. |
- Sous la grille, un bouton secondaire centré « Voir les services » (`variant="quiet" size="pill"`,
  voir P0-4).
- Mobile : une colonne, encarts empilés, image 4/3. Environ 3 × 420 px, contre 3 × 560 px
  aujourd’hui.
- Mouvement : `Reveal as="li"` avec `delay={index * 60}` (motif déjà utilisé).
- Accessibilité : `<ul>` / `<li>`, section nommée par son `h2`.

#### b) `StudioBento` : « Le studio, en vrai. »

Fichier nouveau : `components/sections/StudioBento.tsx`. Remplace Promesses et fait le travail du bento
« Enchantés » de levupp, **avec des faits vérifiables uniquement**.

Grille : `mt-gap-lg grid gap-gap-sm md:grid-cols-2 lg:grid-cols-4 lg:grid-rows-2`.

| Cellule | Placement lg | Contenu | Source |
| --- | --- | --- | --- |
| A · Atelier | `lg:col-span-2 lg:row-span-2` | Photo `about-atelier.jpg` en `.plate-in`, en ratio 4/3 en mobile et en hauteur libre (`object-cover h-full`) en lg. Légende : `GEO_LINE` en `text-body text-ink-muted`. | `lib/constants.ts` |
| B · Chiffre | 1 cellule, `.encart--sable` | **« 1 »** en `font-serif font-light text-display-lg tabular-nums`, puis « seul interlocuteur : celui qui conçoit et qui développe. » | `PROMISES[2]` |
| C · Chiffre | 1 cellule, `.encart--sable`, lien vers `/realisations` | **`{REALISATIONS.length}`**, calculé et jamais écrit en dur, puis « projets livrés, montrés écran par écran. » | `lib/data/realisations.ts` |
| D · Engagement | 1 cellule | H3 « Des dates, pas des estimations », 1 phrase (≤ 20 mots) | `PROMISES[0]`, raccourci |
| E · Engagement | 1 cellule | H3 « Tout vous appartient », « Le code, les accès, le domaine. » | `PROMISES[1]` |

- Sous la grille : un bouton secondaire « Découvrir le studio » vers `/about`.
- **Emplacement fondateur, prêt à recevoir** : `lib/data/site.ts` → `export const FONDATEUR:
  { prenom: string; role: string; photo: string; alt: string } | undefined = undefined;`. S’il est
  renseigné, la cellule A montre la photo du fondateur et « {prenom}, {role} » à la place de l’atelier.
  **Tant que la photo n’existe pas, rien n’est rendu** : pas de silhouette, pas d’initiales. La photo
  suit la charte §5 : mains au travail ou trois-quarts, lumière de côté, jamais un sourire face à
  l’objectif.
- Newsreader n’est utilisé que pour les deux chiffres (charte §3). Aucune terre cuite dans le bento.
- Mobile : une colonne, dans l’ordre A, B, C, D, E ; chiffres en `text-display-md`.
- 48 h n’apparaît **pas** ici : le délai reste annoncé une seule fois, dans le bloc d’audit.

#### c) FAQ : « Vos questions. »

`components/sections/FaqSection.tsx` et `components/ui/Accordion.tsx` :

- `SectionHead` avec le titre « Vos questions. ». La colonne des questions est centrée :
  `mx-auto mt-gap-lg max-w-[46rem]`. Le vide à droite disparaît.
- Le signe `→` est remplacé par un **plus dessiné** (deux barres de 1,5 px en `bg-ink-muted`, sans
  caractère ni émoji) qui tourne de 45° à l’ouverture (`transition-transform duration-state ease-out`).
  Il se lit comme un dépliant, pas comme un lien.
- Questions en `text-title-sm font-bold`, cible ≥ 44 px (`py-gap-sm` déjà en place).
- `FAQ_ITEMS` reste la source commune de l’affichage et du JSON-LD. Pas de nouvelle question.

#### d) Audit : l’appel final

`components/sections/AuditSection.tsx` :

- Il devient la **dernière section** avant le pied de page.
- Les deux lignes sous le bouton sont remplacées par **une seule** : « Ou écrivez-nous : contact@… »
  en `text-note text-canvas/60`. `GEO_LINE` et les horaires restent dans le pied de page.
- Il ne reste qu’un écart sous la fiche avant le bouton : `mt-gap-md`.
- Le reste est inchangé : fiche, lampe, `on-ink`, bouton `inverse`.

**Effets attendus** : environ 6 700 px en 1440 (au lieu de 8 623), environ 450 mots (au lieu de 635),
6 sections et une conditionnelle.

**Tests à mettre à jour** : `e2e/smoke.spec.ts`, lignes 45 (liste d’ids de sections) et 126
(`/#approche`) ; vérifier `e2e/lumiere.spec.ts` et `e2e/mouvement-degrade.spec.ts` s’ils visent
`#metier`, `#promesses` ou `#methode`. `HOME_SECTIONS` (`lib/data/site.ts`) : à supprimer avec la
colonne du pied de page (P0-6).

### P0-4 · Navigation en pilule, et un seul vocabulaire d’action

**Fichiers** : `components/layout/Header.tsx`, `app/globals.css` (`--header-height`),
`components/ui/Button.tsx`, `lib/data/site.ts` (`NAV_ITEMS`).

**Structure.** L’en-tête garde une hauteur **constante** pour ne jamais décaler la page :
`--header-height: 4.5rem` **[nouveau, remplace 3.75rem]**.

```tsx
<header class="sticky top-0 z-50 flex h-[var(--header-height)] items-center px-3 md:px-5">
  <nav class="mx-auto flex h-14 w-full items-center justify-between gap-gap-sm rounded-full border
              pl-5 pr-2 transition-[max-width,background-color,border-color] duration-state ease-out
              {scrolled ? 'max-w-[54rem] border-line bg-surface'
                        : 'max-w-site border-transparent bg-transparent'}">
    <LogoLink />
    <ul class="hidden md:flex gap-gap-md">…3 liens…</ul>
    <Button href="/contact" size="pill" track="clic_audit">Audit gratuit</Button>   (md+)
    <button …>Menu</button>                                                           (< md)
  </nav>
</header>
```

- **État haut** (`scrollY ≤ 8`) : la barre a la largeur du contenu (`max-w-site`), sans fond ni
  filet, comme aujourd’hui.
- **État défilé** : pilule de 54 rem (864 px) au plus, sur **`bg-surface` opaque** et filet
  `border-line`. **Pas de `backdrop-blur`, pas d’ombre** : le verre est dans le négatif de la charte,
  l’ombre est interdite. Le bouton se loge dans la pilule avec 8 px de retrait (`pr-2`), comme chez
  levupp.
- Le header lui-même reste transparent : on voit la page entre le haut de l’écran et la pilule.
- **3 liens** : Services, Réalisations, Le studio. « Contact » sort de la barre, puisque le bouton y
  mène déjà ; il reste dans le menu mobile et le pied de page. `NAV_ITEMS` sert au pied de page :
  créer `HEADER_ITEMS` (3 entrées) plutôt que modifier `NAV_ITEMS`.
- **Mobile (< md)** : la pilule est **toujours** en état défilé (`bg-surface border-line`). À
  l’intérieur, le logo et **un seul** bouton « Menu » (`h-11 rounded-full bg-ink px-4 text-note
  font-semibold text-canvas`). La pilule contour « Audit gratuit » disparaît de la barre. Le panneau
  s’ouvre sous la pilule, à sa largeur (`rounded-plate border border-line bg-surface p-2`) : liens en
  `text-title font-bold`, puis `Button` plein « Demander mon audit » en `w-full`, puis le courriel en
  `text-note`. Piège de focus, Échap, `inert` : inchangés.
  *Contrepartie à mesurer : l’audit perd un clic direct en mobile. Suivre `clic_audit` (déjà
  instrumenté) deux semaines avant et après ; revenir en arrière si la baisse est nette.*
- **Mouvement** : la transition porte sur `max-width`, `background-color` et `border-color` en
  `--dur-state` / `--ease-out`, sur un seul élément ; la mise en page recalculée se limite à la barre.
  Avec `prefers-reduced-motion: reduce`, le changement est instantané (règle globale existante). La
  lecture de `scrollY` en `requestAnimationFrame` est déjà en place.
- `scroll-padding-top` suit automatiquement `--header-height`.

**Vocabulaire d’action**, partout sur le site :

| Rôle | Libellé | Composant |
| --- | --- | --- |
| Action principale, dans la barre | Audit gratuit | `Button size="pill"` (primaire) |
| Action principale, dans les pages | Demander mon audit → | `Button` (primaire ou `inverse` sur l’encre) |
| Envoi du formulaire | Envoyer ma demande → | inchangé |
| Suites de section | Voir les services · Voir les 4 réalisations · Découvrir le studio | `Button variant="quiet" size="pill" arrow` |

On supprime « Commencer par un audit » et « Découvrir notre approche ».

**Button**, nouvelle taille `pill` **[nouveau]** :
`SHAPE.pill = 'h-11 px-6'`, `LABEL_SIZE.pill = 'text-note'`. On obtient 44 px (cible tactile
minimale) au lieu des 36 px de `sm`, qui reste utilisé ailleurs s’il existe d’autres usages.

### P0-5 · Héros resserré, avec une preuve immédiate

**Fichier** : `components/sections/HeroSection.tsx`.

1. Étiquette `Studio digital · Marseille` : inchangée.
2. H1 inchangé, mais `savoir-faire` est enveloppé dans `<span className="whitespace-nowrap">` pour que
   le mobile ne coupe plus au trait d’union. Rien ne bouge côté LCP.
3. **Chapô raccourci à 15 mots** (réécriture de l’actuel, sans nouvelle promesse) : « Sites, fiches
   Google et outils sur mesure pour les commerces et les artisans de Marseille. »
   Classe : `lede mx-auto mt-gap-sm max-w-[44ch]`.
4. Appels : `Button` primaire « Demander mon audit » vers `/contact`, suivi de
   `Button variant="quiet" size="pill" arrow` « Voir les réalisations » vers `/realisations`.
   Le lien texte en terre cuite disparaît : c’est une terre cuite rendue à l’écran.
5. Mention « Gratuit · Réponse écrite · Sans engagement » : inchangée.
6. **Ligne de preuve [nouveau]**, entre la mention et la photo, à `mt-gap-lg` :
   ```html
   <p class="eyebrow">Ils nous ont confié leur outil</p>
   <ul class="mt-gap-xs flex flex-wrap justify-center gap-x-gap-md gap-y-2">
     <li><a href="/realisations/{id}" class="link-draw text-title-sm font-extrabold
             tracking-[-0.03em] text-ink-muted transition-colors hover:text-ink">Nuréa Parfums</a></li>
     …
   </ul>
   ```
   - Données : `REALISATIONS.map(({ id, nom }) => …)`, **jamais une liste écrite à la main**.
   - Les noms sont **composés en Plus Jakarta Sans** et non affichés en logos : pas de faux logo, pas
     de couleur de marque qui casserait la palette, et c’est plus honnête qu’un « mur » de 4 logos.
   - **À vérifier par le studio** : chaque client accepte d’être nommé sur l’accueil (ils le sont
     déjà sur leurs études de cas). Si « Nuréa Parfums » et « Conciergerie Nuréa » sont le même
     client, ne garder qu’un nom.
   - Mobile : 2 lignes centrées. Pas de défilement automatique : 4 noms n’en ont pas besoin, et une
     bande qui tourne répéterait les noms pour faire nombre.
   - **Emplacement avis Google, prêt à recevoir** : `lib/data/site.ts` → `export const AVIS_GOOGLE:
     { note: number; nombre: number; href: string } | undefined = undefined;`. Une fois renseigné
     avec les valeurs **réelles** de la fiche, on ajoute au bout de la ligne « {note} sur Google ·
     {nombre} avis », avec un lien vers la fiche. Tant que c’est `undefined`, on n’affiche rien. Pas
     de données structurées `Review` (même raison que dans l’en-tête de `temoignages.ts`).
7. Plaque 16/9 : inchangée (`tirage`). En 1440, son bord supérieur affleure en bas du premier écran,
   ce qui invite à défiler.

Budget de terre cuite dans le premier écran : le point du logo, et c’est tout. Il reste deux
emplacements libres.

### P0-6 · Pied de page en carte, avec « Un projet ? »

**Fichier** : `components/layout/Footer.tsx`.

```
<footer class="bg-canvas pb-gap-md pt-gap-lg">
  <div class="site-container">
    <div class="grid gap-gap-lg rounded-plate-lg bg-surface p-gap-lg md:grid-cols-3 md:items-center">
      [Coordonnées]            [Logo + signature + réseaux]        [« Un projet ? » + action]
    </div>
    <div class="mt-gap-md flex flex-col gap-gap-sm md:flex-row md:items-center md:justify-between">
      © 2026 WebTreize         Services · Réalisations · Le studio · Contact · Mentions légales · Confidentialité · CGV
    </div>
  </div>
</footer>
```

- **Colonne 1, coordonnées** : `GEO_LINE`, courriel, téléphone s’il existe, horaires « Du lundi au
  vendredi, 9 h – 18 h ». Sous `<address>`, nœud identique au JSON-LD : la règle NAP de l’en-tête
  actuel est conservée.
- **Colonne 2, centrée** : `Logo`, puis la signature en une ligne, « Studio digital, Marseille »
  (`text-note text-ink-muted`), puis les réseaux sur une ligne en `nav-link`. Snapchat reste, mais en
  dernier ; LinkedIn en premier dès que `NEXT_PUBLIC_LINKEDIN_URL` est défini.
- **Colonne 3** : « Un projet ? » en `text-title font-extrabold`, `Button` « Demander mon audit »,
  puis le lien « ou écrire à contact@webtreize.com » en `link-draw text-note`.
- **Ligne basse** : © à gauche ; à droite, les liens des pages et des pages légales sur une seule
  ligne (`text-note text-ink-faint`, `nav-link`, `gap-x-gap-sm flex-wrap`). Trois `<nav>` nommés
  deviennent **deux** (« Plan du site », « Informations légales »), toujours nommés par
  `aria-labelledby` (intitulés en `sr-only` si on ne veut pas les afficher).
- **Supprimé** : la colonne « L’accueil » (`HOME_SECTIONS`). Toutes les routes restent liées depuis
  chaque page.
- Mobile : la carte passe sur une colonne, dans l’ordre « Un projet ? », logo, coordonnées : l’action
  d’abord. Liens bas en `flex-wrap`, © en dernier.
- Pas de lettre d’information : il n’y en a pas.

---

### P1-1 · /services : une page de services, pas un texte

**Fichiers** : `app/services/page.tsx`, `components/sections/ServicesPageContent.tsx`,
`lib/data/site.ts`.

Ordre :

1. **En-tête** (P1-4, centré) : H1 « Sites, visibilité, outils. » (3 mots au lieu de 5), chapô actuel
   raccourci : « Quatre chantiers, un seul objectif : que vos clients vous trouvent. »
2. **La citation déplacée depuis l’accueil** : `SerifQuote`, « Nous ne livrons pas des sites. Nous
   livrons des clients qui *vous trouvent*. » C’est la seule citation de la page ; le mot en
   `accent-deep` compte comme une terre cuite.
3. **Un bloc par service** (4), chacun `id="site|visibilite|outils|google"` (pour les ancres de
   l’accueil), sur fond ivoire continu, séparés par `gap-gap-xl` et non par un filet :
   - grille `md:grid-cols-12 gap-gap-lg` ;
   - **colonne gauche (`md:col-span-5`, `md:sticky md:top-[calc(var(--header-height)+1rem)]`
     `md:self-start`)** : `eyebrow`, H2 `text-display-sm`, puis un **paragraphe en deux tons** : la
     première phrase de `description` en `text-ink`, la suite en `text-ink-muted`, le tout en
     `text-body-lg`. Il faut découper `description` en `accroche` et `suite` dans les données.
     Ensuite, les **livrables en étiquettes** : `points` rendus en `<ul class="flex flex-wrap
     gap-2">`, chaque `<li>` en `inline-flex h-8 items-center rounded-full bg-sand px-3 text-note
     text-ink`. Aplats sable, pas de bordure. Les étiquettes doivent être raccourcies à 2 à 4 mots
     (« Une action par page », « Mesuré avant mise en ligne », « Code et domaine à vous ») ;
     supprimer « Core Web Vitals ».
   - **colonne droite (`md:col-span-7`)** : `Accordion` de 2 à 4 questions propres au service, dans
     `SERVICE_FAQ: Record<ServiceId, { q: string; a: string }[]>` **[nouveau]**. **À écrire par le
     studio à partir des questions réellement posées**, comme `FAQ_ITEMS`. Si la liste d’un service est
     vide, la colonne affiche à la place l’encart du projet lié.
   - **projet lié** : un encart lien sous l’accordéon, avec la couverture du projet
     (`projet.couverture`), son nom et « Voir l’étude de cas → ». Correspondance par
     `categories` (Site web → web, Application métier → apps, etc.). Si aucun projet ne correspond
     (fiche Google, par exemple), pas d’encart.
4. **« Comment ça se passe. »** : `ProcessSection` déplacée ici, avec `SectionHead` centré et 4 encarts
   numérotés (`grid gap-gap-sm sm:grid-cols-2 lg:grid-cols-4`). Le numéro « 01 » passe en
   `font-serif font-light text-display-sm tabular-nums`, un grand chiffre selon la charte ; le reste
   est inchangé.
5. **« Combien ça coûte ? »** : bloc prêt à recevoir les vrais tarifs, **sans aucun montant
   inventé** :
   ```ts
   export const TARIFS: readonly {
     serviceId: 'site' | 'visibilite' | 'outils' | 'google';
     titre: string;
     inclus: readonly string[];          // repris des points réels du service
     aPartirDe?: number;                 // en euros HT — à renseigner par le studio, sinon absent
     delai?: string;                     // idem
   }[] = [ /* … */ ];
   ```
   Rendu : `SectionHead` « Combien ça coûte ? », puis 3 ou 4 encarts `md:grid-cols-3` (titre, liste
   `inclus`, puis **si `aPartirDe` est défini** « À partir de {n} € HT » en
   `font-serif font-light text-display-sm`, **sinon** « Sur devis, ligne par ligne, après l’audit. »
   en `text-body text-ink`). Phrase commune sous la grille, reprise de la FAQ existante : « Chaque
   devis est détaillé ligne par ligne : vous voyez ce que vous payez et pourquoi. » Pas d’encart
   « mis en avant » surélevé tant qu’il n’y a pas de vraie offre à recommander.
6. **Bloc final** (P1-4).

Mobile : colonnes empilées, sans colonne collante ; étiquettes sur 2 à 3 lignes ; accordéon pleine
largeur.

### P1-2 · /contact : le formulaire dans le premier écran

**Fichiers** : `app/contact/page.tsx`, `components/layout/PageShell.tsx`.

- `PageShell` reçoit `compact` **[nouveau]** : `pt-gap-lg pb-gap-md`, sans filet dessous.
  H1 « Parlons de votre activité. », chapô ≤ 15 mots.
- Une seule section, `pb-section`, grille `md:grid-cols-12 gap-gap-lg` :
  - **gauche (`md:col-span-5`)** : un encart sable avec « Ce que vous recevez », les 3 lignes de
    `AUDIT.brief` en liste sous filets, puis « Réponse écrite sous 48 heures ouvrées. » (c’est la
    seule mention du délai sur la page ; retirer celle de `ContactChannels` sur /contact). En
    dessous, les canaux (courriel, téléphone, horaires), repris de `ContactChannels` en version
    compacte.
  - **droite (`md:col-span-7`)** : le formulaire dans un `.encart` (`p-gap-md`). La phrase « 3 champs
    obligatoires, le téléphone est facultatif. » passe en `text-note text-ink-faint` au-dessus du
    premier champ. Le H2 « Trois champs obligatoires. » disparaît : le formulaire est nommé par
    `aria-labelledby` vers un H2 `sr-only` « Formulaire de contact ».
- La section « Du lundi au vendredi… » est supprimée (fusionnée à gauche).
- Objectif mesurable : en 1440 × 900, le premier champ est visible sans défiler. Viser un H1 à
  y ≈ 130 et un premier champ à y ≈ 420.
- Mobile : le formulaire **d’abord**, la colonne « Ce que vous recevez » ensuite (`order-first` sur le
  formulaire sous `md`).

### P1-3 · /about : un visage, moins de mots

**Fichier** : `app/about/page.tsx`.

- Nouvel ordre : en-tête centré, **encart fondateur** (si `FONDATEUR` est défini, voir P0-3 b :
  photo 3/4 à gauche, citation courte signée à droite, du genre de levupp `/agence` mais sans sourire
  face à l’objectif et sans icônes flottantes), la citation « Un petit studio, *volontairement*. »,
  « Où nous sommes », « Ce que nous ne faisons pas », puis le bloc final.
- « Où nous sommes » : 3 paragraphes (132 mots) ramenés à **2 paragraphes, 70 mots au plus**. Le
  paragraphe 2 fait doublon avec « un seul interlocuteur » (déjà dans le bento de l’accueil et dans
  l’encart fondateur).
- « Trois choses que vous ne verrez jamais ici. » devient « Ce que nous refusons. » (3 mots), en
  3 encarts `md:grid-cols-3` au lieu de filets, pour ne pas reproduire la forme des engagements.
- **Supprimé** : la section « Du lundi au vendredi » (doublon du pied de page et de /contact).
- **Production photo** (hors code) : un portrait du fondateur et, si possible, une vraie photo de
  l’espace de travail, selon la charte §5 et le prompt C. En attendant, rien n’est affiché.

### P1-4 · Pages internes : même en-tête, même fin

**Fichiers** : `components/layout/PageShell.tsx`, `components/sections/PageCtaBand.tsx`,
`components/sections/AuditSection.tsx`.

- `PageShell` : l’en-tête par défaut passe **centré**, comme l’accueil (`text-center`, `mx-auto` sur
  H1 et chapô), avec H1 `text-display-lg max-w-[16ch]` et chapô `max-w-[44ch]`. Une prop
  `align="left"` reste disponible pour `/realisations` (index), au choix du développeur en charge.
- **Même fin partout** (l’équivalent du « Le niveau supérieur, ça vous tente ? » de levupp) : `AuditSection`
  reçoit une prop `variant="band"` qui garde l’étiquette, le titre, la fiche et le bouton, et retire
  la lampe si elle pèse trop sur les pages courtes. `PageCtaBand` et ses titres variables (« Commençons
  simplement. », « Le vôtre ressemblerait à quoi ? ») sont remplacés par ce bloc sur /services,
  /about et /realisations. **Pas sur /contact** (règle actuelle : pas de reconversion sur la page de
  conversion).
- Contrôle de la règle « 48 h une fois par page » : le bloc final porte le délai ; aucune autre
  mention sur /services, /about et /realisations.

### P1-5 · Césure et chapôs

**Fichier** : `app/globals.css`.

- `p, li { hyphens: auto }` devient `hyphens: manual` par défaut.
- `hyphens: auto` est réactivé seulement là où la colonne est étroite et justifiée à gauche, avec des
  mots longs : `.legal-prose p, .legal-prose li`.
- Résultat : plus de « introu-/vables » ni de « lo-/cal » dans les chapôs centrés.
  `text-wrap: pretty` reste en place.

### P1-6 · Avis : la structure est prête, on la place

**Fichiers** : `components/sections/TestimonialsSection.tsx`, `app/page.tsx`.

- Le composant rend déjà `null` quand `TEMOIGNAGES` est vide : **aucune fausse citation**.
- Le jour où le premier vrai avis arrive, on le passe au gabarit du site : `SectionHead` « Ce qu’ils en
  disent. », encarts `md:grid-cols-2` (ou 3 à partir de 3 avis), citation en Newsreader 300
  `text-title`, auteur en `text-note font-semibold`, source et date en dessous, **lien vers l’avis
  public**. Pas d’étoiles dessinées : si l’avis vient de Google, la note est celle de la source et
  s’écrit en toutes lettres (« 5 sur 5 sur Google »).
- Placement sur l’accueil : juste après les réalisations (la preuve par le travail, puis la preuve par
  la parole), comme chez levupp.
- Pour l’obtenir (hors code) : demander l’avis par écrit aux 4 clients existants, avec leur accord de
  publication (règles en tête de `temoignages.ts`).

---

### P2-1 · Ponctuation optique et point du logotype

- Nouveau composant `components/ui/Titre.tsx` **[nouveau]** : enveloppe la ponctuation finale d’un
  titre display (`.`, `,`, `?`) dans `<span class="-ml-[0.06em]">`, et l’apostrophe courbe dans
  `<span class="-mr-[0.04em]">`. À utiliser dans `SectionHead`, le H1 de l’accueil et `PageShell`.
  Vérifier à l’œil sur `audit/zoom-h1.png` avant/après : le point doit se lire comme la fin du mot,
  pas comme un caractère isolé.
- `components/ui/Logo.tsx` : retirer `gap-px` et poser le point à `-ml-[0.02em]`. La charte §4 :
  le point « ferme le mot comme on termine une phrase ». Ne changer ni sa couleur ni sa taille.

### P2-2 · Finitions de mouvement

- **Apparition des encarts** : `Reveal` en décalé de 60 ms, **plafonné à 4 éléments** (au-delà, même
  délai que le 4e). Un décalage de 300 ms se voit et retarde la lecture.
- **Pilule de navigation** : au premier passage à l’état défilé, un fondu du filet (`border-color`) en
  `--dur-state`. Rien d’autre : pas de rebond, pas de rétrécissement du logo.
- **Chiffres du bento** : **pas** de compteur animé (« 0 → 4 » est un effet de logiciel, et le
  chiffre doit être lisible tout de suite). Le chiffre est rendu en dur côté serveur.
- `prefers-reduced-motion: reduce` : aucune transformation, aucun décalage ; seuls les changements de
  couleur restent, en instantané (règle globale existante).
- Rappel de doctrine : rien de ce qui est dans le premier écran ne dépend d’un script (voir la section
  « Reveal » de `globals.css`).

### P2-3 · /realisations : moins de filtres (à transmettre au développeur en charge)

Avec 4 projets, les 6 filtres, dont 4 à 1 seul projet, font catalogue vide. Proposition : n’afficher
les filtres qu’à partir de 8 projets, ou limiter à 3 catégories larges (Site web, Application métier,
Commande en ligne). Rendu calculé depuis `categories`, jamais une liste en dur.

### P2-4 · Photographie

C’est le poste le plus important selon la charte (§5), et c’est ce que levupp a en plus : de vraies
photos (équipe, bureaux). À produire :

1. un portrait de travail du fondateur (prompt C adapté, lumière de côté, pas de sourire face à
   l’objectif) ;
2. l’espace de travail réel du studio, pour remplacer l’ambiance générée de `about-atelier.jpg` ;
3. une ou deux photos d’un client dans son commerce, avec son accord, l’écran livré visible dans le
   cadre. C’est la preuve la plus forte possible pour un artisan.

### P2-5 · Disponibilité réelle (l’équivalent honnête de « 2 places pour le printemps »)

`lib/data/site.ts` → `export const DISPONIBILITE: string | undefined = undefined;`, par exemple
« Prochain démarrage possible : novembre 2026 ». Renseignée par le studio, **uniquement si c’est
vrai et tenu à jour**. Rendue dans l’étiquette du héros (`Studio digital · Marseille ·
{DISPONIBILITE}`) et à gauche sur /contact. Absente : rien n’est rendu. Aucun compteur de places.

---

## 4 · Plan de page d’accueil cible

### 4.1 Les sections, dans l’ordre

| # | Section (composant) | Titre (H2) | Rôle | Objet | Suite |
| --- | --- | --- | --- | --- | --- |
| 1 | Héros (`HeroSection`) | H1 « Votre savoir-faire mérite d’être trouvé. » | Dire quoi, pour qui, où, et prouver tout de suite | Ligne des noms clients, puis plaque 16/9 | « Demander mon audit », « Voir les réalisations » |
| 2 | `ServicesTeaser` | « Ce que nous faisons. » | Les 3 métiers en 10 secondes | 3 encarts avec photo | « Voir les services » |
| 3 | `WorkSection` | « Quelques réalisations. » | La preuve par le travail | 3 cartes à couverture | « Voir les 4 réalisations » |
| 4 | `TestimonialsSection` *(conditionnelle)* | « Ce qu’ils en disent. » | La preuve par la parole | encarts d’avis vérifiables | — |
| 5 | `StudioBento` | « Le studio, en vrai. » | Qui, où, et ce qui est écrit au devis | bento : atelier (ou fondateur), 1, {n} projets, 2 engagements | « Découvrir le studio » |
| 6 | `FaqSection` | « Vos questions. » | Lever les objections (prix, délai, compétences) | accordéon centré | — |
| 7 | `AuditSection` | « Ce qui vous freine, par écrit. » | Convertir | la fiche d’audit | « Demander mon audit » |
| — | `Footer` | « Un projet ? » | Dernier appel, coordonnées | carte en 3 colonnes | « Demander mon audit » |

Rythme : **titre centré, objet, pilule**, six fois. Fond ivoire continu. Une seule rupture, le bloc
d’encre, placé en dernier : la page monte vers lui.

### 4.2 Comment la section Réalisations doit s’insérer (refonte en cours)

Sans entrer dans le détail des cartes, qui reviennent à l’autre développeur :

- **Même en-tête que les autres sections** : `SectionHead`, titre centré « Quelques réalisations. »,
  pas de chapô. Le chapô actuel peut rester, s’il fait 20 mots au plus.
- **Pas de bande de fond** : les cartes se posent sur l’ivoire continu (aujourd’hui la section est sur
  `bg-canvas`, entre deux sections `bg-surface` : ce sont ces dernières qui disparaissent).
- **Ce sont les seules couleurs saturées de la page** (les couleurs des clients) : elles doivent être
  encadrées par deux sections calmes. C’est le cas dans le plan : services juste avant, bento juste
  après.
- **Espacements alignés sur les encarts** : grille `gap-gap-sm` (ou `gap-gap-md` si les cartes n’ont
  pas de fond), rayon `rounded-plate`, `section-pad`.
- **La suite est une pilule**, pas le bouton bordé de 330 px : `Button variant="quiet" size="pill"
  arrow`, « Voir les {REALISATIONS.length} réalisations », centré à `mt-gap-lg`. La mention des
  données d’exemple suit, centrée, en `text-note text-ink-faint`, `mt-gap-sm`.
- Mobile : 3 cartes empilées au plus (pas de carrousel), puis la pilule.

### 4.3 Coupes

| Retiré de l’accueil | Destination | Gain approximatif en 1440 |
| --- | --- | --- |
| `ApproachSection` (H2 de 22 px, citation, 38 mots) | Citation sur /services | −670 px |
| `CraftSection` (zigzag de 3 blocs) | Remplacé par `ServicesTeaser` (3 encarts sur une ligne) | −900 px |
| `PromisesSection` | Repris dans `StudioBento` (D, E, et B pour « un seul interlocuteur ») | −680 px, compensés par le bento |
| `ProcessSection` | /services, « Comment ça se passe. » | −730 px |
| Lien « Découvrir notre approche » | Supprimé (l’ancre disparaît) | 1 terre cuite de moins |
| Chapô du héros : 30 → 15 mots | — | 1 ligne |
| 2 lignes sous le bouton d’audit | Pied de page | ~80 px |
| Colonne « L’accueil » du pied de page | Supprimée | — |
| Pilule contour « Audit gratuit » dans la barre mobile | Menu | 1 bouton de moins en 390 px |

Hauteur visée : **environ 6 700 px en 1440** (8 623 aujourd’hui) ; environ 450 mots (635).

### 4.4 Ordre de mise en œuvre conseillé

1. P0-1 et P0-2 (`SectionHead`, `.encart`, `size="pill"`) : les briques, sans rien casser.
2. P0-3 et P0-5 (accueil et héros), avec la mise à jour des tests e2e.
3. P0-4 (navigation), puis P0-6 (pied de page).
4. P1-4, puis P1-1, P1-2, P1-3 (pages internes) et P1-5 (césure).
5. P2 au fil de l’eau ; P2-4 (photographie) à lancer tout de suite en parallèle, car c’est le plus
   long.

Après chaque étape : captures 1440 et 390 avec le même script (défilement écran par écran), et
contrôle de la règle des trois terres cuites, écran par écran.
