# TSTG — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса TSTG, вынесенные из `endpoints/TSTG.md`. Сигнатуры и типы — там же и в `schemas/TSTG.md`.

## Action

### `GET /Action`

## Пример запроса:
`GET /Action`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Принять",
    "code": "Accept"
  },
  "2": {
    "name": "Отклонить",
    "code": "Reject"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 204 NoContent: действия не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ActionList`.

## AssigneeSelectionRules

### `GET /AssigneeSelectionRules`

## Пример запроса:
`GET /AssigneeSelectionRules`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Правило по навыкам",
    "requiredSkillRatio": 0.5,
    "optionalSkillRatio": 0.2,
    "workTypeRatio": 0.1,
    "preffereableRatio": 0.05,
    "managerRatio": 0.05,
    "assetResponsibilityRatio": 0.05,
    "customerRatio": 0.02,
    "districtRatio": 0.01,
    "oftenAssignedRatio": 0.01,
    "workScheduleRatio": 0.01
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 204 NoContent: правила не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssigneeSelectionRuleList`.

### `GET /AssigneeSelectionRules/{id}`

## Пример запроса:
`GET /AssigneeSelectionRules/1`
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "name": "Правило по навыкам",
  "requiredSkillRatio": 0.5,
  "optionalSkillRatio": 0.2,
  "workTypeRatio": 0.1,
  "preffereableRatio": 0.05,
  "managerRatio": 0.05,
  "assetResponsibilityRatio": 0.05,
  "customerRatio": 0.02,
  "districtRatio": 0.01,
  "oftenAssignedRatio": 0.01,
  "workScheduleRatio": 0.01,
  "deleted": null
}
```
            
## Негативные сценарии:
- 204 NoContent: правило с указанным идентификатором не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssigneeSelectionRuleGet`.

## Branches

### `GET /Branches`

## Пример запроса:
`GET /Branches`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "nameRu": "Основная ветка",
    "isExclusiveMode": false,
    "color": "#4CAF50"
  },
  "2": {
    "nameRu": "Альтернативная ветка",
    "isExclusiveMode": true,
    "color": "#FF9800"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 204 NoContent: ветки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `BranchesList`.

## Requirements

### `GET /Requirements/requirements`

## Пример запроса:
`GET /Requirements/requirements`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "code": "PhotoRequired",
    "name": "Фото обязательно",
    "description": "Требуется приложить фото выполненной работы"
  },
  "2": {
    "code": "SignatureRequired",
    "name": "Подпись обязательна",
    "description": "Требуется подпись заказчика"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: требования не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `RequirementList`.

## TaskStageComponents

### `GET /TaskStageComponents/availability`

## Пример запроса:
`GET /TaskStageComponents/availability?roleID=9&taskStageID=28&taskTypeID=79&taskTypeID=80`
            
## Пример успешного ответа (200):
```json
{
  "components": [
    {
      "component": {
        "id": 1,
        "code": "locationID",
        "description": "Адрес"
      },
      "availability": {
        "taskStageID": 28,
        "taskTypes": [79],
        "roleID": 9,
        "capabilityID": 2
      }
    }
  ],
  "attributes": [
    {
      "attribute": {
        "id": 15,
        "name": "Комментарий",
        "type": {
          "code": "Text",
          "name": "Текст"
        }
      },
      "availability": {
        "taskStageID": 28,
        "taskTypes": [79, 80],
        "roleID": 9,
        "capabilityID": 1
      }
    }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: компоненты и атрибуты по заданным фильтрам не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ComponentsAvailabilityList`.

## TaskStageLinks

### `GET /TaskStageLinks`

## Пример запроса:
`GET /TaskStageLinks?taskTypeID=1&taskStageFromID=2&userID=500&roleID=101`
            
## Пример успешного ответа (206):
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStage": { "id": 2, "name": "Назначена" },
    "toTaskStage": { "id": 3, "name": "В работе" },
    "taskStatus": { "id": 5, "name": "Принята" },
    "branch": { "id": 1, "name": "Основная ветка" },
    "name": "Принять",
    "description": "Принять заявку",
    "isPositiveResult": true,
    "permissionUiID": 10,
    "sortOrder": 1,
    "timeoutSeconds": null,
    "timeoutToDeadlineSeconds": null,
    "roles": [
      { "id": 101, "name": "Инженер", "description": "Роль инженера" }
    ]
  }
]
```
## Негативные сценарии:
- 204 NoContent: переходы по заданным фильтрам не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkList`.

### `GET /TaskStageLinks/overridings`

## Пример запроса:
`GET /TaskStageLinks/overridings?taskTypeID=1&taskStageFromID=2&roleID=101`
            
## Пример успешного ответа (206):
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStage": { "id": 2, "name": "Назначена" },
    "toTaskStage": { "id": 3, "name": "В работе" },
    "name": "Принять",
    "description": "Переопределение для роли",
    "isPositiveResult": true,
    "role": { "id": 101, "name": "Инженер" }
  }
]
```
## Негативные сценарии:
- 204 NoContent: переопределения по заданным фильтрам не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkOverrideList`.

## TaskStages

### `GET /TaskStages`

## Пример запроса:
`GET /TaskStages?triggerID=1`
            
## Пример успешного ответа (200):
```json
{
  "2": {
    "id": 2,
    "name": "Назначена",
    "description": "Заявка назначена исполнителю",
    "color": "FF5722",
    "messageTriggerCount": 3,
    "taskViewTemplate": { "id": 1, "name": "Стандартная форма" },
    "action": { "id": 1, "name": "Назначить" },
    "assigneeSelectionRule": { "id": 2, "name": "По навыкам" },
    "assignToUser": { "id": 500, "name": "Иванов И.И." },
    "assignToRole": { "id": 101, "name": "Инженер" },
    "isShowTechnicianOnMap": true,
    "deleted": null
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 204 NoContent: стадии по заданным фильтрам не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStagesList`.

### `HEAD /TaskStages`

## Пример запроса:
`HEAD /TaskStages?isAutoAssignmentExists=true`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. В заголовке `Content-Range` возвращается общее количество найденных стадий, например: `items 0-0/5`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageAutoAssignmentList`.

### `GET /TaskStages/{id}`

## Пример запроса:
`GET /TaskStages/2`
            
## Пример успешного ответа (200):
```json
{
  "id": 2,
  "name": "Назначена",
  "description": "Заявка назначена исполнителю",
  "color": "FF5722",
  "messageTriggerCount": 3,
  "taskViewTemplate": { "id": 1, "name": "Стандартная форма" },
  "action": { "id": 1, "name": "Назначить" },
  "assigneeSelectionRule": { "id": 2, "name": "По навыкам" },
  "assignToUser": { "id": 500, "name": "Иванов И.И." },
  "assignToRole": { "id": 101, "name": "Инженер" },
  "isShowTechnicianOnMap": true,
  "deleted": null,
  "requirements": [
    { "id": 1, "name": "Фото до работ" }
  ],
  "messageTriggers": [
    { "id": 1, "name": "При назначении" }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: стадия с указанным идентификатором не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageGet`.

### `GET /TaskStages/{id}/messageTriggers`

## Пример запроса:
`GET /TaskStages/2/messageTriggers`
            
## Пример успешного ответа (200):
```json
[
  { "id": 1, "name": "При назначении" },
  { "id": 2, "name": "При завершении" }
]
```
            
## Негативные сценарии:
- 204 NoContent: триггеры сообщений для указанной стадии не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageGet`.

### `GET /TaskStages/{id}/requirements`

## Пример запроса:
`GET /TaskStages/2/requirements`
            
## Пример успешного ответа (200):
```json
[
  {
    "taskStageID": 2,
    "requirementID": 1,
    "requirementName": "Фото до работ"
  },
  {
    "taskStageID": 2,
    "requirementID": 2,
    "requirementName": "Подпись заказчика"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 204 NoContent: требования для указанной стадии не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageRequirementGet`.
