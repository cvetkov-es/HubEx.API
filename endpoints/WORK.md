# WORK — справочник ручек

> **Что здесь:** все ручки сервиса WORK (API for managing tasks and works in HubEx): сигнатуры, параметры, права. Типы — schemas/WORK.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WORK.md`; грабли — `notes/WORK.md` (если есть).
> **Источник:** `snapshots/WORK.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/WORK`

## CheckListItems
- `POST /CheckListItems` — Изменяет элементы чек-листов · права: CheckListItemMerge
  ← body: CheckListItem.MergeData[]
- `DELETE /CheckListItems` — Помечает результат чек-листа по заявке как удаленный · права: CheckListItemDelete
  ← body: CheckListItem.DeleteData[]

## CheckLists
- `GET /CheckLists` — Возвращает список активных чек-листов · права: CheckListsList · paginated
  ← query: searchText?:str, assetID?:any, workTypeID?:any, isAssignedToAsset?:enum(true, false), isAssignedToWorkType?:enum(true, false), searchText?:str → map<CheckLists.ListResult>
- `POST /CheckLists` — Создает чек-листы · права: CheckListAdd
  ← body: CheckList.AddData[] → int[]
- `PUT /CheckLists` — Изменяет чек-листы · права: CheckListUpdate
  ← body: CheckList.UpdateData[]
- `DELETE /CheckLists` — Помечает чек-листы, как удаленные · права: CheckListDelete
  ← body: int[]
- `POST /CheckLists/{checkListID}/assign` — Проставляпет идентификаторы чек-листов в таблицах объектов и видов работ · права: CheckListAssign · paginated
  ← path: checkListID:int; body: CheckListAssignmentData
- `DELETE /CheckLists/{checkListID}/assign` — Удаляет идентификаторы чек-листов из таблиц объектов и видов работ · права: CheckListUnassign · paginated
  ← path: checkListID:int; body: CheckListAssignmentData
- `GET /CheckLists/{checkListID}/items` — Возвращает элементы чек-листа · права: CheckListItemsList · paginated
  ← path: checkListID:int → map<CheckListItemResult>
- `GET /CheckLists/{id}` — Возвращает чек-лист · права: CheckListGet
  ← path: id:int → map<CheckLists.GetResult>
- `DELETE /CheckLists/{id}` — Помечает чек-лист, как удаленный · права: CheckListDelete
  ← path: id:int

## CompletedWorkAttachments
- `POST /CompletedWorkAttachments` — Добавляет загруженный ранее вложенный файл к выполненной работе · права: CompletedWorkAttachmentAdd
  ← body: Common.TaskActionData<CompletedWorkAttachment.AddData>[] → CompletedWorkAttachments.AddResult[]
- `DELETE /CompletedWorkAttachments` — Помечает прикрепленный к выполненной работе файл как удаленный · права: CompletedWorkAttachmentDelete
  ← body: TaskActionData<DeleteData>[]
- `POST /CompletedWorkAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из тела запроса. · права: CompletedWorkAttachmentUpload
  ← body: CompletedWorkBodyUploadData → CompletedWorkAttachments.UploadResult
- `POST /CompletedWorkAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из формы. · права: CompletedWorkAttachmentUpload
  ← query: TaskID?:int, CompletedWorkID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → CompletedWorkAttachments.UploadResult

## CompletedWorks
- `POST /CompletedWorks` — Создаёт выполненные работы по одной или нескольким заявкам · права: CompletedWorkAdd
  ← body: Common.TaskActionData<CompletedWork.AddData>[] → CompletedWorks.AddResult[]
  ## Пример запроса:
`POST /CompletedWorks`
            
Заголовки (опционально):
- `X-Concurrency-Stamp` (Guid) — идемпотентность; повтор с тем же значением даёт конфликт.
- `X-Suppress-Conflict: true` — при конфликте вернуть `200 OK` вместо `409 Conflict`.
            
```json
[
  {
    "taskID": 12345,
    "data": [
      {
        "workTypeID": 10,
        "maintainedAssetID": 500,
        "implementedByUserID": 1001,
        "started": "2026-05-15T08:00:00Z",
        "finished": "2026-05-15T10:30:00Z",
        "notes": "Замена фильтра",
        "quantity": 1.0,
        "measurementUnitID": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "taskID": 12345,
    "id": 1,
    "concurrencyStamp": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
  }
]
```
            
В заголовке ответа `X-Last-Lsn` возвращается метка изменений для синхронизации клиента.
            
## Негативные сценарии:
- 400 BadRequest: заголовок `X-Concurrency-Stamp` передан, но пустой, длиннее 255 символов или не является Guid.
- 409 Conflict: повтор запроса с тем же `X-Concurrency-Stamp`.
- 200 OK: конфликт идемпотентности при заголовке `X-Suppress-Conflict: true`.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompletedWorkAdd`.
- `PUT /CompletedWorks` — Изменяет выполненные работы по заявкам · права: CompletedWorkUpdate
  ← body: Common.TaskActionData<CompletedWork.UpdateData>[]
  ## Пример запроса:
`PUT /CompletedWorks`
            
```json
[
  {
    "taskID": 12345,
    "data": [
      {
        "id": 1,
        "workTypeID": 10,
        "maintainedAssetID": 500,
        "started": "2026-05-15T08:00:00Z",
        "finished": "2026-05-15T11:00:00Z",
        "notes": "Обновлённые примечания",
        "quantity": 2.0,
        "measurementUnitID": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа пустое. В заголовке `X-Last-Lsn` — метка изменений.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompletedWorkUpdate`.
- `DELETE /CompletedWorks` — Помечает выполненные работы по заявкам как удалённые · права: CompletedWorkDelete
  ← body: TaskActionData<Int16>[]
  ## Пример запроса:
`DELETE /CompletedWorks`
            
```json
[
  {
    "taskID": 12345,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа пустое. В заголовке `X-Last-Lsn` — метка изменений.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompletedWorkDelete`.

## RequestMethods
- `GET /RequestMethods` — Возвращает список методов подачи заявок. · права: RequestMethodsList · paginated
  → map<RequestMethods.ListResult>

## TaskActualities
- `GET /TaskActualities` — Возвращает список актуальностей заявок · права: TaskActualitiesList · paginated
  → map<TaskActualities.ListResult>
- `POST /TaskActualities` — Создает актуальности заявки · права: TaskActualityAdd
  ← body: TaskActuality.AddData[] → int[]
- `PUT /TaskActualities` — Изменяет актуальности заявок · права: TaskActualityUpdate
  ← body: TaskActuality.UpdateData[]
- `DELETE /TaskActualities` — Помечает актуальности заявок, как удаленные · права: TaskActualityDelete
  ← body: int[]
- `GET /TaskActualities/{id}` — Возвращает актуальность заявки · права: TaskActualityGet
  ← path: id:int → TaskActualities.ListResult
- `DELETE /TaskActualities/{id}` — Помечает актуальность заявки как удаленную · права: TaskActualityDelete
  ← path: id:int

## TaskAssignmentHistory
- `POST /TaskAssignmentHistory` — Назначает новые заявки на пользователя. · права: TaskAssignmentHistoryAdd
  ← body: TaskAssignmentHistory.PostData[] → TaskAssignmentHistory.AddResult[]

## TaskAttachments
- `POST /TaskAttachments` — Свзяывает заявку и вложение · права: TaskAttachmentAdd
  ← body: TaskActionData<Int32>[] → TaskAttachments.PostResult[]
- `DELETE /TaskAttachments` — Помечает связку заявки и вложения как удаленную · права: TaskAttachmentDelete
  ← body: TaskActionData<Int32>[]
- `POST /TaskAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к заявке. Данные будут получены из тела запроса. · права: TaskAttachmentUpload
  ← body: TaskBodyUploadData → TaskAttachments.UploadResult
- `POST /TaskAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к заявке. Данные будут получены из формы. · права: TaskAttachmentUpload
  ← query: TaskID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → TaskAttachments.UploadResult

## TaskAttributes
- `GET /TaskAttributes` — Возвращает значения атрибутов по заявкам · права: TaskAttributeGet · paginated
  ← query: taskID?:any, attributeID?:any → TaskAttributesResult[]
- `POST /TaskAttributes` — Изменяет значения атрибутов по заявкам · права: TaskAttributeMerge
  ← body: ActionData[]

## TaskContacts
- `POST /TaskContacts` — Добавляет контактные лица к заявке · права: TaskContactAdd
  ← body: TaskActionData<Int32>[] → TaskContacts.PostResult
- `DELETE /TaskContacts` — Удаляет контактные лица у заявки · права: TaskContactDelete
  ← body: TaskActionData<Int32>[]

## TaskConversationDeliveries
- `PUT /TaskConversationDeliveries/read` — Устанавливает отметки о прочтении сообщений по заявкам · права: TaskConversationDeliveryUpdate
  ← body: TaskActionData<SetReadData>[]
- `PUT /TaskConversationDeliveries/read/All` — Устанавливает отметки о прочтении всех сообщений по заявкам · права: TaskConversationDeliveryUpdate

## TaskConversations
- `GET /TaskConversations` — Возвращает список сообщений по заявкам, доступным пользователю.
<param name="searchText">Текст для поиска в сообщениях по заявкам</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: TaskConversationsList · paginated
  ← query: searchText?:str, thumbnailSize?:int, isRead?:enum(true, false) → TaskMessageLast[]
- `DELETE /TaskConversations` — Помечает сообщения по заявкам как удаленные. · права: TaskConversationDelete
  ← body: TaskConversation.DeleteData[]
- `HEAD /TaskConversations` — Возвращает заголовок списка сообщений по заявке (для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="searchText">Текст для поиска в сообщениях по заявкам</param> · права: TaskConversationsList
- `DELETE /TaskConversations/remove` — Помечает сообщения по заявкам как удаленные. · права: TaskConversationRemove
  ← body: TaskConversation.DeleteData[]

## TaskFilter
- `GET /TaskFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · права: TasksList
  ← query: selectedOnly?:bool, selectedOnly?:enum(true, false) → FilterListItemProjection[]
- `PUT /TaskFilter` — Обновляет список доступных, для выполняющего операцию пользователя, фильтров и порядок их сортировки · права: TasksList
  ← body: FilterData[]

## TaskListQueries
- `GET /TaskListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · права: TaskListQueryListAll · paginated
  → map<TaskListQueryResult>
- `POST /TaskListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю · права: TaskListQueryAdd · paginated
  ← body: TaskListQuery.AddData[] → int[]
- `PUT /TaskListQueries` — Изменяет сохраненный запрос · права: TaskListQueryUpdate · paginated
  ← body: TaskListQuery.UpdateData[]
- `DELETE /TaskListQueries` — Помечает сохраненные запрос как даленный · права: TaskListQueryDelete · paginated
  ← body: int[]
- `DELETE /TaskListQueries/remove` — Помечает сохраненные запрос как даленный · права: TaskListQueryRemove · paginated
  ← body: int[]
- `GET /TaskListQueries/{id}` — Возвращает сохраненный запрос · права: TaskListQueryGet
  ← path: id:int → map<TaskListQueryResult>
- `DELETE /TaskListQueries/{id}` — Помечает сохраненный запрос как даленный · права: TaskListQueryDelete · paginated
  ← path: id:int
- `DELETE /TaskListQueries/{id}/remove` — Помечает сохраненный запрос как даленный · права: TaskListQueryRemove · paginated
  ← path: id:int

## TaskMaterials
- `POST /TaskMaterials` — Добавляет, изменяет необходимые материалы к заявкам · права: TaskMaterialAdd
  ← body: TaskActionData<MergeData>[] → TaskMaterials.PostResult
- `PUT /TaskMaterials` — Изменяет необходимые материалы в заявках · права: TaskMaterialUpdate
  ← body: Common.TaskActionData<TaskMaterial.UpdateData>[]
- `DELETE /TaskMaterials` — Удаляет необходимые материалы из заявок · права: TaskMaterialDelete
  ← body: TaskActionData<Int16>[]
- `PUT /TaskMaterials/takeOff` — Убирает признак взятия необходимых материалов из заявок · права: TaskMaterialTakeOff
  ← body: TaskActionData<Int16>[]
- `PUT /TaskMaterials/takeOn` — Проставляет признак взятия необходимых материалов из заявок · права: TaskMaterialTakeOn
  ← body: TaskActionData<TakeOnData>[]

## TaskOrderBy
- `GET /TaskOrderBy` — Возвращает список методов сортировки заявок · права: TaskOrderByList · paginated
  → map<TaskOrderBy.ListResult>

## TaskRatings
- `POST /TaskRatings` — Создает оценки по заявкам · права: TaskTechnicianRatingMerge
  ← body: TaskTechnicianRating.MergeData[]

## TaskSkills
- `POST /TaskSkills` — Добавляет навыки к заявкам · права: TaskSkillAdd
  ← body: TaskActionData<Int32>[] → TaskSkills.PostResult
- `DELETE /TaskSkills` — Удаялет навыки из заявок · права: TaskSkillDelete
  ← body: TaskActionData<Int32>[]

## TaskStagingHistory
- `POST /TaskStagingHistory` — Добавляет актуальную запись в историю прохождения заявки по стадиям. · права: TaskStagingHistoryAdd
  ← body: TaskStagingHistory.PostData
- `POST /TaskStagingHistory/batch` — Массовый перевод заявок по стадиям. · права: TaskStagingHistoryAdd
  ← body: BatchRequestPostData
- `POST /TaskStagingHistory/multiple` — Массовый перевод заявок по стадиям. · права: TaskStagingHistoryAdd
  ← body: TaskStagingHistory.PostData[]

## TaskStatuses
- `GET /TaskStatuses` — Возвращает список статусов заявок · права: TaskStatusesList · paginated
  → map<TaskStatuses.ListResult>
- `POST /TaskStatuses` — Создает статус заявки · права: TaskStatusAdd
  ← body: TaskStatus.AddData[] → int[]
- `PUT /TaskStatuses` — Изменяет статусы заявок · права: TaskStatusUpdate
  ← body: TaskStatus.UpdateData[]
- `DELETE /TaskStatuses` — Помечает статусы заявок, как удаленные · права: TaskStatusDelete
  ← body: int[]
- `GET /TaskStatuses/{id}` — Возвращает статус заявки · права: TaskStatusGet
  ← path: id:int → TaskStatuses.ListResult
- `DELETE /TaskStatuses/{id}` — Помечает статус заявки как удаленный · права: TaskStatusDelete
  ← path: id:int

## TaskTags
- `POST /TaskTags` — Привязывает тэг к заявке. Если указанный тэг отсутствует в справочнике, создает его. · права: TaskTagAdd
  ← body: TaskTag.AddData[]
- `DELETE /TaskTags` — Исключает тэг из заявки. В справочнике тэг остается. · права: TaskTagRemove
  ← body: TaskTag.DeleteData[]

## TaskTemplateExcludedAssets
- `POST /TaskTemplateExcludedAssets` — Добавляет или изменяет исключенные объекты к плановой заявке · права: TaskTemplateExcludedAssetMerge
  ← body: TaskTemplateActionData<Int32>[] → TaskTemplateExcludedAssetMergeResult
- `DELETE /TaskTemplateExcludedAssets` — Удаляет исключенные объекты у плановой заявки · права: TaskTemplateExcludedAssetDelete
  ← body: TaskTemplateActionData<Int32>[]

## TaskTemplates
- `GET /TaskTemplates` — Возвращает список шаблонов заявок. · права: TaskTemlatesList · paginated
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, assetTypeID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isAllowForMailboxSender?:enum(true, false), isScheduled?:enum(true, false), isScheduleActive?:enum(true, false), taskTemplateID?:str → map<TaskTemplates.ListResult>
- `POST /TaskTemplates` — Создает шаблоны заявок. · права: TaskTemplateAdd
  ← body: TaskTemplate.AddData[] → str[]
- `PUT /TaskTemplates` — Обновляет шаблоны заявок. · права: TaskTemplateUpdate
  ← body: TaskTemplate.UpdateData[]
- `DELETE /TaskTemplates` — Помечает шаблоны заявок, как удаленные. · права: TaskTemplateDelete
  ← body: str[]
- `HEAD /TaskTemplates` — Возвращает заголовок списка шаблонов заявок. · права: TaskTemlatesList
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isAllowForMailboxSender?:enum(true, false), isScheduled?:enum(true, false), isScheduleActive?:enum(true, false), startWithAssetID?:any
- `GET /TaskTemplates/download` — Возвращает архив qr-кодов в формате svg в соответствии с заданными фильтрами · права: TaskTemlatesList · paginated
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isScheduled?:enum(true, false), isScheduleActive?:enum(true, false)
- `GET /TaskTemplates/{id}` — Возвращает шаблон заявки · права: TaskTemplateGet
  ← path: id:str → TaskTemplates.GetResult
- `GET /TaskTemplates/{id}/assignment` — Возвращает список исполнителей, связанных с шаблоном
  ← path: id:str → TaskTemplateAssignmentDetailsProjection
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /TaskTemplates/{id}/assignment` — Связывает исполнителей с шаблоном. · права: TaskTemplateUpdate
  ← path: id:str; body: int[] → TaskTemplateAssignmentMergeProjection[]
- `GET /TaskTemplates/{id}/download` — Возвращает шаблон заявки · права: TaskTemplateGet
  ← path: id:str
- `GET /TaskTemplates/{id}/public` — Возвращает публичный шаблон заявки по идентификатору, который вычисляется как sha256(QrCode)
  ← path: id:str → GetPublicResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `PUT /TaskTemplates/{id}/publish` — Публикует шаблон заявок. · права: TaskTemplatePublish
  ← path: id:str
- `GET /TaskTemplates/{id}/schedules` — Получить список сгенерированных событий шаблоной зявки · права: TaskTemplateScheduleList · paginated
  ← path: id:str → GetSchedulesResult[]
- `POST /TaskTemplates/{id}/schedules` — Добавить / удалить шаблонные заявки для расписания · права: TaskTemplateScheduleMerge
  ← path: id:str; body: int[]
- `PUT /TaskTemplates/{id}/unpublish` — Отменяет публикацию шаблона заявок · права: TaskTemplateUnpublish
  ← path: id:str
- `DELETE /TaskTemplates/{taskTemplateID}/excludedAssets/{assetID}` — Удаляет исключенный объект у плановой заявки · права: TaskTemplateExcludedAssetDelete
  ← path: taskTemplateID:str, assetID:int
- `PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/activate` — Активация раписания · права: TaskTemplateScheduleChangeState
  ← path: taskTemplateID:str, scheduleID:int
- `POST /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/appointments` — Регенерация событий для раписания · права: ScheduleAppointmentMerge
  ← path: taskTemplateID:str, scheduleID:int
- `PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/deactivate` — Деактивация раписания · права: TaskTemplateScheduleChangeState
  ← path: taskTemplateID:str, scheduleID:int
- `GET /TaskTemplates/{tasktTemplateID}/excludedAssets` — Возвращает список исключенных объектов для плановой заявки · права: TaskTemplateExcludedAssetList · paginated
  ← path: tasktTemplateID:str → map<TaskTemplateExcludedAssetResult>

## TaskTypeDistrict
- `PUT /TaskTypeDistrict` — Изменение привязки типов заявки к участкам · права: TaskTypeDistrictMerge
  ← body: TaskTypeDistrict.MergeData[]

## TaskTypeRoutes
- `POST /TaskTypeRoutes` — Создает маршруты типов заявок · права: TaskTypeRouteAdd
  ← body: TaskStageRoute.AddData[] → int[]
- `PUT /TaskTypeRoutes` — Изменяет маршрут типов заявок · права: TaskTypeRouteUpdate
  ← body: TaskStageRoute.UpdateData[]
- `DELETE /TaskTypeRoutes` — Удаляет маршруты типов заявок · права: TaskTypeRouteDelete
  ← body: int[]
- `DELETE /TaskTypeRoutes/{id}` — Удаляет маршрут типа заявки · права: TaskTypeRouteDelete
  ← path: id:int

## TaskTypes
- `GET /TaskTypes` — Возвращает список типов заявок, доступных пользователю. Доступность определяется привязкой пользователя к участкам. · права: TaskTypesList · paginated
  ← query: companyID?:any, districtID?:any, assetID?:any, workTypeID?:any → map<TaskTypes.ListResult>
- `POST /TaskTypes` — Создает тип заявки · права: TaskTypeAdd
  ← query: relatedToAnyWorkType?:bool, relatedToAnyWorkType?:enum(true, false); body: TaskType.AddData[] → int[]
- `PUT /TaskTypes` — Изменяет типы заявок · права: TaskTypeUpdate
  ← body: TaskType.UpdateData[]
- `DELETE /TaskTypes` — Помечает типы заявок, как удаленные · права: TaskTypeDelete
  ← body: int[]
- `GET /TaskTypes/{id}` — Возвращает тип заявки · права: TaskTypeGet
  ← path: id:int → TaskTypes.ListResult
- `DELETE /TaskTypes/{id}` — Помечает тип заявки как удаленный · права: TaskTypeDelete
  ← path: id:int
- `GET /TaskTypes/{id}/districts` — Метод получения участков для вида работ · права: TaskTypeDistrictList · paginated
  ← path: id:int
- `GET /TaskTypes/{id}/workTypes` — Возвращает список относящихся к типу задачи видов работ · права: TaskTypesList · paginated
  ← path: id:int
- `POST /TaskTypes/{id}/workTypes` — Привязать список видов работ к типу задачи · права: TaskTypeUpdate
  ← path: id:int; body: int[]
- `DELETE /TaskTypes/{id}/workTypes` — Удалить привязку видов работ к типу задачи · права: TaskTypeUpdate
  ← path: id:int; body: int[]
- `GET /TaskTypes/{taskTypeID}/route` — Возвращает маршрут типа заявки · права: TaskTypeRouteGet
  ← path: taskTypeID:int → RouteResult

## TaskWatchLists
- `POST /TaskWatchLists` — добавляет пользователей в watchlist по заявкам · права: TaskWatchListAdd
  ← body: TaskActionData<Int32>[] → TaskWatchLists.AddResult[]
- `DELETE /TaskWatchLists` — Исключает пользователей из watchlist'а по заявкам · права: TaskWatchListDelete
  ← body: TaskActionData<Int32>[]

## Tasks
- `GET /Tasks` — Возвращает список заявок, доступных пользователю. · права: TasksList · paginated
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), topLevelTasksForHierarchy?:enum(true, false), assetTypeID?:any, assetClassID?:any, districtID?:any, assetResponsibleUserID?:any, branchID?:any, erpID?:str, parentID?:any, assetSchemaID?:any, attributeValues?:str, lastModifiedFrom?:any, lastModifiedTill?:any, contactID?:any, payeeCompanyID?:any → map<Tasks.ListResult>
- `POST /Tasks` — Создаёт заявку · права: TaskAdd
  ← body: Task.AddData → Auxiliary.IdResult<System.Int32>
  ## Пример запроса:
`POST /Tasks`
            
Заголовки (опционально):
- `X-Concurrency-Stamp` (Guid) — идемпотентность; повтор с тем же значением даёт конфликт.
            
```json
{
  "assetID": 500,
  "workTypeID": 10,
  "criticalityID": 1,
  "notes": "Неисправность оборудования",
  "requestedStartDateTime": "2026-05-15T08:00:00Z",
  "requestedFinishDateTime": "2026-05-15T12:00:00Z"
}
```
            
## Пример успешного ответа (201):
```json
{
  "id": 12345,
  "number": "T-12345",
  "concurrencyStamp": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
}
```
            
В заголовке ответа `X-Last-Lsn` возвращается метка изменений для синхронизации клиента.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или заголовок `X-Concurrency-Stamp` передан, но пустой, длиннее 255 символов или не является Guid.
- 409 Conflict: повтор запроса с тем же `X-Concurrency-Stamp`.
- 422 UnprocessableEntity: замечания санитайзера текста/HTML в теле заявки.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskAdd`.
- `DELETE /Tasks` — Помечает заявку как удаленную · права: TaskDelete
  ← body: int[]
- `HEAD /Tasks` — Возвращает заголовок списка заявок для получения количества заявок, удовлетворяющих фильтру. · права: TasksList
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), assetTypeID?:any, assetClassID?:any, erpID?:str, parentID?:any, branchID?:any, assetSchemaID?:any, contactID?:any
- `GET /Tasks/changeTypes` — Возвращает список поддерживаемых в логировании разделов (Tab) и секций этих разделов (Sections) · права: TaskGet
  → ChangeTypeResult[]
- `PUT /Tasks/completedWorks/attributes` — Устанавливает результаты для доп.полей по выполненной работе по заявкам · права: CompletedWorkAttributeMerge
  ← body: ActionData<AttributeData>[]
- `DELETE /Tasks/completedWorks/attributes` — Помечает атрибуты выполенной работы заявки удаленные · права: CompletedWorkAttributeDelete
  ← body: ActionData<Int16>[]
- `POST /Tasks/completedWorks/materials` — Добавляет израсходованные материалы к выполненной работе для заявки · права: CompletedWorkMaterialAdd
  ← body: TaskActionData<CompletedWorkMaterialData<Material>>[] → CompletedWorkMaterialPost[]
- `PUT /Tasks/completedWorks/materials` — Изменяет израсходованные материалы у выполненной работы для заявки · права: CompletedWorkMaterialUpdate
  ← body: TaskActionData<CompletedWorkMaterialData<Material>>[]
- `DELETE /Tasks/completedWorks/materials` — Удаляет материалы у выполненных работ по заявке · права: CompletedWorkMaterialDelete
  ← body: TaskActionData<CompletedWorkMaterialData<MaterialDelete>>[]
- `POST /Tasks/completedWorks/report/attachment/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из тела запроса. · права: CompletedWorkReportAttachmentUpload
  ← body: CompletedWorkReportBodyUploadData → CompletedWorkReportAttachment.UploadResult
- `POST /Tasks/completedWorks/report/attachment/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из формы. · права: CompletedWorkReportAttachmentUpload
  ← query: TaskID?:int, JobTitle?:str, Signatory?:str, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → CompletedWorkReportAttachment.UploadResult
- `POST /Tasks/completedWorks/technicians` — Добавляет исполнителей к выполненным работам по заявке · права: CompletedWorkTechnicianAdd
  ← body: TaskActionData<CompletedWorkTechnicianData<Technician>>[] → CompletedWorkTechnicianPost[]
- `PUT /Tasks/completedWorks/technicians` — Изменяет исполнителей у выполненных работы по заявке · права: CompletedWorkTechnicianUpdate
  ← body: TaskActionData<CompletedWorkTechnicianData<Technician>>[]
- `DELETE /Tasks/completedWorks/technicians` — Удаляет исполнителей у выполненных работ по заявке · права: CompletedWorkMaterialDelete
  ← body: TaskActionData<CompletedWorkTechnicianData<Int32>>[]
- `GET /Tasks/count` — Возвращает количество заявок по дням · права: TasksList
  ← query: dateFrom?:datetime, dateTill?:datetime, searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), assetTypeID?:any, assetClassID?:any, districtID?:any, assetResponsibleUserID?:any, branchID?:any, erpID?:str, parentID?:any → map<ListCountResult>
- `GET /Tasks/groupBy/geoHash` — Возвращает краткий список заявок, сгрупированных по хэш-коду геоообласти (кластеризация) · права: TasksList
  ← query: searchText?:str, zoomLevel?:float, disableClustering?:bool, clusteringMode?:ClusteringMode, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, taskTemplateID?:str, requestMethodID?:any, disableClustering?:enum(true, false), clusteringMode?:any → TaskGroupByResult<ClusterResult>[]
- `GET /Tasks/new/meta` — Возвращает метаданные для формы заявки. · права: TaskMetadataGet
  ← query: taskTypeID?:int[] → map<TaskTypeFormMetadataResult>
- `PUT /Tasks/restore` — Воскрешает удаленные заявки · права: TaskRestore
  ← body: int[]
- `GET /Tasks/short` — Возвращает краткий список заявок, доступных пользователю. · права: TasksList · paginated
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), branchID?:any, assetTypeID?:any, assetClassID?:any, erpID?:str, parentID?:any, assetSchemaID?:any, contactID?:any → map<ListShortResult>
- `GET /Tasks/stages/next` — Возвращает список доступных стадий, на котрые могут быть переведены заявки из списка. · права: TaskStagesList
  ← query: id?:int[] → map<ListStagesResult>
- `GET /Tasks/{taskID}` — Возвращает детальные сведения по заявке · права: TaskGet
  ← path: taskID:int; query: taskSnapshotID?:int, includeSchedule?:bool → DetailedInfoResult
- `PUT /Tasks/{taskID}` — Изменяет заявку · права: TaskUpdate
  ← path: taskID:int; body: Task.UpdateData
- `PATCH /Tasks/{taskID}` — Обновляет отдельные поля в заявке · права: TaskUpdate
  ← path: taskID:int; body: PatchData[]
- `DELETE /Tasks/{taskID}` — Помечает заявку как удаленную · права: TaskDelete
  ← path: taskID:int
- `GET /Tasks/{taskID}/assignments` — Возвращает историю назначения заявки · права: TaskAssignmentHistoryList · paginated
  ← path: taskID:int → ListAssignmentHistoryResult
- `GET /Tasks/{taskID}/attachment/{attachmentID}` — Прикрепленный файл к заявке
<param name="taskID">Идентификатор заявки</param><param name="attachmentID">Идентификатор прикрепленного файла к заявке</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: TaskAttachmentGet
  ← path: taskID:int, attachmentID:int; query: thumbnailSize?:int → GetAttachmentResult
- `GET /Tasks/{taskID}/attachments` — Список прикрепленных файлов к заявке
<param name="taskID">Идентификатор заявки</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: TaskAttachmentsList · paginated
  ← path: taskID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: TaskAttachmentDownload · paginated
  ← path: taskID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/attributes` — Возвращает доп.поля по заявке · права: TaskAttributesList · paginated
  ← path: taskID:int; query: isForActualTaskStageOnly?:bool → AttributeResult[]
- `POST /Tasks/{taskID}/autoStaginging` — Активирует запланированный автоматический переход по стадиям заявки · права: TaskStageMoverTerminate · paginated
  ← path: taskID:int
- `DELETE /Tasks/{taskID}/autoStaginging` — Прекращает запланированный автоматический переход по стадиям заявки · права: TaskStageMoverTerminate · paginated
  ← path: taskID:int
- `GET /Tasks/{taskID}/changes` — Возвращает историю изменения заявки · права: TaskGet · paginated
  ← path: taskID:int; query: dateRangeFrom?:any, dateRangeTill?:any, userID?:any, tab?:str, section?:str → HistoryResult[]
- `GET /Tasks/{taskID}/checkCompanyCodeUsed` — Возвращает информацию используется ли код компании при генерации номера заявки · права: IfUsedInTaskNumberGet
  ← path: taskID:int → bool
- `GET /Tasks/{taskID}/checkLists` — Возвращает список чек-листов в заявке · права: TaskCheckListsList · paginated
  ← path: taskID:int → map<TaskCheckListResult>
- `POST /Tasks/{taskID}/checkLists` — Добавляет чек-листы к заявке · права: TaskCheckListAdd
  ← path: taskID:int; body: TaskCheckList.AddData[] → TaskCheckLists.PostResult[]
- `DELETE /Tasks/{taskID}/checkLists` — Помечает чек-листы заявки как удаленные · права: TaskCheckListDelete
  ← path: taskID:int; body: int[]
- `POST /Tasks/{taskID}/checkLists/{taskCheckListID}` — Добавляет чек-лист к заявке · права: TaskCheckListAdd
  ← path: taskID:int, taskCheckListID:int → TaskCheckLists.PostResult[]
- `DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}` — Помечает чек-лист заявки как удаленный · права: TaskCheckListDelete
  ← path: taskID:int, taskCheckListID:int
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Возвращает результаты чек-листа для заявки · права: TaskCheckListResultsList · paginated
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultResult>
- `PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Устанавливает результаты для элементов чек-листа заявки · права: TaskCheckListResultSet
  ← path: taskID:int, taskCheckListID:int; body: TaskCheckListResult.UpdateData[]
- `DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Помечает результы чек-листа заявки как удаленные · права: TaskCheckListResultDelete
  ← path: taskID:int, taskCheckListID:int; body: int[]
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · права: TaskCheckListResultAttachmentList · paginated
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Возвращает результаты чек-листа для заявки · права: TaskCheckListResultsList · paginated
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultV2Result>
- `PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Устанавливает результаты для элементов чек-листа заявки · права: TaskCheckListResultSet
  ← path: taskID:int, taskCheckListID:int; body: UpdateDataV2[]
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · права: TaskCheckListResultAttachmentList · paginated
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments/{attachmentID}` — Получает информацию о прикрепленном к чек-листу по завке файле · права: TaskCheckListResultAttachmentGet
  ← path: taskID:int, taskCheckListID:int, taskChecklistResultID:int, attachmentID:int
- `POST /Tasks/{taskID}/checkLists/{taskCheckListID}/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к чек-листу по заявке. Данные будут получены из формы. · права: TaskCheckListResultAttachmentUpload
  ← path: taskID:int, taskCheckListID:int; body: { Attachments?: TaskCheckListResultAttachment[] /* Вложения в чек- листе по заявке */, TaskCheckListID?: int /* Идентификатор чек- листа по заявке */, TaskCheckListResultID?: int /* Идентификатор результата чек- листа по заявке */ } → TaskCheckListResultAttachment.UploadResult
- `PUT /Tasks/{taskID}/complete` — Помечает заявку, как выполненную · права: TaskComplete
  ← path: taskID:int; body: TaskCompletion.AddData
- `GET /Tasks/{taskID}/completedWorks` — Возвращает список выполненных работ по заявке · права: CompletedWorkList · paginated
  ← path: taskID:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/attachments` — Возвращает список вложенных файлов во все выполненные работы в заявке · права: CompletedWorkAttachmentList · paginated
  ← path: taskID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/attributes` — Возвращает доп.поля для выполненных работ по заявке · права: CompletedWorkAttributeList · paginated
  ← path: taskID:int; query: completedWorkID?:any → CompletedWorkAttributeResult[]
- `GET /Tasks/{taskID}/completedWorks/materials` — Список израсходованных материалов для выполненных работ по заявке · права: CompletedWorkMaterialsList · paginated
  ← path: taskID:int → map<CompletedWorkMaterialResult>
- `GET /Tasks/{taskID}/completedWorks/materialsWithCodes` — Список израсходованных материалов для выполненных работ по заявке (включая коды маркировки). · права: CompletedWorkMaterialsList · paginated
  ← path: taskID:int → map<CompletedWorkMaterialResult>
- `GET /Tasks/{taskID}/completedWorks/report/attachment` — Получает подпись к акту выполненной работы · права: CompletedWorkReportAttachmentGet
  ← path: taskID:int
- `POST /Tasks/{taskID}/completedWorks/report/attachment/v2/{attachmentID}` — Добавляет загруженный ранее вложенный файл к акту выполненной работы · права: CompletedWorkReportAttachmentAdd
  ← path: taskID:int, attachmentID:int; body: AddSignedData
- `POST /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}` — Добавляет загруженный ранее вложенный файл к акту выполненной работы · права: CompletedWorkReportAttachmentAdd
  ← path: taskID:int, attachmentID:int
- `DELETE /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}` — Помечает прикрепленный файл к акту выполненной работы как удаленный · права: CompletedWorkReportAttachmentDelete
  ← path: taskID:int, attachmentID:int
- `GET /Tasks/{taskID}/completedWorks/technicians` — Список исполнителей для выполненных работ по заявке · права: CompletedWorkTechnicianList
  ← path: taskID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments` — Возвращает список вложенных файлов по выполненной работе в заявке · права: CompletedWorkAttachmentList · paginated
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: CompletedWorkAttachmentDownload · paginated
  ← path: taskID:int, attachmentID:int, completedWorkID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Возвращает доп.поля для выполненной работы по заявке · права: CompletedWorkAttributeList · paginated
  ← path: taskID:int, completedWorkID:int → CompletedWorkAttributeResult[]
- `PUT /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Устанавливает результаты для доп.полей по выполненной работе по заявке · права: CompletedWorkAttributeMerge
  ← path: taskID:int, completedWorkID:int; body: AttributeData[]
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Помечает атрибуты выполенной работы заявки удаленный · права: CompletedWorkAttributeDelete
  ← path: taskID:int, completedWorkID:int; body: int[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/attachments` — Возвращает список файлов прикрепленных к атрибутам выполенной работы по заявке · права: CompletedWorkAttributeAttachmentList · paginated
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int, attributeID?:any → map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}` — Помечает атрибут выполенной работы заявки удаленный · права: CompletedWorkAttributeDelete
  ← path: taskID:int, completedWorkID:int, attributeID:int
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}/attachments` — Возвращает список файлов прикрепленных к атрибуту выполненной работы по заявке · права: CompletedWorkAttributeAttachmentList · paginated
  ← path: taskID:int, completedWorkID:int, attributeID:int; query: thumbnailSize?:int → map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Список израсходованных материалов для выполненной работы по заявке · права: CompletedWorkMaterialsList
  ← path: taskID:int, completedWorkID:int → CompletedWorkMaterialResult
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Удаляет материалы у выполненной работы по заявке · права: CompletedWorkMaterialDelete
  ← path: taskID:int, completedWorkID:int; body: MaterialDelete
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Список исполнителей для выполненной работы по заявке · права: CompletedWorkTechnicianList
  ← path: taskID:int, completedWorkID:int → CompletedWorkTechnicianResult
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Удаляет исполнителей у выполненной работы по заявке · права: CompletedWorkMaterialDelete
  ← path: taskID:int, completedWorkID:int; body: int[]
- `POST /Tasks/{taskID}/completedWorks/{completedWorkID}/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к чек-листу по заявке. Данные будут получены из формы. · права: CompletedWorkAttributeAttachmentUpload
  ← path: taskID:int, completedWorkID:int; body: { Attachments?: CompletedWorkAttributeAttachment[] /* Вложения в атрибуте выполненной работы по заявке */, AttributeID?: int /* Идентификатор атрибута выполненной работы по заявке */, CompletedWorkID?: int /* Идентификатор выполненной работы по заявке */ } → CompletedWorkAttachments.UploadResult
- `GET /Tasks/{taskID}/completedWorks/{id}` — Получает информацию о выполненной работе по заявкам · права: CompletedWorkGet
  ← path: taskID:int, id:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/contacts` — Возвращает список контактов заявки · права: TaskContactsList · paginated
  ← path: taskID:int → map<TaskContacts.ListResult>
- `GET /Tasks/{taskID}/contacts/{contactID}` — Возвращает контакт заявки · права: TaskContactGet
  ← path: taskID:int, contactID:int → TaskContacts.GetResult
- `DELETE /Tasks/{taskID}/contacts/{contactID}` — Удаляет контактное лицо у заявки · права: TaskContactDelete
  ← path: taskID:int, contactID:int
- `POST /Tasks/{taskID}/conversation` — Добавляет сообщения по заявкам. · права: TaskConversationAdd
  ← path: taskID:int; body: TaskConversationData → TaskConversations.AddResult[]
- `POST /Tasks/{taskID}/conversation/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к сообщению по заявке. Данные будут получены из формы. · права: TaskConversationAttachmentUpload
  ← path: taskID:int; body: { Attachments?: TaskConversationAttachment[] /* Вложения в сообщение по заявке */, IsExternal?: bool /* Чат с командой или Заказчиком */, Message?: str /* Сообщение по заявке */ } → TaskConversations.UploadResult
- `GET /Tasks/{taskID}/conversations` — Возвращает сообщения по заявке
<param name="taskID">Идентификатор заявки</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param><param name="searchText">Текст для поиска в сообщениях по заявке</param> · права: TaskConversationsList · paginated
  ← path: taskID:int; query: thumbnailSize?:int, searchText?:str, isRead?:enum(true, false) → TaskMessage[]
- `HEAD /Tasks/{taskID}/conversations` — Возвращает заголовок списка сообщений по заявке
(для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="taskID">Идентификатор заявки</param><param name="searchText">Текст для поиска в сообщениях по заявке</param> · права: TaskConversationsList
  ← path: taskID:int; query: searchText?:str, isRead?:enum(true, false), isExternal?:enum(true, false)
- `GET /Tasks/{taskID}/conversations/{taskConversationID}` — Возвращает сообщение по заявке
<param name="taskID">Идентификатор заявки</param><param name="taskConversationID">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: TaskConversationGet · paginated
  ← path: taskID:int, taskConversationID:int; query: thumbnailSize?:int → TaskMessage
- `GET /Tasks/{taskID}/conversations/{taskConversationID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: TaskConversationAttachmentDownload · paginated
  ← path: taskID:int, attachmentID:int, taskConversationID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/conversations/{taskConversationID}/delivery` — Возвращает информацию по доставке и прочтению сообщения по заявке.
<param name="taskID">Идентификатор заявки</param><param name="taskConversationID">Идентификатор сообщения</param> · права: TaskConversationDeliveryList · paginated
  ← path: taskID:int, taskConversationID:int → ListConversationDeliveryResult[]
- `GET /Tasks/{taskID}/materials` — Возвращает список необходимых материалов для заявки · права: TaskMaterialsList · paginated
  ← path: taskID:int → map<TaskMaterials.ListResult>
- `GET /Tasks/{taskID}/meta` — Возвращает метаданные для формы заявки. · права: TaskMetadataGet
  ← path: taskID:int → TaskTypeFormMetadataResult
- `GET /Tasks/{taskID}/ratings` — Возвращает отзывы/рейтинги инжененров по заявке. · права: TaskTechnicianRatingList · paginated
  ← path: taskID:int → RatingResult[]
- `GET /Tasks/{taskID}/ratings/avg` — Возвращает отзывы/рейтинги инжененров по заявке. · права: TaskTechnicianRatingList · paginated
  ← path: taskID:int → RatingResult[]
- `GET /Tasks/{taskID}/skills` — Возвращает список навыков заявки · права: TaskSkillList · paginated
  ← path: taskID:int → map<TaskSkillResult>
- `GET /Tasks/{taskID}/stages` — Возвращает историю перемещения заявки по стадиям. · права: TaskStagingHistoryList · paginated
  ← path: taskID:int; query: includeChangeset?:bool, actionLocationState?:ActionLocationState → ListStagingHistoryResult
- `GET /Tasks/{taskID}/stages/next` — Возвращает список доступных стадий, на котрые может быть переведена заявка. · права: TaskStagesList · paginated
  ← path: taskID:int → map<ListStagesResult>
- `GET /Tasks/{taskID}/tags` — Возвращает тэги по заявке. · права: TaskTagsList · paginated
  ← path: taskID:int → str[]
- `GET /Tasks/{taskID}/watchLists` — WatchList по заявке · права: TaskWatchListList · paginated
  ← path: taskID:int; query: searchText?:str → TaskWatchLists.ListResult[]
- `DELETE /Tasks/{taskId}/completedWorks/marking-codes` — Удаляет все коды маркировки по заявке (во всех выполненных работах). · права: CompletedWorkMaterialDelete
  ← path: taskId:int → TaskCompletedWorksMarkingCodesDeleteResult
  Пример запроса:
```
DELETE /tasks/123/completedWorks/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "deletedCount": 42
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes` — Возвращает коды маркировки для выполненной работы (все материалы). · права: CompletedWorkMaterialsList
  ← path: taskId:int, completedWorkId:int → MarkingCodesListResult
  Пример запроса:
```
GET /tasks/123/completedWorks/1/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": null,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": null,
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    },
    {
      "completedWorkID": 1,
      "materialID": 888,
      "warehouseID": 10,
      "inventoryID": 555002,
      "code": "0104601234567890215QWERTY1234567890\u001d93AAA111",
      "scannedAtUtc": "2026-03-05T14:13:10.000Z",
      "receivedAtUtc": "2026-03-05T14:13:10.500Z",
      "createdBy": 98765
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson),
`404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: `X-Last-Lsn` (`LastLsnHeader`) поддерживается для совместимости. Для операции чтения значение может не измениться.
- `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетная привязка кодов маркировки к материалам выбранной выполненной работы. · права: CompletedWorkMaterialUpdate
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesUpsertRequest → CompletedWorkMaterialsMarkingCodesUpsertResult
  Пример запроса:
```
POST /tasks/123/completedWorks/1/materials/marking-codes
{
  "materials": [
    {
      "materialId": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "codes": [
        { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" }
      ]
    },
    {
      "materialId": 888,
      "warehouseID": 10,
      "codes": [
        { "code": "010...", "scannedAtUtc": null }
      ]
    }
  ]
}
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "items": [
    { "materialID": 777, "warehouseID": 10, "inventoryID": 555001, "code": "010...", "action": "INSERT" },
    { "materialID": 888, "warehouseID": 10, "inventoryID": 555002, "code": "010...", "action": "UPDATE" }
  ],
  "errors": [
    { "materialID": 999, "warehouseID": 10, "inventoryID": null, "code": "010...", "reason": "MaterialContextNotFound", "message": "Material context was not found in the selected completed work." }
  ]
}
```

Поле `items[].action` соответствует SQL Server `$action` из `MERGE` и принимает значения `INSERT`/`UPDATE`.
Важно: `UPDATE` означает восстановление ранее отвязанного кода (soft-delete), а не "обновление активной привязки".


Если код уже существует и активен (привязан в рамках тенанта) — операция завершится ошибкой.


Частичный успех: если хотя бы один код можно корректно привязать — метод вернёт `200 OK`,
а ошибки для остальных кодов будут перечислены в `errors`.


В примере ниже: `INSERT` — создана новая привязка, `UPDATE` — восстановлена ранее отвязанная (soft-delete) привязка.


Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетная перепривязка (перенос) существующих активных кодов маркировки у материалов выбранной выполненной работы. · права: CompletedWorkMaterialUpdate
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesUpdateRequest → CompletedWorkMaterialsMarkingCodesUpdateResult
  Пример запроса:
```
PUT /tasks/123/completedWorks/1/materials/marking-codes
{
  "materials": [
    {
      "materialId": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "codes": [
        { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" }
      ]
    }
  ]
}
```

Важно:
<list type="bullet"><item><description>операция не создаёт новые коды: каждый код из запроса должен уже существовать и быть активным</description></item><item><description>частичный успех: если хотя бы один код можно корректно перенести — метод вернёт `200 OK`, а ошибки для остальных кодов будут перечислены в `errors`</description></item></list>
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "items": [
    {
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123"
    }
  ],
  "errors": [
    { "materialID": 888, "warehouseID": 10, "inventoryID": null, "code": "010...", "reason": "MarkingCodeNotFound", "message": "The marking code was not found or is not active." }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетное удаление привязанных кодов маркировки у материалов выбранной выполненной работы. · права: CompletedWorkMaterialDelete
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesDeleteRequest → CompletedWorkMaterialsMarkingCodesDeleteResult
  Пример запроса:
```
DELETE /tasks/123/completedWorks/1/materials/marking-codes
{
  "materials": [
    { "materialId": 777, "warehouseID": 10, "inventoryID": 555001, "codes": [ "010...", "010..." ] }
  ]
}
```
            
Если часть кодов не найдена — это не ошибка: такие элементы попадут в `notFound`.
Это намеренное поведение API для идемпотентности: сервер не передаёт в хранилище коды, которых нет в текущих привязках.
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "items": [
    {
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "deleted": [ "010...", "010..." ],
      "notFound": [ "010..." ]
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Возвращает коды маркировки для конкретного материала в выполненной работе. · права: CompletedWorkMaterialsList
  ← path: taskId:int, completedWorkId:int, materialId:int; query: warehouseID?:any → MarkingCodesListResult
  Пример запроса:
```
GET /tasks/123/completedWorks/1/materials/777/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": "2026-03-05T14:12:31.123Z",
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson),
`404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: `X-Last-Lsn` (`LastLsnHeader`) поддерживается для совместимости. Для операции чтения значение может не измениться.
- `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Пакетная привязка кодов маркировки к материалу. · права: CompletedWorkMaterialUpdate
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesUpsertForMaterialRequest → MarkingCodesUpsertResult
  Пример запроса:
```
POST /tasks/123/completedWorks/1/materials/777/marking-codes
{
  "warehouseID": 10,
  "inventoryID": 555001,
  "codes": [
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" },
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:15Z" }
  ]
}
```
`warehouseID` обязателен.
`inventoryID` опционален на уровне API: если не передан — сервер попытается определить его по контексту материала
(taskId + completedWorkId + materialId + warehouseID). Если определить однозначно нельзя — вернётся `409 Conflict` (нужно указать `inventoryID`).


Поле `items[].action` соответствует SQL Server `$action` из `MERGE` и принимает значения `INSERT`/`UPDATE`.
Важно: `UPDATE` означает восстановление ранее отвязанного кода (soft-delete), а не "обновление активной привязки".


Частичный успех: если хотя бы один код можно корректно привязать — метод вернёт `200 OK`,
а ошибки для остальных кодов будут перечислены в `errors`.


В примере ниже: `INSERT` — создана новая привязка, `UPDATE` — восстановлена ранее отвязанная (soft-delete) привязка.


Важно про коды ответа:
<list type="bullet"><item><description>если есть хотя бы один успешно обработанный код — ответ `200 OK` и подробности ошибок в `errors`</description></item><item><description>если ни один код не может быть обработан (например, `MaterialContextNotFound`/`DuplicateInRequest`/...) — ответ `409 Conflict` и подробности в `errors`</description></item></list>

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/...).

            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "warehouseID": 10,
  "inventoryID": 555001,
  "items": [
    { "code": "010...", "action": "INSERT" },
    { "code": "010...", "action": "UPDATE" }
  ],
  "errors": [
    { "code": "010...", "reason": "MarkingCodeAlreadyExists", "message": "The marking code is already in use." }
  ]
}
```
            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Пакетная перепривязка (перенос) существующих активных кодов маркировки на указанный материал. · права: CompletedWorkMaterialUpdate
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesUpdateForMaterialRequest → MarkingCodesUpdateResult
  Пример запроса:
```
PUT /tasks/123/completedWorks/1/materials/777/marking-codes
{
  "warehouseID": 10,
  "inventoryID": 555001,
  "codes": [
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" },
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:15Z" }
  ]
}
```
            
Важно:
<list type="bullet"><item><description>операция не создаёт новые коды: каждый код из запроса должен уже существовать и быть активным</description></item><item><description>операция не удаляет коды, которые уже привязаны к материалу, но не перечислены в запросе (для удаления используйте DELETE)</description></item><item><description>частичный успех: если хотя бы один код можно корректно перенести — метод вернёт `200 OK`, а ошибки для остальных кодов будут перечислены в `errors`</description></item></list>
            
После выполнения метод возвращает актуальный список кодов для (materialId + warehouseID + inventoryID).
            

`warehouseID` обязателен.
`inventoryID` опционален на уровне API: если не передан — сервер попытается определить его по контексту материала
(taskId + completedWorkId + materialId + warehouseID). Если определить однозначно нельзя — вернётся `409 Conflict` (нужно указать `inventoryID`).


Важно про коды ответа:
<list type="bullet"><item><description>если есть хотя бы один успешно обработанный код — ответ `200 OK` и подробности ошибок в `errors`</description></item><item><description>если ни один код не может быть обработан (например, `MaterialContextNotFound`/`MarkingCodeNotFound`/...) — ответ `409 Conflict` и подробности в `errors`</description></item></list>

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/...).

            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": "2026-03-05T14:12:31.123Z",
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    }
  ],
  "errors": [
    { "code": "010...", "reason": "MarkingCodeNotFound", "message": "The marking code was not found or is not active." }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Удаление привязанных кодов маркировки у материала. · права: CompletedWorkMaterialDelete
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesDeleteForMaterialRequest → MarkingCodesDeleteResult
  Пример запроса:
```
DELETE /tasks/123/completedWorks/1/materials/777/marking-codes
{
  "warehouseID": 10,
  "inventoryID": 555001,
  "codes": [ "010...", "010..." ]
}
```
            
Если часть кодов не найдена — это не ошибка: такие элементы попадут в `notFound`.
Это намеренное поведение API для идемпотентности: сервер не передаёт в хранилище коды, которых нет в текущих привязках.
            

`warehouseID` обязателен.
`inventoryID` опционален на уровне API: если не передан — сервер попытается определить его по контексту материала
(taskId + completedWorkId + materialId + warehouseID). Если определить однозначно нельзя — вернётся `409 Conflict` (нужно указать `inventoryID`).


Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "warehouseID": 10,
  "inventoryID": 555001,
  "deleted": [ "010...", "010..." ],
  "notFound": [ "010..." ]
}
```
            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.
- `GET /Tasks/{taskId}/marking-codes` — Возвращает коды маркировки для заявки (все выполненные работы). · права: TaskGet
  ← path: taskId:int → MarkingCodesListResult
  Пример запроса:
```
GET /tasks/123/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": null,
  "materialID": null,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": "2026-03-05T14:12:31.123Z",
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    },
    {
      "completedWorkID": 2,
      "materialID": 888,
      "warehouseID": 10,
      "inventoryID": 555002,
      "code": "0104601234567890215QWERTY1234567890\u001d93AAA111",
      "scannedAtUtc": null,
      "receivedAtUtc": "2026-03-05T14:13:10.500Z",
      "createdBy": 98765
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson),
`404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: `X-Last-Lsn` (`LastLsnHeader`) поддерживается для совместимости. Для операции чтения значение может не измениться.

## TemplateQuickResponse
- `GET /TemplateQuickResponse` — Возвращает список быстрых ответов · права: QuickResponseList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), taskTypeID?:any → map<TemplateQuickResponse.ListResult>
- `POST /TemplateQuickResponse` — Создаёт новый быстрый ответ · права: QuickResponseAdd
  ← body: TemplateQuickResponse.AddData[] → int[]
- `PUT /TemplateQuickResponse` — Обновляет быстрый ответ. · права: QuickResponseUpdate
  ← body: TemplateQuickResponse.UpdateData[]
- `DELETE /TemplateQuickResponse` — Помечает быстрые ответы, как удалённые · права: QuickResponseDelete
  ← body: int[]
- `PUT /TemplateQuickResponse/taskTypes` — Создает или изменяет привязку быстрых ответов к типам заявок. · права: TaskTypeQuickResponseMerge
  ← body: TemplateQuickResponse.MergeData[]
- `GET /TemplateQuickResponse/{id}` — Возвращает быстрый ответ · права: QuickResponseGet
  ← path: id:int → TemplateQuickResponse.GetResult

## UserTaskFavourites
- `POST /UserTaskFavourites` — Добавляет заявки в список избранных для текущего пользователя. · права: UserTaskFavouriteAdd · paginated
  ← body: int[]
- `DELETE /UserTaskFavourites` — Добавляет заявки в список избранных для текущего пользователя. · права: UserTaskFavouriteDelete · paginated
  ← body: int[]

## WorkTypes
- `GET /WorkTypes` — Возвращает список видов работ. · права: WorkTypeList · paginated
  ← query: searchText?:str, assetID?:any, taskTypeID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false), erpID?:str → map<WorkTypes.ListResult>
- `POST /WorkTypes` — Создает вид работ · права: WorkTypeAdd
  ← query: relatedToAnyTaskType?:bool, relatedToAnyAsset?:bool, relatedToAnyTaskType?:enum(true, false); body: WorkType.AddData[] → int[]
- `PUT /WorkTypes` — Изменяет виды работ · права: WorkTypeUpdate
  ← body: WorkType.UpdateData[]
- `DELETE /WorkTypes` — Помечает виды работ, как удаленные · права: WorkTypeDelete
  ← body: int[]
- `PUT /WorkTypes/publish` — Публикует выполненные работы · права: WorkTypePublish
  ← body: int[]
- `PUT /WorkTypes/unpublish` — Отменяет публикацию выполненных работы · права: WorkTypeUnpublish
  ← body: int[]
- `GET /WorkTypes/{id}` — Возвращает данные для вида работы. · права: WorkTypeGet · paginated
  ← path: id:int → WorkTypes.GetResult
- `DELETE /WorkTypes/{id}` — Помечает вид работ как удаленный · права: WorkTypeDelete
  ← path: id:int
- `PUT /WorkTypes/{id}/publish` — Помечает вид работ как опубликованный · права: WorkTypePublish
  ← path: id:int
- `GET /WorkTypes/{id}/taskTypes` — Возвращает список относящихся к виду работ типов задач · права: TaskTypesList · paginated
  ← path: id:int
- `POST /WorkTypes/{id}/taskTypes` — Привязать список типов задач к виду работ · права: TaskTypeUpdate
  ← path: id:int; body: int[]
- `DELETE /WorkTypes/{id}/taskTypes` — Удалить привязку типу задач к виду работ · права: TaskTypeUpdate
  ← path: id:int; body: int[]
- `PUT /WorkTypes/{id}/unpublish` — Помечает вид работ как опубликованный · права: WorkTypeUnpublish
  ← path: id:int
- `GET /WorkTypes/{parentWorkTypeID}/workTypes` — Возвращает список дочерних видов работ (вниз по графу). · права: WorkTypeList · paginated
  ← path: parentWorkTypeID:int; query: searchText?:str, assetID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false) → map<WorkTypes.ListResult>
- `GET /WorkTypes/{parentWorkTypeID}/workTypes/all` — Возвращает список всех дочерних видов работ (вниз по графу). · права: WorkTypeList · paginated
  ← path: parentWorkTypeID:int; query: searchText?:str, assetID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false) → map<WorkTypes.ListResult>
- `GET /WorkTypes/{workTypeID}/checkLists` — Возвращает список чек-листов вида работ · права: WorkTypeCheckListList · paginated
  ← path: workTypeID:int → map<CheckLists.GetResult[]>
- `POST /WorkTypes/{workTypeID}/checkLists` — Добавляет чек-листы к типу работ · права: WorkTypeCheckListAdd
  ← path: workTypeID:int; body: int[]
- `DELETE /WorkTypes/{workTypeID}/checkLists` — Помечает чек-листы у типа работ как удаленные · права: WorkTypeCheckListDelete
  ← path: workTypeID:int; body: int[]
- `POST /WorkTypes/{workTypeID}/checkLists/{checkListID}` — Добавляет чек-лист к типу работ · права: WorkTypeCheckListAdd
  ← path: workTypeID:int, checkListID:int
- `DELETE /WorkTypes/{workTypeID}/checkLists/{checkListID}` — Помечает чек-лист у типа работ как удаленный · права: WorkTypeCheckListDelete
  ← path: workTypeID:int, checkListID:int
