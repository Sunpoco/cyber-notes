# 🕶️ Mission 2.3 – Shadow JS & DOM Hunting

---

## 🎯 Objectif
Lire et analyser du JavaScript côté client, repérer une logique vulnérable manipulant le DOM, et injecter un payload pour prouver l’exécution de code.

---

## 🔍 Contexte du challenge

**Lab utilisé :**  
[PortSwigger – DOM-based XSS using `document.write()`](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink)

**Comportement observé :**
Le code JavaScript utilise `document.write(location.hash);` pour injecter du contenu HTML depuis l'URL, **sans aucune validation**.

---

## 💥 Exploit réalisé

### 🔹 Payload injecté dans l’URL :
```text
#"><svg onload=alert(1)>
https://<lab-id>.web-security-academy.net/#"><svg onload=alert(1)>


🚩 Pourquoi c’est critique
N’importe quel utilisateur peut créer une URL piégée

L’exécution de code JavaScript peut :

Voler des cookies (document.cookie)

Modifier l’apparence de la page (phishing)

Injecter un keylogger

Mission validée
Badge débloqué : 🕶️ JS Shadow

Niveau atteint : 2.4 / 100

Date : 27 avril 2025
