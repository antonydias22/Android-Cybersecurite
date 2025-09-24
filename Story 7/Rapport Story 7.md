## User Story 7: Recompilation de l'APK

**EN TANT que** développeur

**JE VEUX** recompiler l'APK avec Apktool

**AFIN DE** vérifier que la décompilation est réversible

## Definition of Done (DoD):

- Fichier APK recompilé livré
- Log de build documenté

## Procédure réalisée

### 1. Commande utilisée pour la recompilation

apktool b "chemin/vers/dossier_décompilé" -o "chemin/vers/app_recompile.apk"

### 2. Log après execution de la commande :

I: Using Apktool 2.12.1 on app.apk with 8 threads
I: Checking whether sources have changed...
I: Checking whether resources have changed...
I: Building resources with aapt2...
I: Building apk file...
I: Importing assets...
I: Importing lib...
I: Importing unknown files...
I: Built apk into: app_recompile
