# Automates
Le jeu de la vie a été inventé par le mathématicien John Conway dans les années 70. Il consiste à regarder l'évolution d'un automate cellulaire au cours du temps avec les règles suivantes: 

- Une cellule (case noire) survit au tour suivant si elle a deux ou trois cellules voisines. Elle disparaît (devient case blanche) sinon.

- Une cellule naît (passe de case blanche à case noire) au tour suivant si elle a 3 cellules (cases noires) voisines.

L'utilisateur peut voir l'évolution de l'automate selon le nombre d'itérations choisi. Il peut également modifier la taille de la grille.

**Tags**: *VUE 3, Options API*

![Image](https://github.com/AvirKarakitsos/VUEautomate/blob/main/src/assets/screenshot.png?raw=true)

Reference: ScienceEtonnante https://www.youtube.com/watch?v=S-W0NX97DB0

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```