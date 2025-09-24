# US9 - Vérification Firebase

## User Story 9: Vérification Firebase

**EN TANT que** pentesteur  
**JE VEUX** tester l'accès public à une éventuelle base Firebase  
**AFIN DE** évaluer le risque de fuite de données

## RÉSUMÉ EXÉCUTIF

**URL Firebase Testée**: `https://application-client-nickel.firebaseio.com`  
**Source**: Découvert dans strings.xml (US5)  
**Status Sécurité**: **SÉCURISÉ**  
**Risque de fuite**: **FAIBLE**

## TESTS EFFECTUÉS

### 1. Test d'Accès Principal - GET /.json

**Commande**:

```powershell
Invoke-WebRequest -Uri "https://application-client-nickel.firebaseio.com/.json" -Method GET
```

**Capture de la Réponse**:

```json
{
  "error": "Permission denied"
}
```

### 2. Test Endpoints Sensibles

**Commande**:

```powershell
$endpoints = @("/.json", "/users.json", "/config.json", "/public.json", "/test.json")
foreach($endpoint in $endpoints) {
    # Test de chaque endpoint
}
```

**Capture des Réponses**:

```
PROTECTED: /.json - Le serveur distant a retourné une erreur : (401) Non autorisé.
PROTECTED: /users.json - Le serveur distant a retourné une erreur : (401) Non autorisé.
PROTECTED: /config.json - Le serveur distant a retourné une erreur : (401) Non autorisé.
PROTECTED: /public.json - Le serveur distant a retourné une erreur : (401) Non autorisé.
PROTECTED: /test.json - Le serveur distant a retourné une erreur : (401) Non autorisé.
```

### 3. Test Méthodes HTTP

**Commande**:

```powershell
$methods = @("GET", "POST", "PUT", "DELETE")
foreach($method in $methods) {
    # Test de chaque méthode HTTP
}
```

**Capture des Réponses**:

```
PROTECTED: GET - Status: Unauthorized
PROTECTED: POST - Status: BadRequest
PROTECTED: PUT - Status: BadRequest
PROTECTED: DELETE - Status: Unauthorized
```

### 4. Test Requêtes Spéciales Firebase

**Commande**:

```powershell
Invoke-RestMethod -Uri "https://application-client-nickel.firebaseio.com/.json?shallow=true" -Method GET
```

**Capture de la Réponse**:

```
PROTECTED shallow query - Status: Unauthorized

**Outils Utilisés**:
- PowerShell `Invoke-WebRequest`
- PowerShell `Invoke-RestMethod`
- Tests d'endpoints multiples
- Analyse des codes de réponse HTTP

**Approche**:
1. Test de l'endpoint principal découvert en US5
2. Énumération d'endpoints sensibles courants
3. Test de méthodes HTTP variées
4. Vérification des paramètres Firebase spéciaux
5. Documentation complète des réponses
```
