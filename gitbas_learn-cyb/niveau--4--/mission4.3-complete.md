
# 🧨 Mission 4.3 – Scan de fichiers sensibles & endpoints cachés

---

## 🎯 Objectif de la mission
Découvrir, par reconnaissance active, l'existence de fichiers oubliés ou sensibles (`.bak`, `.log`, `.php`, `.jsp`, etc.) et d'endpoints non documentés sur un serveur cible.

---

## 🧠 Compétences développées

| 🔑 N° | Compétence |
|------|------------|
| 1️⃣ | Utiliser `ffuf` pour découvrir des fichiers en bruteforce |
| 2️⃣ | Interpréter les codes HTTP (`200`, `302`, `403`, etc.) |
| 3️⃣ | Analyser la structure du site selon son extension serveur |
| 4️⃣ | Formuler des hypothèses offensives basées sur la réponse |
| 5️⃣ | Savoir filtrer les faux positifs avec `-fs` |
| 6️⃣ | Préparer une stratégie future d’automatisation personnalisée |

---

## 🛠️ Commande exécutée

```bash
ffuf -u http://demo.testfire.net/FUZZ -w ~/SecLists/Discovery/Web-Content/raft-small-files.txt -e .php,.txt,.log,.bak,.sql,.env,.zip -fs 1219 -t 40 -timeout 5
```

---

## 📂 Résultats significatifs

| Chemin trouvé        | Status | Taille | Commentaire |
|----------------------|--------|--------|-------------|
| `/index.jsp`         | 200    | 9405   | Page principale |
| `/login.jsp`         | 200    | 8555   | Page d’authentification |
| `/search.jsp`        | 200    | 7009   | Formulaire public |
| `/feedback.jsp`      | 200    | 8535   | Interface de feedback |
| `/logout.jsp`        | 302    | 0      | Redirection |
| `/account.jsp`       | 302    | 0      | Redirection |
| `/style.css`         | 200    | 1251   | Ressource statique |
| `/disclaimer.htm`    | 200    | 2080   | Ancienne page HTML |
| `.`                  | 200    | 9405   | Requête vers la racine (`/.`) – identique à `/index.jsp` |

---

## 🔎 Analyse technique

- Le site repose sur des fichiers **JSP**, typiques d’un backend Java (Tomcat, Servlet).
- Les pages `.jsp` sont actives : login, search, feedback
- Le point `.` représente un appel vers la racine (`/`), ce qui explique une taille identique à `index.jsp`

---

## 💡 Hypothèse offensive

> Ces endpoints indiquent une structure classique orientée JSP. Des pages comme `/feedback.jsp` ou `/search.jsp` pourraient servir à injecter du contenu (XSS, manipulation DOM).  
> Les pages redirigées (`logout.jsp`, `account.jsp`) sont protégées par auth.  
> À des niveaux supérieurs, on pourrait tester :
> - des injections côté formulaire
> - des exfiltrations via paramètres GET/POST
> - des attaques CSRF ou XSS ciblées

---

## 🛠️ Note stratégique – Projet personnel

📌 À partir du **Niveau 7 ou 8**, une mission spéciale sera introduite :  
> 🎯 *Créer ton propre mini-fuzzer web en Python*  
Inspiré de `ffuf`, ce projet te permettra de :
- Scanner des chemins automatiquement
- Gérer les codes HTTP, redirections
- Lire une wordlist et l’appliquer à des URLs

🔐 Ce projet sera placé **après ta maîtrise des sockets, des requêtes HTTP, et des threads en Python.**

---

## ✅ Mission validée

- [x] Scanner actif exécuté
- [x] Analyse des extensions, codes et comportements
- [x] Observation des réponses redirigées
- [x] Hypothèse offensive rédigée
- [x] Point stratégique identifié pour futur outil

---

## 🏅 Badge débloqué :
📦🕳️ **File Forensics**  
> *"Tu retrouves les traces qu’ils pensaient avoir supprimées."*

---

## ⏭️ Mission suivante : Mission 4.4  
➡️ Upload, fichiers temporaires et scripts mal configurés
