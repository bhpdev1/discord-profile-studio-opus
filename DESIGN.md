# PFPair — direction artistique — édition Opus

Version : 24 août 2026 · édition Claude Opus 5 · fichier unique `bench.css`

## La scène

Quelqu'un est assis devant son écran, sur le point de changer l'image que des milliers de
gens verront de lui. Il ne consulte pas une landing page : il **juge une image**. Il regarde
un cadrage, une couleur, un raccord à quelques pixels près.

Cette phrase impose deux choses :

1. **Le chrome ne doit pas avoir de couleur.** On ne juge pas une image contre du crème,
   du bleu nuit ou du violet. On la juge contre un gris neutre — c'est la raison d'être
   d'une cabine de contrôle colorimétrique et du gris 18 % en photographie.
2. **L'outil doit ressembler à un instrument, pas à un site.** Angles vifs, filets d'un
   pixel, cotes chiffrées, repères de calage.

Référence nommée : **face d'instrument Braun × table de proofing photo.** Gris neutre pour
le chrome, dalle noire pour la machine, une seule couleur.

## La règle de couleur

> PFPair n'a pas de couleur de marque. Il prend celle de l'endroit où tu vas.

Toute la palette est à **chroma 0**. La seule chroma de la page vient de `--dest`, pilotée
par la destination sélectionnée. Choisir Twitch fait passer la barre de progression, la
pastille active, le point de vie du compositeur, le soulignement des étapes et le bouton
d'export en violet Twitch. Choisir SoundCloud les fait passer en orange.

Ce n'est pas un effet : c'est la promesse du produit rendue visible. Le principe existait
dans la version d'origine (« chrome neutre, accent de la destination active ») mais un
violet de marque le contredisait ; ici il est poussé jusqu'au bout.

### Tokens

```
--bench-0  oklch(0.868 0 0)   champ de la page
--bench-1  oklch(0.923 0 0)   surface posée dessus
--bench-2  oklch(0.818 0 0)   creux, fonds d'image
--slab-0   oklch(0.188 0 0)   dalle outil, offre gratuite, footer
--slab-1   oklch(0.243 0 0)   puits de contrôle
--slab-2   oklch(0.305 0 0)   état sélectionné sur dalle

--ink       oklch(0.185 0 0)  texte principal
--ink-2     oklch(0.37  0 0)  texte secondaire       4.5:1 sur bench-0 et bench-1
--ink-3     oklch(0.44  0 0)  méta mono 11 px        4.5:1 sur bench-0 et bench-1
--on-slab   oklch(0.968 0 0)
--on-slab-2 oklch(0.742 0 0)                         4.5:1 jusque sur slab-2
--on-slab-3 oklch(0.665 0 0)                         4.5:1 sur slab-0 et slab-1
```

Un champ gris comprime la plage d'encre utilisable : ces valeurs sont les plus **claires**
qui tiennent 4.5:1. Les éclaircir casse le contraste, les assombrir écrase la hiérarchie.
Ne pas y toucher sans revérifier.

`--dest` est la couleur de marque réelle (pastilles, filets, points d'état).
`--dest-fill` en est une variante assombrie qui garantit 4.5:1 avec du blanc — c'est elle
qu'on utilise dès qu'un texte se pose dessus. Les dix couples sont déclarés en tête de
`bench.css` par `[data-platform="…"]`, `data-platform` étant posé sur `<html>` par `app.js`.

Cas particulier : X. Son accent officiel est un blanc cassé, invisible sur un champ clair.
Le CSS le remplace par `#101010`, qui est la couleur réelle de la marque sur fond clair.

## Typographie

**Archivo** seul, exploité sur son axe de chasse. La hiérarchie vient de la largeur autant
que de la graisse : `wdth` 86–90 pour les grands titres, 94–96 pour les intertitres et les
boutons, 100 pour le texte courant. Une seule famille tenue fermement bat une paire timide.

**JetBrains Mono** est réservé aux **nombres et aux mesures** : dimensions, cotes, ratios,
labels de colonne, index de fichiers. Jamais pour du texte courant — le mono comme
signifiant « technique » est un costume ; ici il porte de la donnée.

- H1 et CTA final : `clamp(2.8rem, 1.1rem + 6.2vw, 5.2rem)`, `wdth` 90, `wght` 800,
  interlettrage −0.042em, interligne 0.94.
- Les `<em>` des titres passent en `wght` 300 et en `display: block` — la seconde ligne
  est la respiration, pas un dégradé.
- Plafond d'affichage 5.2rem, plancher d'interlettrage −0.042em : au-delà on crie.

## Mouvement

- Contrôles : 140 ms. Transitions d'état : 220 ms. Révélations : 420 ms.
- Courbes : `cubic-bezier(.22,1,.36,1)` et `cubic-bezier(.16,1,.3,1)`. Pas de rebond.
- **Le changement de destination est instantané, sans transition.** Ce n'est pas un choix
  esthétique : Chrome ne réinvalide pas une transition `background-color` dont la valeur
  vient d'une variable CSS modifiée sur un ancêtre, et l'élément restait figé sur la
  couleur précédente. Toutes les propriétés alimentées par `--dest` sont donc déclarées
  sans transition. Ne pas les réintroduire sans revérifier le studio sur quatre plateformes
  d'affilée.
- Les révélations **enrichissent un contenu déjà visible**. L'état masqué est conditionné
  à `.motion-ready`, classe posée par `visuals.js` ; sans JS, tout s'affiche.
- `prefers-reduced-motion: reduce` neutralise tout et supprime le reflet de la plaque hero.

## Composants

- **Boutons** : rectangles à 2 px de rayon. Le primaire est encre pleine ; au survol il
  projette une ombre dure de 3 px dans la couleur de la destination — le seul « effet » du
  site, et il porte une information.
- **Plaque hero** : la scène maître cotée comme un plan technique, avec cotes verticale et
  horizontale en mono et quatre repères de calage posés autour du cadre, sur la plaque.
- **Dalle outil** : le studio est une seule dalle noire. Les trois modules de réglage sont
  des zones séparées par des filets, jamais des cartes dans une carte.
- **Répertoire de formats** : un tableau, pas dix cartes identiques. Six colonnes,
  destination / bannière / avatar / placement / action.

  **Deux systèmes de couleur y cohabitent, et il faut les distinguer.** `--dest` est la
  destination *active du studio*, posée sur `<html>` par `app.js` : elle pilote la barre de
  progression, le bouton d'export, le point du compositeur. `--row` est la destination
  *propre à chaque ligne*, déclarée par `.format-card[data-open-platform="…"]` : elle
  pilote la teinte de la ligne, sa pastille et sa flèche. Survoler Twitch montre donc le
  violet Twitch même quand le studio est sur Discord — le répertoire est une liste de
  destinations, chacune se présente avec sa propre couleur.

  Les deux blocs de valeurs sont adjacents en tête de `bench.css` et doivent rester
  synchronisés. Ils sont écrits en hex littéral des deux côtés, sans token commun
  intermédiaire, pour rester lisibles au même endroit.
- **Formes de placement** : carré plein = calibré, cercle = dépend de la fenêtre,
  losange = kit avec zone sûre. La légende est sous le tableau.
- **Diagrammes de comparaison** : à gauche une bande et un disque détachés aux cadrages
  visiblement différents ; à droite une seule bande avec la fenêtre avatar tracée dedans.
  La continuité est vraie par construction, pas simulée.
- **Schémas des pages guides** : l'avatar rond reprend l'image du cadre via
  `background: inherit` puis `background-origin: border-box`, `background-size: 454.5%` et
  `background-position: 7.7% 78.6%`. Ces trois valeurs sont calculées pour que la découpe
  ronde prolonge exactement la bannière, quelle que soit la largeur d'écran. Elles
  dépendent de la géométrie déclarée (`width: 22%`, `bottom: -18%`, ratio 20:7) — si l'une
  change, il faut les recalculer.


## Les pages d'outils

Même grammaire que le studio, appliquée à quatorze surfaces : filet de section avec
la donnée en bout de ligne, h1 en Archivo étroit, puis **une dalle noire unique** coupée en
deux — l'aperçu à gauche, les réglages à droite. Aucune carte, seulement des filets.

- **Le damier de transparence** du `.tool-stage` n'est pas décoratif : le détourage produit
  des zones transparentes qu'il faut pouvoir distinguer d'un aplat blanc.
- **La couleur de destination reste la seule chroma.** Point de vie du compositeur, case
  active de la grille de position, bouton d'export, contour des zones de floutage : tous
  pilotés par `--dest`, comme le studio.
- **La hauteur de la dalle est réservée en CSS** (`min-height: clamp(500px, 72vh, 780px)`)
  parce que `tools.js` la remplit après le premier rendu. Sans cette réserve, le CLS
  atteignait 0,5. L'aperçu occupe la ligne `1fr` de `.tool-main` : la place réservée
  devient une zone d'aperçu plus grande, pas du vide.
- **Chaque page porte une note « Bon à savoir »** sous la dalle. Elle dit ce que l'outil ne
  fait pas — pas d'IA pour le détourage, pas de reconstruction pour l'agrandissement, pas
  de capture d'URL pour HTML en image. C'est une règle de voix, pas une option.

## La jointure du raccord

Le bord de l'avatar est l'endroit le plus sensible du site : c'est là que la promesse se
vérifie à l'œil. **Rien de décoratif ne doit y être tracé.** Un contour, même à 32 %
d'opacité, fait lire une rupture là où les pixels sont exactement continus.

Ce que la géométrie garantit, mesuré et non supposé : la bannière échantillonne la scène
en (0, 0, 600, 210) vers 1200 × 420, l'avatar en (59, 129.67, 159.33, 159.33) vers
512 × 512. Deux transformations affines uniformes sur la **même** scène, sans arrondi
intermédiaire. Une corrélation croisée entre les deux exports place l'optimum à
exactement (0, 0), avec un bassin symétrique — donc sans biais, même d'un demi-pixel.

## À éviter

- Texte en dégradé, verre décoratif, ombres colorées diffuses.
- Un accent de marque PFPair. Il n'y en a pas et il ne doit pas y en avoir : ce serait une
  deuxième couleur en concurrence avec la destination.
- Le kicker capitalisé espacé au-dessus de chaque section. Le repère de section est ici un
  **filet horizontal** avec un libellé bas de casse à gauche et une **donnée réelle** à
  droite (« 10 destinations », « ratio 20:7 »), et il ne s'applique pas à toutes les
  sections.
- Les numéros `01 / 02 / 03` en décor. Ils n'existent qu'à deux endroits où l'ordre porte
  une information : les trois gestes du workflow et les trois modules de réglage.
- Les rayons supérieurs à 2 px, les capsules, les cartes inclinées.
- Toucher aux niveaux d'encre sans revérifier les contrastes.
- Annoncer un outil comme « IA » quand il ne l'est pas. Trois outils diffèrent de leur
  équivalent commercial ; la note sous la dalle le dit à chaque fois.
- **Laisser une colonne de grille implicite `auto` dans la dalle.** `.preview-panel` et
  `.controls-panel` déclarent explicitement `grid-template-columns: minmax(0, 1fr)`. Sans
  cela, la colonne se dimensionne sur le `max-content` : un nom de fichier long et
  insécable (`9bb45c…e2dc0e.jpg`) fait passer la colonne de 325 à 428 px, le contenu
  déborde la dalle et toute la mise en page se décale à droite. `min-width: 0` sur le
  panneau ne suffit pas — il autorise le panneau à rétrécir, pas la colonne interne. Toute
  nouvelle zone ajoutée dans la dalle doit suivre la même règle.

## Vérifier après modification

```powershell
python -m http.server 4180
```

Lighthouse accessibilité doit rester à 100 sur `/` et sur une page guide. Vérifier ensuite
à 390 px que rien ne déborde en dehors du rail de destinations, et changer de plateforme
pour contrôler que la couleur se propage à la barre de progression, à la pastille active
et au bouton d'export.
