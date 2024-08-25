# Profile API Documentatie

**Laatste Update:** *8/25/2024*

## Inleiding

De Profile API biedt endpoints waarmee gebruikers hun profielgegevens, biografie en schoolinformatie kunnen ophalen. Deze API is ontworpen om eenvoudig te integreren in verschillende applicaties zoals mobiele apps en webportals, waardoor gebruikers toegang hebben tot hun persoonlijke en academische informatie.

## Basis-URL

```plaintext
https://flashlearn.nl/api
```

## Endpoints Overzicht

### 1. [Haal profielgegevens op](#1-haal-profielgegevens-op)

---

## 1. Haal profielgegevens op

Dit endpoint haalt de profielgegevens op voor de ingelogde gebruiker.

- **URL**: `/profile`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **Response**:
  - **200 OK**:
    ```json
    {
        "account": {
            "id": 1,
            "name": "Gebruikersnaam",
            "email": "email@example.com",
            "created_at": "2024-01-01 00:00:00",
            "updated_at": "2024-01-01 00:00:00",
            ...
        }
    }
    ```

### Beschrijving van de Response

- **`account`**: Bevat de profielgegevens van de ingelogde gebruiker.
  - **`id`**: De unieke ID van de gebruiker.
  - **`name`**: De naam van de gebruiker.
  - **`email`**: Het e-mailadres van de gebruiker.
  - **`created_at`**: Datum en tijd waarop het account is aangemaakt.
  - **`updated_at`**: Datum en tijd waarop het account voor het laatst is bijgewerkt.
    
### Error Responses

- **401 Unauthorized**: Als de gebruiker niet geauthenticeerd is of geen geldige token heeft verstrekt.
  ```json
  {
      "message": "Unauthenticated."
  }
  ```

### Gebruik van de API

### Authenticatie

Deze API is beveiligd met `auth:sanctum`, wat betekent dat je een geldige access token moet verstrekken in de `Authorization` header om toegang te krijgen tot de endpoints. Als je niet bent geauthenticeerd, ontvang je een `401 Unauthorized` fout.

### Toepassingsscenario's

1. **Toon Profielgegevens**:
   - Integreer deze API in een gebruikersdashboard om profielgegevens weer te geven, inclusief de naam, e-mail en biografie van de gebruiker.
  
2. **Schoolinformatie Weergave**:
   - Gebruik deze API om de schoolinformatie van een gebruiker op te halen en weer te geven, zodat gebruikers altijd weten met welke school ze zijn verbonden.
