# TSTG — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса TSTG (API for task life cycle administration in HubEx): сигнатуры, параметры, права. Типы — schemas/TSTG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/TSTG.md`; грабли — `notes/TSTG.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/TSTG`
> Примеры ответов вынесены в [../examples/TSTG.md](../examples/TSTG.md).

**Оглавление**

- Action — строки 20–22
- AssigneeSelectionRules — строки 24–28
- Branches — строки 30–32
- Requirements — строки 34–36
- TaskStageComponents — строки 38–40
- TaskStageLinks — строки 42–46
- TaskStages — строки 48–58

## Action
- `GET /Action` — Метод получения списка  действий · права: ActionList · paginated · коды: 200, 206
  → map<ActionResult>

## AssigneeSelectionRules
- `GET /AssigneeSelectionRules` — Возвращает список правил выбора исполнителя · права: AssigneeSelectionRuleList · paginated · коды: 200, 206
  → map<AssigneeSelectionRule.ListResult>
- `GET /AssigneeSelectionRules/{id}` — Возвращает правило выбора исполнителя · права: AssigneeSelectionRuleGet · коды: 200
  ← path: id:int → AssigneeSelectionRule.GetResult

## Branches
- `GET /Branches` — Возвращает список веток · права: BranchesList · paginated · коды: 200, 206
  → map<BranchResult>

## Requirements
- `GET /Requirements/requirements` — Возвращает требования · права: RequirementList · коды: 200
  → Requirements.ListResult[]

## TaskStageComponents
- `GET /TaskStageComponents/availability` — Возвращает компонент и его доступность для указанных ролей на указанных стадиях · права: ComponentsAvailabilityList · коды: 200
  ← query: roleID?:int[], taskStageID?:int[], taskTypeID?:int[] → AvailabilityListResult

## TaskStageLinks
- `GET /TaskStageLinks` — Получение списка переходов между стадиями заявок · права: TaskStageLinkList · paginated · коды: 200, 204, 206 · примеры
  ← query: taskTypeID?:any, taskStageFromID?:any, taskStageToID?:any, userID?:any, roleID?:any → TaskStageLinks.ListResult[]
- `GET /TaskStageLinks/overridings` — Возвращает список переопределений переходов для стадий заявки · права: TaskStageLinkOverrideList · paginated · коды: 200, 206
  ← query: taskTypeID?:any, taskStageFromID?:any, taskStageToID?:any → OverrideListResult[]

## TaskStages
- `GET /TaskStages` — Возвращает справочник существующихъ в тенанте стадий заявок. Ключ - идентификаторъ стадии. · права: TaskStagesList · paginated · коды: 200, 206
  ← query: triggerID?:any → TaskStages.ListResult[]
- `HEAD /TaskStages` — Возвращает список стадий заявки с автораспределением · права: TaskStageAutoAssignmentList · коды: 200
  ← query: isAutoAssignmentExists?:bool
- `GET /TaskStages/{id}` — Возвращает стадию заявки · права: TaskStageGet · коды: 200
  ← path: id:int → TaskStages.GetResult
- `GET /TaskStages/{id}/messageTriggers` — Возвращает триггеры сообщений · права: TaskStageGet · коды: 200
  ← path: id:int → IdNameResult<Int16>[]
- `GET /TaskStages/{id}/requirements` — Возвращает требования для стадии заявки · права: TaskStageRequirementGet · paginated · коды: 200, 206
  ← path: id:int → TaskStageRequirementResult
