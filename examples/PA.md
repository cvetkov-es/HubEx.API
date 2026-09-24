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

### `POST /AssetAssignments`

## Пример запроса:
`POST /AssetAssignments`
            
```json
[
  {
    "userID": 101,
    "assetID": 5001,
    "dateFrom": "2026-08-19T08:00:00Z",
    "dateTill": "2026-08-19T18:00:00Z"
  }
]
```
            
## Пример успешного ответа (201):
Тело ответа отсутствует. Код `201` возвращается, когда для переданных данных создаётся новое назначение.
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Код `202` возвращается, когда хотя бы одно из переданных назначений было обновлено.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAssignmentMerge`.

### `DELETE /AssetAssignments`

## Пример запроса:
`DELETE /AssetAssignments`
            
```json
[
  {
    "userID": 101,
    "assetID": 5001
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAssignmentDelete`.

## Employment

### `POST /Employment`

## Пример запроса:
`POST /Employment`
            
```json
{
  "userID": 123,
  "data": [
    {
      "position": "Сервисный инженер",
      "orgUnitID": 8,
      "dateFrom": "2026-01-01T00:00:00Z",
      "dateTill": "2026-12-31T23:59:59Z"
    }
  ]
}
```
            
## Пример успешного ответа (201):
```json
[
  {
    "userID": 123,
    "id": 101
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или содержит некорректные данные.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `EmploymentAdd`.

### `PUT /Employment`

## Пример запроса:
`PUT /Employment`
            
```json
{
  "userID": 123,
  "data": [
    {
      "id": 101,
      "position": "Старший сервисный инженер",
      "orgUnitID": 8,
      "dateFrom": "2026-01-01T00:00:00Z",
      "dateTill": "2026-12-31T23:59:59Z"
    }
  ]
}
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или содержит некорректные данные.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `EmploymentUpdate`.

### `DELETE /Employment`

## Пример запроса:
`DELETE /Employment`
            
```json
{
  "userID": 123,
  "data": [
    { "id": 101 },
    { "id": 102 }
  ]
}
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или содержит некорректные идентификаторы.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `EmploymentRemove`.

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

### `POST /RatingCriteria`

## Пример запроса:
`POST /RatingCriteria`
            
```json
[
  {
    "name": "Скорость реагирования",
    "weight": 1.25,
    "isSystem": false
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  1
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RatingCriteriaAdd`.
- 409 Conflict: создание не выполнено из-за конфликта данных.

### `PUT /RatingCriteria`

## Пример запроса:
`PUT /RatingCriteria`
            
```json
[
  {
    "id": 1,
    "name": "Скорость реакции",
    "weight": 1.5,
    "isSystem": false
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RatingCriteriaUpdate`.
- 409 Conflict: обновление не выполнено из-за конфликта данных.

### `DELETE /RatingCriteria`

## Пример запроса:
`DELETE /RatingCriteria`
            
```json
[
  1,
  2
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RatingCriteriaDelete`.
- 409 Conflict: удаление не выполнено из-за конфликта данных.

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

### `DELETE /RatingCriteria/{id}`

## Пример запроса:
`DELETE /RatingCriteria/1`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RatingCriteriaDelete`.
- 409 Conflict: удаление не выполнено из-за конфликта данных.

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

### `POST /Skills`

## Пример запроса:
`POST /Skills`
            
```json
[
  {
    "name": "Монтаж",
    "description": "Навык для монтажных работ",
    "isOptional": false
  },
  {
    "name": "Диагностика",
    "description": "Навык для диагностики оборудования",
    "isOptional": true
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "skillID": 10
  },
  {
    "skillID": 11
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: в результате обработки не было создано ни одной записи.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SkillAdd`.

### `PUT /Skills`

## Пример запроса:
`PUT /Skills`
            
```json
[
  {
    "id": 10,
    "name": "Монтаж и настройка",
    "description": "Обновленное описание навыка",
    "isOptional": false
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SkillUpdate`.

### `DELETE /Skills`

## Пример запроса:
`DELETE /Skills`
            
```json
[10, 11]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SkillDelete`.

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

### `DELETE /Skills/{id}`

## Пример запроса:
`DELETE /Skills/10`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `SkillDelete`.
- 409 Conflict: навык не может быть удалён из-за связанных данных.

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

## UserSkills

### `POST /UserSkills`

## Пример запроса:
`POST /UserSkills`
            
```json
[
  {
    "userID": 101,
    "data": [
      {
        "skillID": 10,
        "dateFrom": "2026-01-01T00:00:00Z",
        "dateTill": "2026-12-31T23:59:59Z"
      }
    ]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "skillID": 10,
    "userID": 101,
    "dateTill": "2026-12-31T23:59:59Z"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: в результате обработки не было создано ни одной связи.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserSkillAdd`.

### `PUT /UserSkills`

## Пример запроса:
`PUT /UserSkills`
            
```json
[
  {
    "userID": 101,
    "data": [
      {
        "skillID": 10,
        "dateFrom": "2026-01-01T00:00:00Z",
        "sourceDateTill": "2026-12-31T23:59:59Z",
        "dateTill": "2027-06-30T23:59:59Z"
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserSkillUpdate`.

### `DELETE /UserSkills`

## Пример запроса:
`DELETE /UserSkills`
            
```json
[
  {
    "userID": 101,
    "data": [10]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserSkillDelete`.

## Users

### `PUT /Users/onshift/end/{userID}`

## Пример запроса:
`PUT /Users/onshift/end/101`
            
```json
"2026-08-19T16:30:00Z"
```
            
## Пример успешного ответа (202):
```json
{
  "id": 15,
  "isDayOff": false,
  "date": "2026-08-19T00:00:00",
  "timeFrom": "08:00:00",
  "timeTill": "16:30:00"
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkShiftOnShift`.
- 409 Conflict: завершение смены не выполнено из-за конфликтующих данных.

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

### `PUT /Users/onshift/start/{userID}`

## Пример запроса:
`PUT /Users/onshift/start/101`
            
```json
{
  "from": "2026-08-19T08:00:00Z",
  "till": "2026-08-19T17:00:00Z"
}
```
            
## Пример успешного ответа (202):
```json
[
  {
    "id": 15,
    "isDayOff": false,
    "date": "2026-08-19T00:00:00",
    "timeFrom": "08:00:00",
    "timeTill": "17:00:00"
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса не содержит корректные данные для старта смены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkShiftOnShift`.
- 409 Conflict: старт смены не выполнен из-за конфликтующих данных.

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

### `POST /Users/onshift/{userID}`

## Пример запроса:
`POST /Users/onshift/101`
            
```json
[
  {
    "date": "2026-08-19T00:00:00",
    "isDayOff": false,
    "workShifts": [
      {
        "timeFrom": "08:00:00",
        "timeTill": "17:00:00"
      }
    ]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "id": 15,
    "isDayOff": false,
    "date": "2026-08-19T00:00:00",
    "timeFrom": "08:00:00",
    "timeTill": "17:00:00"
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса не содержит данные графика рабочих смен.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkShiftAdd`.
- 409 Conflict: создание графика не выполнено из-за конфликтующих данных.

### `DELETE /Users/onshift/{userID}`

## Пример запроса:
`DELETE /Users/onshift/101`
            
```json
[
  "2026-08-19T00:00:00Z"
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkShiftDelete`.
- 409 Conflict: удаление графика не выполнено из-за конфликтующих данных.

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

### `POST /Users/{userID}/workTypes`

## Пример запроса:
`POST /Users/101/workTypes`
            
```json
[
  7,
  9
]
```
            
## Пример успешного ответа (201):
```json
{
  "101": [
    7,
    9
  ]
}
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса не содержит список видов работ.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkTypeAdd`.

### `DELETE /Users/{userID}/workTypes`

## Пример запроса:
`DELETE /Users/101/workTypes`
            
```json
[
  7,
  9
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса не содержит список видов работ.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `UserWorkTypeDelete`.
