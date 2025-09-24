En tant que ingénieure Sécurité
## Je veux décompliler le bytecode de mon apk
## afin de touver vunérabilité logique ou mauvaise pratiques

DoD : code_findings.md avec explication pour chaque extrait

Vulnérabilité 1: Utilisation du mode CBC avec padding PKCS5/PKCS7
Gravité: Élevée
Description simple:
L'application utilise le mode de chiffrement CBC (Cipher Block Chaining) avec le padding PKCS5/PKCS7. Cette combinaison est vulnérable aux attaques par "padding oracle". Un attaquant peut exploiter cette vulnérabilité pour déchiffrer progressivement des données chiffrées sans connaître la clé de chiffrement.
Comment ça fonctionne:

1.  Le mode CBC divise les données en blocs et les chiffre séquentiellement
2.  Le padding PKCS5/PKCS7 ajoute des octets à la fin du message pour compléter le dernier bloc
3.  Dans une attaque par "padding oracle", l'attaquant modifie les blocs chiffrés et observe si l'application renvoie une erreur de padding ou non
4.  En analysant ces réponses, l'attaquant peut déduire le contenu des données chiffrées
    Fichiers concernés:
    com/oblador/keychain/cipherStorage/CipherStorageKeystoreAESCBC.java
    com/pushwoosh/internal/a/a.java

Impact:
Compromission potentielle des données sensibles chiffrées
Possibilité de déchiffrer des informations confidentielles comme des jetons d'authentification, mots de passe, etc.

Vulnérabilité 2: Fichiers contenant des informations sensibles codées en dur
Gravité: Moyenne (mais impact potentiellement élevé)
Description simple:
L'application contient des fichiers avec des informations sensibles codées en dur comme des noms d'utilisateur, mots de passe, clés, etc. Ces informations peuvent être facilement extraites par quiconque décompile l'application.
Comment ça fonctionne:

1.  Les développeurs ont intégré directement dans le code des informations sensibles (comme des clés API, des identifiants, etc.)
2.  Ces informations sont stockées en texte clair dans le code de l'application
3.  N'importe qui peut décompiler l'APK et lire ces informations sensibles
4.  Ces informations peuvent être utilisées pour accéder à des services, contourner l'authentification ou compromettre la sécurité
    Fichiers concernés:
    com/bumptech/glide/load/Option.java
    com/bumptech/glide/load/engine/DataCacheKey.java
    com/bumptech/glide/load/engine/EngineResource.java
    com/bumptech/glide/load/engine/ResourceCacheKey.java
    com/pushwoosh/reactnativeplugin/InboxUiStyleManager.java
    Impact:
    Exposition de secrets qui devraient rester confidentiels
    Possibilité d'accès non autorisé à des services tiers
    Contournement potentiel des mécanismes d'authentification
    Compromission de la sécurité de l'application et des données utilisateur

Vulnérabilité 3: Utilisation d'un générateur de nombres aléatoires non sécurisé
Gravité: Moyenne (mais critique pour la sécurité cryptographique)
Description simple:
L'application utilise un générateur de nombres aléatoires non sécurisé. Les nombres générés peuvent être prévisibles, ce qui compromet toutes les fonctionnalités de sécurité qui en dépendent, comme la génération de clés, de tokens ou de valeurs d'authentification.
Comment ça fonctionne:

1. L'application utilise probablement java.util.Random au lieu de java.security.SecureRandom
2. Les générateurs non sécurisés produisent des séquences prévisibles
3. Un attaquant peut prédire les "nombres aléatoires" générés
4. Cela permet de deviner des tokens de session, des clés temporaires ou d'autres valeurs censées être aléatoires
   Fichiers concernés:
   com/pushwoosh/internal/a/d.java
   com/pushwoosh/q.java
   Impact:

- Prédictibilité des valeurs supposées aléatoires
- Compromission des mécanismes de sécurité basés sur l'aléatoire
- Possibilité de deviner des tokens d'authentification
- Affaiblissement des algorithmes cryptographiques
