# TSTG — справочник ручек

> **Что здесь:** все ручки сервиса TSTG (API for task life cycle administration in HubEx): сигнатуры, параметры, права. Типы — schemas/TSTG.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/TSTG.md`; грабли — `notes/TSTG.md` (если есть).

Base: `{BASE_URL}/TSTG`
> Примеры ответов вынесены в [../examples/TSTG.md](../examples/TSTG.md).

**Оглавление**

- Action — строки 21–24
- AssigneeSelectionRules — строки 26–39
- Branches — строки 41–44
- Requirements — строки 46–48
- TaskStageComponents — строки 50–56
- TaskStageLinks — строки 58–80
- TaskStageMessageTriggers — строки 82–84
- TaskStageRequirements — строки 86–88
- TaskStages — строки 90–114

## Action
- `GET /Action` — Возвращает справочник действий по стадиям заявок. · paginated · коды: 200, 204, 206 · примеры
  → map<ActionsResult>
  Поддерживает ограничение результата через заголовок `Range`.

## AssigneeSelectionRules
- `GET /AssigneeSelectionRules` — Возвращает список правил выбора исполнителя. · paginated · коды: 200, 204, 206 · примеры
  → map<RASRListResult>
  Поддерживает ограничение результата через заголовок `Range`.
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
- `GET /Branches` — Возвращает список веток жизненного цикла заявок. · paginated · коды: 200, 204, 206 · примеры
  → map<BranchResult>
  Поддерживает ограничение результата через заголовок `Range`.

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
- `GET /TaskStageLinks` — Получение списка переходов между стадиями заявок · paginated · коды: 204, 206 · примеры
  ← query: taskTypeID?:int, taskStageFromID?:int, taskStageToID?:int, userID?:int, roleID?:int → RTSLListResult[]
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `POST /TaskStageLinks` — Создание переходов между стадиями заявок · коды: 201, 400 · примеры
  ← body: TSTGTSLAddData[]
- `PUT /TaskStageLinks` — Обновление переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLUpdateData[]
- `DELETE /TaskStageLinks` — Удаление переходов между стадиями заявок · коды: 202, 400 · примеры
  ← body: TSTGTSLDeleteData[]
- `POST /TaskStageLinks/copy` — Копирование переходов стадий заявок из одного типа заявок в другой · коды: 201, 400 · примеры
  ← body: TSTGTSLCopyData[]
- `GET /TaskStageLinks/overridings` — Получение списка переопределений переходов между стадиями заявок · paginated · коды: 204, 206 · примеры
  ← query: taskTypeID?:int, taskStageFromID?:int, taskStageToID?:int, roleID?:int → OverrideListResult[]
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
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
- `GET /TaskStages` — Возвращает справочник стадий заявок тенанта. · paginated · коды: 200, 204, 206 · примеры
  ← query: triggerID?:int → map<RTSListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
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
- `GET /TaskStages/{id}/requirements` — Возвращает требования для стадии заявки. · paginated · коды: 200, 204, 206 · примеры
  ← path: id:int → TaskStageRequirementResult[]
  Поддерживает ограничение результата через заголовок `Range`.
