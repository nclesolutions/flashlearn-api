# FlashLearn API Documentatie: Grades Management

**Laatste Update:** *8/27/2024*

## Inleiding

Deze API biedt functionaliteit om cijfers (grades) te beheren, inclusief het ophalen van alle cijfers voor de ingelogde gebruiker en het bekijken van een specifiek cijfer.

## Basis-URL

```plaintext
https://flashlearn.nl/api
```

## Endpoints Overzicht

### 1. [Haal alle cijfers op](#1-haal-alle-cijfers-op)
### 2. [Bekijk een specifiek cijfer](#2-bekijk-een-specifiek-cijfer)

---

## 1. Haal alle cijfers op

Haal een lijst op van alle cijfers voor de ingelogde gebruiker. De cijfers worden gegroepeerd op vak.

- **URL**: `/grades`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **Response**:
  - **200 OK**: 
    ```json
    {
        "grades": {
            "Mathematics": [
                {
                    "id": 1,
                    "unique_id": "abc123",
                    "user_id": 1,
                    "course_id": 101,
                    "grade": "A",
                    "teacher_id": 201,
                    "date_awarded": "2024-08-15",
                    "remarks": "Excellent performance"
                    ...
                }
            ],
            "Science": [
                {
                    "id": 2,
                    "unique_id": "def456",
                    "user_id": 1,
                    "course_id": 102,
                    "grade": "B+",
                    "teacher_id": 202,
                    "date_awarded": "2024-08-20",
                    "remarks": "Good effort"
                    ...
                }
            ]
        }
    }
    ```

### Beschrijving van de Response:

- **`grades`**: Een object waarin de sleutels de namen van de vakken zijn (bijvoorbeeld `"Mathematics"`) en de waarden arrays zijn van cijfers die voor die vakken zijn geregistreerd.
- **Vak Naam**: De vakken worden gegroepeerd op basis van hun naam, waarbij elk vak een array van cijfers bevat.

## 2. Bekijk een specifiek cijfer

Haal de details op van een specifiek cijfer voor de ingelogde gebruiker.

- **URL**: `/grades/{id}`
- **Methode**: `GET`
- **Headers**:
  - `Authorization: Bearer <access_token>`
- **URL Parameters**:
  - `id` (vereist): De unieke ID (`unique_id`) van het cijfer dat je wilt bekijken.
- **Response**:
  - **200 OK**:
    ```json
    {
        "grade": {
            "id": 1,
            "unique_id": "abc123",
            "user_id": 1,
            "course_id": 101,
            "grade": "A",
            "teacher_id": 201,
            "date_awarded": "2024-08-15",
            "remarks": "Excellent performance"
            ...
        }
    }
    ```
  - **404 Not Found**:
    ```json
    {
        "error": "Cijfer niet gevonden"
    }
    ```

### Beschrijving van de Response:

- **`grade`**: De details van het specifieke cijfer dat is opgevraagd.

### Error Response
- **404 Not Found**: Als het cijfer met het opgegeven ID niet bestaat of niet toebehoort aan de ingelogde gebruiker.
