## User Story 3: Extractions de fichier

**EN TANT** que reverse-engineer

**JE VEUX** extraire classes.dex / AndroidManifest.xml de l’APK

**AFIN DE** préparer une décompilation

## Definition of Done (DoD)

Livrer les fichiers classes.dex et manifest.xml avec hash256.

## Résultat

On décompose l’APK à l’aide apktool et on se rend compte que les classes sont alors nombreuses à l’intérieur de classes.dex (plusieurs dizaines), en convertissant le fichier APK en ZIP, on peut alors accéder au classes.dex ainsi qu’a son hash256 grâce à la commande :

```powershell
Get-FileHash classes.dex -Algorithm SHA256
```

Ce qui nous donne :

```
57898C5978715DA96560ED2692B4A8FA1A8E914B37988DCF369CC59951F6C429
```

Le fichier AndroidManifest.xml quant à lui donne ceci en hash256 :

```
80B9B101E3BF02F03EEC4F2C9C9CCF4D61403612E1435949B51CEC8B85D7A276
```
