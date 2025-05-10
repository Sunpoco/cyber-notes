
---

## 📄 `missions/mission-3.3.md` – XSS dans attributs HTML

```markdown
# 🧪 Mission 3.3 – XSS via attribut HTML (href, title, src…)

## 🎯 Objectif
Exploiter un attribut HTML injecté dynamiquement, malgré un encodage partiel (HTML-encoded).

## 🔍 Contexte
- Le site affiche un lien ou une image avec un attribut basé sur l’entrée utilisateur
- Les guillemets et chevrons (`<`, `>`, `"`) sont encodés, mais pas l’ensemble de la chaîne
- Injection possible avec `javascript:` ou événement HTML

## 💉 Payload injecté
```html
"><img src=x onerror=alert(1)>

✅ Comportement observé
L’attribut HTML est mal filtré

L’alerte est déclenchée sans passer par une balise <script>

Le contexte de l’attribut permet une exécution JS

🧠 Analyse technique
Injection dans un attribut comme href, sans échapper la valeur complète

Le navigateur interprète javascript: comme un lien → exécution JS

🛡️ Contre-mesures
Ne jamais insérer directement une entrée utilisateur dans un attribut

Si nécessaire, valider et forcer les schémas (http://, https://)

Appliquer rel="noopener noreferrer" pour les liens externes

Encodage strict ou templating sécurisé

🏅 Badge : Attribute Hacker