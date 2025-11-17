FILE HTPASSWD

- Dans le repertoire robots.txt j'ai un fichier htpasswd.
- dans ce fichier j'ai ceci:
root:437394baff5aa33daa618be47b75cb49

Si je decrypt 437394baff5aa33daa618be47b75cb49 en md5 j'obtiens: qwerty123@

- Le fichier .htpasswd sert à stocker des identifiants (noms d'utilisateur et mots de passe) pour protéger l'accès à des répertoires ou fichiers sur un serveur web, généralement Apache.

- ok j'ai compris quand je vais dans la partie /admin/ je peux me connecter ici:
et si je rentre les identifiants je peux me connecter à cet espace

RESOLUTION FAILLE:

- Proteger les routes et eviter de donner du contenu sensible comme des mots de passe en clair
