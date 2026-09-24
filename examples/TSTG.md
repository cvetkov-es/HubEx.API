# TSTG — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса TSTG, вынесенные из `endpoints/TSTG.md`. Сигнатуры и типы — там же и в `schemas/TSTG.md`.

## AssigneeSelectionRules

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

## TaskStages

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
