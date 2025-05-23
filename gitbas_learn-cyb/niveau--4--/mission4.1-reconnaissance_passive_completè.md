# 🧭 Mission 4.1 – Reconnaissance passive complète

---

## 🎯 Objectif
Effectuer une analyse de reconnaissance passive complète d’un domaine cible, sans scanner ni interagir directement avec ses serveurs. Identifier les sous-domaines, la stack technique, l’infrastructure réseau, et les opportunités d’attaque indirecte (OSINT).

---

## 🧠 Cible analysée
**Domaine principal** : `tiktok.com`  
**Sous-domaine étudié** : `ads-service.tiktok.com`

---

## 1. 🔍 Sous-domaines détectés

- ads-service.tiktok.com
- (autres sous-domaines analysés mais non actifs ou redirigés)

📌 Méthode :
- Recherche via [https://crt.sh/?q=%25.tiktok.com](https://crt.sh/?q=%25.tiktok.com)
- Certificats SSL examinés pour extraction des CN/SAN (Common Name / Subject Alternative Name)

---

## 2. ⚙️ Technologies détectées

- Aucun front-end détectable sur `ads-service.tiktok.com`
- Résolution DNS obtenue : service répond uniquement par IP
- Pas de framework JS, CDN ou CMS observable
- Absence d’interaction HTTP confirmée (probablement service API ou interne)

---

## 3. 🌐 Analyse DNS & Réseau

- Résolution IP (via `nslookup`) :
  - `ads-service.tiktok.com` → `209.127.230.4`
- Informations WHOIS / IP :
  - Organisation : **LARK ENTERPRISE APPLICATIONS INC.**
  - ASN : **AS398175**
  - Localisation : **Leesburg, Virginia, USA**
  - Reverse DNS : `va-1-4.ptr.blmpb.com`
- Fournisseur identifié : prestataire tiers (pas TikTok/Bytedance direct, ni Cloudflare)

📌 Observation :
> Le sous-domaine est **résolu activement** sans passer par un CDN comme Cloudflare ou Akamai. Cela indique une **exposition potentielle directe** (infra hébergée par un tiers).

---

## 4. 🕵️ OSINT & traces publiques

### 🔍 Recherche GitHub :
- Mots-clés testés : `tiktok.com`, `ads.tiktok.com`, `api.tiktok.com`, `token`
- Aucun token/API leaké trouvé
- Repos officiels uniquement, pas d’erreur de configuration visible

### 📂 robots.txt :
- Accès : [https://www.tiktok.com/robots.txt](https://www.tiktok.com/robots.txt)
- Contenu :
Disallow: /admin/
Disallow: /internal/
Disallow: /api/private/

- 📌 Bonne pratique appliquée : les répertoires sensibles sont explicitement disallow.

---

## 5. 🧠 Hypothèse d’exploitation future

> Le service `ads-service.tiktok.com`, bien que non actif côté web, est **résolu DNS et exposé directement** sans reverse proxy. Il est hébergé sur une IP publique d’un prestataire externe non protégé par CDN.
> Une attaque de niveau 5 pourrait inclure :
> - Tentative de fingerprinting réseau via HTTP headers
> - Fuzzing d’URL/API s’il y a un front latent
> - Brute-force de routes REST/API sur base d’anciennes versions documentées
> 
> **Mais surtout**, comme dans de nombreuses organisations, **la faille humaine** reste dominante :
> Une **campagne de phishing ciblée** sur des employés en lien avec l'infrastructure publicitaire (Ads, Analytics, Dev) pourrait être un levier efficace de compromission initiale.

---

## ✅ Mission validée

🎯 Tous les objectifs atteints :
- [x] Sous-domaines identifiés
- [x] Stack et IP analysées
- [x] Hébergeur externe détecté
- [x] Recherches OSINT menées
- [x] Hypothèse d’exploitation formulée

---

## 🏅 Badge obtenu :
🕵️‍♂️🌐 **Surface Seeker**  
> *"Tu ne frappes pas au hasard. Tu vois les points faibles avant même qu’ils sachent que tu es là."*

---

## ⏭️ Prochaine étape : Mission 4.2
> Passage à la reconnaissance active (test d’URL, endpoints, fichiers cachés…)

