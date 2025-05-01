# 🛡️ Mission 2.4 – DOM XSS via `<select>` + `document.write`

---

## 🎯 Objectif de la mission

Comprendre et exploiter une vulnérabilité **DOM-based XSS** où une valeur injectée depuis l’URL (`location.search`) est insérée dans le DOM via `document.write`, dans un élément `<select>`.  
L’objectif est de **déclencher une exécution de code JavaScript malveillant** côté client.

---

## 🌐 Lab utilisé

🔗 [PortSwigger Academy – Lab DOM XSS in document.write() using location.search inside select](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element)

---

## 🧠 Analyse technique

- Le site extrait un paramètre depuis `location.search` → `storeId`
- Le paramètre est inséré **dans un `<select>` HTML** via `document.write()` sans échappement
- En fermant la balise `</select>`, on peut injecter **des balises HTML supplémentaires**
- En insérant un élément comme `<img onerror=...>` on déclenche l’exécution de JavaScript

---

## 🧪 Payload utilisé

```html
"></select><img src=x onerror=alert(1)>


🔗 URL complète utilisée
https://0a01007e0453b77980cc5d0200ba00e2.web-security-academy.net/product?productId=1&storeId="></select><img src=x onerror=alert(1)>


✅ Résultat
Le script JavaScript est exécuté par le navigateur

Affichage d'une popup d’alerte → preuve de vulnérabilité XSS

La faille est confirmée : injection DOM-based XSS dans document.write → <select>
    

⚠️ Pourquoi c’est dangereux
L’utilisateur peut injecter du HTML/JS directement dans la page

Peut être exploité pour :

Vol de cookies

Attaques de type phishing

Prise de contrôle de sessions


🛡️ Contre-mesures (défensive)
Ne jamais utiliser document.write() avec des données contrôlées par l’utilisateur

Préférer des méthodes comme textContent, ou échapper les entrées avec une librairie

Mettre en place une politique de sécurité CSP pour bloquer les scripts inline

🏁 Mission validée
🔓 Vulnérabilité XSS DOM identifiée et exploitée

🏅 Badge obtenu : DOM Splitter

📈 Niveau atteint : 2.5 / 100

📆 Date : 28 avril 2025
