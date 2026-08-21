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
