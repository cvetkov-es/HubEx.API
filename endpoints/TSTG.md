# TSTG — справочник ручек

> **Что здесь:** все ручки сервиса TSTG (API for task life cycle administration in HubEx): сигнатуры, параметры, права. Типы — schemas/TSTG.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/TSTG.md`; грабли — `notes/TSTG.md` (если есть).
> **Источник:** `snapshots/TSTG.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/TSTG`

## Action
- `GET /Action` — Метод получения списка  действий · права: ActionList · paginated
  → map<ActionResult>

## AssigneeSelectionRules
- `GET /AssigneeSelectionRules` — Возвращает список правил выбора исполнителя · права: AssigneeSelectionRuleList · paginated
  → map<AssigneeSelectionRule.ListResult>
- `POST /AssigneeSelectionRules` — Создает  правило выбора исполнителя · права: AssigneeSelectionRuleAdd
  ← body: AssigneeSelectionRule.AddData[] → int[]
- `PUT /AssigneeSelectionRules` — Изменяет правила выбора исполнителя · права: AssigneeSelectionRuleUpdate
  ← body: AssigneeSelectionRule.UpdateData[]
- `DELETE /AssigneeSelectionRules` — Помечает правила выбора исполнителя как удаленные · права: AssigneeSelectionRuleDelete
  ← body: int[]
- `GET /AssigneeSelectionRules/{id}` — Возвращает правило выбора исполнителя · права: AssigneeSelectionRuleGet
  ← path: id:int → AssigneeSelectionRule.GetResult
- `DELETE /AssigneeSelectionRules/{id}` — Помечает правило выбора исполнителя как удаленное · права: AssigneeSelectionRuleDelete
  ← path: id:int

## Branches
- `GET /Branches` — Возвращает список веток · права: BranchesList · paginated
  → map<BranchResult>

## Requirements
- `GET /Requirements/requirements` — Возвращает требования · права: RequirementList
  → Requirements.ListResult[]

## TaskStageComponents
- `POST /TaskStageComponents` — Добавляет или изменяет доступность компонента для указанных ролей на указанных стадиях · права: ComponentsAvailabilityMerge
  ← body: TaskStageComponent.MergeData[]
- `GET /TaskStageComponents/availability` — Возвращает компонент и его доступность для указанных ролей на указанных стадиях · права: ComponentsAvailabilityList
  ← query: roleID?:int[], taskStageID?:int[], taskTypeID?:int[] → AvailabilityListResult
- `POST /TaskStageComponents/templates` — Заполняет стадию заявки компонентами из TaskViewTemplate · права: ComponentsAvailabilityMerge
  ← body: TemplateMergeData[]

## TaskStageLinks
- `GET /TaskStageLinks` — Получение списка переходов между стадиями заявок · права: TaskStageLinkList · paginated
  ← query: taskTypeID?:any, taskStageFromID?:any, taskStageToID?:any, userID?:any, roleID?:any → TaskStageLinks.ListResult[]
  ## Пример запроса:
`GET /TaskStageLinks?taskTypeID=1&taskStageFromID=2&userID=500&roleID=101`
            
## Пример успешного ответа (200):
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
- `POST /TaskStageLinks` — Создание переходов между стадиями заявок · права: TaskStageLinkAdd
  ← body: TaskStageLink.AddData[] → int[]
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
    "permissionUiID": 10,
    "isPositiveResult": true,
    "timeoutSeconds": null,
    "timeoutToDeadlineSeconds": null,
    "roles": [101]
  }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkAdd`.
- `PUT /TaskStageLinks` — Обновление переходов между стадиями заявок · права: TaskStageLinkUpdate
  ← body: TaskStageLink.UpdateData[]
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
    "permissionUiID": 10,
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
- `DELETE /TaskStageLinks` — Удаление переходов между стадиями заявок · права: TaskStageLinkDelete
  ← body: TaskStageLink.DeleteData[]
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
- `POST /TaskStageLinks/copy` — Копирование переходов стадий заявок из одного типа заявок в другой · права: TaskStageLinkAdd
  ← body: TaskStageLink.CopyData[]
  ## Пример запроса:
`POST /TaskStageLinks/copy`
            
```json
[
  { "sourceTaskTypeID": 1, "targetTaskTypeID": 2 }
]
```
## Негативные сценарии:
- 400 BadRequest: некорректный формат данных копирования.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskStageLinkAdd`.
- `GET /TaskStageLinks/overridings` — Возвращает список переопределений переходов для стадий заявки · права: TaskStageLinkOverrideList · paginated
  ← query: taskTypeID?:any, taskStageFromID?:any, taskStageToID?:any → OverrideListResult[]
- `POST /TaskStageLinks/overridings` — Создает переходы стадий заявок · права: TaskStageLinkOverrideAdd
  ← body: TaskStageLinkOverride.AddData[] → int[]
- `PUT /TaskStageLinks/overridings` — Изменяет переходы стадий заявок · права: TaskStageLinkOverrideUpdate
  ← body: TaskStageLinkOverride.UpdateData[]
- `DELETE /TaskStageLinks/overridings` — Помечает переходы стадий заявок, как удаленные · права: TaskStageLinkOverrideDelete
  ← body: TaskStageLinkOverride.DeleteData[]
- `POST /TaskStageLinks/reorder` — Сохранение порядка сортировки переходов между стадиями заявок · права: TaskStageLinkReorder
  ← body: SortData[] → int[]
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
- `POST /TaskStageMessageTriggers` — Добавляет или изменяет стадии заявок для триггеров · права: TriggerTaskStageMerge
  ← body: TriggerTaskStage.MergeData[]

## TaskStageRequirements
- `POST /TaskStageRequirements` — Добавляет или изменяет требования на указанных стадиях · права: TaskStageRequirementMerge
  ← body: TaskStageRequirement.MergeData[]

## TaskStages
- `GET /TaskStages` — Возвращает справочник существующихъ в тенанте стадий заявок. Ключ - идентификаторъ стадии. · права: TaskStagesList · paginated
  ← query: triggerID?:any → TaskStages.ListResult[]
- `POST /TaskStages` — Создает стадии заявок · права: TaskStageAdd
  ← body: TaskStage.AddData[] → int[]
- `PUT /TaskStages` — Изменяет стадии заявок · права: TaskStageUpdate
  ← body: TaskStage.UpdateData[]
- `DELETE /TaskStages` — Помечает стадии заявок, как удаленные · права: TaskStageDelete
  ← body: int[]
- `HEAD /TaskStages` — Возвращает список стадий заявки с автораспределением · права: TaskStageAutoAssignmentList
  ← query: isAutoAssignmentExists?:bool
- `POST /TaskStages/copy` — Копирует стадии заявок · права: TaskStageAdd
  ← body: TaskStage.CopyData[] → int[]
- `GET /TaskStages/{id}` — Возвращает стадию заявки · права: TaskStageGet
  ← path: id:int → TaskStages.GetResult
- `DELETE /TaskStages/{id}` — Помечает стадию заявки как удаленную · права: TaskStageDelete
  ← path: id:int
- `POST /TaskStages/{id}/assign` — Добавляет или изменяет триггеры уведомлений для указанной стадии · права: TaskStageMessageTriggerAssign
  ← path: id:int; body: TaskStageMessageTrigger.MergeData
- `GET /TaskStages/{id}/messageTriggers` — Возвращает триггеры сообщений · права: TaskStageGet
  ← path: id:int → IdNameResult<Int16>[]
- `GET /TaskStages/{id}/requirements` — Возвращает требования для стадии заявки · права: TaskStageRequirementGet · paginated
  ← path: id:int → TaskStageRequirementResult
