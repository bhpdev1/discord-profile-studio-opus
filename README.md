# PFPair Studio — Édition Opus

*[Read in English](README.en.md)*

<p align="center">
  <a href="https://pfpair-opus.vercel.app">
    <img src="https://img.shields.io/badge/Demo%20en%20Direct%20(Vercel)-pfpair--opus.vercel.app-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Live Demo Vercel" />
  </a>
  <img src="https://img.shields.io/badge/Traitement-100%25%20Local%20(Navigateur)-22c55e?style=for-the-badge" alt="100% Local" />
  <img src="https://img.shields.io/badge/Plateformes-10%20Presets%20Calibr%C3%A9s-3b82f6?style=for-the-badge" alt="10 Destinations" />
  <img src="https://img.shields.io/badge/Bo%C3%AEte%20%C3%A0%20outils-14%20Modules-f59e0b?style=for-the-badge" alt="14 Tools" />
  <img src="https://img.shields.io/badge/Mod%C3%A8le-Claude%20Opus%205-d97757?style=for-the-badge" alt="Claude Opus 5" />
</p>

> **Studio web gratuit pour créer un avatar et une bannière parfaitement raccordés, à partir d'une seule image.**  
> Démo en ligne accessible immédiatement sur : **[https://pfpair-opus.vercel.app](https://pfpair-opus.vercel.app)**

---

## 🎯 À quoi sert PFPair ?

Sur Discord, X, LinkedIn ou YouTube, l'avatar et la bannière sont deux images séparées,
aux dimensions différentes, mais affichées l'une sur l'autre. Les recadrer séparément
casse presque toujours la continuité : l'épaule coupée ne se prolonge pas, le décor ne
s'aligne pas, la photo de profil « flotte » au-dessus de la bannière.

**PFPair découpe les deux formats dans la même scène.** On importe une seule image, on la
cale une fois, et le site exporte l'avatar et la bannière aux dimensions exactes de la
plateforme, alignés au pixel près à l'endroit où l'avatar chevauche la bannière.

> *Un redimensionneur coupe deux fois. PFPair coupe une seule fois.*

### Trois gestes, moins d'une minute

| Étape | Action |
|:---:|---|
| **01 — Importe** | Dépose une photo JPG, PNG ou WebP. Elle reste dans ton navigateur. |
| **02 — Cale** | Choisis la destination, déplace et zoome la scène, contrôle le raccord en direct sur un aperçu fidèle au vrai profil. |
| **03 — Exporte** | Récupère un ZIP avec les deux PNG nommés et dimensionnés correctement. |

### Pour qui ?

- **Utilisateurs Discord** qui veulent un profil cohérent (aperçu *profil complet* et *mini-profil*, calibré sur l'interface desktop).
- **Créateurs, streamers et community managers** qui doivent décliner la même identité visuelle sur plusieurs réseaux.
- **Tous ceux qui veulent un outil rapide et privé** : aucun compte, aucun filigrane, aucune image envoyée sur un serveur.

### 10 plateformes calibrées

| Plateforme | Bannière | Avatar |
|---|---|---|
| Discord | 1200 × 420 | 512 × 512 |
| X / Twitter | 1500 × 500 | 400 × 400 |
| Facebook | 851 × 315 | 320 × 320 |
| LinkedIn | 1584 × 396 | 400 × 400 |
| SoundCloud, YouTube, Twitch, Pinterest, Mastodon, Reddit | presets dédiés | presets dédiés |

Chaque preset embarque la géométrie mesurée de l'avatar (position, taille, forme) pour que
l'aperçu corresponde à ce que la plateforme affiche réellement, avec la source utilisée
(spécifications officielles ou interface calibrée).

### Confidentialité vérifiable

Tout le traitement se fait dans le navigateur (canvas). La politique de sécurité du site
(`connect-src 'self'`) **interdit techniquement toute requête sortante** : la promesse
« aucune image n'est envoyée » est garantie par le navigateur, pas seulement annoncée.

### Modèle gratuit

- **PFPair Free — 0 €, sans compte** : 10 plateformes, aperçu Discord complet et compact, export avatar + bannière en PNG et ZIP, sans filigrane.
- **PFPair Creator — bientôt** : brand kits sauvegardés, variantes, exports en lot, overlays et projets clients. L'export de base restera toujours gratuit.

---

## 📸 Aperçu & Interface

| La scène maître & le raccord parfait | Le studio & le compositeur en direct |
| :---: | :---: |
| ![Scène maître](screenshots/hero.png) | ![Studio](screenshots/studio.png) |

| Boîte à outils complète (14 outils navigateur) | Vue mobile responsive |
| :---: | :---: |
| ![Boîte à outils](screenshots/tools.png) | ![Vue mobile](screenshots/mobile.png) |

---

## 🤖 Deux versions, deux modèles — un seul auteur

PFPair existe en deux versions, toutes deux conçues par moi [bhpdev1](https://github.com/bhpdev1). J'ai développé le même produit avec deux modèles d'IA différents, pour comparer leur approche du design et de l'ingénierie sur une base fonctionnelle identique :

- **`pfpair-studio-openai`** — version réalisée avec **GPT 5.6 Sol**
- **`pfpair-studio-anthropic`** — **cette version**, réalisée avec **Claude Opus 5**

Les deux versions sont indépendantes et peuvent tourner côte à côte pour comparer.

| | Version GPT 5.6 Sol (`pfpair-studio-openai`) | **Version Claude Opus 5 (`pfpair-studio-anthropic`, celle-ci)** |
|---|---|---|
| Fond | graphite `#0b0c0f` + WebGL polarisé violet/bleu | gris neutre calibré, chroma 0, trame de plaque |
| Accent de marque | violet PFPair `#8a7cf6` | **aucun** — la seule chroma vient de la destination active |
| Typographie | Figtree (300–900) | Archivo exploité sur l'axe `wdth` 86–100 + JetBrains Mono pour les chiffres |
| Géométrie | rayons 7–18 px, cartes flottantes en perspective | angles vifs (0–2 px), filets d'1 px, repères de calage |
| Hero | carte produit inclinée, lumière réactive | plaque cotée comme un plan technique |
| Formats | grille de 10 cartes | répertoire tabulaire à 6 colonnes |
| Feuilles de style | `styles.css` + `pfpair-ui.css` + `seo-pages.css` (~172 Ko) | `bench.css` (~62 Ko) |

La direction artistique complète, les tokens et les anti-patterns sont dans
[`DESIGN.md`](DESIGN.md).

## Ce qui est repris tel quel

- `platforms.js` — les 10 presets, dimensions et géométries d'avatar mesurées.
- `app.js` — import, drag, zoom, rendu canvas, export PNG et ZIP sans dépendance.
- `visuals.js` — icônes Lucide locales, logos Simple Icons, révélations au scroll,
  galerie d'exemples.

## Les modifications apportées au JS

Elles corrigent des défauts constatés au navigateur, pas la direction artistique :

1. `app.js` / `renderPlatformPicker()` — `scrollIntoView({block:"nearest"})` faisait remonter
   toute la page vers le studio au premier rendu. Remplacé par un recentrage horizontal du
   rail (`scrollLeft`).
2. `app.js` / `renderPlatformPicker()` — suppression de `role="listitem"` sur les boutons de
   destination : `aria-pressed` n'y est pas autorisé. Le rail est un `role="group"`.
3. `visuals.js` / `initShowcaseGallery()` — le nom accessible du bouton de changement
   d'exemple ne contenait pas son libellé visible (« changer »).
4. `app.js` et `tools.js` / `triggerDownload()` — l'URL blob était révoquée 1,5 s (studio)
   et 4 s (outils) après le clic, et l'ancre retirée dans la même tâche. Si Chrome lit
   encore le blob à ce moment — analyse antivirus, disque lent, invite de la barre de
   téléchargement — le fichier écrit est tronqué et s'ouvre en pixels aberrants. L'URL est
   désormais gardée vivante jusqu'au `pagehide`, avec un filet à 10 minutes, et l'ancre
   est retirée au tick suivant.
5. `app.js` / `draw()` — un contour décoratif de 1,25 px en couleur d'accent était tracé
   sur le bord de l'avatar, c'est-à-dire exactement sur la jointure du raccord. Les pixels
   dessous étaient parfaitement continus, mais un trait coloré posé sur le joint fait lire
   une rupture. Retiré : Discord n'en dessine pas non plus, son anneau étant déjà simulé
   par le cercle extérieur rempli en couleur de profil.
6. `tools.js` / filigrane — l'ancrage utilisait la taille de police comme demi-largeur.
   « PFPair » en 56 px mesure 179 px, donc un filigrane ancré à droite sortait du cadre ;
   une rotation aggravait le débordement. L'ancrage mesure désormais la marque réelle
   (`measureText` ou dimensions de l'image) et tient compte de la boîte pivotée.

## La suite d'outils

Un onglet **Outils** dans la navigation ouvre `tools/`, un annuaire de quatorze entrées :
le studio natif plus les treize outils d'iLoveIMG, reconstruits pour tourner
entièrement dans le navigateur.

| Outil | Page | Lot | Particularité |
|---|---|:---:|---|
| Compresser | `tools/compress-image/` | oui | affiche l'octet gagné avant export |
| Redimensionner | `tools/resize-image/` | oui | pixels ou pourcentage, verrou de ratio |
| Recadrer | `tools/crop-image/` | — | éditeur visuel + coordonnées, 6 ratios |
| Convertir en JPG | `tools/convert-to-jpg/` | oui | couleur de fond pour la transparence |
| Convertir depuis JPG | `tools/jpg-to-image/` | oui | vers PNG ou WebP |
| Éditeur photo | `tools/photo-editor/` | — | filtres natifs, cadre, légende positionnable |
| Agrandir | `tools/upscale-image/` | — | ×2/×3/×4, passes successives + accentuation |
| Détourer | `tools/remove-background/` | — | remplissage par diffusion depuis les bords |
| Générateur de mèmes | `tools/meme-generator/` | — | Impact, contour, retour à la ligne automatique |
| Pivoter | `tools/rotate-image/` | oui | quarts de tour, miroirs, angle libre |
| Filigrane | `tools/watermark-image/` | oui | texte ou logo, 9 positions, mosaïque |
| Flouter | `tools/blur-face/` | — | zones tracées, flou/pixels/aplat |
| HTML en image | `tools/html-to-image/` | — | SVG foreignObject, sortie PNG/JPG/SVG |

### Architecture

Un registre unique dans `tools.js` décrit chaque outil : ses contrôles, sa fonction de
rendu et son format de sortie. Le moteur en déduit l'interface, l'aperçu en direct, le
traitement par lot et l'export — les pages HTML ne contiennent qu'un
`<div id="toolRoot" data-tool="…">`. Ajouter un outil, c'est ajouter une entrée au
registre puis régénérer la page.

L'archive ZIP est produite par un empaqueteur *store* embarqué dans `tools.js`, sans
dépendance externe, comme celui du studio.

### Trois écarts assumés avec iLoveIMG

Ces outils portent le même nom que leur équivalent commercial mais reposent sur une
technique différente. C'est écrit sur chaque page concernée, pas seulement ici :

1. **Le détourage n'utilise pas d'IA.** Il retire les pixels proches d'une couleur de
   référence par diffusion depuis les bords. Excellent sur fond uni ou studio,
   approximatif sur une scène complexe.
2. **L'agrandissement ne reconstruit rien.** Interpolation multi-passes avec masque flou,
   pas de modèle génératif : aucun détail absent de l'original n'apparaît.
3. **HTML en image part de code collé, pas d'une URL.** Capturer un site distant exigerait
   un serveur de rendu, ce que PFPair n'utilise pas.

Le compromis est assumé : la contrepartie est qu'aucune image ne quitte l'appareil et
qu'aucun de ces outils n'a besoin de réseau une fois la page chargée.

## Contenu

Une page principale avec le studio, un annuaire d'outils et ses treize pages,
et cinq pages éditoriales (`discord-pfp-banner-maker/`, `matching-pfp-banner/`,
`discord-banner-size/`, `x-header-avatar-maker/`, `linkedin-profile-kit/`). Les dimensions,
sources officielles et FAQ sont reprises ; seules la structure de page et la voix
rédactionnelle suivent la nouvelle direction.

## Vérifications effectuées

Chrome 151, viewports 1440 × 900 et 390 × 844 :

- Lighthouse **accessibilité 100 / bonnes pratiques 100 / SEO 100** sur la page principale,
  une page guide, l'annuaire d'outils et une page d'outil ;
- les treize outils testés au navigateur : rendu obtenu, aperçu correct, et export vérifié
  par signature binaire (ZIP `50 4b 03 04`, JPEG `ff d8`, PNG `89 50 4e 47`) ;
- chaîne d'export contrôlée de bout en bout sur le floutage : le blob est redécodé et ses
  pixels comparés à l'aperçu, puis le fichier écrit sur le disque est vérifié en taille,
  en en-tête et en marqueur de fin ;
- aucun message console, aucune ressource en 404 ;
- pas de débordement horizontal à 390 px (seul le rail de destinations défile, par
  conception) ;
- contrastes : `--ink-2`, `--ink-3`, `--on-slab-2` et `--on-slab-3` sont les valeurs les plus
  claires qui tiennent 4.5:1 sur leurs surfaces respectives — le champ gris comprime la
  plage utilisable, les tokens sont calés en conséquence ;
- `prefers-reduced-motion: reduce` neutralise transitions, animations et révélations ;
- le contenu reste visible si le JS échoue : l'état masqué des révélations est conditionné
  à la classe `motion-ready` posée par `visuals.js`.

## Licences

Archivo et JetBrains Mono sont distribués sous SIL Open Font License 1.1. Lucide est sous
licence ISC. Simple Icons est sous CC0-1.0 ; les marques représentées restent la propriété
de leurs détenteurs et servent uniquement à identifier les destinations d'export.

## Mise en production

Projet statique : aucun build, aucune dépendance serveur. `vercel.json` est déjà en place
et couvre trois choses.

**`trailingSlash: true`** — tous les liens internes et le `sitemap.xml` utilisent des URL
terminées par `/` (`/tools/compress-image/`). Sans ce réglage, Vercel redirigerait chaque
lien en 308.

**Une CSP qui rend la promesse de confidentialité vérifiable.** Le site répète partout
qu'aucune image n'est envoyée ; `connect-src 'self'` le fait respecter par le navigateur
lui-même, quoi que fasse le JavaScript. Les autres directives autorisent strictement ce
dont le site a besoin :

| Directive | Pourquoi |
|---|---|
| `script-src 'self'` | aucun script tiers, aucun script en ligne |
| `style-src 'self' 'unsafe-inline' fonts.googleapis.com` | la feuille Google Fonts, et les styles posés par `tools.js` |
| `font-src 'self' fonts.gstatic.com` | Archivo et JetBrains Mono |
| `img-src 'self' data: blob: cdn.jsdelivr.net` | images locales, SVG en `data:` de HTML-en-image, décodage en `blob:`, logos Simple Icons |
| `connect-src 'self'` | **aucune requête sortante possible** |
| `frame-ancestors 'none'` | le site ne peut pas être embarqué dans une iframe |

**Cache long sur `/assets/`** uniquement : ces images ne changent jamais. Le reste garde
le défaut Vercel, revalidé à chaque visite, pour qu'un redéploiement soit visible tout de
suite.

---

## 📄 Licence & Droits

Ce dépôt constitue la vitrine publique et la documentation technique du projet **PFPair**.  
Le code source complet de l'application est maintenu dans un dépôt privé propriétaire.

Tous droits réservés © 2026.

## 👤 Crédits

Développé par [bhpdev1](https://github.com/bhpdev1)
