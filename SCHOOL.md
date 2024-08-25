# School API Documentatie

**Laatste Update:** *8/25/2024*

## Inleiding

De School API biedt endpoints waarmee gebruikers informatie over hun school en relevante nieuwsbrieven kunnen ophalen. Deze API is ontworpen om eenvoudig te integreren in verschillende applicaties zoals mobiele apps en webportals.

## Basis-URL

```plaintext
https://yourdomain.com/api
```

## Endpoints Overzicht

### 1. [Haal schoolinformatie en nieuwsbrieven op](#1-haal-schoolinformatie-en-nieuwsbrieven-op)

---

## 1. Haal schoolinformatie en nieuwsbrieven op

Dit endpoint haalt de schoolinformatie en nieuwsbrieven op voor de ingelogde gebruiker. Als de gebruiker aan een school is gekoppeld, wordt de schoolinformatie samen met relevante nieuwsbrieven geretourneerd. Het combineert zowel school-specifieke nieuwsbrieven als algemene nieuwsbrieven (als de gebruiker niet aan een school is gekoppeld).

- **URL**: `/school`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **Response**:
  - **200 OK**:
    ```json
    {
        "schoolInfo": {
            "org_id": 1,
            "school_name": "School Naam",
            "address": "Straatnaam 123",
            "city": "Stad",
            "postal_code": "1234 AB",
            "created_at": "2024-01-01 00:00:00",
            "updated_at": "2024-01-01 00:00:00"
        },
        "newsletter": [
            {
                "id": 1,
                "title": "Nieuwsbrief Titel",
                "content": "Inhoud van de nieuwsbrief...",
                "created_at": "2024-02-01 10:00:00",
                "updated_at": "2024-02-01 10:00:00",
                "firstname": "Voornaam",
                "lastname": "Achternaam"
            },
            {
                "id": 2,
                "title": "Algemene Nieuwsbrief",
                "content": "Algemene inhoud van de nieuwsbrief...",
                "created_at": "2024-01-15 09:00:00",
                "updated_at": "2024-01-15 09:00:00",
                "firstname": "Algemeen",
                "lastname": "Gebruiker"
            }
            // Meer nieuwsbrieven...
        ]
    }
    ```

### Beschrijving van de Response

- **`schoolInfo`**: Bevat informatie over de school waaraan de gebruiker is gekoppeld. Als de gebruiker niet aan een school is gekoppeld, zal dit `null` zijn.
  - **`org_id`**: De ID van de school.
  - **`school_name`**: De naam van de school.
  - **`address`**: Het adres van de school.
  - **`city`**: De stad waar de school zich bevindt.
  - **`postal_code`**: De postcode van de school.
  - **`created_at`**: Datum en tijd waarop de schoolinformatie is aangemaakt.
  - **`updated_at`**: Datum en tijd waarop de schoolinformatie voor het laatst is bijgewerkt.

- **`newsletter`**: Een array van nieuwsbrieven die relevant zijn voor de gebruiker. Dit kan zowel school-specifieke als algemene nieuwsbrieven bevatten, gesorteerd op de meest recente datum.
  - **`id`**: De unieke ID van de nieuwsbrief.
  - **`title`**: De titel van de nieuwsbrief.
  - **`content`**: De inhoud van de nieuwsbrief.
  - **`created_at`**: Datum en tijd waarop de nieuwsbrief is aangemaakt.
  - **`updated_at`**: Datum en tijd waarop de nieuwsbrief voor het laatst is bijgewerkt.
  - **`firstname`**: De voornaam van de gebruiker die de nieuwsbrief heeft gemaakt.
  - **`lastname`**: De achternaam van de gebruiker die de nieuwsbrief heeft gemaakt.

### Error Responses

- **401 Unauthorized**: Als de gebruiker niet geauthenticeerd is.
  ```json
  {
      "message": "Unauthenticated."
  }
  ```

---

## Gebruik van de API

### Authenticatie

Deze API is beveiligd met `auth:sanctum`, wat betekent dat je een geldige access token moet verstrekken in de `Authorization` header om toegang te krijgen tot de endpoints. Als je niet bent geauthenticeerd, ontvang je een `401 Unauthorized` fout.

### Toepassingsscenario's

1. **Toon Schoolinformatie**:
   - Integreer deze API in een dashboard om gebruikers hun schoolinformatie te tonen.
2. **Nieuwsbrieven Weergave**:
   - Gebruik deze API om een lijst van nieuwsbrieven weer te geven die relevant zijn voor de gebruiker, zowel school-specifieke als algemene nieuwsbrieven.

### Beperkingen
- De API retourneert maximaal 3 nieuwsbrieven, waarbij de meest recente nieuwsbrieven eerst worden weergegeven.
- Als de gebruiker niet aan een school is gekoppeld, worden alleen algemene nieuwsbrieven weergegeven.
