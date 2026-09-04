# `public/images/` — où déposer les photos

Ce dossier ne contient que des **fichiers servis en ligne**. Les fichiers d’origine sortis de
ChatGPT (les « masters ») restent sur votre disque, hors du dépôt : ils sont trop lourds.

La liste complète des images attendues, leurs prompts et leurs dimensions sont dans
[`docs/imagerie.md`](../../docs/imagerie.md).

## 1 · Nommage

Un fichier = un identifiant du tableau B de `docs/imagerie.md`, en minuscules, sans accent,
sans espace, mots séparés par un tiret.

```
public/images/hero-atelier.jpg
public/images/craft-site.jpg
public/images/craft-visibilite.jpg
public/images/craft-outils.jpg
public/images/about-atelier.jpg
public/images/fond-aplat.jpg
public/images/og-defaut.jpg
public/images/og-accueil.jpg
public/images/og-services.jpg
public/images/og-about.jpg
public/images/og-contact.jpg
```

> N’utilisez **pas** `.png` : le `.gitignore` du dépôt ignore actuellement tous les `*.png`, le
> fichier ne serait jamais versionné. Le JPEG est le bon format de dépôt.

## 2 · Deux familles, deux traitements

| Famille | Fichiers | Ce que vous déposez | Qui optimise |
| --- | --- | --- | --- |
| Images de page | `hero-*`, `craft-*`, `about-*`, `fond-*` | un seul JPEG de qualité 82, à la dimension source du tableau B | `next/image`, qui produit les dérivés WebP/AVIF à la volée |
| Images de partage | `og-*` | un JPEG 1200 × 630 définitif, ≤ 300 ko | personne — le fichier est servi tel quel aux réseaux sociaux |

Les réseaux (WhatsApp, LinkedIn, Slack) ne lisent pas l’AVIF de façon fiable : les `og-*` restent
en JPEG, sans exception.

## 3 · Redimensionner et compresser

`sharp` est déjà installé dans le dépôt : aucune installation supplémentaire. Lancez les commandes
depuis la racine du projet, en remplaçant le chemin du master.

**Image de page (héro, 2400 px de large)**

```bash
node -e "require('sharp')('C:/masters/hero-atelier.png').resize(2400).jpeg({quality:82,mozjpeg:true,chromaSubsampling:'4:4:4'}).toFile('public/images/hero-atelier.jpg')"
```

**Image de page (plaques 4/3, 1600 px de large)**

```bash
node -e "require('sharp')('C:/masters/craft-site.png').resize(1600).jpeg({quality:82,mozjpeg:true}).toFile('public/images/craft-site.jpg')"
```

**Image de partage (recadrage strict en 1200 × 630)**

```bash
node -e "require('sharp')('C:/masters/og-accueil.png').resize(1200,630,{fit:'cover',position:'attention'}).jpeg({quality:80,mozjpeg:true}).toFile('public/images/og-accueil.jpg')"
```

**Dérivés AVIF/WebP à la main** (facultatif — seulement si vous voulez court-circuiter
l’optimiseur de Next)

```bash
node -e "require('sharp')('public/images/hero-atelier.jpg').avif({quality:62,effort:6}).toFile('public/images/hero-atelier.avif')"
node -e "require('sharp')('public/images/hero-atelier.jpg').webp({quality:78}).toFile('public/images/hero-atelier.webp')"
```

**Sans Node, avec ffmpeg**

```bash
ffmpeg -i hero-atelier.png -vf scale=2400:-1 -q:v 3 public/images/hero-atelier.jpg
```

## 4 · Vérifier le poids

```bash
node -e "const fs=require('fs');fs.readdirSync('public/images').filter(f=>/\.(jpg|avif|webp)$/.test(f)).forEach(f=>console.log((fs.statSync('public/images/'+f).size/1024).toFixed(0).padStart(5)+' ko  '+f))"
```

Les plafonds sont dans le tableau B de `docs/imagerie.md`. Au-dessus, on rebaisse la qualité JPEG
de 82 à 78 — jamais on ne réduit les dimensions.

## 5 · Brancher l’image dans le site

Le composant est déjà prêt. Pour les trois plaques de la page d’accueil, il suffit d’ajouter le
chemin dans `lib/data/site.ts` :

```ts
{
  id: 'site',
  // …
  imageSrc: '/images/craft-site.jpg',
  imageAlt: 'Un téléphone posé à plat sur le comptoir en bois clair d’un commerce, …',
}
```

Pour la plaque héro, la ligne exacte à écrire est en commentaire dans
`components/sections/HeroSection.tsx`.

Les textes alternatifs définitifs sont déjà rédigés : ne les réécrivez pas, recopiez-les depuis
`docs/imagerie.md`.
