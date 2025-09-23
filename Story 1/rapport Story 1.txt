# Vérification de l'APK - US1 
## User Story 1: Téléchargement et vérification de l'APK 

**EN TANT que** testeur   

**JE VEUX** recevoir l'APK vulnérable déjà fourni par le PO   

**AFIN DE** travailler sur une base commune   

## Definition of Done (DoD) 

Chaque étudiant vérifie le hash avec sha256sum app.apk et documente le résultat. 

## Résultat de la vérification 
### Hash SHA256 

``` 

F01F08C8B6E2FE4612E81BC7E3A3BA9440DAD0D7A962F4E67640390DD721D528 

``` 
### Commande utilisée 

```powershell 

Get-FileHash -Path "PATH" -Algorithm SHA256 

``` 

```Lixux  

sha256Sum [filename]

```