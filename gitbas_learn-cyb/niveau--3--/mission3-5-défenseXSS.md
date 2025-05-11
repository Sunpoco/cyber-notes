# 🛡️ Mission 3.5 – Défense XSS : Lecture & Audit de sécurité HTTP

---

## 🎯 Objectif
Analyser en profondeur la configuration de sécurité d’un site réel (GitHub), repérer les mécanismes anti-XSS en place, comprendre leur fonctionnement, identifier les points faibles, et proposer des améliorations concrètes.

---

## 🌐 Cible analysée
**https://github.com**

---

## 🔍 Headers de sécurité observés

### ✅ `Content-Security-Policy` (CSP)

default-src 'none';
connect-src 'self' uploads.github.com www.githubstatus.com collector.github.com raw.githubusercontent.com api.github.com github-cloud.s3.amazonaws.com github-production-repository-file-5c1aeb.s3.amazonaws.com github-production-upload-manifest-file-7fdce7.s3.amazonaws.com github-production-user-asset-6210df.s3.amazonaws.com .rel.tunnels.api.visualstudio.com wss://.rel.tunnels.api.visualstudio.com;


**Analyse :**
- 🔐 Stratégie ultra défensive : tout est bloqué par défaut (`default-src 'none'`)
- ✅ Seules les sources explicites sont autorisées dans chaque directive (`connect-src`, `script-src`, etc.)
- ✅ `script-src` exclut `'unsafe-inline'` → empêche tous les scripts inline
- 🧠 Architecture CSP typique d’un site critique (whitelist only)

---

### ✅ `X-Content-Type-Options: nosniff`
- Empêche le navigateur de forcer un Content-Type incorrect
- Bloque les attaques de type MIME-sniffing
- 🔐 Protège contre certains scénarios XSS où un script serait chargé via un fichier CSS ou image déguisée

---

### ✅ `X-Frame-Options: deny`
- Empêche l'inclusion du site dans une `<iframe>`
- 🛡️ Protection contre le **clickjacking**

---

### ✅ `Strict-Transport-Security`

Strict-Transport-Security: max-age=31536000; includeSubDomains; preload

yaml
Copier
Modifier
- 🔐 Force l’usage du HTTPS même lors d’une redirection
- Protège contre les attaques **SSL stripping**

---

### ✅ `Set-Cookie:` avec protections
Extrait observé : et-Cookie: logged_in=yes; Domain=github.com; Path=/; Secure; HttpOnly; SameSite=Lax;


**Analyse :**
- `Secure` → seulement transmis via HTTPS
- `HttpOnly` → inaccessible depuis JavaScript
- `SameSite=Lax` → réduit les attaques CSRF sur des requêtes simples

---

### ⚠️ Observations pertinentes

#### ❌ `X-XSS-Protection: 0`
- Le header **désactive le filtre anti-XSS intégré** dans Chrome
- MAIS : il est déprécié, et sa désactivation **est aujourd’hui une bonne pratique**
- GitHub utilise sa **propre CSP**, bien plus fiable

#### ✅ `default-src 'none'` n’est **pas une faiblesse**
- C’est au contraire la base d’une CSP “par défaut restrictive” (meilleure pratique)
- Toutes les permissions sont **déclarées explicitement**, ce qui évite les oublis

---

## 🚫 Payloads bloqués par cette configuration

| Payload testé                   | Résultat | Pourquoi ? |
|--------------------------------|----------|------------|
| `<script>alert(1)</script>`    | ❌ bloqué | CSP interdit tous les scripts inline |
| `<img src=x onerror=alert(1)>` | ❌ bloqué | `img-src` restreint les sources ; `onerror` interdit |
| `javascript:alert(1)` dans un `href` | ❌ bloqué | Pas d’exécution inline permise |

---

## 🧱 Recommandations professionnelles (améliorations possibles)

### 1. Ajouter un mécanisme de **report de violations CSP**

```http
Content-Security-Policy: ...; report-uri /csp-report

➡️ Permet de logguer les tentatives de XSS bloquées pour analyse

2. Ajouter un header Permissions-Policy
Exemple :

http
Copier
Modifier
Permissions-Policy: camera=(), microphone=(), geolocation=()
➡️ Durcit l’accès aux fonctions sensibles du navigateur

🧠 Conclusion
GitHub applique une stratégie de défense XSS exemplaire :

CSP très stricte

Cookies protégés (Secure, HttpOnly)

Aucune inclusion non contrôlée

Headers de sécurité cohérents et efficaces

La désactivation de X-XSS-Protection est volontaire et justifiée, car la CSP prend le relais de manière bien plus fiable.

🏅 Badge obtenu :
🛡️⚙️ Guardian of the DOM

"Tu ne fais plus que survivre au XSS. Tu sais le désarmer, le détecter, et le prouver."
