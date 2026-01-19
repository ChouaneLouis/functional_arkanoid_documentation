## Cahier des charges -- sujet
Le jeu Arkanoid est un casse-brique commercialisé en 1986 1. Le but de ce projet est de reproduire plus ou moins le comportement de ce type de jeu, notamment en traitant a minima les points suivants : 
- simuler le mouvement et les rebonds d’une balle, sur la raquette, les briques et les bords de l’écran. La balle sera constamment et très légèrement accélérée au fur et à mesure de la partie et en cas de rebond sur un objet. Elle sera également soumise à la pesanteur (comme en TP). 
- gérer le déplacement de la raquette, en fonction des mouvements de la souris. La vitesse de la raquette lors du contact avec la balle doit permettre de communiquer une certaine impulsion à cette dernière, afin de accélérer ou de la ralentir horizontalement. 
- représenter les briques présentes et détecter les collisions avec la balle, auquel cas les briques touchées disparaissent. 
- calculer et afficher un score en fonction par exemple des briques touchées, qui peuvent porter des valeurs différentes. 
- gérer la perte de balle et le redémarrage ou non de la partie en fonction du nombre de balles restantes

## Usage et fonctionnalité
**Coté utilisateur :**
- contrôle via la sourie
- interface graphique
- nombre de vie -> défaite/victoire
- affichage du score
**Coté dev :**
- représentation de vecteur et forme géométrique : [[geometry]]
- représentation et logique du jeu : [[game]]
- simulation physique : déplacement + collision  ([[physic]])
- input utilisateur : flux d'[[input]] (mouse move, mouse click) 
- *machine à état* : permet de représenté l'état de l'interface (game over, en cours de partie, entre 2 balles)