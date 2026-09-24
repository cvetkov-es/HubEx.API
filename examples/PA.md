# PA — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса PA, вынесенные из `endpoints/PA.md`. Сигнатуры и типы — там же и в `schemas/PA.md`.

## AssetAssignments

### `GET /AssetAssignments`

## Пример запроса:
`GET /AssetAssignments?userID=101&assetID=5001&validOn=2026-08-19T00:00:00Z`
            
## Пример успешного ответа (200):
```json
[
  {
    "user": {
      "id": 101,
      "firstName": "Иван",
      "lastName": "Иванов",
      "deleted": false
    },
    "asset": {
      "id": 5001,
      "name": "Сканер штрихкодов",
      "deleted": false
    },
    "validityPeriod": {
      "from": "2026-08-01T00:00:00Z",
      "till": "2026-08-31T23:59:59Z"
    },
    "notes": "Назначено на период инвентаризации."
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть списка в пределах заголовка `Range`.
            
## Негативные сценарии:
- 204 NoContent: по заданным условиям назначения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAssignmentList`.

## Employment

### `GET /Employment/{userID}`

## Пример запроса:
`GET /Employment/123?validFrom=2026-01-01T00:00:00Z&validTill=2026-12-31T23:59:59Z`
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 101,
    "personnelNumber": "EMP-00123",
    "erpID": "ERP-123",
    "position": "Сервисный инженер",
    "userGroup": { "id": 2, "name": "Инженеры" },
    "orgUnit": { "id": 15, "name": "Северный филиал" },
    "company": { "id": 3, "name": "ООО Хабэкс" },
    "scheduleRule": { "id": 7, "name": "Пятидневка" },
    "dutyScheduleRule": { "id": 9, "name": "Ночные дежурства" },
    "validityPeriod": {
      "from": "2026-01-01T00:00:00Z",
      "till": "2026-12-31T23:59:59Z"
    }
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть списка в пределах заголовка `Range`.
            
## Негативные сценарии:
- 204 NoContent: для указанного пользователя записи о трудоустройстве не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `EmploymentList`.

## GeoTrackingModes

### `GET /GeoTrackingModes`

## Пример запроса:
`GET /GeoTrackingModes`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Отключен"
  },
  "2": {
    "name": "Периодический"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть словаря в пределах заголовка `Range`.
            
## Негативные сценарии:
- 204 NoContent: режимы геотрекинга не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `GeoTrackingModesList`.

## Mobilities

### `GET /Mobilities`

## Пример запроса:
`GET /Mobilities`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Пешая",
    "maxDistanceFromDefaultLocation": 10,
    "maxDistanceFromActualLocation": 3
  },
  "2": {
    "name": "На автомобиле",
    "maxDistanceFromDefaultLocation": 50,
    "maxDistanceFromActualLocation": 15
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть словаря в пределах заголовка `Range`.
            
## Негативные сценарии:
- 204 NoContent: для текущего тенанта не найдено ни одной мобильности.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MobilitiesList`.

## Moblities

### `GET /Moblities`

## Пример запроса:
`GET /Mobilities`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Пешая",
    "maxDistanceFromDefaultLocation": 10,
    "maxDistanceFromActualLocation": 3
  },
  "2": {
    "name": "На автомобиле",
    "maxDistanceFromDefaultLocation": 50,
    "maxDistanceFromActualLocation": 15
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть словаря в пределах заголовка `Range`.
            
## Негативные сценарии:
- 204 NoContent: для текущего тенанта не найдено ни одной мобильности.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MobilitiesList`.

## RatingCriteria

### `GET /RatingCriteria`

## Пример запроса:
`GET /RatingCriteria`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Скорость реагирования",
    "weight": 1.25,
    "isSystem": true
  }
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RatingCriteriaList`.

### `GET /RatingCriteria/{id}`

## Пример запроса:
`GET /RatingCriteria/1`
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "name": "Скорость реагирования",
  "weight": 1.25,
  "isSystem": true
}
```
            
## Негативные сценарии:
- 204 NoContent: критерий рейтинга с указанным идентификатором не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RatingCriteriaGet`.

## Sexes

### `GET /Sexes`

## Пример запроса:
`GET /Sexes`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Мужской"
  },
  "2": {
    "name": "Женский"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только записи из запрошенного диапазона `Range`.
            
## Негативные сценарии:
- 204 NoContent: справочник полов не содержит записей.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SexList`.

## Skills

### `GET /Skills`

## Пример запроса:
`GET /Skills?isDeleted=false`
            
## Пример успешного ответа (200):
```json
{
  "10": {
    "id": 10,
    "name": "Монтаж",
    "isOptional": false,
    "counters": {
      "tasks": 12,
      "assets": 4,
      "users": 15
    }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 204 NoContent: для заданных условий навыки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SkillList`.

### `GET /Skills/{id}`

## Пример запроса:
`GET /Skills/10`
            
## Пример успешного ответа (200):
```json
{
  "id": 10,
  "name": "Монтаж",
  "description": "Навык для монтажных работ",
  "isOptional": false,
  "deleted": null
}
```
            
## Негативные сценарии:
- 204 NoContent: навык с указанным идентификатором не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SkillGet`.

## Technicians

### `GET /Technicians/taskSchedules`

## Пример запроса:
`GET /Technicians/taskSchedules?validFrom=2026-08-19T00:00:00Z&validTill=2026-08-19T23:59:59Z`
            
## Пример успешного ответа (200):
```json
[
  {
    "period": {
      "from": "2026-08-19T10:00:00Z",
      "till": "2026-08-19T13:00:00Z"
    },
    "taskPeriod": {
      "from": "2026-08-19T10:00:00Z",
      "till": "2026-08-19T13:00:00Z"
    },
    "taskAssignmentPeriod": {
      "from": "2026-08-19T09:30:00Z",
      "till": "2026-08-19T13:30:00Z"
    },
    "description": "Монтаж оборудования и проверка подключения.",
    "assignedTo": {
      "id": 101,
      "firstName": "Иван",
      "lastName": "Иванов",
      "deleted": false
    },
    "listAssignedTo": [
      {
        "id": 101,
        "firstName": "Иван",
        "lastName": "Иванов",
        "deleted": false
      }
    ],
    "task": {
      "id": 50001,
      "number": "SR-50001",
      "notes": "Проверить оборудование на объекте.",
      "asset": { "id": 7001, "name": "Терминал", "deleted": false },
      "criticality": { "id": 1, "name": "Высокая", "color": "#FF0000" },
      "isClosed": false,
      "isCompleted": false,
      "deadline": "2026-08-20T18:00:00Z",
      "taskType": { "id": 3, "name": "Выезд" },
      "workType": { "id": 5, "name": "Монтаж" }
    },
    "company": { "id": 3, "name": "ООО Хабэкс", "deleted": null },
    "location": {
      "id": 15,
      "address": "г. Москва, ул. Тверская, д. 1",
      "coordinate": "55.751244:37.618423",
      "description": "Центральный вход, 2 этаж.",
      "deleted": null
    }
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: по указанным параметрам данные для диаграммы Ганта не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ScheduleTaskListForTenantMember`.

### `GET /Technicians/{userID}/rating`

## Пример запроса:
`GET /Technicians/101/rating`
            
## Пример успешного ответа (200):
```json
{
  "total": { "rating": 4.9, "trend": 1 },
  "lastYear": { "rating": 4.8, "trend": 1 },
  "lastFourMonths": { "rating": 4.7, "trend": 0 },
  "lastMonth": { "rating": 4.8, "trend": 1 },
  "lastWeek": { "rating": 5.0, "trend": 1 },
  "lastTenTasks": { "rating": 4.9, "trend": 1 },
  "lastFiftyTasks": { "rating": 4.8, "trend": 0 },
  "lastHundredTasks": { "rating": 4.7, "trend": -1 },
  "timestamp": "2026-08-19T09:30:00Z"
}
```
            
## Негативные сценарии:
- 204 NoContent: для указанного специалиста статистика рейтинга отсутствует.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TechnicianRatingGet`.

### `GET /Technicians/{userID}/taskRatings`

## Пример запроса:
`GET /Technicians/101/taskRatings`
            
## Пример успешного ответа (200):
```json
[
  {
    "taskID": 50001,
    "taskNumber": "SR-50001",
    "taskCompleted": "2026-08-18T15:30:00Z",
    "ratingCriteria": { "id": 1, "name": "Скорость реагирования" },
    "rating": 5,
    "comment": "Работа выполнена вовремя",
    "isIgnore": false,
    "ignoreReason": null
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: для указанного специалиста оценки по заявкам отсутствуют.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskTechnicianRatingList`.

### `GET /Technicians/{userID}/workSchedules`

## Пример запроса:
`GET /Technicians/101/workSchedules?validFrom=2026-08-19T00:00:00Z&validTill=2026-08-25T23:59:59Z`
            
## Пример успешного ответа (200):
```json
{
  "2026-08-19": {
    "workPeriod": {
      "from": "2026-08-19T08:00:00Z",
      "till": "2026-08-19T17:00:00Z"
    },
    "plannedWorkMinutes": 480,
    "taskWorkMinutes": 240,
    "isNightShift": false
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: для указанного специалиста расписание не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TechnicianWorkScheduleListForTenantMember`.

### `GET /Technicians/{userID}/workSchedules/appointments`

## Пример запроса:
`GET /Technicians/101/workSchedules/appointments?validOn=2026-08-19T00:00:00Z&showTransitionalAppointments=true&showWholeDayEvents=true`
            
## Пример успешного ответа (200):
```json
[
  {
    "period": {
      "from": "2026-08-19T10:00:00Z",
      "till": "2026-08-19T11:30:00Z"
    },
    "taskPeriod": {
      "from": "2026-08-19T10:00:00Z",
      "till": "2026-08-19T12:00:00Z"
    },
    "isContinuedOnTheNextDay": false,
    "task": {
      "id": 50001,
      "number": "SR-50001",
      "notes": "Диагностика оборудования",
      "asset": { "id": 7001, "name": "Терминал", "deleted": false },
      "criticality": { "id": 2, "name": "Средняя", "color": "#FFA500" },
      "isClosed": false,
      "isCompleted": false
    },
    "coordinate": "55.751244:37.618423"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: для указанного специалиста назначения в расписании не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ScheduleTaskListForTenantMember`.

## TenantSettings

### `GET /TenantSettings`

## Пример запроса:
`GET /TenantSettings`
            
## Пример успешного ответа (200):
```json
{
  "maxRatingMark": 5
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: доступ запрещён (пользователь не является членом тенанта).

## UserGroups

### `GET /UserGroups`

## Пример запроса:
`GET /UserGroups`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Сервисные инженеры"
  },
  "2": {
    "name": "Супервайзеры"
  }
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserGroupsList`.

## Users

### `GET /Users/onshift/schedules`

## Пример запроса:
`GET /Users/onshift/schedules?userID=101&validFrom=2026-08-19T00:00:00Z&validTill=2026-08-19T23:59:59Z`
            
## Пример успешного ответа (200):
```json
{
  "101": [
    {
      "isDayOff": false,
      "isCustomSchedule": true,
      "isPublicHoliday": false,
      "id": 15,
      "isNightShift": false,
      "dateWork": "2026-08-19T00:00:00",
      "timeFrom": "2026-08-19T09:00:00",
      "timeTill": "2026-08-19T18:00:00"
    }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: по указанным фильтрам смены не найдены.
- 400 BadRequest: параметры фильтрации не прошли валидацию.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkShiftList`.

### `GET /Users/onshift/status`

## Пример запроса:
`GET /Users/onshift/status?userID=101`
            
## Пример успешного ответа (200):
```json
[
  {
    "userID": 101,
    "onShift": true,
    "timeFrom": "2026-08-19T08:00:00",
    "timeTill": "2026-08-19T17:00:00"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: статусы по указанным пользователям не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkShiftList`.

### `GET /Users/{userID}/workTypes`

## Пример запроса:
`GET /Users/101/workTypes`
            
## Пример успешного ответа (200):
```json
{
  "101": [
    {
      "workType": {
        "id": 7,
        "name": "Монтаж",
        "description": null
      },
      "workClass": {
        "id": 2,
        "name": "Электромонтаж"
      }
    }
  ]
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть результата в пределах заголовка `Range`.
            
## Негативные сценарии:
- 204 NoContent: для указанного пользователя виды работ не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkTypeList`.
