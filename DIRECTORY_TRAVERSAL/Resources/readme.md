FAILLE SUR REMONTEE DES DOSSIERS DEPUIS L'URL POUR ALLER CHERCHER DES FICHIERS INTERNES

je vais a taton tout simplement:

- l'url final est http://localhost:8080/?page=../../../../../../../etc/passwd
- Mais avant de trouver ca j'ai du y aller a taton ou j'avais a chaque fois des alert s'affichant me donnant des indices en quelques sortes.
- donc a force d'ajouter des ../ à taton j'ai trouver le bon path


RESOLUTION FAILLE

- Proteger les routes que l'utilisateur peut acceder, gere les droits d'acces sur les fichiers du serveur

