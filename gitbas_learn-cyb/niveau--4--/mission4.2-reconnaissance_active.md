# 🧨 Mission 4.2 – Reconnaissance Active : Répertoires et Fichiers Cachés

---

## 🎯 Objectif
Effectuer une reconnaissance **active et contrôlée** sur une cible web autorisée, afin de détecter l'existence de répertoires, fichiers ou endpoints non exposés publiquement, mais accessibles via force brute intelligente (wordlist).

---

## 🧠 Compétences clés développées

| 🔑 N° | Compétence |
|------|------------|
| 1️⃣ | Utiliser un scanner actif (`ffuf`) sur une cible web |
| 2️⃣ | Interpréter les codes HTTP (`200`, `302`, `403`, etc.) |
| 3️⃣ | Différencier fichiers, répertoires, endpoints |
| 4️⃣ | Optimiser une wordlist pour gagner en pertinence |
| 5️⃣ | Filtrer les pages génériques avec `-fs` |
| 6️⃣ | Valider manuellement les résultats et redirections |

---

## 🧪 Cible analysée

- **URL cible** : `http://demo.testfire.net`
- **Méthode utilisée** : `ffuf`
- **Wordlist utilisée** : `quickhits.txt` de SecLists
- **Commande exécutée** :
  ```bash
  ffuf -u http://demo.testfire.net/FUZZ -w ~/SecLists/Discovery/Web-Content/quickhits.txt -fs 1219 -t 30 -timeout 5

## 📂 Résultats du scan
Chemin trouvé	Code HTTP	Taille	Interprétation
/admin/	302	0	Redirection vers login
/admin/test/	302	0	Répertoire existant, protégé
/admin/.config	302	0	Fichier ou config, sécurisé

## 🔐 Validation manuelle
Après avoir accédé manuellement à :

http://demo.testfire.net/admin/

http://demo.testfire.net/admin/.config

http://demo.testfire.net/admin/test/

➡️ Le site redirige systématiquement vers :

http://demo.testfire.net/login.jsp

## 📌 Confirmation :

Le répertoire /admin existe réellement

Accès restreint par mécanisme d’authentification

Potentiellement exploitable via attaque de session, brute-force ou CSRF

## 🧠 Hypothèse offensive
Le dossier /admin/ est protégé mais bel et bien actif.
Une attaque future pourrait viser :

Le contournement de l’authentification (login.jsp)

Le bruteforce de credentials (niveau supérieur)

La découverte de fichiers laissés derrière cette route (admin/upload, admin/config.jsp, etc.)

✅ Mission validée
 Scanner exécuté avec succès

 Résultats pertinents interprétés

 Comportement confirmé manuellement

 Hypothèse offensive construite

🏅 Badge débloqué :
📂🔍 Directory Diver

"Tu sais où gratter. Même dans les dossiers qu’ils croyaient avoir bien cachés."