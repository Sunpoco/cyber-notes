# 🧪 Mission 3.2 – Bypass de filtres XSS (XSS via vecteur alternatif)

## 🎯 Objectif
Déclencher une alerte malgré un filtre HTML bloquant `<script>` et d'autres éléments suspects.

## 🔍 Contexte
- Le champ de saisie est filtré.
- La balise `<script>` est bloquée.
- D’autres événements comme `onclick`, `onload` sont possibles.

## 💉 Payload injecté
```html
<img src=x onerror=alert(1)>
✅ Comportement observé
Image cassée déclenche onerror

Alerte s’exécute malgré les restrictions

🧠 Analyse technique
Contournement via un élément autorisé (img)

Utilisation d’un événement déclencheur (onerror)

Le filtre HTML ne bloque pas ce pattern → injection réussie

🛡️ Contre-mesures
Encoder les entrées côté serveur (< → &lt;)

Appliquer une whitelist stricte de balises/attributs autorisés

CSP : interdire JS inline (script-src 'self')

🏅 Badge : Filter Breaker