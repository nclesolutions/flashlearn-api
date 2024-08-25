# Absence Management API Documentatie

**Laatste Update:** *8/25/2024*

## Inleiding

Deze API biedt functionaliteit om afwezigheden (absences) te beheren, inclusief het ophalen van alle afwezigheden voor de ingelogde gebruiker en het bekijken van een specifieke afwezigheid.

## Basis-URL

```plaintext
https://flashlearn.nl/api
```

## Endpoints Overzicht

### 1. [Haal alle afwezigheden op](#1-haal-alle-afwezigheden-op)
### 2. [Bekijk een specifieke afwezigheid](#2-bekijk-een-specifieke-afwezigheid)

---

## 1. Haal alle afwezigheden op

Haal een lijst op van alle afwezigheden voor de ingelogde gebruiker. De afwezigheden worden gegroepeerd op datum.

- **URL**: `/absences`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **Response**:
  - **200 OK**: 
    ```json
    {
        "absences": {
            "01_Januari_2024": [
                {
                    "id": 1,
                    "unique_id": "abc123",
                    "user_id": 1,
                    "gemaakt_date": "2024-01-01",
                    "description": "Ziek",
                    ...
                }
            ],
            "02_Februari_2024": [
                {
                    "id": 2,
                    "unique_id": "def456",
                    "user_id": 1,
                    "gemaakt_date": "2024-02-02",
                    "description": "Afwezig",
                    ...
                }
            ]
        }
    }
    ```

### Beschrijving van de Response:

- **`absences`**: Een object waarin de sleutels datums zijn (geformatteerd zonder spaties, bijvoorbeeld `"02_Februari_2024"`) en de waarden arrays zijn van afwezigheden die op die datums zijn geregistreerd.
- **Datum Formattering**: De datums zijn geformatteerd als `"dd_MMM_yyyy"` (bijvoorbeeld `"02_Februari_2024"`), waarbij spaties zijn vervangen door underscores `_`.

## 2. Bekijk een specifieke afwezigheid

Haal de details op van een specifieke afwezigheid voor de ingelogde gebruiker, evenals een overzicht van alle afwezigheden gegroepeerd op datum.

- **URL**: `/absences/{id}`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **URL Parameters**:
  - `id` (vereist): De unieke ID (`unique_id`) van de afwezigheid die je wilt bekijken.
- **Response**:
  - **200 OK**:
    ```json
    {
        "absence": {
            "id": 1,
            "unique_id": "abc123",
            "user_id": 1,
            "gemaakt_date": "2024-01-01",
            "description": "Ziek",
            ...
        }
    }
    ```
  - **404 Not Found**:
    ```json
    {
        "error": "Afwezigheid niet gevonden"
    }
    ```

### Beschrijving van de Response:

- **`absence`**: De details van de specifieke afwezigheid die is opgevraagd.

### Error Response
- **404 Not Found**: Als de afwezigheid met het opgegeven ID niet bestaat of niet toebehoort aan de ingelogde gebruiker.
