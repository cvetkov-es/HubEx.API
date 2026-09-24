# TSTG — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса TSTG (API for task life cycle administration in HubEx): сигнатуры, параметры, права. Типы — schemas/TSTG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/TSTG.md`; грабли — `notes/TSTG.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/TSTG`
> Примеры ответов вынесены в [../examples/TSTG.md](../examples/TSTG.md).

**Оглавление**

- Action — строки 46–49
- Пример запроса: — строки 51–52
- Пример успешного ответа (200): — строки 54–66
- Пример успешного ответа (206): — строки 68–69
- Негативные сценарии: — строки 71–74
- AssigneeSelectionRules — строки 76–79
- Пример запроса: — строки 81–82
- Пример успешного ответа (200): — строки 84–101
- Пример успешного ответа (206): — строки 103–104
- Негативные сценарии: — строки 106–111
- Branches — строки 113–116
- Пример запроса: — строки 118–119
- Пример успешного ответа (200): — строки 121–135
- Пример успешного ответа (206): — строки 137–138
- Негативные сценарии: — строки 140–143
- Requirements — строки 145–147
- TaskStageComponents — строки 149–151
- TaskStageLinks — строки 153–156
- Пример запроса: — строки 158–159
- Пример успешного ответа (206): — строки 161–181
- Негативные сценарии: — строки 183–189
- Пример запроса: — строки 191–192
- Пример успешного ответа (206): — строки 194–206
- Негативные сценарии: — строки 208–211
- TaskStages — строки 213–216
- Пример запроса: — строки 218–219
- Пример успешного ответа (200): — строки 221–239
- Пример успешного ответа (206): — строки 241–242
- Негативные сценарии: — строки 244–256
- Пример запроса: — строки 258–259
- Пример успешного ответа (200): — строки 261–275
- Пример успешного ответа (206): — строки 277–278
- Негативные сценарии: — строки 280–283

## Action
- `GET /Action` — Возвращает справочник действий по стадиям заявок. · коды: 200, 204, 206
  → map<ActionsResult>
  Поддерживает ограничение результата через заголовок `Range`.
            
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
- `GET /AssigneeSelectionRules` — Возвращает список правил выбора исполнителя. · коды: 200, 204, 206
  → map<RASRListResult>
  Поддерживает ограничение результата через заголовок `Range`.
            
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
- `GET /AssigneeSelectionRules/{id}` — Возвращает правило выбора исполнителя по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RASRGetResult

## Branches
- `GET /Branches` — Возвращает список веток жизненного цикла заявок. · коды: 200, 204, 206
  → map<BranchResult>
  Поддерживает ограничение результата через заголовок `Range`.
            
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
- `GET /Requirements/requirements` — Возвращает справочник требований тенанта. · коды: 200, 204 · примеры
  → map<RRListResult>

## TaskStageComponents
- `GET /TaskStageComponents/availability` — Возвращает компоненты и их доступность для указанных ролей на указанных стадиях. · коды: 200, 204 · примеры
  ← query: roleID?:int[], taskStageID?:int[], taskTypeID?:int[] → AvailabilityListResult

## TaskStageLinks
- `GET /TaskStageLinks` — Получение списка переходов между стадиями заявок · коды: 204, 206
  ← query: taskTypeID?:int, taskStageFromID?:int, taskStageToID?:int, userID?:int, roleID?:int → RTSLListResult[]
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
            
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
- `GET /TaskStageLinks/overridings` — Получение списка переопределений переходов между стадиями заявок · коды: 204, 206
  ← query: taskTypeID?:int, taskStageFromID?:int, taskStageToID?:int, roleID?:int → OverrideListResult[]
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
            
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
- `GET /TaskStages` — Возвращает справочник стадий заявок тенанта. · коды: 200, 204, 206
  ← query: triggerID?:int → map<RTSListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
            
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
- `HEAD /TaskStages` — Возвращает количество стадий заявок с автораспределением. · коды: 200 · примеры
  ← query: isAutoAssignmentExists?:bool
- `GET /TaskStages/{id}` — Возвращает стадию заявки по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RTSGetResult
- `GET /TaskStages/{id}/messageTriggers` — Возвращает триггеры сообщений для стадии заявки. · коды: 200, 204 · примеры
  ← path: id:int → IdNameResultOfShort[]
- `GET /TaskStages/{id}/requirements` — Возвращает требования для стадии заявки. · коды: 200, 204, 206
  ← path: id:int → TaskStageRequirementResult[]
  Поддерживает ограничение результата через заголовок `Range`.
            
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
