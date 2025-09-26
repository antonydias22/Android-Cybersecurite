# Rapport d'analyse de sécurité - Décompilation d'APK

## Objectif
En tant qu'ingénieure Sécurité, je veux décompiler le bytecode de mon APK afin de trouver des vulnérabilités logiques ou mauvaises pratiques.

## Vulnérabilités identifiées

### Vulnérabilité 1: Utilisation du mode CBC avec padding PKCS5/PKCS7
**Gravité**: Élevée

**Description**:  
L'application utilise le mode de chiffrement CBC (Cipher Block Chaining) avec le padding PKCS5/PKCS7. Cette combinaison est vulnérable aux attaques par "padding oracle". Un attaquant peut exploiter cette vulnérabilité pour déchiffrer progressivement des données chiffrées sans connaître la clé de chiffrement.

**Comment ça fonctionne**:
1. Le mode CBC divise les données en blocs et les chiffre séquentiellement
2. Le padding PKCS5/PKCS7 ajoute des octets à la fin du message pour compléter le dernier bloc
3. Dans une attaque par "padding oracle", l'attaquant modifie les blocs chiffrés et observe si l'application renvoie une erreur de padding ou non
4. En analysant ces réponses, l'attaquant peut déduire le contenu des données chiffrées

**Fichiers concernés**:
- `com/oblador/keychain/cipherStorage/CipherStorageKeystoreAESCBC.java`
- `com/pushwoosh/internal/a/a.java`

**Impact**:
- Compromission potentielle des données sensibles chiffrées
- Possibilité de déchiffrer des informations confidentielles comme des jetons d'authentification, mots de passe, etc.

### Vulnérabilité 2: Fichiers contenant des informations sensibles codées en dur
**Gravité**: Moyenne (mais impact potentiellement élevé)

**Description**:  
L'application contient des fichiers avec des informations sensibles codées en dur comme des noms d'utilisateur, mots de passe, clés, etc. Ces informations peuvent être facilement extraites par quiconque décompile l'application.

**Comment ça fonctionne**:
1. Les développeurs ont intégré directement dans le code des informations sensibles (comme des clés API, des identifiants, etc.)
2. Ces informations sont stockées en texte clair dans le code de l'application
3. N'importe qui peut décompiler l'APK et lire ces informations sensibles
4. Ces informations peuvent être utilisées pour accéder à des services, contourner l'authentification ou compromettre la sécurité

**Fichiers concernés**:
- `com/bumptech/glide/load/Option.java`
- `com/bumptech/glide/load/engine/DataCacheKey.java`
- `com/bumptech/glide/load/engine/EngineResource.java`
- `com/bumptech/glide/load/engine/ResourceCacheKey.java`
- `com/pushwoosh/reactnativeplugin/InboxUiStyleManager.java`

**Impact**:
- Exposition de secrets qui devraient rester confidentiels
- Possibilité d'accès non autorisé à des services tiers
- Contournement potentiel des mécanismes d'authentification
- Compromission de la sécurité de l'application et des données utilisateur

### Vulnérabilité 3: Injection SQL dans les requêtes brutes et stockage non sécurisé
**Gravité**: Élevée

**Description**:  
L'application utilise des requêtes SQL brutes avec des entrées utilisateur non filtrées, ce qui peut conduire à des injections SQL. De plus, les informations sensibles sont stockées dans la base de données sans chiffrement approprié.

**Comment ça fonctionne**:
1. L'application exécute des requêtes SQL brutes sans paramétrage adéquat
2. Les entrées utilisateur sont directement concaténées dans les requêtes SQL
3. Un attaquant peut injecter du code SQL malveillant pour manipuler la base de données
4. Les données sensibles sont stockées en clair, sans chiffrement, dans la base SQLite

**Exemple vunérable**:
 Construction de requête non sécurisée : 
String query = "SELECT * FROM inbox_messages WHERE message_id = '" + messageId + "'";
database.rawQuery(query, null);

**attaque**:
SELECT * FROM inbox_messages WHERE message_id = '' OR '1'='1'
Permet de récupérer tous les messages.

**Fichiers concernés**:
- `com/pushwoosh/inapp/f/b.java`
- `com/pushwoosh/inbox/e/b/b.java`
- `com/pushwoosh/internal/network/f.java`
- `com/pushwoosh/repository/LockScreenMediaStorageImpl.java`
- `com/pushwoosh/repository/PushBundleStorageImpl.java`
- `com/pushwoosh/repository/c.java`

**Impact**:
- Accès non autorisé aux données de la base
- Manipulation des données stockées (lecture, modification, suppression)
- Vol d'informations sensibles stockées sans chiffrement
- Élévation de privilèges potentielle dans l'application