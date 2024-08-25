# Homework API Documentatie

**Laatste Update:** *8/25/2024*

## Inleiding

De Homework API biedt endpoints waarmee gebruikers hun huiswerkopdrachten kunnen ophalen. De data wordt geretourneerd in JSON-formaat, gegroepeerd op inleverdatum. De datumsleutels in de response zijn geformatteerd zonder spaties, wat zorgt voor eenvoudige integratie in applicaties.

## Basis-URL

```plaintext
https://flashlearn.nl/api
```

## Endpoints Overzicht

### 1. [Haal al het huiswerk op](#1-haal-al-het-huiswerk-op)
### 2. [Haal een specifiek huiswerk op](#2-haal-een-specifiek-huiswerk-op)

---

## 1. Haal al het huiswerk op

Dit endpoint haalt alle huiswerkopdrachten op voor de ingelogde gebruiker, gegroepeerd op inleverdatum. De datumsleutels zijn geformatteerd zonder spaties.

- **URL**: `/homework`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **Response**:
  - **200 OK**:
    ```json
    {
        "homework": {
            "27_Augustus_2024": [
                {
                    "id": 1,
                    "title": "Wiskunde opdracht",
                    "description": "Maak opdracht 1 t/m 10",
                    "inlever_date": "2024-08-27",
                    ...
                }
            ],
            "28_September_2024": [
                {
                    "id": 2,
                    "title": "Engels essay",
                    "description": "Schrijf een essay over Shakespeare",
                    "inlever_date": "2024-09-28",
                    ...
                }
            ]
        }
    }
    ```

### Beschrijving van de Response:

- **`homework`**: Een object waarin de sleutels datums zijn zonder spaties, en de waarden arrays van huiswerkopdrachten die op die datums moeten worden ingeleverd.
  - **`id`**: De unieke ID van de huiswerkopdracht.
  - **`title`**: De titel van de huiswerkopdracht.
  - **`description`**: Een korte beschrijving van de huiswerkopdracht.
  - **`inlever_date`**: De datum waarop het huiswerk moet worden ingeleverd.

### Error Responses:

- **401 Unauthorized**: Als de gebruiker niet geauthenticeerd is.
  ```json
  {
      "message": "Unauthenticated."
  }
  ```

---

## 2. Haal een specifiek huiswerk op

Dit endpoint haalt een specifieke huiswerkopdracht op basis van de unieke ID, samen met andere huiswerkopdrachten, gegroepeerd op inleverdatum.

- **URL**: `/homework/{id}`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **URL Parameters**:
  - `id` (vereist): De unieke ID van het huiswerk dat je wilt ophalen.
- **Response**:
  - **200 OK**:
    ```json
    {
        "homework": {
            "id": 1,
            "title": "Wiskunde opdracht",
            "description": "Maak opdracht 1 t/m 10",
            "inlever_date": "2024-08-27",
            "formatted_date": "27_Augustus_2024",
            ...
        }
    }
    ```

### Beschrijving van de Response:

- **`homework`**: De details van de specifieke huiswerkopdracht, inclusief een geformatteerde inleverdatum.
  - **`id`**: De unieke ID van de huiswerkopdracht.
  - **`title`**: De titel van de huiswerkopdracht.
  - **`description`**: Een korte beschrijving van de huiswerkopdracht.
  - **`inlever_date`**: De datum waarop het huiswerk moet worden ingeleverd.
  - **`formatted_date`**: De inleverdatum, geformatteerd zonder spaties.
  - 
### Error Responses:

- **403 Forbidden**: Als de gebruiker probeert toegang te krijgen tot huiswerk dat niet van hem of haar is.
  ```json
  {
      "error": "Homework not found or unauthorized access."
  }
  ```
