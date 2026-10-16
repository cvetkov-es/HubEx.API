# TSTG — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса TSTG (API for task life cycle administration in HubEx): сигнатуры, параметры, права. Типы — schemas/TSTG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/TSTG.md`; грабли — `notes/TSTG.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/TSTG`
> Примеры ответов вынесены в [../examples/TSTG.md](../examples/TSTG.md).

**Оглавление**

- Action — строки 20–23
- AssigneeSelectionRules — строки 25–30
- Branches — строки 32–35
- Requirements — строки 37–39
- TaskStageComponents — строки 41–43
- TaskStageLinks — строки 45–51
- TaskStages — строки 53–65

## Action
- `GET /Action` — Возвращает справочник действий по стадиям заявок. · paginated · коды: 200, 204, 206 · примеры
  → map<ActionsResult>
  Поддерживает ограничение результата через заголовок `Range`.

## AssigneeSelectionRules
- `GET /AssigneeSelectionRules` — Возвращает список правил выбора исполнителя. · paginated · коды: 200, 204, 206 · примеры
  → map<RASRListResult>
  Поддерживает ограничение результата через заголовок `Range`.
- `GET /AssigneeSelectionRules/{id}` — Возвращает правило выбора исполнителя по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RASRGetResult

## Branches
- `GET /Branches` — Возвращает список веток жизненного цикла заявок. · paginated · коды: 200, 204, 206 · примеры
  → map<BranchResult>
  Поддерживает ограничение результата через заголовок `Range`.

## Requirements
- `GET /Requirements/requirements` — Возвращает справочник требований тенанта. · коды: 200, 204 · примеры
  → map<RRListResult>

## TaskStageComponents
- `GET /TaskStageComponents/availability` — Возвращает компоненты и их доступность для указанных ролей на указанных стадиях. · коды: 200, 204 · примеры
  ← query: roleID?:int[], taskStageID?:int[], taskTypeID?:int[] → AvailabilityListResult

## TaskStageLinks
- `GET /TaskStageLinks` — Получение списка переходов между стадиями заявок · paginated · коды: 204, 206 · примеры
  ← query: taskTypeID?:int, taskStageFromID?:int, taskStageToID?:int, userID?:int, roleID?:int → RTSLListResult[]
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `GET /TaskStageLinks/overridings` — Получение списка переопределений переходов между стадиями заявок · paginated · коды: 204, 206 · примеры
  ← query: taskTypeID?:int, taskStageFromID?:int, taskStageToID?:int, roleID?:int → OverrideListResult[]
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.

## TaskStages
- `GET /TaskStages` — Возвращает справочник стадий заявок тенанта. · paginated · коды: 200, 204, 206 · примеры
  ← query: triggerID?:int → map<RTSListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `HEAD /TaskStages` — Возвращает количество стадий заявок с автораспределением. · коды: 200 · примеры
  ← query: isAutoAssignmentExists?:bool
- `GET /TaskStages/{id}` — Возвращает стадию заявки по идентификатору. · коды: 200, 204 · примеры
  ← path: id:int → RTSGetResult
- `GET /TaskStages/{id}/messageTriggers` — Возвращает триггеры сообщений для стадии заявки. · коды: 200, 204 · примеры
  ← path: id:int → IdNameResultOfShort[]
- `GET /TaskStages/{id}/requirements` — Возвращает требования для стадии заявки. · paginated · коды: 200, 204, 206 · примеры
  ← path: id:int → TaskStageRequirementResult[]
  Поддерживает ограничение результата через заголовок `Range`.
