
# 🛡️ Mission 2.5 – XSS Persistant (Stored XSS)

## ✅ Objectif atteint :
Tu as réussi à exploiter une vulnérabilité de type **XSS persistant** (Stored XSS) en autonomie, avec compréhension du mécanisme.

---

## 🔍 Qu'est-ce que le XSS Persistant ?
Le **XSS persistant** se produit lorsque l'entrée malveillante d'un utilisateur est **stockée côté serveur** (ex : base de données) puis **renvoyée à d'autres utilisateurs** sans être filtrée ou encodée.

---

## 🧪 Exemple d'injection réussie :
```html
<script>alert('XSS Persistant')</script>
```

Cette payload est stockée dans le serveur (ex : champ de commentaire) et exécutée à chaque chargement de la page concernée.

---

## ⚠️ Risques associés :
- Vol de cookies/session utilisateur
- Détournement de compte
- Défiguration de l’interface
- Attaques ciblées (phishing, redirection, etc.)

---

## 🛡️ Contre-mesures :
- **Encodage en sortie** (HTML encoding)
- **Validation/filtrage côté serveur** selon le contexte
- Mise en place d’une **CSP** (Content Security Policy)
- Éviter les injections dynamiques dans le DOM

---

## 🧠 Compétences acquises :
- Détection d’un champ vulnérable au XSS
- Injection et stockage d’un script malveillant
- Compréhension de la différence entre XSS réfléchi et persistant
- Esprit d’analyse offensive

---

🎉 Mission accomplie !
