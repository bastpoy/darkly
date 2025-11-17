HEADER EXPLOIT

ici c'est sur cette page:

- http://localhost:8080/index.php?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f
- Quand on ouvre la console nous avons des indices: 
    "You must come from : "https://www.nsa.gov/"
    "Let's use this browser : "ft_bornToSec". It will help you a lot."

ce sont des indices et des guides qui nous permettent de réaliser une requête en modifiant les headers.
- le premier commentaire nous dit de quelle référence nous devons provenir: ceci se traduit par le header Referer: 
    refere est un header qui permet de specifier de quelle url l'utilisateur provient permetttant d'afficher la page actuelle
- Le deuxième commentaire nous dit quelle navigateur utilise. Ca tombe bien le header User-agent Ajoute des informations sur le navigateur utilisé pour la requete et d'autres informations comme le système d'exploitation, version, etc...
- Donc ce qui reste à faire est de réaliser une requête sur cette page actuelle en utilisant ces headers:
 curl "http://localhost:8080/index.php?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f" \
  -H "Referer: https://www.nsa.gov/" \
  -H "User-Agent: ft_bornToSec" \

- Nous avons donc la même page qui s'affiche mais avec le flag

RESOLUTION FAILLE:

- Ne pas mettre a disposition des informations sensible seulement en utilisant des headers cote client. utiliser plutot une authentification

