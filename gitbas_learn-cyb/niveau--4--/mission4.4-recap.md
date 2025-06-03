
# 🧨 Mission 4.4 – Upload, Fichier temporaire & Exécution webshell (RCE)

---

## 🎯 Objectif
Exploiter un formulaire d’upload vulnérable pour injecter un fichier `.php` et obtenir une exécution de code distante (RCE), en contournant les protections basées sur le type MIME.

---

## 🧠 Compétences développées

| Compétence | Détail |
|------------|--------|
| 🔎 Analyse des headers | Comprendre `Content-Type` et `Content-Disposition` |
| 🧠 Interception de requête | Utiliser Burp Suite pour manipuler une requête `POST` |
| 🎭 Bypass MIME | Contourner la protection côté serveur en trompant le type MIME |
| 💻 RCE Webshell | Obtenir l’exécution d’un script `.php` en environnement réel |
| 🔥 Observation serveur | Vérifier les erreurs de type 403/404 ou les changements de comportement |

---

## 📂 Détail de l’attaque réalisée

- **Fichier uploadé** : `shell.php`
- **Payload** :
```php
```
- **Outil utilisé** : Burp Suite
- **Modification** : `Content-Type` changé en `image/jpeg` manuellement
- **URL d’accès** : `/files/shell.php?cmd=whoami` (exécution confirmée)
- **Réponse du serveur** : le shell PHP a été interprété et la commande exécutée

---

## 🛡️ Comportement du serveur

| Élément | Observation |
|---------|-------------|
| Extension `.php` | Acceptée si `Content-Type` est masqué |
| Contrôle MIME | Filtrage léger basé sur l’en-tête uniquement |
| Upload | Pas de whitelist réelle ni de vérification serveur |
| Résultat | Le fichier `.php` est stocké et interprété |

---

## 🌟 Évaluation stratégique

| Attaque | Risque | Réalisme |
|---------|--------|----------|
| Webshell Upload avec MIME Bypass | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

> 💡 Attaque très critique encore présente dans des applications legacy, intranet, outils low-code mal configurés.

---

## 🧠 Hypothèse offensive

Un attaquant pourrait :
- Prendre le contrôle du serveur via `system()` ou `exec()`
- Uploader un backdoor PHP pour persistance
- Enchaîner sur une élévation de privilèges Linux

---

## 🏅 Badge débloqué

📥💀 **Payload Smuggler**  
> *"Tu sais faire passer un poison dans un costume d’image innocente."*

---

## ✅ Mission validée

- [x] Upload réussi avec contournement MIME
- [x] Exécution du fichier `.php` vérifiée
- [x] Burp Suite utilisé pour manipuler la requête
- [x] Analyse du serveur complétée
- [x] Hypothèse d’exploitation rédigée

---

## ⏭️ Suite proposée : Mission 4.5 – Upload + bypass extension & double encoding
