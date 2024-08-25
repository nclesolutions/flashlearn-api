# Rooster API Documentatie

Deze API biedt functionaliteit om het rooster van de huidige week op te halen. De response bevat het rooster voor elke dag van de week, inclusief details over de lessen, locaties, en docenten.

## Basis-URL

```plaintext
http://flashlearn.nl/api
```

## Endpoint Overzicht

### 1. [Bekijk het rooster voor de huidige week](#1-bekijk-het-rooster-voor-de-huidige-week)

---

## 1. Bekijk het rooster voor de huidige week

Deze endpoint retourneert het rooster voor de huidige week. De data bevat informatie over de weeknummers, startdatum van de week, en een overzicht van het lesrooster voor elke dag.

- **URL**: `/rooster`
- **Methode**: `GET`
- **Query Parameters**: Geen
- **Response**:
  - **200 OK**:
    ```json
    {
        "currentWeekRooster": {
            "week_number": 34,
            "start_date": "1970-01-01",
            "days": [
                {
                    "day_of_week": "Maandag",
                    "schedule": [
                        {
                            "time": "08:30 tot 09:30",
                            "lesson": "Engels",
                            "location": "Lokaal 2",
                            "teacher": "H. Vermeer"
                        },
                        {
                            "time": "09:45 tot 10:45",
                            "lesson": "Wiskunde",
                            "location": "Lokaal 5",
                            "teacher": "H. Vermeer"
                        },
                        {
                            "time": "11:00 tot 12:00",
                            "lesson": "Geschiedenis",
                            "location": "Lokaal 1",
                            "teacher": "J. van Boom"
                        },
                        {
                            "time": "13:00 tot 14:00",
                            "lesson": "Engels",
                            "location": "Lokaal 2",
                            "teacher": "H. Vermeer"
                        },
                        {
                            "time": "14:00 tot 15:00",
                            "lesson": "Biologie",
                            "location": "Lokaal 3",
                            "teacher": "J. Pieter"
                        }
                    ]
                },
                // Verdere dagen van de week...
            ]
        },
        "weeks": [
            {
                "week_number": 34,
                "start_date": "1970-01-01",
                "days": [
                    {
                        "day_of_week": "Maandag",
                        "schedule": [
                            {
                                "time": "08:30 tot 09:30",
                                "lesson": "Engels",
                                "location": "Lokaal 2",
                                "teacher": "1"
                            },
                            {
                                "time": "09:45 tot 10:45",
                                "lesson": "Wiskunde",
                                "location": "Lokaal 5",
                                "teacher": "1"
                            },
                            {
                                "time": "11:00 tot 12:00",
                                "lesson": "Geschiedenis",
                                "location": "Lokaal 1",
                                "teacher": "3"
                            },
                            {
                                "time": "13:00 tot 14:00",
                                "lesson": "Engels",
                                "location": "Lokaal 2",
                                "teacher": "1"
                            },
                            {
                                "time": "14:00 tot 15:00",
                                "lesson": "Biologie",
                                "location": "Lokaal 3",
                                "teacher": "2"
                            }
                        ]
                    },
                    // Verdere dagen van de week...
                ]
            }
        ],
        "weekNumber": "34"
    }
    ```

### Beschrijving van de response

- **currentWeekRooster**: Het rooster voor de huidige week.
  - **week_number**: Het nummer van de week volgens de kalender.
  - **start_date**: De startdatum van de week.
  - **days**: Een lijst met dagen van de week en hun roosters.
    - **day_of_week**: De dag van de week (bijv. "Maandag").
    - **schedule**: Een lijst met lessen voor die dag.
      - **time**: De tijd van de les (bijv. "08:30 tot 09:30").
      - **lesson**: De naam van de les (bijv. "Engels").
      - **location**: De locatie van de les (bijv. "Lokaal 2").
      - **teacher**: De naam van de docent (bijv. "H. Vermeer").

- **weeks**: Dit veld bevat dezelfde informatie als `currentWeekRooster`, maar kan een historische of toekomstige weergave van het rooster bevatten.
  - **week_number**: Het nummer van de week.
  - **start_date**: De startdatum van de week.
  - **days**: Een lijst met dagen van de week en hun roosters.
    - **day_of_week**: De dag van de week (bijv. "Maandag").
    - **schedule**: Een lijst met lessen voor die dag.
      - **time**: De tijd van de les.
      - **lesson**: De naam van de les.
      - **location**: De locatie van de les.
      - **teacher**: De ID van de docent.

- **weekNumber**: Het huidige weeknummer, wat overeenkomt met de kalenderweek.

---

### Voorbeeldgebruik

- **Rooster voor de huidige week ophalen**:
  ```http
  GET http://flashlearn.nl/api/rooster
  ```
