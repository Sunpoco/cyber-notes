# 📝 Mission 2.2 – Formulaires Web & Injection de Données

---

## 🎯 Objectif de la mission

Comprendre le fonctionnement des formulaires HTML et apprendre à intercepter, manipuler, puis injecter des données dans les champs pour tester la réaction du serveur.

---

## 🧱 Compétences acquises

- 🔍 Lecture d’un formulaire HTML (balises `<form>`, `<input>`, `<button>`)
- 🧠 Compréhension des méthodes `GET` vs `POST`
- 📡 Observation des requêtes réseau (F12 → Network)
- 📤 Analyse de la structure des paramètres envoyés
- 💉 Injection de payloads simples dans les champs
- 🛡️ Observation du comportement du serveur face à du contenu potentiellement malveillant

---

## 🧪 Payloads testés

| Champ    | Payload injecté               | Réaction du serveur                   |
|----------|-------------------------------|---------------------------------------|
| custname | `<script>alert(1)</script>`   | Réinjecté tel quel → pas échappé      |
| custtel  | `' OR '1'='1`                 | Affiché dans la réponse → non filtré  |

➡️ Conclusion : Le serveur renvoie les valeurs **sans les filtrer ni les échapper**  
➡️ Indice potentiel de **XSS réfléchi** ou **vulnérabilité à l’injection**

---

## 🧰 Outils utilisés

- Navigateur Web (F12 – DevTools)
- Onglet Réseau pour voir les headers + payloads
- Formulaire de test : https://httpbin.org/forms/post

---

## 🛡️ Comportement de sécurité observé

- Absence de filtrage sur le contenu HTML injecté
- Absence d'échappement dans la réponse (reflected XSS possible)
- Headers de sécurité manquants détectés :
  - `x-content-type-options`
  - `cache-control`
  - `server` trop bavard

---

## 🏅 Badge obtenu

### 📝 Formu-Killer  
*"Les champs te parlent, et tu réponds avec du code acide."*

---

## ✅ Mission validée : **OUI**  
**Date de complétion :** 25 avril 2025  
**Niveau actuel :** 2.3 / 100
