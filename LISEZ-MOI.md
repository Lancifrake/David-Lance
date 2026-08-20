# davidlance.com

Une page, un fichier : `index.html`. Aucune dépendance, aucun build, aucun
`npm install`. Elle s'ouvre en double-cliquant dessus et se dépose telle quelle
sur n'importe quel hébergeur statique.

## Ce qu'il manque, et rien d'autre

1. ~~La photo~~ ✅ posée le 20/08, en `portrait.png`.
   Le fichier peut s'appeler `portrait.png`, `.jpeg` ou `.jpg` indifféremment :
   les trois sont déclarés, la première qui existe gagne. C'est délibéré, parce
   qu'un fond CSS qui pointe un fichier absent ne casse rien de visible, il rend
   simplement la page NOIRE, sans erreur.

2. **La ville**, tout en bas de `index.html`, écrite « Ville à remplir ».
   Je ne l'ai pas devinée exprès.

3. **Le nom**, si « David Lance » n'est pas exactement ce que tu veux afficher.
   Je l'ai pris du nom de ce dossier.

## Les deux réglages qui changent tout

- **La couleur d'accent** : une seule ligne, `--accent` en haut du `<style>`.
  Elle est en ambre par défaut parce que l'ambre tient sur presque tous les
  fonds sombres. À régler CONTRE la photo une fois qu'elle est là, c'est le
  genre de couleur qui ne se juge pas dans le vide.

- **Le cadrage de la photo** : `background-position`, et il y en a DEUX,
  un pour le téléphone et un pour le grand écran. Ils ne se règlent pas
  ensemble : sur grand écran il s'agit de pousser le visage à droite de la
  colonne de texte, sur téléphone de le ramener au centre, parce qu'une photo
  paysage posée sur un écran vertical déborde énormément sur les côtés.

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
