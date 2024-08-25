# Project Management API Documentatie

Deze API biedt functionaliteit om werkstukken (projects) te beheren, inclusief het ophalen, aanmaken, bijwerken, en verwijderen van werkstukken. Daarnaast biedt de API de mogelijkheid om beschikbare vakken op te halen.

## Basis-URL

```plaintext
https://flashlearn.nl/api
```

## Endpoints Overzicht

### 1. [Haal alle werkstukken op](#1-haal-alle-werkstukken-op)
### 2. [Bekijk een specifiek werkstuk](#2-bekijk-een-specifiek-werkstuk)
### 3. [Maak een nieuw werkstuk aan](#3-maak-een-nieuw-werkstuk-aan)
### 4. [Werk een bestaand werkstuk bij](#4-werk-een-bestaand-werkstuk-bij)
### 5. [Verwijder een werkstuk](#5-verwijder-een-werkstuk)
### 6. [Haal beschikbare vakken op](#6-haal-beschikbare-vakken-op)

---

## 1. Haal alle werkstukken op

Haal een lijst op van alle werkstukken, eventueel gefilterd op een specifiek vak.

- **URL**: `/projects`
- **Methode**: `GET`
- **Query Parameters**:
  - `vak` (optioneel): Het vak waarop je wilt filteren. Als deze niet wordt meegegeven, worden alle werkstukken opgehaald.
- **Response**:
  - **200 OK**: 
    ```json
    {
        "werkstukken": [
            {
                "id": 1,
                "title": "Werkstuk Titel",
                "vak": "Wiskunde",
                "niveau": "VWO",
                "content": "Inhoud van het werkstuk...",
                "owner_id": 1,
                "unique_id": "abcd1234-5678-90ef-ghij-klmn1234opqr",
                "creator": {
                    "id": 1,
                    "name": "John Doe",
                    "email": "john.doe@example.com"
                },
                "total_characters": 456
            }
            // Meer werkstukken...
        ],
        "vak": "Wiskunde"
    }
    ```

## 2. Bekijk een specifiek werkstuk

Haal de details op van een specifiek werkstuk op basis van zijn unieke ID.

- **URL**: `/projects/{id}`
- **Methode**: `GET`
- **URL Parameters**:
  - `id` (vereist): De unieke ID van het werkstuk dat je wilt bekijken.
- **Response**:
  - **200 OK**:
    ```json
    {
        "werkstuk": {
            "id": 1,
            "title": "Werkstuk Titel",
            "vak": "Wiskunde",
            "niveau": "VWO",
            "content": "Inhoud van het werkstuk...",
            "owner_id": 1,
            "unique_id": "abcd1234-5678-90ef-ghij-klmn1234opqr"
        },
        "creator": {
            "id": 1,
            "name": "John Doe",
            "email": "john.doe@example.com"
        }
    }
    ```
  - **404 Not Found**:
    ```json
    {
        "error": "Werkstuk niet gevonden"
    }
    ```

## 3. Maak een nieuw werkstuk aan

Maak een nieuw werkstuk aan met de opgegeven gegevens.

- **URL**: `/projects`
- **Methode**: `POST`
- **Body Parameters**:
  - `title` (vereist): De titel van het werkstuk.
  - `niveau` (vereist): Het niveau van het werkstuk (bijv. VWO, HAVO).
  - `vak` (vereist): Het vak waarvoor het werkstuk is.
  - `content` (vereist): De inhoud van het werkstuk.
- **Response**:
  - **201 Created**:
    ```json
    {
        "success": "Werkstuk succesvol aangemaakt.",
        "werkstuk": {
            "id": 1,
            "title": "Werkstuk Titel",
            "vak": "Wiskunde",
            "niveau": "VWO",
            "content": "Inhoud van het werkstuk...",
            "owner_id": 1,
            "unique_id": "abcd1234-5678-90ef-ghij-klmn1234opqr"
        }
    }
    ```

## 4. Werk een bestaand werkstuk bij

Werk een bestaand werkstuk bij met de opgegeven gegevens.

- **URL**: `/projects/{id}`
- **Methode**: `PUT`
- **URL Parameters**:
  - `id` (vereist): De unieke ID van het werkstuk dat je wilt bijwerken.
- **Body Parameters**:
  - `title` (vereist): De titel van het werkstuk.
  - `niveau` (vereist): Het niveau van het werkstuk.
  - `vak` (vereist): Het vak waarvoor het werkstuk is.
  - `editor` (vereist): De nieuwe inhoud van het werkstuk.
- **Response**:
  - **200 OK**:
    ```json
    {
        "success": "Werkstuk succesvol bijgewerkt."
    }
    ```
  - **403 Forbidden**:
    ```json
    {
        "error": "Werkstuk niet gevonden of je hebt geen rechten om dit werkstuk bij te werken."
    }
    ```

## 5. Verwijder een werkstuk

Verwijder een werkstuk op basis van zijn unieke ID. Alleen de eigenaar van het werkstuk kan dit doen.

- **URL**: `/projects/{id}`
- **Methode**: `DELETE`
- **URL Parameters**:
  - `id` (vereist): De unieke ID van het werkstuk dat je wilt verwijderen.
- **Response**:
  - **200 OK**:
    ```json
    {
        "success": "Werkstuk succesvol verwijderd."
    }
    ```
  - **403 Forbidden**:
    ```json
    {
        "error": "Werkstuk niet gevonden of je hebt geen rechten om dit werkstuk te verwijderen."
    }
    ```

## 6. Haal beschikbare vakken op

Haal een lijst op van alle beschikbare vakken die ten minste één werkstuk hebben.

- **URL**: `/projects/vakken/available`
- **Methode**: `GET`
- **Response**:
  - **200 OK**:
    ```json
    {
        "vakken": [
            "Wiskunde",
            "Nederlands",
            "Geschiedenis"
            // Meer vakken...
        ]
    }
    ```

---
