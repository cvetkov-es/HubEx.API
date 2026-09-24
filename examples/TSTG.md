# TSTG — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса TSTG, вынесенные из `endpoints/TSTG.md`. Сигнатуры и типы — там же и в `schemas/TSTG.md`.

## AssigneeSelectionRules

### `POST /AssigneeSelectionRules`

## Пример запроса:
`POST /AssigneeSelectionRules`
            
```json
[
  {
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
]
```
            
## Пример успешного ответа (201):
```json
[1, 2]
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssigneeSelectionRuleAdd`.

### `PUT /AssigneeSelectionRules`

## Пример запроса:
`PUT /AssigneeSelectionRules`
            
```json
[
  {
    "id": 1,
    "name": "Правило по навыкам (обновлено)",
    "requiredSkillRatio": 0.6,
    "optionalSkillRatio": 0.15,
    "workTypeRatio": 0.1,
    "preffereableRatio": 0.05,
    "managerRatio": 0.05,
    "assetResponsibilityRatio": 0.03,
    "customerRatio": 0.01,
    "districtRatio": 0.005,
    "oftenAssignedRatio": 0.005,
    "workScheduleRatio": 0.01
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssigneeSelectionRuleUpdate`.

### `DELETE /AssigneeSelectionRules`

## Пример запроса:
`DELETE /AssigneeSelectionRules`
            
```json
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssigneeSelectionRuleDelete`.

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

### `DELETE /AssigneeSelectionRules/{id}`

## Пример запроса:
`DELETE /AssigneeSelectionRules/1`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssigneeSelectionRuleDelete`.

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

### `POST /TaskStageComponents`

## Пример запроса:
`POST /TaskStageComponents`
            
```json
[
  {
    "taskStageID": 28,
    "taskTypeID": 79,
    "components": [
      {
        "id": 1,
        "roleID": 9,
        "capabilityID": 2,
        "permissionUiID": 10
      }
    ],
    "attributes": [
      {
        "id": 15,
        "roleID": 9,
        "capabilityID": 1,
        "permissionUiID": null
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ComponentsAvailabilityMerge`.

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

### `POST /TaskStageComponents/templates`

## Пример запроса:
`POST /TaskStageComponents/templates`
            
```json
[
  {
    "taskStageID": 28,
    "taskTypeID": 79,
    "taskViewTemplateID": 3
  }
]
```
            
## Пример успешного ответа (201):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ComponentsAvailabilityMerge`.

## TaskStageLinks

### `POST /TaskStageLinks`

## Пример запроса:
`POST /TaskStageLinks`
            
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStageID": 2,
    "toTaskStageID": 3,
    "name": "Принять",
    "description": "Принять заявку",
    "applyTaskStatusID": 5,
    "branchID": 1,
    "isPositiveResult": true,
    "timeoutSeconds": null,
    "timeoutToDeadlineSeconds": null,
    "roles": [101]
  }
]
```
            
## Пример успешного ответа (201):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkAdd`.

### `PUT /TaskStageLinks`

## Пример запроса:
`PUT /TaskStageLinks`
            
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStageID": 2,
    "toTaskStageID": 3,
    "name": "Принять (обновлено)",
    "description": "Обновленное описание",
    "applyTaskStatusID": 5,
    "branchID": 1,
    "isPositiveResult": true,
    "timeoutSeconds": 300,
    "timeoutToDeadlineSeconds": null,
    "roles": [101, 102]
  }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkUpdate`.

### `DELETE /TaskStageLinks`

## Пример запроса:
`DELETE /TaskStageLinks`
            
```json
[
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 3 }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных удаления.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkDelete`.

### `POST /TaskStageLinks/copy`

## Пример запроса:
`POST /TaskStageLinks/copy`
            
```json
[
  { "sourceTaskTypeID": 1, "targetTaskTypeID": 2 }
]
```
            
## Пример успешного ответа (201):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных копирования.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkAdd`.

### `POST /TaskStageLinks/overridings`

## Пример запроса:
`POST /TaskStageLinks/overridings`
            
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStageID": 2,
    "toTaskStageID": 3,
    "name": "Принять",
    "description": "Переопределение для роли",
    "isPositiveResult": true,
    "roles": [101]
  }
]
```
            
## Пример успешного ответа (201):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkOverrideAdd`.

### `PUT /TaskStageLinks/overridings`

## Пример запроса:
`PUT /TaskStageLinks/overridings`
            
```json
[
  {
    "taskTypeID": 1,
    "fromTaskStageID": 2,
    "toTaskStageID": 3,
    "name": "Принять (обновлено)",
    "description": "Обновлённое переопределение для роли",
    "isPositiveResult": true,
    "roles": [101]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkOverrideUpdate`.

### `DELETE /TaskStageLinks/overridings`

## Пример запроса:
`DELETE /TaskStageLinks/overridings`
            
```json
[
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 3, "roles": [101] }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных удаления.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkOverrideDelete`.

### `POST /TaskStageLinks/reorder`

## Пример запроса:
`POST /TaskStageLinks/reorder`
            
```json
[
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 3, "sortOrder": 1 },
  { "taskTypeID": 1, "fromTaskStageID": 2, "toTaskStageID": 5, "sortOrder": 2 }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных сортировки.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkReorder`.

## TaskStageMessageTriggers

### `POST /TaskStageMessageTriggers`

## Пример запроса:
`POST /TaskStageMessageTriggers`
            
```json
[
  {
    "triggerID": 5,
    "data": [10, 12]
  },
  {
    "triggerID": 6,
    "data": [14]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TriggerTaskStageMerge`.

## TaskStageRequirements

### `POST /TaskStageRequirements`

## Пример запроса:
`POST /TaskStageRequirements`
            
```json
[
  {
    "taskStageID": 10,
    "data": [
      {
        "id": 1,
        "argumentsJson": "{\"minLength\": 10}"
      },
      {
        "id": 2,
        "argumentsJson": null
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageRequirementMerge`.

## TaskStages

### `POST /TaskStages`

## Пример запроса:
`POST /TaskStages`
            
```json
[
  {
    "taskViewTemplateID": 1,
    "name": "В работе",
    "description": "Заявка выполняется исполнителем",
    "actionID": 1,
    "assigneeSelectionRuleID": 2,
    "assignToUserID": 500,
    "assignToRoleID": 101,
    "isShowTechnicianOnMap": true,
    "color": "FF5722"
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  10,
  11
]
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageAdd`.

### `PUT /TaskStages`

## Пример запроса:
`PUT /TaskStages`
            
```json
[
  {
    "id": 2,
    "taskViewTemplateID": 1,
    "name": "В работе (обновлено)",
    "description": "Обновлённое описание стадии",
    "actionID": 1,
    "assigneeSelectionRuleID": 2,
    "assignToUserID": 500,
    "assignToRoleID": 101,
    "isShowTechnicianOnMap": false,
    "color": "4CAF50"
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageUpdate`.

### `DELETE /TaskStages`

## Пример запроса:
`DELETE /TaskStages`
            
```json
[2, 3]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageDelete`.

### `HEAD /TaskStages`

## Пример запроса:
`HEAD /TaskStages?isAutoAssignmentExists=true`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. В заголовке `Content-Range` возвращается общее количество найденных стадий, например: `items 0-0/5`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageAutoAssignmentList`.

### `POST /TaskStages/copy`

## Пример запроса:
`POST /TaskStages/copy`
            
```json
[
  {
    "sourceID": 2,
    "name": "В работе (копия)",
    "description": "Копия стадии «В работе»"
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  12
]
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageAdd`.
- 409 Conflict: копирование не выполнено из-за конфликта данных. Тело ответа — `List<ErrorModel>`.

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

### `DELETE /TaskStages/{id}`

## Пример запроса:
`DELETE /TaskStages/2`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageDelete`.
- 409 Conflict: удаление не выполнено из-за конфликта связанных данных. Тело ответа — `List<ErrorModel>`.

### `POST /TaskStages/{id}/assign`

## Пример запроса:
`POST /TaskStages/2/assign`
            
```json
{
  "messageTriggers": [1, 2, 3]
}
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageMessageTriggerAssign`.

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
