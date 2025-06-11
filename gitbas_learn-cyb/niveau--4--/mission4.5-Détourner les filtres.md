🧨 Mission 4.5 – Contournement d’Extension via Double Encodage
🎯 Objectif initial
Uploader un fichier PHP en contournant un filtre de sécurité basé sur la blacklist d’extension, puis valider son exécution à distance (RCE).

✅ Résultats obtenus par toi
Étape	Résultat
💉 Contournement du filtre via filename="shell.p%252ephp"	✅ Réussi
📤 Upload accepté par le serveur	✅ Réussi
🌍 Fichier visible à l’URL attendue	✅ Réussi
💥 Exécution du code PHP (?cmd=whoami)	❌ Bloquée par configuration serveur

🧠 Ce que tu as appris
Comment fonctionne un filtrage basé sur l’extension

L’impact du double encodage (%252e ➜ %2e ➜ .)

L’usage précis de Burp Suite pour manipuler une requête multipart/form-data

Comment observer le comportement réel du serveur :

Message de rejet explicite

Accès autorisé mais sans interprétation

La différence entre upload réussi et code exécuté

📌 Pourquoi l’exécution est bloquée
Le serveur stocke le fichier mais empêche toute interprétation PHP dans le dossier de destination (/avatars/, /files/, etc.)
Cela reflète une mesure de sécurité réaliste (souvent mise en place dans les vraies entreprises) via .htaccess ou configuration Apache.

🏅 Badge débloqué
🌀🪤 Filename Forger

Tu as réussi à tromper les filtres avec une extension déguisée — une attaque subtile mais très utilisée.

📈 Tu valides la mission pédagogique mais pas encore le lab complet
Et c’est OK : cette mission repose sur un comportement serveur que tu apprendras à contourner dans un prochain niveau (niveau 7 ou 8 probablement).

