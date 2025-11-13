FAILLE SUR LE LOGIN PAS DEPUIS LA PAGE
BRUTEFORCE

Le but est de bruteforce les mots de passe pour l'utilisateur admin.

On recupere une liste de mots de passes en ligne les plus couramment utilises

source des mots de passes:
- https://gist.github.com/richardkundl/b68afdcf68240dcff50a

Ensuite on utilise un outil hydra qui permet de tester un nombre de mots de passes. avec cette commande:

hydra -l admin -P passwords.txt -s 8080 -f -V 127.0.0.1 \ 
  http-get-form \
  "/index.php:page=signin&username=^USER^&password=^PASS^&Login=Login:S=flag"

on passe en parametre:
- -l qui est une liste d'utilisateur => pour nous ce sera seulement admin
- -P fichier contenant tous les mdp
- -s le port sur lequel on effectue la requete
- l'ip correspondant au localhost
- l'url
- :S=flag => parametre hydra permettant de donner la condition de succes qui est le mot cle flag

le flag est: b3a6e43ddf8b4bbb4125e5e7d23040433827759d4de1c04ea63907479a80a6b2