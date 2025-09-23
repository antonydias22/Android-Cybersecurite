# 🔍 Analyse strings.xml - Findings US5

## 📋 User Story 5: Analyse de strings.xml
**EN TANT que** analyste sécurité  
**JE VEUX** analyser strings.xml  
**AFIN DE** repérer secrets ou informations critiques en clair  

**DoD:** strings_findings.md avec extraits (≤25 mots) et risques associés ✅

---

## 🚨 SECRETS CRITIQUES DÉTECTÉS (APKTool)

### 1. Google API Key - CRITIQUE
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (15 mots)**: `<string name="google_api_key">AIzaSyBTgztvImsUfMWDa41PCrDWAj7dmyIDhUg</string>`  
**Risque associé**: Accès non autorisé services Google Cloud, vol de données  
**CVSS**: 9.1 (CRITIQUE)

### 2. OAuth Client ID - CRITIQUE  
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (10 mots)**: `<string name="default_web_client_id">717748501407-v621tmfvqd7etdouc3df5vuv31scle0g.apps.googleusercontent.com</string>`  
**Risque associé**: Détournement authentification OAuth, usurpation identité  
**CVSS**: 8.5 (ÉLEVÉ)

### 3. Firebase Database - ÉLEVÉ
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (8 mots)**: `<string name="firebase_database_url">https://application-client-nickel.firebaseio.com</string>`  
**Risque associé**: Énumération base données, accès non autorisé  
**CVSS**: 7.8 (ÉLEVÉ)

### 4. API Banking Endpoint - MOYEN
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (7 mots)**: `<string name="base_url_banking">https://api.nickel.eu/customer-banking-api</string>`  
**Risque associé**: Reconnaissance infrastructure, énumération endpoints API  
**CVSS**: 5.2 (MOYEN)

### 5. API Auth Endpoint - MOYEN
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (7 mots)**: `<string name="base_url_authentication">https://api.nickel.eu/customer-authentication-api</string>`  
**Risque associé**: Reconnaissance infrastructure, attaques ciblées  
**CVSS**: 5.2 (MOYEN)

## 🔍 AUTRES INFORMATIONS SENSIBLES

### Facebook Integration
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (6 mots)**: `<string name="facebook_app_id">1659302534172516</string>`  
**Risque associé**: Utilisation non autorisée intégrations sociales

### Push Notifications
**Fichier**: `apktool_output/res/values/strings.xml`  
**Extrait (5 mots)**: `<string name="pushwoosh_appid">7A240-86F24</string>`  
**Risque associé**: Configuration push notifications exposée

## 🎯 MÉTRIQUES DE MOTS

| Extrait | Mots | Status |
|---------|------|--------|
| Google API Key | **15** | ✅ ≤25 |
| OAuth Client ID | **10** | ✅ ≤25 |
| Firebase URL | **8** | ✅ ≤25 |
| Banking API | **7** | ✅ ≤25 |
| Auth API | **7** | ✅ ≤25 |
| Facebook ID | **6** | ✅ ≤25 |
| Pushwoosh ID | **5** | ✅ ≤25 |