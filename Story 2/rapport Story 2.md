## Permissions dangereuses

- **android.permission.READ_CONTACTS** (Dangereux) - Lecture des données de contacts
  Cette permission permet à l'application de lire toutes les données de contacts (carnet d'adresses) stockées sur votre téléphone. Des applications malveillantes pourraient utiliser cette fonctionnalité pour envoyer vos données personnelles à des tiers sans votre consentement. Cette permission représente un risque pour la confidentialité des données personnelles des utilisateurs.

- **android.permission.WRITE_EXTERNAL_STORAGE** (Dangereux) - Lecture/modification/suppression du contenu du stockage externe
  Cette permission autorise l'application à écrire sur le stockage externe de l'appareil. Cela peut permettre à l'application d'accéder, modifier ou supprimer des fichiers qui ne lui appartiennent pas, créant ainsi un risque potentiel pour l'intégrité des données de l'utilisateur.

## Vulnérabilités critiques

- **Compatibilité avec des versions Android non sécurisées**
  L'application peut être installée sur d'anciennes versions d'Android (4.4-4.4.4, minSdk=19) qui présentent de nombreuses vulnérabilités non corrigées. Ces appareils ne reçoivent plus de mises à jour de sécurité de la part de Google. Il est recommandé de prendre en charge Android version 10 (API 29) ou supérieure pour bénéficier de mises à jour de sécurité raisonnables.

- **Trafic en clair activé pour l'application**
  [android:usesCleartextTraffic=true] (Critique) - L'application est configurée pour utiliser du trafic réseau non chiffré, comme HTTP en clair, FTP, DownloadManager et MediaPlayer. La valeur par défaut pour les applications ciblant l'API 27 ou inférieure est "true", tandis que les applications ciblant l'API 28 ou supérieure ont une valeur par défaut de "false". L'utilisation de trafic en clair présente des risques majeurs : absence de confidentialité, d'authenticité et de protection contre les manipulations. Un attaquant sur le réseau peut intercepter les données transmises et les modifier sans être détecté.

- **Utilisation d'un mode de chiffrement vulnérable**
  L'application utilise le mode de chiffrement CBC avec le padding PKCS5/PKCS7. Cette configuration est vulnérable aux attaques par oracle de padding. 
  - Référence CWE: CWE-649: Dépendance à l'obscurcissement ou au chiffrement des entrées liées à la sécurité sans vérification d'intégrité
  - OWASP Top 10: M5: Cryptographie insuffisante
  - OWASP MASVS: MSTG-CRYPTO-3
  
  Fichiers concernés:
  - com/oblador/keychain/cipherStorage/CipherStorageKeystoreAESCBC.java
  - com/pushwoosh/internal/a/a.java