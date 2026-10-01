# Fluidité — audit d’interaction au regard du skill « apple-design »

Audit en lecture seule, après le commit `c90828e` (galerie, carte inclinée, navigation).
Build de production (`npm run build`, Next 16.1.7) servi par `next start -p 3002`, piloté par
Playwright (Chromium) en 1440 × 900 et 390 × 844 (`hasTouch`, `isMobile`), avec émulation de
`prefers-reduced-motion`, `prefers-reduced-transparency` et `prefers-contrast`.

**Ce qui fait autorité.** `docs/charte-graphique.md` pour l’identité (ivoire, sable, terre cuite,
encre ; pas d’ombre, pas de dégradé décoratif, esprit calme). Le skill pour l’interaction, le
mouvement, la typographie fine et l’accessibilité du mouvement. `NIVEAU-SUPERIEUR.md` pour la
structure. Aucune nouvelle dépendance n’est proposée : les ressorts restent maison, en
`requestAnimationFrame` ; les seules API ajoutées sont natives (View Transitions, `inert`, `:active`).

**Priorités.** P0 : défaut visible ou rupture d’un principe cardinal (réponse, interruptibilité,
cohérence spatiale), à corriger avant toute autre finition. P1 : écart net, peu coûteux. P2 :
finition.

---

## 0. Mesures

| Mesure | Résultat | Verdict |
| --- | --- | --- |
| Appui souris sur `Button` (`.press`) | `scale` 1 → 0,978 à 46 ms, 0,97 atteint à ~160 ms | Réponse au pointer-down : oui. Courbe à 150 ms (et non 100 ms) |
| Appui puis glisser hors du bouton, relâcher | Aucune navigation | Annulation par glissement : conforme |
| Appui tactile maintenu 300 ms (bouton Menu, carte) | `transform: none` sur toute la durée | Aucun retour d’appui au toucher |
| Appui sur un filtre /realisations, sur une question FAQ | Aucune variation (ni `transform` ni couleur) | Aucun retour d’appui |
| Entrée du pointeur sur une carte projet | Première frame : `rotateX 1,66°`, `rotateY −2,15°` directement | **Saut** : pas de ressort à l’entrée |
| Sortie du pointeur | `rotateY` 2,13 → 2,49 (vitesse transmise) → 0 en ~650 ms, sans dépassement | Passage de vitesse : oui |
| Retour sur la carte pendant le retour au repos | `rotateY` passe de la valeur en vol à −2,13 en une frame | **Coupure** : non interruptible |
| Barre de navigation, passage à l’état défilé (1440) | `max-width` 1120 → 864 px en ~240 ms ; flou activé d’un coup | Anime une propriété de mise en page (coût limité à la barre) |
| Menu mobile, ouverture | Opacité 0 → 1 et `translateY −6 → 0` en ~250 ms ; `transform-origin` : centre du panneau (182 px 181 px) | Origine non ancrée au bouton |
| Menu mobile, fermeture | `visibility: hidden` dès la première frame, l’opacité s’anime sur un élément invisible | **Fermeture coupée** : aucun chemin de sortie visible |
| Menu mobile, ouverture interrompue à 90 ms | L’opacité repart de 0,92 vers 0, mais le panneau disparaît à la frame suivante | Inversion invisible |
| FAQ, ouverture | 83 → 153 px en ~240 ms | Conforme |
| FAQ, fermeture interrompue à 80 ms puis réouverture | 153 → 88 → 153 px, continu, sans saut | **Interruptible : conforme** |
| Changement de page (lien Services, depuis `scrollY` 2500) | La nouvelle page défile **visiblement** de 1833 à 0 en ~740 ms | **Défaut** : défilement doux appliqué au saut de route |
| Retour arrière | La page d’accueil défile de 0 à 1561 en ~700 ms | Même défaut |
| Filtre /realisations | 4 → 2 cartes à la frame suivante, page raccourcie d’un coup | Aucune continuité |
| Formulaire : champ e-mail « abc » puis sortie du champ | Aucune erreur, `aria-invalid` absent | Pas de validation en ligne |
| Formulaire : envoi vide | 3 erreurs, focus sur « name », formulaire +142 px d’un coup | Saut de mise en page à l’erreur |
| CLS sur l’accueil, défilement complet (1440) | 0 ; aucune tâche longue | Conforme |
| Galerie mobile, lancer de 150 px | Défile jusqu’à 127 px puis revient à 0 (aimantation native) | Natif ; le lancer synthétique de Chromium est faible, sans valeur probante |
| `prefers-reduced-motion` | Cartes à plat, aucun voile, défilement `auto`, animations au défilement coupées | Conforme, sauf : FAQ toujours animée en 250 ms (`::details-content`) ; `scale(0.97)` d’appui conservé |
| `prefers-reduced-transparency` | Barre et pastille ↗ opaques, sans flou | Conforme |
| `prefers-contrast: more` | Barre opaque, filet `line-strong` 0,78, sourdines assombries | Conforme |

Animations au défilement en cours sur l’accueil : `line-mask` (clip-path, horloge du document),
`tirage-pose` et `brief-set` (transform), `titre-decouvre` × 5 (clip-path), `pli-rasant` × 4
(opacity + transform). Hors transform/opacity : `clip-path` (×6), `max-width` (barre),
`block-size` (FAQ), `background-size` (`.link-draw`), dégradé radial de `.lamp` (repeint).

---

## 1. Réponse : supprimer la latence

**État.** `.press` (`app/globals.css:582-588`) pose `scale(0.97)` sur `:active` : la réponse
existe à la souris. Mais l’utilitaire Tailwind `transition` posé à côté (`components/ui/Button.tsx:134`,
`components/layout/Header.tsx:222` et `:232`) écrase `transition-duration` : 150 ms mesurés au lieu de
100 ms. Le commentaire de `Button.tsx:27-32` est faux (il annonce `scale(0.985)` et 80 ms).

**Écarts.**
- P0 — **Aucun retour d’appui au toucher.** Mesuré : rien en 300 ms d’appui maintenu. Sur iOS
  Safari, `:active` n’est appliqué que si la page porte un écouteur `touchstart`. C’est pourtant le
  premier écran du public visé (artisans, sur téléphone).
- P0 — **Contrôles sans retour d’appui** : filtres (`components/realisations/ProjectIndex.tsx:43-48`),
  question FAQ (`app/globals.css:628-630`), liens du menu mobile (`Header.tsx:256`, seulement
  `hover:bg-sand`, donc rien au toucher).
- P2 — durée d’appui à 150 ms au lieu de 100 ms ; commentaire périmé.

**Corrections.**

```tsx
// components/ClientShell.tsx — dans le useEffect existant ou un second.
// iOS Safari n’applique :active qu’en présence d’un écouteur touchstart.
useEffect(() => {
  const noop = () => {};
  document.addEventListener('touchstart', noop, { passive: true });
  return () => document.removeEventListener('touchstart', noop);
}, []);
```

```css
/* app/globals.css — .press porte seul ses transitions ; plus d’utilitaire `transition` à côté. */
.press {
  transition:
    transform 100ms var(--ease-out),
    color var(--dur-micro) var(--ease-out),
    background-color var(--dur-micro) var(--ease-out),
    border-color var(--dur-micro) var(--ease-out);
}
.press:active { transform: scale(0.97); }

/* Question FAQ : le signe se resserre à l’appui, la question s’assombrit. Instantané. */
.faq-item > summary:active { color: var(--color-ink-muted); }
.faq-item > summary:active .faq-sign { transform: scale(0.85); transition-duration: 100ms; }
.faq-item[open] > summary:active .faq-sign { transform: rotate(45deg) scale(0.85); }
```

- `Button.tsx:134` : remplacer `'group press … transition'` par `'group press …'` ; idem
  `Header.tsx:222` et `:232`. Corriger le commentaire `Button.tsx:27-32` (0,97 ; 100 ms).
- `ProjectIndex.tsx:44` : ajouter `press` et remplacer `transition-colors` (qui redéfinit
  `transition-property` et figerait le `transform`) — `.press` porte déjà les couleurs.
- `Header.tsx:256` : `hover:bg-sand` → `hover:bg-sand active:bg-sand` (et `transition-colors`
  laissé, l’arrivée du sable à l’appui est instantanée car `:active` change avant la frame).

## 2. Manipulation directe : suivi 1:1

**État.** Une seule surface manipulable : la galerie mobile `.projet-rail`
(`app/globals.css:371-405`), en défilement natif avec aimantation. Suivi 1:1 natif, capture native :
c’est le bon choix, il ne faut **pas** le réécrire en JavaScript.

**Écart.**
- P1 — la carte inclinée mesure `getBoundingClientRect()` de la **couverture transformée** à chaque
  `pointermove` (`components/realisations/ProjectCard.tsx:125`). Le rectangle inclut l’inclinaison
  que l’on vient d’écrire : boucle de rétroaction (faible) et mise en page forcée à chaque
  évènement, puisque `paint()` vient d’écrire un `style.transform`.

**Correction.** Mesurer une fois à `pointerenter`, sur le lien (jamais transformé par le ressort),
et réutiliser ce rectangle jusqu’à `pointerleave` (voir le code complet en §3).

## 3. Interruptibilité — le principe cardinal

**État.** FAQ conforme (mesuré : fermeture interrompue à 80 ms, repart de 88 px sans saut). Barre de
navigation conforme (transition CSS réversible). Les apparitions (`Reveal`) sont à sens unique,
c’est normal.

**Écarts.**
- **P0 — Carte de projet : saut à l’entrée, coupure au retour** (`ProjectCard.tsx:115-147`).
  `onPointerMove` écrit `channel.value = target` : le premier évènement pose l’inclinaison complète
  en une frame (mesuré : 0 → 1,66° / −2,15°), et un retour sur la carte pendant le retour au repos
  arrête le ressort (`stopAnimation()`, l. 121) et saute à la cible. Le ressort n’existe qu’à la
  sortie ; il faut qu’il porte **tout** le mouvement : le pointeur ne fait que déplacer la cible.
- **P0 — Menu mobile : fermeture coupée, inversion invisible** (`Header.tsx:238-245`). Le panneau
  passe en `invisible` à la fermeture et Tailwind `transition` n’anime pas `visibility` : il disparaît
  à la première frame (mesuré), l’opacité s’anime ensuite sur un élément invisible. Une ouverture
  interrompue repart bien de l’opacité courante (0,92), mais on ne la voit pas.

**Corrections.**

Ressort maison, paramétré comme Apple (amortissement + réponse) :

```ts
// lib/motion/spring.ts — aucun import, ~25 lignes.
export type Spring = { value: number; velocity: number; target: number };

/** Réponse (s) et amortissement → raideur et frottement, masse 1. */
export function springConstants(response: number, damping: number) {
  const omega = (2 * Math.PI) / response;
  return { stiffness: omega * omega, friction: 2 * damping * omega };
}

/** Euler semi-implicite, pas plafonné : stable à 30 comme à 120 Hz. */
export function stepSpring(s: Spring, dt: number, k: number, c: number): boolean {
  const a = -k * (s.value - s.target) - c * s.velocity;
  s.velocity += a * dt;
  s.value += s.velocity * dt;
  const resting = Math.abs(s.value - s.target) < 0.001 && Math.abs(s.velocity) < 0.001;
  if (resting) { s.value = s.target; s.velocity = 0; }
  return !resting;
}
```

Valeurs : le survol ne porte pas d’élan, donc **amortissement 1,0, réponse 0,35 s** à l’aller comme
au retour (`stiffness ≈ 322`, `friction ≈ 35,9`). Les valeurs actuelles (`-190`, `-25`, l. 93)
valent amortissement 0,91, réponse 0,46 s : un léger flottement sans justification de geste.

```tsx
// ProjectCard.tsx — principe (remplace les l. 64-154).
const springs = useRef({ rx: s0(), ry: s0(), tx: s0(), ty: s0() }); // s0 = { value:0, velocity:0, target:0 }
const rect = useRef<DOMRect | null>(null);
const { stiffness: K, friction: C } = springConstants(0.35, 1);

const loop = (now: number) => {
  const dt = Math.min((now - (last.current || now)) / 1000, 1 / 30);
  last.current = now;
  let moving = false;
  for (const s of Object.values(springs.current)) moving = stepSpring(s, dt, K, C) || moving;
  paint();                                   // écrit les deux transform, comme aujourd’hui
  frame.current = moving ? requestAnimationFrame(loop) : 0;
  if (!moving) { last.current = 0; coverRef.current?.removeAttribute('data-moving'); }
};
const kick = () => { if (!frame.current) frame.current = requestAnimationFrame(loop); };

const onPointerEnter = (e: React.PointerEvent<HTMLAnchorElement>) => {
  if (e.pointerType === 'touch' || reduced()) return;
  // Mesure unique, sur un cadre neutre qui enveloppe la couverture et ne se transforme jamais :
  // <div ref={frameRef}><div ref={coverRef} className="projet-carte__couverture">…</div></div>
  rect.current = frameRef.current!.getBoundingClientRect();
  coverRef.current?.setAttribute('data-moving', '');
};
const onPointerMove = (e: React.PointerEvent<HTMLAnchorElement>) => {
  const r = rect.current; if (!r) return;
  const x = clamp(((e.clientX - r.left) / r.width - 0.5) * 2);
  const y = clamp(((e.clientY - r.top) / r.height - 0.5) * 2);
  const s = springs.current;
  s.rx.target = -y * 1.8; s.ry.target = x * 2.2; s.tx.target = x * 2.5; s.ty.target = y * 2;
  kick();                                    // jamais stopAnimation() : on change la cible, pas le mouvement
};
const onPointerLeave = () => {
  rect.current = null;
  for (const s of Object.values(springs.current)) s.target = 0;
  kick();
};
```

Le rectangle de mesure doit être celui d’un élément non transformé (le lien ou un enveloppeur
neutre) ; s’il faut le garder à jour au défilement, le relire sur `scroll` passif, jamais au
`pointermove`. Le vecteur 2D est déjà décomposé en canaux indépendants (X, Y) : conforme au §3.

Menu mobile : voir le code du §7 (transition de `visibility` retardée à la fermeture, immédiate à
l’ouverture), qui rend la sortie visible **et** l’inversion lisible.

## 4. Le comportement plutôt que l’animation : les ressorts

**État.** Deux courbes et quatre durées dans `:root` (`app/globals.css:20-25`). `--ease-out`
(`0.32, 0.72, 0, 1`) est la courbe des feuilles iOS : un bon choix pour tout ce qui n’est pas
touché. Le seul ressort est celui de la carte.

**Écarts.**
- P1 — paramètres du ressort de la carte exprimés en raideur / frottement bruts
  (`ProjectCard.tsx:93`) : illisibles, et sous-amortis sans élan. Corrigé par `springConstants`
  (§3).
- P2 — aucune règle écrite pour choisir CSS ou ressort. À poser en tête de `globals.css`, section
  « Mouvement » : *ce que l’on touche ou que l’on peut interrompre → ressort (amortissement 1,0,
  réponse 0,3–0,4 s) ; ce qui apparaît seul → transition CSS `--ease-out` ; rebond (amortissement
  0,8) uniquement après un geste porteur d’élan — le site n’en a aucun aujourd’hui.*

## 5. Passage de vitesse

**État.** La carte transmet la vitesse du pointeur au ressort de sortie (mesuré : `rotateY` monte de
2,13 à 2,49° après la sortie, puis revient sans dépasser). La galerie confie le passage au
défilement natif : conforme.

**Écart.** P2 — la vitesse est estimée sur un seul intervalle et plafonnée à 60 (`ProjectCard.tsx:139`),
bruitée. Avec le ressort-suiveur du §3, la vitesse est celle du ressort lui-même : l’estimation
disparaît.

## 6. Projection de l’élan

**État.** Seule la galerie mobile reçoit un lancer. `scroll-snap-type: inline mandatory`
(`app/globals.css:382`) délègue au navigateur la décélération **et** le choix du cran à partir du
point projeté : c’est exactement la projection décrite par le skill, faite par le système.

**Écart.** Aucun. Ne pas réécrire en JavaScript. Le test synthétique de Chromium (lancer de 150 px
revenu à 0) n’est pas probant : le lancer émulé est faible. À vérifier sur un vrai iPhone et un
Android d’entrée de gamme (§17).

## 7. Cohérence spatiale — chemins symétriques, origines ancrées

**Écarts.**
- **P0 — Menu mobile non ancré, sortie absente** (`Header.tsx:238-245`). `transform-origin` au
  centre du panneau (mesuré 182 px 181 px) alors que le déclencheur est à droite de la pilule ;
  entrée par le haut, sortie… nulle part (§3).
- P2 — `.projet-carte__ouvrir` (`app/globals.css:441`) est bien ancré en haut à droite : conforme.

**Correction.** Remplacer les utilitaires du panneau par une classe dédiée :

```tsx
// Header.tsx:238-245
<div
  id="mobile-menu"
  ref={panelRef}
  inert={!open}
  data-open={open ? '' : undefined}
  className="menu-panel absolute inset-x-0 top-full pt-2 md:hidden"
>
```

```css
/* app/globals.css — couche components */
.menu-panel {
  /* Le panneau naît sous le bouton « Menu », pas en son centre. */
  transform-origin: calc(100% - 2.75rem) 0;
  opacity: 0;
  transform: translateY(-6px) scale(0.97);
  visibility: hidden;
  /* Sortie : même chemin, courbe miroir, puis seulement le masquage. */
  transition:
    opacity 200ms var(--ease-in-mirror),
    transform 200ms var(--ease-in-mirror),
    visibility 0s linear 200ms;
}
.menu-panel[data-open] {
  opacity: 1;
  transform: none;
  visibility: visible;
  transition:
    opacity var(--dur-micro) var(--ease-out),
    transform var(--dur-state) var(--ease-out),
    visibility 0s;
}
```

```css
:root {
  /* Miroir de --ease-out (points de contrôle inversés : 1−x2, 1−y2, 1−x1, 1−y1). */
  --ease-in-mirror: cubic-bezier(1, 0, 0.68, 0.28);
}
```

Le trajet de sortie est le trajet d’entrée à l’envers (remonte de 6 px, se resserre vers le
bouton). La sortie est plus courte (200 ms) que l’entrée (250 ms) : on ne fait pas attendre une
fermeture. `inert` reste posé immédiatement à la fermeture : rien n’est cliquable pendant la sortie.
Une ouverture interrompue repart de la valeur courante (comportement natif des transitions CSS),
et cette fois on la voit.

## 8. Indiquer la direction du geste

**État.** L’inclinaison de la carte se penche vers le pointeur ; les flèches des liens glissent de
3–4 px vers la destination ; le signe de la FAQ tourne d’un huitième de tour : conformes.

**Écarts.**
- P1 — filtres /realisations (`ProjectIndex.tsx:42` et `:61-65`) : les cartes conservées sautent à
  leur nouvelle place, les autres disparaissent. Rien ne dit ce qui a changé.
- P2 — le panneau du menu doit grandir **depuis** le bouton (§7).

**Correction (filtres), sans dépendance** — View Transitions du navigateur, avec repli :

```tsx
// ProjectIndex.tsx
import { flushSync } from 'react-dom';

const choisir = (categorie: string | null) => {
  const reduit = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  if (!document.startViewTransition || reduit) return setActif(categorie);
  document.startViewTransition(() => flushSync(() => setActif(categorie)));
};
// …
<li key={entree.id} style={{ viewTransitionName: `projet-${entree.id}` }}>{entree.carte}</li>
```

```css
::view-transition-group(*) {
  animation-duration: var(--dur-state);
  animation-timing-function: var(--ease-out);
}
::view-transition-old(*),
::view-transition-new(*) {
  animation-duration: var(--dur-micro);
}
@media (prefers-reduced-motion: reduce) {
  ::view-transition-group(*),
  ::view-transition-old(*),
  ::view-transition-new(*) { animation: none !important; }
}
```

Les cartes conservées glissent à leur nouvelle place, les autres se fondent. Limite connue : une
View Transition n’est pas interruptible (un second clic termine la première instantanément) ; à
250 ms, c’est acceptable pour un filtre. Le nom de transition doit être unique par carte : le
`id` du projet l’est.

## 9. Rubber-banding — bornes souples

**État.** Aucune surface de glisser maison. La galerie confie ses bords au système (rebond natif
sur iOS ; `overscroll-behavior-inline: contain`, `app/globals.css:380`, garde ce rebond local et
n’entraîne pas la page). Conforme ; ne rien ajouter.

## 10. Détails des gestes

**État.** Cibles de 44 px (filtres `min-h-11`, Menu `h-11`, bouton `pill` `h-11`). Glisser hors
d’un bouton avant de relâcher annule la navigation (mesuré). Pas de double-tap, donc pas de délai
de désambiguïsation ; le délai de 300 ms est supprimé par la balise `viewport`.

**Écarts.**
- P1 — **survol collant au toucher**. Les variantes `hover:` de Tailwind 3 ne sont pas filtrées par
  `@media (hover: hover)` : après un appui sur un bouton plein, il reste terre cuite
  (`Button.tsx:107-109`) ; idem `.link-draw:hover` (`app/globals.css:576-579`) et
  `.group:hover .link-draw` (`:456-459`), qui laissent un soulignement dessiné après un appui.
- P2 — la carte entière porte `.press` (`ProjectCard.tsx:160`) : dans la galerie, un doigt qui
  commence un glisser sur une carte la rétrécit. iOS annule `:active` dès que le défilement part ;
  vérifier sur appareil.

**Corrections.**

```ts
// tailwind.config.ts — à la racine de la config
future: { hoverOnlyWhenSupported: true },
```

```css
/* app/globals.css:456-459 et :576-579 — sous @media (hover: hover) */
@media (hover: hover) {
  .group:hover .link-draw,
  .link-draw:hover { background-size: 100% 1px; }
}
.group:focus-visible .link-draw,
.link-draw:focus-visible { background-size: 100% 1px; }
```

## 11. Fluidité à la frame

**État.** CLS mesuré à 0 sur l’accueil défilé de bout en bout, aucune tâche longue. `will-change`
posé seulement pendant le mouvement de la carte (`data-moving`) : bonne pratique.

**Écarts (propriétés animées hors transform/opacity).**
- P2 — barre de navigation : `max-width` animé (`Header.tsx:188`), donc mise en page à chaque frame
  pendant 250 ms. Mesuré sans tâche longue ; le recalcul est confiné à la barre. **Acceptable** ; si
  un jour elle saccade sur Android d’entrée de gamme, animer à la place un pseudo-élément de fond
  en `clip-path: inset(0 calc((100% - 54rem) / 2) round 999px)` et laisser le contenu se placer
  sans transition.
- P2 — `.lamp` (`app/globals.css:545-558`, `components/motion/Lamp.tsx:63-67`) : le commentaire dit
  « seule la position du dégradé change » ; en réalité la variable CSS modifie un
  `radial-gradient`, qui est **repeint** sur toute la section à chaque frame. Remplacer par un disque
  de 42 rem en `position: absolute` déplacé en `transform: translate3d(x, y, 0)` : composé, sans
  repeinture.
- P2 — `clip-path` animé (`line-mask`, `titre-decouvre`, ×6) : repeint à chaque frame de défilement
  sur les navigateurs qui ne le composent pas. Coût réel faible (titres courts) ; à surveiller, pas
  à corriger.
- P2 — `block-size` de la FAQ : mise en page par frame, inévitable pour un dépliant ; confinée à la
  question.

## 12. Matériaux et profondeur

**État.** Barre : `rgba(255, 253, 250, 0.9)` + `blur(18px) saturate(135%)` + filet `line`
(`app/globals.css:687-699`), transparente en haut de page sur grand écran, toujours matière en
mobile. Panneau du menu : `bg-surface` opaque, posé sur la barre translucide — on n’empile pas
deux surfaces translucides : conforme. Replis `prefers-reduced-transparency` et
`prefers-contrast` présents et mesurés conformes (`:974-996`).

**Justification de la translucidité de la barre (à conserver).** Elle est fonctionnelle, pas
décorative : la barre flotte au-dessus d’un contenu qui défile (photos, section encre) ; laisser
deviner ce qui passe dessous garde le lecteur dans sa page sans consommer une bande opaque. À
90 % d’opacité, le texte encre reste au-dessus de 15:1 quel que soit le fond ; aucune ombre, aucun
reflet, aucune teinte froide — le blanc chaud de la charte. Cette décision contredit
`NIVEAU-SUPERIEUR.md` (« `bg-surface` opaque, pas de `backdrop-blur` ») : **mettre la spécification à
jour** pour qu’une seule règle fasse foi.

**Écarts.**
- P1 — `.projet-carte__ouvrir` (`app/globals.css:435-445`) : pastille en verre (`blur(14px)`) bordée
  de blanc (`rgba(255, 255, 255, 0.48)`) posée sur une photo. C’est du verre décoratif — le blanc pur
  et le flou n’y apportent aucune information — et la charte n’a pas de blanc pur. Remplacer par un
  aplat : `background: var(--color-surface); border: 1px solid var(--color-line); backdrop-filter: none;`.
- P2 — `saturate(135%)` sur la barre : rehausse les couleurs des photos qui passent dessous, effet
  plus « verre iOS » que « papier ». Passer à `backdrop-filter: blur(16px)` seul.
- P2 — lisibilité sur matière (vibrancy) : `.nav-link` en `ink-muted` 500 sur la barre translucide.
  Sur la pilule, passer à `font-weight: 600` ou à `text-ink` pour l’état non survolé.
- P1 — **le menu mobile est modal sans le dire visuellement.** Il piège le focus
  (`Header.tsx:110-169`) mais la page reste pleinement lumineuse et défilable dessous. Le skill :
  une tâche modale associe sa surface à un voile. Ajouter un voile fonctionnel, encre à 12 %, sous
  le panneau, qui ferme au toucher :

```tsx
// Header.tsx — frère du <nav>, dans le <header>
<div
  aria-hidden="true"
  data-open={open ? '' : undefined}
  onPointerDown={() => setOpen(false)}
  className="menu-voile md:hidden"
/>
```

```css
.menu-voile {
  position: fixed; inset: 0; z-index: -1;
  background: rgba(23, 19, 15, 0.12);   /* l’encre de la charte, pas un noir */
  opacity: 0; visibility: hidden;
  transition: opacity 200ms var(--ease-in-mirror), visibility 0s linear 200ms;
}
.menu-voile[data-open] {
  opacity: 1; visibility: visible;
  transition: opacity var(--dur-state) var(--ease-out), visibility 0s;
}
```

Ce voile remplace aussi l’écouteur `pointerdown` global des l. 155-160 (plus simple, et le geste
« toucher à côté pour fermer » devient visible).

## 13. Retour multimodal

**État.** Ni son ni vibration. C’est juste pour un site vitrine : la règle d’utilité du skill
l’interdit hors moments significatifs, et le seul candidat (envoi du formulaire réussi) ne la
justifie pas — le Vibration API n’existe pas sur iOS et surprendrait sur Android. Aucune action.

## 14. Mouvement réduit et accessibilité

**État.** Mesuré conforme : cartes à plat, aucun bloc voilé, défilement `auto`, animations
pilotées par le défilement enveloppées dans `no-preference` (doctrine bien écrite,
`app/globals.css:809-833`), lampe non montée, barre et pastille opaques sous transparence réduite,
contraste renforcé appliqué.

**Écarts.**
- P1 — **la FAQ s’anime toujours sous `reduce`** (mesuré : `0.25s, 0.25s`). La règle globale
  `*, *::before, *::after` (`app/globals.css:1024-1030`) n’atteint pas `::details-content`. Ajouter :

```css
@media (prefers-reduced-motion: reduce) {
  .faq-item::details-content { transition-duration: 0.01ms !important; }
}
```

- P2 — le `scale(0.97)` d’appui reste appliqué (instantané) sous `reduce`. Il est minuscule et non
  vestibulaire, mais le skill préfère un équivalent non spatial : sous `reduce`, remplacer par un
  assombrissement.

```css
@media (prefers-reduced-motion: reduce) {
  .press:active { transform: none; filter: brightness(0.92); }
}
```

- P2 — sous `reduce`, le menu mobile devient une coupure franche (0,01 ms). Garder un fondu
  d’opacité court, sans déplacement : `transform: none` et `transition: opacity 150ms ease,
  visibility 0s linear 150ms !important` sur `.menu-panel` (le sélecteur spécifique avec
  `!important` l’emporte sur la règle universelle).
- P2 — passer en revue les autres pseudo-éléments non couverts par la règle universelle :
  `::view-transition-*` (traité au §8), `::backdrop`, `::marker`.

## 15. Typographie — taille optique, approche, interligne

**État (mesuré en 1440).** h1 96 px / 0,98 / −0,05 em ; h2 54 px / 1,03 / −0,04 em ; h3 22 px / 1,3
/ −0,03 em ; question FAQ 19 px / −0,025 em ; chapô 17 px / 1,72 / 0 ; corps 16 px / 1,7 / 0 ;
étiquette 13 px / 1,4 / +0,1 em capitales. L’approche se resserre avec la taille, l’interligne
aussi, la hiérarchie combine graisse et taille : **conforme**. `font-optical-sizing: auto`, tailles
en `rem`, plancher `max(1rem, 16px)` qui respecte la taille de texte de l’utilisateur : conformes.
Police propriétaire justifiée par la charte (Plus Jakarta Sans 800, Newsreader 300).

**Écarts.**
- P2 — l’approche est fixe sur toute la plage d’un `clamp()` : `display-xl` vaut −0,05 em à 96 px
  **et** à 42 px (390 px de large). À 42 px, −0,05 em est serré pour du 800. Resserrer moins en
  petit :

```ts
// tailwind.config.ts:52-55 — l’approche suit la taille.
'display-xl': ['clamp(2.625rem, 7.4vw, 6rem)', { lineHeight: '0.98', letterSpacing: 'clamp(-0.05em, -0.02em - 0.25vw, -0.03em)' }],
```

  (même principe pour `display-lg` : de −0,03 em en petit à −0,05 em en grand.) Vérifier le rendu
  sur « savoir-faire » à 390 px.
- P2 — `text-note` (14 px) à 0 : un léger `+0.005em` aide la lecture en petit corps sur la pilule
  translucide (§12, vibrancy).

## 16. Fondations

**État.** Libellés précis (« Le studio », « Réalisations »), une action principale, retour
d’état à l’envoi (bouton « Envoi en cours… » à largeur figée), confirmation au succès avec focus
sur le titre, échec annoncé et répété à l’écran : conformes. Filtres réversibles (« Tout »).

**Écarts.**
- P1 — **orientation : la page courante n’est pas montrée.** `aria-current="page"` est posé
  (`Header.tsx:201` et `:255`) mais aucune règle ne le stylise (aucune occurrence dans
  `globals.css`). Réponse visuelle à « où suis-je ? » :

```css
.nav-link[aria-current='page'] { color: var(--color-ink); font-weight: 600; }
#mobile-menu a[aria-current='page'] { background: var(--color-sand); }
```

- P1 — **validation en ligne absente** (`components/forms/ContactForm.tsx:106-109`) : `useForm`
  tourne en mode `onSubmit` par défaut. Mesuré : « abc » dans l’e-mail puis sortie du champ → rien.
  Le skill : « valider en ligne, pas à l’envoi ». Passer en `mode: 'onTouched'` (première
  validation à la sortie du champ, puis à chaque frappe ; jamais pendant la première saisie).
- P1 — **l’erreur pousse le formulaire d’un coup** (+142 px à l’envoi vide, `components/ui/Field.tsx:120-124`).
  Faire entrer le message par une grille `0fr → 1fr` :

```tsx
// Field.tsx:120-124 — toujours monté, ouvert quand il y a une erreur
<div className="field-error" data-open={error ? '' : undefined}>
  <p id={errorId} className="text-note font-medium text-accent-deep">{error ?? ''}</p>
</div>
```

```css
.field-error { display: grid; grid-template-rows: 0fr; opacity: 0;
  transition: grid-template-rows var(--dur-state) var(--ease-out), opacity var(--dur-micro) var(--ease-out); }
.field-error > p { overflow: hidden; }
.field-error[data-open] { grid-template-rows: 1fr; opacity: 1; }
```

  Garder `aria-describedby` conditionnel (l. 59-60) : un nœud vide ne doit pas être annoncé.
- P2 — passage formulaire → confirmation (`ContactForm.tsx:207`) : échange instantané, la page
  change de hauteur. Un `Reveal`-like en opacité seule (150 ms) sur le panneau de confirmation
  suffit.
- P0 — **changement de page** : voir l’écart transversal ci-dessous.

### Écart transversal P0 — le défilement doux contamine la navigation

`html { scroll-behavior: smooth }` (`app/globals.css:38`) s’applique aussi au retour en haut que
Next fait à chaque changement de route, et à la restauration du retour arrière. Mesuré : depuis le
milieu de l’accueil, la page Services **défile visiblement** de 1833 à 0 px en ~740 ms ; le retour
arrière redescend de 0 à 1561 px en ~700 ms. Le visiteur voit la nouvelle page glisser sous lui à
chaque clic : c’est le contraire de la réponse immédiate.

Next 16 ne neutralise le défilement doux pendant la navigation **que si** `<html>` porte
`data-scroll-behavior="smooth"` (vérifié dans `node_modules/next/dist`). Correction en une ligne :

```tsx
// app/layout.tsx:115
<html lang="fr" data-scroll-behavior="smooth" suppressHydrationWarning>
```

Les ancres internes gardent leur défilement doux, les changements de route redeviennent
instantanés. Ajouter un test (§17).

P2, plus tard : une transition de page en fondu (View Transitions, `experimental.viewTransition`
de Next 16) — à n’envisager qu’une fois ce défaut corrigé, et seulement en opacité, 150 ms.

## 17. Méthode

**État.** `e2e/fluidite.spec.ts` couvre déjà le retour au repos de la carte, le mouvement réduit
et la largeur de la galerie ; `e2e/mouvement-degrade.spec.ts` couvre la dégradation. Bonne base.

**Tests à ajouter** (même technique que cet audit : échantillonnage par `requestAnimationFrame` ;
attention, la CSP refuse `eval` — passer des fonctions, pas des chaînes, ou `bypassCSP: true`) :

1. *Carte* : à l’entrée du pointeur, l’écart de `rotateY` entre deux frames consécutives reste
   sous 0,6° ; au retour pendant le repos, pas de saut supérieur à 0,6°.
2. *Menu* : à la fermeture, le panneau est encore `visible` avec une opacité > 0 à 60 ms ;
   `transform-origin` horizontal > 70 % de la largeur.
3. *Route* : depuis `scrollY = 2500`, clic sur Services → `scrollY === 0` à la première frame.
4. *Mouvement réduit* : `transitionDuration` de `.faq-item::details-content` ≤ 0,01 ms.
5. *Toucher* : contexte `hasTouch`, appui maintenu sur `.press` → `transform` ≠ `none` avant 120 ms
   (à valider sur Safari iOS réel, que Chromium n’émule pas pour `:active`).
6. *Formulaire* : « abc » dans l’e-mail puis `blur` → `aria-invalid="true"`.

Et, hors automates : relire chaque mouvement image par image (DevTools → Animations, vitesse
10 %), et tester la galerie et le menu sur un iPhone et un Android d’entrée de gamme réels — la
projection de l’élan et le rebond de bord ne s’émulent pas.

---

## Récapitulatif

### P0
| # | Écart | Fichiers |
| --- | --- | --- |
| 1 | Changement de route et retour arrière défilent visiblement (~740 ms) | `app/layout.tsx:115`, `app/globals.css:38` |
| 2 | Carte : saut d’inclinaison à l’entrée, coupure au retour pendant le repos | `components/realisations/ProjectCard.tsx:115-154` (+ `lib/motion/spring.ts` à créer) |
| 3 | Menu mobile : fermeture coupée (`visibility` immédiate), origine au centre, inversion invisible | `components/layout/Header.tsx:238-245`, `app/globals.css` (`.menu-panel`, `--ease-in-mirror`) |
| 4 | Aucun retour d’appui au toucher ; filtres, questions FAQ et liens du menu sans retour d’appui | `components/ClientShell.tsx`, `components/realisations/ProjectIndex.tsx:43-48`, `app/globals.css:628-630`, `components/layout/Header.tsx:256` |

### P1
- Validation en ligne (`mode: 'onTouched'`) — `components/forms/ContactForm.tsx:106-109`.
- Entrée des messages d’erreur sans saut — `components/ui/Field.tsx:120-124`.
- Page courante visible (`aria-current`) — `app/globals.css:681-683`.
- FAQ animée sous mouvement réduit — `app/globals.css:998-1031`.
- Survol collant au toucher (`hoverOnlyWhenSupported`, `.link-draw`) — `tailwind.config.ts`, `app/globals.css:456-459`, `:576-579`.
- Filtres en View Transition — `components/realisations/ProjectIndex.tsx:42`, `:61-65`.
- Pastille ↗ sans verre ni blanc pur — `app/globals.css:435-445`.
- Voile du menu modal — `components/layout/Header.tsx:155-160`, `:238`.
- Mesure du pointeur hors élément transformé ; ressort amortissement 1,0 / réponse 0,35 s — `ProjectCard.tsx:93`, `:125`.

### P2
- `.press` à 100 ms et commentaire de `Button.tsx:27-32` ; retirer l’utilitaire `transition` (`Button.tsx:134`, `Header.tsx:222`, `:232`).
- Lampe composée en `transform` au lieu d’un dégradé repeint — `components/motion/Lamp.tsx`, `app/globals.css:545-558`.
- Approche typographique qui suit le `clamp()` — `tailwind.config.ts:52-55`.
- Barre : `saturate` retiré, liens plus lisibles sur matière ; mettre `NIVEAU-SUPERIEUR.md` à jour sur la translucidité.
- Mouvement réduit : appui en luminosité, menu en fondu court.
- `max-width` de la barre, `clip-path` des titres : surveiller, ne pas corriger.
- Confirmation du formulaire en fondu ; transition de page en fondu, après le P0 n° 1.
