# TSTG — справочник ручек

> **Что здесь:** все ручки сервиса TSTG (API for task life cycle administration in HubEx): сигнатуры, параметры, права. Типы — schemas/TSTG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/TSTG.md`; грабли — `notes/TSTG.md` (если есть).

Base: `{BASE_URL}/TSTG`
> Примеры ответов вынесены в [../examples/TSTG.md](../examples/TSTG.md).

**Оглавление**

- Action — строки 47–50
- Пример запроса: — строки 52–53
- Пример успешного ответа (200): — строки 55–67
- Пример успешного ответа (206): — строки 69–70
- Негативные сценарии: — строки 72–75
- AssigneeSelectionRules — строки 77–80
- Пример запроса: — строки 82–83
- Пример успешного ответа (200): — строки 85–102
- Пример успешного ответа (206): — строки 104–105
- Негативные сценарии: — строки 107–120
- Branches — строки 122–125
- Пример запроса: — строки 127–128
- Пример успешного ответа (200): — строки 130–144
- Пример успешного ответа (206): — строки 146–147
- Негативные сценарии: — строки 149–152
- Requirements — строки 154–156
- TaskStageComponents — строки 158–164
- TaskStageLinks — строки 166–169
- Пример запроса: — строки 171–172
- Пример успешного ответа (206): — строки 174–194
- Негативные сценарии: — строки 196–210
- Пример запроса: — строки 212–213
- Пример успешного ответа (206): — строки 215–227
- Негативные сценарии: — строки 229–240
- TaskStageMessageTriggers — строки 242–244
- TaskStageRequirements — строки 246–248
- TaskStages — строки 250–253
- Пример запроса: — строки 255–256
- Пример успешного ответа (200): — строки 258–276
- Пример успешного ответа (206): — строки 278–279
- Негативные сценарии: — строки 281–305
- Пример запроса: — строки 307–308
- Пример успешного ответа (200): — строки 310–324
- Пример успешного ответа (206): — строки 326–327
- Негативные сценарии: — строки 329–332

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
- `POST /AssigneeSelectionRules` — Создаёт правила выбора исполнителя. · коды: 201, 400 · примеры
  ← body: TSTGASRAddData[] → int[]
- `PUT /AssigneeSelectionRules` — Изменяет правила выбора исполнителя. · коды: 202, 400 · примеры
  ← body: TSTGASRUpdateData[]
- `DELETE /AssigneeSelectionRules` — Помечает правила выбора исполнителя как удалённые. · коды: 202, 400 · примеры
  ← body: int[]
- `GET /AssigneeSelectionRules/{id}` — Возвращает правило выбора исполнителя по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RASRGetResult
- `DELETE /AssigneeSelectionRules/{id}` — Помечает правило выбора исполнителя как удалённое. · коды: 202 · примеры
  ← path: id:int

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
- `POST /TaskStageComponents` — Добавляет или изменяет доступность компонента для указанных ролей на указанных стадиях. · коды: 202, 400 · примеры
  ← body: TSTGTSCMergeData[]
- `GET /TaskStageComponents/availability` — Возвращает компоненты и их доступность для указанных ролей на указанных стадиях. · коды: 200, 204 · примеры
  ← query: roleID?:int[], taskStageID?:int[], taskTypeID?:int[] → AvailabilityListResult
- `POST /TaskStageComponents/templates` — Заполняет стадию заявки компонентами из шаблона отображения заявки. · коды: 201, 400 · примеры
  ← body: TemplateMergeData[]

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
- `POST /TaskStageLinks` — Создание переходов между стадиями заявок · коды: 201, 400 · примеры
  ← body: TSTGTSLAddData[]
- `PUT /TaskStageLinks` — Обновление переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLUpdateData[]
- `DELETE /TaskStageLinks` — Удаление переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLDeleteData[]
- `POST /TaskStageLinks/copy` — Копирование переходов стадий заявок из одного типа заявок в другой · коды: 201, 400 · примеры
  ← body: TSTGTSLCopyData[]
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
- `POST /TaskStageLinks/overridings` — Создание переопределений переходов между стадиями заявок · коды: 201, 400 · примеры
  ← body: TSTGTSLOAddData[]
- `PUT /TaskStageLinks/overridings` — Обновление переопределений переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLOUpdateData[]
- `DELETE /TaskStageLinks/overridings` — Удаление переопределений переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLODeleteData[]
- `POST /TaskStageLinks/reorder` — Сохранение порядка сортировки переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLSortData[]

## TaskStageMessageTriggers
- `POST /TaskStageMessageTriggers` — Добавляет или изменяет стадии заявок для триггеров уведомлений. · коды: 202, 400 · примеры
  ← body: MSGTTSMergeData[]

## TaskStageRequirements
- `POST /TaskStageRequirements` — Добавляет или изменяет требования на указанных стадиях. · коды: 202, 400 · примеры
  ← body: TSTGTSRMergeData[]

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
- `POST /TaskStages` — Создаёт стадии заявок. · коды: 201, 400 · примеры
  ← body: TSTGTSAddData[] → int[]
- `PUT /TaskStages` — Изменяет стадии заявок. · коды: 202, 400 · примеры
  ← body: TSTGTSUpdateData[]
- `DELETE /TaskStages` — Помечает стадии заявок как удалённые. · коды: 202, 400 · примеры
  ← body: int[]
- `HEAD /TaskStages` — Возвращает количество стадий заявок с автораспределением. · коды: 200 · примеры
  ← query: isAutoAssignmentExists?:bool
- `POST /TaskStages/copy` — Копирует стадии заявок. · коды: 201, 400, 409 · примеры
  ← body: TSTGTSCopyData[] → int[]
- `GET /TaskStages/{id}` — Возвращает стадию заявки по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RTSGetResult
- `DELETE /TaskStages/{id}` — Помечает стадию заявки как удалённую. · коды: 202, 409 · примеры
  ← path: id:int
- `POST /TaskStages/{id}/assign` — Назначает триггеры уведомлений для стадии заявки. · коды: 202, 400 · примеры
  ← path: id:int; body: TSTGTSMTMergeData
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
