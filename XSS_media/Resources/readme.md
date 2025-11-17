FAILLE XSS ON URL

the url is: http://localhost:8080/?page=media&src=data

- src ici j'ai essayé de produire une faille xss avec ce code:
http://localhost:8080/?page=media&src=<script>alert('XSS')</script>
- Ceci me sort une 404 dans la page actuelle dans une balise table.
- mais je me rends compte que la data est retourné tel qu'elle dans une balise data:
<td style="vertical-align:middle;"><object data="<script>alert('XSS')</script>"></object></td>
- Je me dis que je dois exploiter quelque chose à ce niveau la
- J'ai essayer de casser la balse data avec ceci: x"></object><script>alert('XSS')</script>
- ceci referme la balise data et genere le code ensuite mais ceci ne produit rien non plus
- le code script injecté n'est pas interprété car les caractères sont encodés en entités html
- Enfaite j'ai seulement à faire une injection html par exemple:
?page=media&src=data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==
Ca me permet de récupérer le flag
- c'est une attaque plus spécifique et plus poussé en XSS. Enfaite je vais exploiter la non vérification du contenu envoye dans data: data:[MIME-type][;encoding],[données]
Au lieu de lui envoyer de la donnée que le serveur va encoder comme les caractères < et > d'une balise script on va directement lui envoyer du html encoder. Que le navigateur va décoder car on lui dit que c'est du base64 donc lui va décoer ca en base64 ce qui va donner:
<script>alert(1)</script>

- Enfaite c'est une faille inline, ou de la data est préchargé sans vérification dans l'attribut data et nous on va donc envoyer de la data encoder que le navigateur va pouvoir utiliser. Inline correspond à de la data direct sans redirection. elle est donc déja "chargé" dans l'attribut.

Pour se prémunir de ce genre de faille:
CSP => content security policy qui va ajouter un header qui bloque les datas URI, ou bloquer tout simplement data dans l'uri. Bloquer explicitement data.