FAILLE SUR LA PAGE SURVEY

- Celui est pour la modification du chiffre depuis le front. Le site ne fait pas de vérif de l'input 
- vu que c'est un chiffre entre 1 et 10 l'objectif est de rentrer un nombre supérieur
- j'ai rentré 1000000 et en reotur le flag s'affiche.

RESOLUTION FAILLE:

- Securiser dans le back, sanitize l'input et ne pas lire automatiquement la valeur
