# davidlance.com

Une page, un fichier : `index.html`. Aucune dépendance, aucun build, aucun
`npm install`. Elle s'ouvre en double-cliquant dessus et se dépose telle quelle
sur n'importe quel hébergeur statique.

## Ce qu'il manque, et rien d'autre

1. ~~La photo~~ ✅ posée le 20/08, remplacée le 21/08 par la version dessinée
   `davinci__image1__transform_the_attached_photo_into_a_styli.png`.
   ⚠️ Si tu la remplaces, change le chemin dans le `.decor::before` du
   `<style>`. Un fond CSS qui pointe un fichier absent ne casse rien de visible :
   il rend simplement la page NOIRE, sans erreur et sans image manquante, et on
   cherche ailleurs.

2. ~~La ville~~ ✅ `CMR` (Cameroun), posée le 20/08.

3. ~~Le nom~~ ✅ « David Lance » confirmé le 20/08.

## Les deux réglages qui changent tout

- **La couleur d'accent** : une seule ligne, `--accent` en haut du `<style>`.
  Elle est en ambre par défaut parce que l'ambre tient sur presque tous les
  fonds sombres. À régler CONTRE la photo une fois qu'elle est là, c'est le
  genre de couleur qui ne se juge pas dans le vide.

- **Le cadrage de la photo** : il y en a DEUX, et ce ne sont pas deux réglages
  du même cadrage, ce sont deux mises en page.

  Sur **grand écran** (et sur téléphone COUCHÉ), la photo prend tout le cadre en
  `cover` et le `background-position` pousse le visage à droite de la colonne de
  texte.

  Sur **téléphone debout**, la photo est RÉDUITE à une bande haute : le visage
  entier y tient, et le bas de l'image se fond dans le noir par un masque. En
  `cover` sur un écran de 390 de large, une image de 1376x768 est agrandie près
  de quatre fois, le visage remplit tout l'écran, crâne et menton coupés hors
  cadre, et on ne reconnaît plus personne.

  ⚠️ Deux pièges si tu touches à ce réglage. Une image qui ne couvre plus laisse
  un BORD NET, c'est ce que le masque efface en bas ; et il ne fond que le bas,
  donc un écran plus large que haut repasse en `cover`, sinon la photo devient un
  petit rectangle flottant.

  ⚠️ Si tu changes la photo pour une VERTICALE, le réglage du grand écran
  redeviendra sans effet : `background-position` ne décale que s'il y a un
  débordement à décaler, et une photo verticale en `cover` remplit exactement
  la largeur. Il faudra alors `background-size: 135% auto`. C'est écrit dans le
  fichier, à l'endroit concerné.

## La traînée de jetons

Le curseur sème BTC, ETH, SOL et ADA derrière lui. Toujours rien à installer :
les quatre logos sont des SVG posés dans un `<template>` en bas d'`index.html`,
et le script qui les lâche tient en trente lignes.

Trois réglages, groupés en haut du script :

- `RONDE` — combien de jetons tournent en boucle (12). ⚠️ Un multiple de 4, sinon
  l'ordre BTC, ETH, SOL, ADA se décale d'un tour à l'autre.
- `PAS` — les pixels **parcourus** entre deux jetons. C'est de la distance, pas du
  temps : un `pointermove` tire cent événements par seconde, en poser un à chaque
  fois donne un tas de logos empilés sur place au lieu d'une trajectoire.
- `VIE` — la durée du fondu.

⚠️ **Rien sur téléphone**, et c'est voulu : sans souris il n'y a pas de curseur,
donc pas de traînée. Le script s'arrête à sa première ligne et ne construit rien.

⚠️ **La coupure « moins de mouvement » est dans le SCRIPT, pas dans le `<style>`.**
Une animation lancée en JavaScript ne lit aucune règle CSS : le
`@media (prefers-reduced-motion)` en bas de la feuille ne l'atteint pas.

⚠️ Les couleurs des logos ne sont pas toutes celles des chartes. Le bleu Cardano
officiel (`#0033AD`) est presque invisible sur un fond noir, il est éclairci.
Les tracés `d`, eux, sont les officiels : ils ne se retouchent pas à la main, on
remplace un SVG entier ou on n'y touche pas.

## Les cartes de contact

En bas, le pavé ambre « Write to me » et la carte Instagram ont laissé place à
une rangée de pions et à **une seule carte** qui voyage de l'un à l'autre. Une
carte par pion, ce sont deux cartes qui se croisent en fondu au moment du
passage ; une seule carte qui glisse, c'est un objet qu'on suit des yeux.

Pour ajouter un réseau, il faut **deux blocs qui se répondent** :

1. un `<article class="social-apercu" id="apercu-xxx">` dans `.social-carte`,
2. un `<a class="social-pion" … aria-describedby="apercu-xxx">` dans
   `.social-liste`, **dans le même ordre**.

⚠️ L'ordre compte : le script apparie les pions et les aperçus par leur RANG,
pas par leur `id`. Un aperçu ajouté au milieu et une carte affiche le mauvais
compte.

⚠️ **L'adresse mail ne se lit plus sans survol** : elle est dans la carte. C'est
le prix de la rangée, et c'est le seul vrai recul par rapport au pavé d'avant.
Le pion mail garde donc l'aplat ambre, seule couleur pleine de la page : sans
elle, la page ne demande plus rien, elle liste deux liens.

⚠️ **Au doigt, le premier appui ouvre la carte, le second suit le lien.** Un
écran tactile n'a pas de survol : sans cette règle, la carte ne s'afficherait
qu'en quittant la page, donc jamais.

Le « moins de mouvement » n'a rien demandé de spécial ici : tout est en
transitions CSS, que le `@media (prefers-reduced-motion)` de la feuille coupe
déjà. La carte s'ouvre alors d'un coup, sans voyage ni flou.

## Les trois langues

La page existe en anglais, en français et en espagnol. La langue est choisie
d'après celle du NAVIGATEUR (`navigator.languages`), pas d'après le pays : le
Cameroun est bilingue, un pays ne dit pas dans quelle langue on lit. Un
sélecteur `EN FR ES`, au bout du filet de la première accroche, permet de
forcer, et le choix est retenu dans le navigateur.

Les langues qu'on ne parle pas ont un repli par **proximité**, dans
`PROCHES` : le portugais, le galicien et le catalan reçoivent l'espagnol, tout
le reste reçoit l'anglais. Un Brésilien lit l'espagnol bien plus facilement que
l'anglais.

⚠️ La proximité est testée langue par langue **dans l'ordre**, pas à la fin en
dernier recours. Chrome ajoute souvent l'anglais en secondaire
(`["pt-BR", "pt", "en-US", "en"]`) : un repli cherché après coup trouverait cet
anglais-là et le servirait à quelqu'un qui a demandé le portugais en premier.

⚠️ L'italien n'est PAS dans la table, volontairement : il est aussi près du
français que de l'espagnol, le choix serait arbitraire. Deviner faux agace plus
que l'anglais, qui ne se lit jamais comme une erreur, seulement comme un défaut.

Chaque phrase existe **trois fois** dans `index.html`, en trois éléments qui se
suivent, chacun avec sa classe `trad` et son attribut `lang`. Le CSS cache les
deux qui ne servent pas. Pour changer une phrase, il faut donc en changer trois.

⚠️ **Le petit script du `<head>` doit rester dans le `<head>`.** Il ne fait que
poser la langue sur la balise `<html>`, mais il la pose AVANT le premier
affichage. Descendu en bas du fichier, la page s'afficherait une fraction de
seconde en anglais avant de basculer, à chaque visite.

⚠️ **La règle CSS ne fait que cacher**, elle ne montre jamais. Une règle qui
montrerait (`display: block`) écraserait le `flex` de `.accroche` et du `.lieu`
et casserait leur mise en page dans deux langues sur trois.

⚠️ Trois choses ne sont PAS traduites par le CSS, parce qu'elles ne sont pas
dans le corps de la page : le titre de l'onglet et l'étiquette du sélecteur, que
le script réécrit à la main, et la **description pour les réseaux sociaux**
(`<meta name="description">` et `og:`), qui reste en anglais pour tout le monde.

⚠️ Les trois versions sont dans le fichier, donc un moteur de recherche voit les
trois sur la même adresse. Sans importance pour une page de présentation ; le
jour où le référencement par langue compte, il faudra trois adresses distinctes,
et ce n'est plus un fichier unique.

⚠️ Sans JavaScript, la page reste en anglais et les trois boutons ne font rien.
C'est le repli voulu : `<html lang="en" data-langue="en">` est écrit en dur.

## Mettre en ligne

Le plus simple, sans compte à créer ni configuration :

```
npx vercel deploy --prod
```

depuis ce dossier. Vercel détecte un site statique tout seul. Le domaine
`davidlance.com` se branche ensuite dans les réglages du projet.

## L'ordre des blocs

Identité, puis cinq grandes lignes, puis les contacts, puis la ville.

Chaque grande ligne est un `<p class="ligne">` suivi d'un `<p class="note">`
optionnel, dont le début en gras sert d'étiquette. C'est le seul motif de la
page : pour ajouter ou retirer une idée, on ajoute ou on retire cette paire.

⚠️ Le gros texte est le seul endroit où la page hausse la voix. Un deuxième
niveau de grande taille ailleurs et l'effet tombe.

⚠️ Ce dépôt est PUBLIC et le fichier est servi tel quel : tout ce qu'on écrit
en commentaire se lit en « afficher la source » sur le site en ligne.
