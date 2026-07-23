# WORK — справочник ручек

> **Что здесь:** все ручки сервиса WORK (API for managing tasks and works in HubEx): сигнатуры, параметры, права. Типы — schemas/WORK.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WORK.md`; грабли — `notes/WORK.md` (если есть).

Base: `{BASE_URL}/WORK`
> Примеры ответов вынесены в [../examples/WORK.md](../examples/WORK.md).

**Оглавление**

- CheckListItems — строки 43–47
- CheckLists — строки 49–67
- CompletedWorkAttachments — строки 69–77
- CompletedWorks — строки 79–85
- RequestMethods — строки 87–89
- TaskActualities — строки 91–103
- TaskAssignmentHistory — строки 105–107
- TaskAttachments — строки 109–117
- TaskAttributes — строки 119–123
- TaskContacts — строки 125–129
- TaskConversationDeliveries — строки 131–134
- TaskConversations — строки 136–145
- TaskFilter — строки 147–151
- TaskListQueries — строки 153–169
- TaskMaterials — строки 171–181
- TaskOrderBy — строки 183–185
- TaskRatings — строки 187–189
- TaskSkills — строки 191–195
- TaskStagingHistory — строки 197–203
- TaskStatuses — строки 205–217
- TaskTags — строки 219–223
- TaskTemplateExcludedAssets — строки 225–229
- TaskTemplates — строки 231–273
- TaskTypeDistrict — строки 275–277
- TaskTypeRoutes — строки 279–287
- TaskTypes — строки 289–311
- TaskWatchLists — строки 313–317
- Tasks — строки 319–530
- TemplateQuickResponse — строки 532–544
- UserTaskFavourites — строки 546–550
- WorkTypes — строки 552–592

## CheckListItems
- `POST /CheckListItems` — Изменяет элементы чек-листов · права: CheckListItemMerge · коды: 202
  ← body: CheckListItem.MergeData[] → ICheckListItemMergeEntity
- `DELETE /CheckListItems` — Помечает результат чек-листа по заявке как удаленный · права: CheckListItemDelete · коды: 202
  ← body: CheckListItem.DeleteData[]

## CheckLists
- `GET /CheckLists` — Возвращает список активных чек-листов · права: CheckListsList · paginated · коды: 200, 206
  ← query: searchText?:str, assetID?:any, workTypeID?:any, isAssignedToAsset?:enum(true, false), isAssignedToWorkType?:enum(true, false), searchText?:str → map<CheckLists.ListResult>
- `POST /CheckLists` — Создает чек-листы · права: CheckListAdd · коды: 201
  ← body: CheckList.AddData[] → int[]
- `PUT /CheckLists` — Изменяет чек-листы · права: CheckListUpdate · коды: 202
  ← body: CheckList.UpdateData[]
- `DELETE /CheckLists` — Помечает чек-листы, как удаленные · права: CheckListDelete · коды: 202
  ← body: int[]
- `POST /CheckLists/{checkListID}/assign` — Проставляпет идентификаторы чек-листов в таблицах объектов и видов работ · права: CheckListAssign · paginated · коды: 202, 206
  ← path: checkListID:int; body: CheckListAssignmentData
- `DELETE /CheckLists/{checkListID}/assign` — Удаляет идентификаторы чек-листов из таблиц объектов и видов работ · права: CheckListUnassign · paginated · коды: 202, 206
  ← path: checkListID:int; body: CheckListAssignmentData
- `GET /CheckLists/{checkListID}/items` — Возвращает элементы чек-листа · права: CheckListItemsList · paginated · коды: 200, 206
  ← path: checkListID:int → map<CheckListItemResult>
- `GET /CheckLists/{id}` — Возвращает чек-лист · права: CheckListGet · коды: 200
  ← path: id:int → map<CheckLists.GetResult>
- `DELETE /CheckLists/{id}` — Помечает чек-лист, как удаленный · права: CheckListDelete · коды: 202, 409
  ← path: id:int

## CompletedWorkAttachments
- `POST /CompletedWorkAttachments` — Добавляет загруженный ранее вложенный файл к выполненной работе · права: CompletedWorkAttachmentAdd · коды: 201, 500
  ← body: Common.TaskActionData<CompletedWorkAttachment.AddData>[] → CompletedWorkAttachments.AddResult[]
- `DELETE /CompletedWorkAttachments` — Помечает прикрепленный к выполненной работе файл как удаленный · права: CompletedWorkAttachmentDelete · коды: 202, 500
  ← body: TaskActionData<DeleteData>[]
- `POST /CompletedWorkAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из тела запроса. · права: CompletedWorkAttachmentUpload · коды: 201, 500
  ← body: CompletedWorkBodyUploadData → CompletedWorkAttachments.UploadResult
- `POST /CompletedWorkAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из формы. · права: CompletedWorkAttachmentUpload · коды: 201, 500
  ← query: TaskID?:int, CompletedWorkID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → CompletedWorkAttachments.UploadResult

## CompletedWorks
- `POST /CompletedWorks` — Создаёт выполненные работы по одной или нескольким заявкам · права: CompletedWorkAdd · коды: 200, 201, 400, 409 · примеры
  ← body: Common.TaskActionData<CompletedWork.AddData>[] → CompletedWorks.AddResult[]
- `PUT /CompletedWorks` — Изменяет выполненные работы по заявкам · права: CompletedWorkUpdate · коды: 202 · примеры
  ← body: Common.TaskActionData<CompletedWork.UpdateData>[]
- `DELETE /CompletedWorks` — Помечает выполненные работы по заявкам как удалённые · права: CompletedWorkDelete · коды: 202 · примеры
  ← body: TaskActionData<Int16>[]

## RequestMethods
- `GET /RequestMethods` — Возвращает список методов подачи заявок. · права: RequestMethodsList · paginated · коды: 200, 206
  → map<RequestMethods.ListResult>

## TaskActualities
- `GET /TaskActualities` — Возвращает список актуальностей заявок · права: TaskActualitiesList · paginated · коды: 200, 206
  → map<TaskActualities.ListResult>
- `POST /TaskActualities` — Создает актуальности заявки · права: TaskActualityAdd · коды: 201
  ← body: TaskActuality.AddData[] → int[]
- `PUT /TaskActualities` — Изменяет актуальности заявок · права: TaskActualityUpdate · коды: 202
  ← body: TaskActuality.UpdateData[]
- `DELETE /TaskActualities` — Помечает актуальности заявок, как удаленные · права: TaskActualityDelete · коды: 202
  ← body: int[]
- `GET /TaskActualities/{id}` — Возвращает актуальность заявки · права: TaskActualityGet · коды: 200
  ← path: id:int → TaskActualities.ListResult
- `DELETE /TaskActualities/{id}` — Помечает актуальность заявки как удаленную · права: TaskActualityDelete · коды: 202, 409
  ← path: id:int

## TaskAssignmentHistory
- `POST /TaskAssignmentHistory` — Назначает новые заявки на пользователя. · права: TaskAssignmentHistoryAdd · коды: 201, 500
  ← body: TaskAssignmentHistory.PostData[] → TaskAssignmentHistory.AddResult[]

## TaskAttachments
- `POST /TaskAttachments` — Свзяывает заявку и вложение · права: TaskAttachmentAdd · коды: 201, 500
  ← body: TaskActionData<Int32>[] → TaskAttachments.PostResult[]
- `DELETE /TaskAttachments` — Помечает связку заявки и вложения как удаленную · права: TaskAttachmentDelete · коды: 202, 500
  ← body: TaskActionData<Int32>[]
- `POST /TaskAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к заявке. Данные будут получены из тела запроса. · права: TaskAttachmentUpload · коды: 201, 500
  ← body: TaskBodyUploadData → TaskAttachments.UploadResult
- `POST /TaskAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к заявке. Данные будут получены из формы. · права: TaskAttachmentUpload · коды: 201, 500
  ← query: TaskID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → TaskAttachments.UploadResult

## TaskAttributes
- `GET /TaskAttributes` — Возвращает значения атрибутов по заявкам · права: TaskAttributeGet · paginated · коды: 200, 206
  ← query: taskID?:any, attributeID?:any → TaskAttributesResult[]
- `POST /TaskAttributes` — Изменяет значения атрибутов по заявкам · права: TaskAttributeMerge · коды: 202
  ← body: ActionData[]

## TaskContacts
- `POST /TaskContacts` — Добавляет контактные лица к заявке · права: TaskContactAdd · коды: 201, 409
  ← body: TaskActionData<Int32>[] → TaskContacts.PostResult
- `DELETE /TaskContacts` — Удаляет контактные лица у заявки · права: TaskContactDelete · коды: 202, 409
  ← body: TaskActionData<Int32>[]

## TaskConversationDeliveries
- `PUT /TaskConversationDeliveries/read` — Устанавливает отметки о прочтении сообщений по заявкам · права: TaskConversationDeliveryUpdate · коды: 202
  ← body: TaskActionData<SetReadData>[]
- `PUT /TaskConversationDeliveries/read/All` — Устанавливает отметки о прочтении всех сообщений по заявкам · права: TaskConversationDeliveryUpdate · коды: 202

## TaskConversations
- `GET /TaskConversations` — Возвращает список сообщений по заявкам, доступным пользователю.
<param name="searchText">Текст для поиска в сообщениях по заявкам</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: TaskConversationsList · paginated · коды: 200, 206
  ← query: searchText?:str, thumbnailSize?:int, isRead?:enum(true, false) → TaskMessageLast[]
- `DELETE /TaskConversations` — Помечает сообщения по заявкам как удаленные. · права: TaskConversationDelete · коды: 202, 500
  ← body: TaskConversation.DeleteData[]
- `HEAD /TaskConversations` — Возвращает заголовок списка сообщений по заявке (для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="searchText">Текст для поиска в сообщениях по заявкам</param> · права: TaskConversationsList · коды: 200
- `DELETE /TaskConversations/remove` — Помечает сообщения по заявкам как удаленные. · права: TaskConversationRemove · коды: 202, 500
  ← body: TaskConversation.DeleteData[]

## TaskFilter
- `GET /TaskFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · права: TasksList · коды: 200
  ← query: selectedOnly?:bool, selectedOnly?:enum(true, false) → FilterListItemProjection[]
- `PUT /TaskFilter` — Обновляет список доступных, для выполняющего операцию пользователя, фильтров и порядок их сортировки · права: TasksList · коды: 202
  ← body: FilterData[]

## TaskListQueries
- `GET /TaskListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · права: TaskListQueryListAll · paginated · коды: 200, 206
  → map<TaskListQueryResult>
- `POST /TaskListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю · права: TaskListQueryAdd · paginated · коды: 201, 206
  ← body: TaskListQuery.AddData[] → int[]
- `PUT /TaskListQueries` — Изменяет сохраненный запрос · права: TaskListQueryUpdate · paginated · коды: 202, 206
  ← body: TaskListQuery.UpdateData[]
- `DELETE /TaskListQueries` — Помечает сохраненные запрос как даленный · права: TaskListQueryDelete · paginated · коды: 202, 206
  ← body: int[]
- `DELETE /TaskListQueries/remove` — Помечает сохраненные запрос как даленный · права: TaskListQueryRemove · paginated · коды: 202, 206
  ← body: int[]
- `GET /TaskListQueries/{id}` — Возвращает сохраненный запрос · права: TaskListQueryGet · коды: 200
  ← path: id:int → map<TaskListQueryResult>
- `DELETE /TaskListQueries/{id}` — Помечает сохраненный запрос как даленный · права: TaskListQueryDelete · paginated · коды: 202, 206
  ← path: id:int
- `DELETE /TaskListQueries/{id}/remove` — Помечает сохраненный запрос как даленный · права: TaskListQueryRemove · paginated · коды: 202, 206
  ← path: id:int

## TaskMaterials
- `POST /TaskMaterials` — Добавляет, изменяет необходимые материалы к заявкам · права: TaskMaterialAdd · коды: 201, 409
  ← body: TaskActionData<MergeData>[] → TaskMaterials.PostResult
- `PUT /TaskMaterials` — Изменяет необходимые материалы в заявках · права: TaskMaterialUpdate · коды: 202, 409
  ← body: Common.TaskActionData<TaskMaterial.UpdateData>[]
- `DELETE /TaskMaterials` — Удаляет необходимые материалы из заявок · права: TaskMaterialDelete · коды: 202, 409
  ← body: TaskActionData<Int16>[]
- `PUT /TaskMaterials/takeOff` — Убирает признак взятия необходимых материалов из заявок · права: TaskMaterialTakeOff · коды: 202, 409
  ← body: TaskActionData<Int16>[]
- `PUT /TaskMaterials/takeOn` — Проставляет признак взятия необходимых материалов из заявок · права: TaskMaterialTakeOn · коды: 202, 409
  ← body: TaskActionData<TakeOnData>[]

## TaskOrderBy
- `GET /TaskOrderBy` — Возвращает список методов сортировки заявок · права: TaskOrderByList · paginated · коды: 200, 206
  → map<TaskOrderBy.ListResult>

## TaskRatings
- `POST /TaskRatings` — Создает оценки по заявкам · права: TaskTechnicianRatingMerge · коды: 202, 500
  ← body: TaskTechnicianRating.MergeData[]

## TaskSkills
- `POST /TaskSkills` — Добавляет навыки к заявкам · права: TaskSkillAdd · коды: 201, 409
  ← body: TaskActionData<Int32>[] → TaskSkills.PostResult
- `DELETE /TaskSkills` — Удаялет навыки из заявок · права: TaskSkillDelete · коды: 202, 409
  ← body: TaskActionData<Int32>[]

## TaskStagingHistory
- `POST /TaskStagingHistory` — Добавляет актуальную запись в историю прохождения заявки по стадиям. · права: TaskStagingHistoryAdd · коды: 201, 500
  ← body: TaskStagingHistory.PostData
- `POST /TaskStagingHistory/batch` — Массовый перевод заявок по стадиям. · права: TaskStagingHistoryAdd · коды: 202, 409, 500
  ← body: BatchRequestPostData → BatchRequestResult
- `POST /TaskStagingHistory/multiple` — Массовый перевод заявок по стадиям. · права: TaskStagingHistoryAdd · коды: 202, 500
  ← body: TaskStagingHistory.PostData[] → BatchRequestResult

## TaskStatuses
- `GET /TaskStatuses` — Возвращает список статусов заявок · права: TaskStatusesList · paginated · коды: 200, 206, 500
  → map<TaskStatuses.ListResult>
- `POST /TaskStatuses` — Создает статус заявки · права: TaskStatusAdd · коды: 201
  ← body: TaskStatus.AddData[] → int[]
- `PUT /TaskStatuses` — Изменяет статусы заявок · права: TaskStatusUpdate · коды: 202
  ← body: TaskStatus.UpdateData[]
- `DELETE /TaskStatuses` — Помечает статусы заявок, как удаленные · права: TaskStatusDelete · коды: 202
  ← body: int[]
- `GET /TaskStatuses/{id}` — Возвращает статус заявки · права: TaskStatusGet · коды: 200
  ← path: id:int → TaskStatuses.ListResult
- `DELETE /TaskStatuses/{id}` — Помечает статус заявки как удаленный · права: TaskStatusDelete · коды: 202, 409
  ← path: id:int

## TaskTags
- `POST /TaskTags` — Привязывает тэг к заявке. Если указанный тэг отсутствует в справочнике, создает его. · права: TaskTagAdd · коды: 201, 409
  ← body: TaskTag.AddData[]
- `DELETE /TaskTags` — Исключает тэг из заявки. В справочнике тэг остается. · права: TaskTagRemove · коды: 202, 409
  ← body: TaskTag.DeleteData[]

## TaskTemplateExcludedAssets
- `POST /TaskTemplateExcludedAssets` — Добавляет или изменяет исключенные объекты к плановой заявке · права: TaskTemplateExcludedAssetMerge · коды: 201, 409
  ← body: TaskTemplateActionData<Int32>[] → TaskTemplateExcludedAssetMergeResult
- `DELETE /TaskTemplateExcludedAssets` — Удаляет исключенные объекты у плановой заявки · права: TaskTemplateExcludedAssetDelete · коды: 202, 409
  ← body: TaskTemplateActionData<Int32>[]

## TaskTemplates
- `GET /TaskTemplates` — Возвращает список шаблонов заявок. · права: TaskTemlatesList · paginated · коды: 200, 206
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, assetTypeID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isAllowForMailboxSender?:enum(true, false), isScheduled?:enum(true, false), isScheduleActive?:enum(true, false), taskTemplateID?:str → map<TaskTemplates.ListResult>
- `POST /TaskTemplates` — Создает шаблоны заявок. · права: TaskTemplateAdd · коды: 201, 500
  ← body: TaskTemplate.AddData[] → str[]
- `PUT /TaskTemplates` — Обновляет шаблоны заявок. · права: TaskTemplateUpdate · коды: 202, 500
  ← body: TaskTemplate.UpdateData[]
- `DELETE /TaskTemplates` — Помечает шаблоны заявок, как удаленные. · права: TaskTemplateDelete · коды: 202, 500
  ← body: str[]
- `HEAD /TaskTemplates` — Возвращает заголовок списка шаблонов заявок. · права: TaskTemlatesList · коды: 200
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isAllowForMailboxSender?:enum(true, false), isScheduled?:enum(true, false), isScheduleActive?:enum(true, false), startWithAssetID?:any
- `GET /TaskTemplates/download` — Возвращает архив qr-кодов в формате svg в соответствии с заданными фильтрами · права: TaskTemlatesList · paginated · коды: 200, 206
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isScheduled?:enum(true, false), isScheduleActive?:enum(true, false)
- `GET /TaskTemplates/{id}` — Возвращает шаблон заявки · права: TaskTemplateGet · коды: 200
  ← path: id:str → TaskTemplates.GetResult
- `GET /TaskTemplates/{id}/assignment` — Возвращает список исполнителей, связанных с шаблоном · коды: 200, 500
  ← path: id:str → TaskTemplateAssignmentDetailsProjection
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `POST /TaskTemplates/{id}/assignment` — Связывает исполнителей с шаблоном. · права: TaskTemplateUpdate · коды: 201, 500
  ← path: id:str; body: int[] → TaskTemplateAssignmentMergeProjection[]
- `GET /TaskTemplates/{id}/download` — Возвращает шаблон заявки · права: TaskTemplateGet · коды: 200
  ← path: id:str
- `GET /TaskTemplates/{id}/public` — Возвращает публичный шаблон заявки по идентификатору, который вычисляется как sha256(QrCode) · коды: 200, 500
  ← path: id:str → GetPublicResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `PUT /TaskTemplates/{id}/publish` — Публикует шаблон заявок. · права: TaskTemplatePublish · коды: 202
  ← path: id:str → str
- `GET /TaskTemplates/{id}/schedules` — Получить список сгенерированных событий шаблоной зявки · права: TaskTemplateScheduleList · paginated · коды: 200, 206
  ← path: id:str → GetSchedulesResult[]
- `POST /TaskTemplates/{id}/schedules` — Добавить / удалить шаблонные заявки для расписания · права: TaskTemplateScheduleMerge · коды: 202
  ← path: id:str; body: int[]
- `PUT /TaskTemplates/{id}/unpublish` — Отменяет публикацию шаблона заявок · права: TaskTemplateUnpublish · коды: 202
  ← path: id:str
- `DELETE /TaskTemplates/{taskTemplateID}/excludedAssets/{assetID}` — Удаляет исключенный объект у плановой заявки · права: TaskTemplateExcludedAssetDelete · коды: 202, 409
  ← path: taskTemplateID:str, assetID:int
- `PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/activate` — Активация раписания · права: TaskTemplateScheduleChangeState · коды: 202
  ← path: taskTemplateID:str, scheduleID:int
- `POST /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/appointments` — Регенерация событий для раписания · права: ScheduleAppointmentMerge · коды: 202
  ← path: taskTemplateID:str, scheduleID:int
- `PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/deactivate` — Деактивация раписания · права: TaskTemplateScheduleChangeState · коды: 202
  ← path: taskTemplateID:str, scheduleID:int
- `GET /TaskTemplates/{tasktTemplateID}/excludedAssets` — Возвращает список исключенных объектов для плановой заявки · права: TaskTemplateExcludedAssetList · paginated · коды: 200, 206
  ← path: tasktTemplateID:str → map<TaskTemplateExcludedAssetResult>

## TaskTypeDistrict
- `PUT /TaskTypeDistrict` — Изменение привязки типов заявки к участкам · права: TaskTypeDistrictMerge · коды: 202
  ← body: TaskTypeDistrict.MergeData[]

## TaskTypeRoutes
- `POST /TaskTypeRoutes` — Создает маршруты типов заявок · права: TaskTypeRouteAdd · коды: 201
  ← body: TaskStageRoute.AddData[] → int[]
- `PUT /TaskTypeRoutes` — Изменяет маршрут типов заявок · права: TaskTypeRouteUpdate · коды: 202
  ← body: TaskStageRoute.UpdateData[]
- `DELETE /TaskTypeRoutes` — Удаляет маршруты типов заявок · права: TaskTypeRouteDelete · коды: 202
  ← body: int[]
- `DELETE /TaskTypeRoutes/{id}` — Удаляет маршрут типа заявки · права: TaskTypeRouteDelete · коды: 202, 409
  ← path: id:int

## TaskTypes
- `GET /TaskTypes` — Возвращает список типов заявок, доступных пользователю. Доступность определяется привязкой пользователя к участкам. · права: TaskTypesList · paginated · коды: 200, 206, 500
  ← query: companyID?:any, districtID?:any, assetID?:any, workTypeID?:any → map<TaskTypes.ListResult>
- `POST /TaskTypes` — Создает тип заявки · права: TaskTypeAdd · коды: 201
  ← query: relatedToAnyWorkType?:bool, relatedToAnyWorkType?:enum(true, false); body: TaskType.AddData[] → int[]
- `PUT /TaskTypes` — Изменяет типы заявок · права: TaskTypeUpdate · коды: 202
  ← body: TaskType.UpdateData[]
- `DELETE /TaskTypes` — Помечает типы заявок, как удаленные · права: TaskTypeDelete · коды: 202
  ← body: int[]
- `GET /TaskTypes/{id}` — Возвращает тип заявки · права: TaskTypeGet · коды: 200
  ← path: id:int → TaskTypes.ListResult
- `DELETE /TaskTypes/{id}` — Помечает тип заявки как удаленный · права: TaskTypeDelete · коды: 202, 409
  ← path: id:int
- `GET /TaskTypes/{id}/districts` — Метод получения участков для вида работ · права: TaskTypeDistrictList · paginated · коды: 202, 206
  ← path: id:int → map<TaskTypeDistrictList>
- `GET /TaskTypes/{id}/workTypes` — Возвращает список относящихся к типу задачи видов работ · права: TaskTypesList · paginated · коды: 202, 206
  ← path: id:int → IdNameEntity<Int16>[]
- `POST /TaskTypes/{id}/workTypes` — Привязать список видов работ к типу задачи · права: TaskTypeUpdate · коды: 200
  ← path: id:int; body: int[]
- `DELETE /TaskTypes/{id}/workTypes` — Удалить привязку видов работ к типу задачи · права: TaskTypeUpdate · коды: 200
  ← path: id:int; body: int[]
- `GET /TaskTypes/{taskTypeID}/route` — Возвращает маршрут типа заявки · права: TaskTypeRouteGet · коды: 200
  ← path: taskTypeID:int → RouteResult

## TaskWatchLists
- `POST /TaskWatchLists` — добавляет пользователей в watchlist по заявкам · права: TaskWatchListAdd · коды: 201
  ← body: TaskActionData<Int32>[] → TaskWatchLists.AddResult[]
- `DELETE /TaskWatchLists` — Исключает пользователей из watchlist'а по заявкам · права: TaskWatchListDelete · коды: 202
  ← body: TaskActionData<Int32>[]

## Tasks
- `GET /Tasks` — Возвращает список заявок, доступных пользователю. · права: TasksList · paginated · коды: 200, 206
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), topLevelTasksForHierarchy?:enum(true, false), assetTypeID?:any, assetClassID?:any, districtID?:any, assetResponsibleUserID?:any, branchID?:any, erpID?:str, parentID?:any, assetSchemaID?:any, attributeValues?:str, lastModifiedFrom?:any, lastModifiedTill?:any, contactID?:any, payeeCompanyID?:any → map<Tasks.ListResult>
- `POST /Tasks` — Создаёт заявку · права: TaskAdd · коды: 201, 400, 409, 422 · примеры
  ← body: Task.AddData → Auxiliary.IdResult<System.Int32>
- `DELETE /Tasks` — Помечает заявку как удаленную · права: TaskDelete · коды: 202
  ← body: int[] → TaskDeleteResult[]
- `HEAD /Tasks` — Возвращает заголовок списка заявок для получения количества заявок, удовлетворяющих фильтру. · права: TasksList · коды: 200
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), assetTypeID?:any, assetClassID?:any, erpID?:str, parentID?:any, branchID?:any, assetSchemaID?:any, contactID?:any
- `GET /Tasks/changeTypes` — Возвращает список поддерживаемых в логировании разделов (Tab) и секций этих разделов (Sections) · права: TaskGet · коды: 200, 500
  → ChangeTypeResult[]
- `PUT /Tasks/completedWorks/attributes` — Устанавливает результаты для доп.полей по выполненной работе по заявкам · права: CompletedWorkAttributeMerge · коды: 202
  ← body: ActionData<AttributeData>[] → ActionData<AttributeData>[]
- `DELETE /Tasks/completedWorks/attributes` — Помечает атрибуты выполенной работы заявки удаленные · права: CompletedWorkAttributeDelete · коды: 202
  ← body: ActionData<Int16>[]
- `POST /Tasks/completedWorks/materials` — Добавляет израсходованные материалы к выполненной работе для заявки · права: CompletedWorkMaterialAdd · коды: 201, 409
  ← body: TaskActionData<CompletedWorkMaterialData<Material>>[] → CompletedWorkMaterialPost[]
- `PUT /Tasks/completedWorks/materials` — Изменяет израсходованные материалы у выполненной работы для заявки · права: CompletedWorkMaterialUpdate · коды: 202, 409
  ← body: TaskActionData<CompletedWorkMaterialData<Material>>[]
- `DELETE /Tasks/completedWorks/materials` — Удаляет материалы у выполненных работ по заявке · права: CompletedWorkMaterialDelete · коды: 202, 409
  ← body: TaskActionData<CompletedWorkMaterialData<MaterialDelete>>[]
- `POST /Tasks/completedWorks/report/attachment/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из тела запроса. · права: CompletedWorkReportAttachmentUpload · коды: 201, 500
  ← body: CompletedWorkReportBodyUploadData → CompletedWorkReportAttachment.UploadResult
- `POST /Tasks/completedWorks/report/attachment/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из формы. · права: CompletedWorkReportAttachmentUpload · коды: 201, 500
  ← query: TaskID?:int, JobTitle?:str, Signatory?:str, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → CompletedWorkReportAttachment.UploadResult
- `POST /Tasks/completedWorks/technicians` — Добавляет исполнителей к выполненным работам по заявке · права: CompletedWorkTechnicianAdd · коды: 201, 409
  ← body: TaskActionData<CompletedWorkTechnicianData<Technician>>[] → CompletedWorkTechnicianPost[]
- `PUT /Tasks/completedWorks/technicians` — Изменяет исполнителей у выполненных работы по заявке · права: CompletedWorkTechnicianUpdate · коды: 202, 409
  ← body: TaskActionData<CompletedWorkTechnicianData<Technician>>[]
- `DELETE /Tasks/completedWorks/technicians` — Удаляет исполнителей у выполненных работ по заявке · права: CompletedWorkMaterialDelete · коды: 202, 409
  ← body: TaskActionData<CompletedWorkTechnicianData<Int32>>[]
- `GET /Tasks/count` — Возвращает количество заявок по дням · права: TasksList · коды: 200
  ← query: dateFrom?:datetime, dateTill?:datetime, searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), assetTypeID?:any, assetClassID?:any, districtID?:any, assetResponsibleUserID?:any, branchID?:any, erpID?:str, parentID?:any → map<ListCountResult>
- `GET /Tasks/groupBy/geoHash` — Возвращает краткий список заявок, сгрупированных по хэш-коду геоообласти (кластеризация) · права: TasksList · коды: 200
  ← query: searchText?:str, zoomLevel?:float, disableClustering?:bool, clusteringMode?:ClusteringMode, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, taskTemplateID?:str, requestMethodID?:any, disableClustering?:enum(true, false), clusteringMode?:any → TaskGroupByResult<ClusterResult>[]
- `GET /Tasks/new/meta` — Возвращает метаданные для формы заявки. · права: TaskMetadataGet · коды: 200, 500
  ← query: taskTypeID?:int[] → map<TaskTypeFormMetadataResult>
- `PUT /Tasks/restore` — Воскрешает удаленные заявки · права: TaskRestore · коды: 202, 409
  ← body: int[]
- `GET /Tasks/short` — Возвращает краткий список заявок, доступных пользователю. · права: TasksList · paginated · коды: 200, 206
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), branchID?:any, assetTypeID?:any, assetClassID?:any, erpID?:str, parentID?:any, assetSchemaID?:any, contactID?:any → map<ListShortResult>
- `GET /Tasks/stages/next` — Возвращает список доступных стадий, на котрые могут быть переведены заявки из списка. · права: TaskStagesList · коды: 200, 500
  ← query: id?:int[] → map<ListStagesResult>
- `GET /Tasks/{taskID}` — Возвращает детальные сведения по заявке · права: TaskGet · коды: 200
  ← path: taskID:int; query: taskSnapshotID?:int, includeSchedule?:bool → DetailedInfoResult
- `PUT /Tasks/{taskID}` — Изменяет заявку · права: TaskUpdate · коды: 202, 422
  ← path: taskID:int; body: Task.UpdateData
- `PATCH /Tasks/{taskID}` — Обновляет отдельные поля в заявке · права: TaskUpdate · коды: 202
  ← path: taskID:int; body: PatchData[]
- `DELETE /Tasks/{taskID}` — Помечает заявку как удаленную · права: TaskDelete · коды: 202
  ← path: taskID:int → TaskDeleteResult[]
- `GET /Tasks/{taskID}/assignments` — Возвращает историю назначения заявки · права: TaskAssignmentHistoryList · paginated · коды: 200, 206, 500
  ← path: taskID:int → ListAssignmentHistoryResult
- `GET /Tasks/{taskID}/attachment/{attachmentID}` — Прикрепленный файл к заявке
<param name="taskID">Идентификатор заявки</param><param name="attachmentID">Идентификатор прикрепленного файла к заявке</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: TaskAttachmentGet · коды: 200, 500
  ← path: taskID:int, attachmentID:int; query: thumbnailSize?:int → GetAttachmentResult
- `GET /Tasks/{taskID}/attachments` — Список прикрепленных файлов к заявке
<param name="taskID">Идентификатор заявки</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: TaskAttachmentsList · paginated · коды: 200, 206, 500
  ← path: taskID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: TaskAttachmentDownload · paginated · коды: 206, 303
  ← path: taskID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/attributes` — Возвращает доп.поля по заявке · права: TaskAttributesList · paginated · коды: 200, 206
  ← path: taskID:int; query: isForActualTaskStageOnly?:bool → AttributeResult[]
- `POST /Tasks/{taskID}/autoStaginging` — Активирует запланированный автоматический переход по стадиям заявки · права: TaskStageMoverTerminate · paginated · коды: 202, 206, 404
  ← path: taskID:int
- `DELETE /Tasks/{taskID}/autoStaginging` — Прекращает запланированный автоматический переход по стадиям заявки · права: TaskStageMoverTerminate · paginated · коды: 200, 206, 404
  ← path: taskID:int
- `GET /Tasks/{taskID}/changes` — Возвращает историю изменения заявки · права: TaskGet · paginated · коды: 200, 206, 500
  ← path: taskID:int; query: dateRangeFrom?:any, dateRangeTill?:any, userID?:any, tab?:str, section?:str → HistoryResult[]
- `GET /Tasks/{taskID}/checkCompanyCodeUsed` — Возвращает информацию используется ли код компании при генерации номера заявки · права: IfUsedInTaskNumberGet · коды: 200
  ← path: taskID:int → bool
- `GET /Tasks/{taskID}/checkLists` — Возвращает список чек-листов в заявке · права: TaskCheckListsList · paginated · коды: 200, 206
  ← path: taskID:int → map<TaskCheckListResult>
- `POST /Tasks/{taskID}/checkLists` — Добавляет чек-листы к заявке · права: TaskCheckListAdd · коды: 201
  ← path: taskID:int; body: TaskCheckList.AddData[] → TaskCheckLists.PostResult[]
- `DELETE /Tasks/{taskID}/checkLists` — Помечает чек-листы заявки как удаленные · права: TaskCheckListDelete · коды: 202
  ← path: taskID:int; body: int[]
- `POST /Tasks/{taskID}/checkLists/{taskCheckListID}` — Добавляет чек-лист к заявке · права: TaskCheckListAdd · коды: 201
  ← path: taskID:int, taskCheckListID:int → TaskCheckLists.PostResult[]
- `DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}` — Помечает чек-лист заявки как удаленный · права: TaskCheckListDelete · коды: 202
  ← path: taskID:int, taskCheckListID:int
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Возвращает результаты чек-листа для заявки · права: TaskCheckListResultsList · paginated · коды: 200, 206
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultResult>
- `PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Устанавливает результаты для элементов чек-листа заявки · права: TaskCheckListResultSet · коды: 202
  ← path: taskID:int, taskCheckListID:int; body: TaskCheckListResult.UpdateData[] → TaskChecListResults.PostResult[]
- `DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Помечает результы чек-листа заявки как удаленные · права: TaskCheckListResultDelete · коды: 202
  ← path: taskID:int, taskCheckListID:int; body: int[]
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · права: TaskCheckListResultAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Возвращает результаты чек-листа для заявки · права: TaskCheckListResultsList · paginated · коды: 200, 206
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultV2Result>
- `PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Устанавливает результаты для элементов чек-листа заявки · права: TaskCheckListResultSet · коды: 202
  ← path: taskID:int, taskCheckListID:int; body: UpdateDataV2[] → TaskChecListResults.PostResult[]
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · права: TaskCheckListResultAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments/{attachmentID}` — Получает информацию о прикрепленном к чек-листу по завке файле · права: TaskCheckListResultAttachmentGet · коды: 200, 204, 500
  ← path: taskID:int, taskCheckListID:int, taskChecklistResultID:int, attachmentID:int
- `POST /Tasks/{taskID}/checkLists/{taskCheckListID}/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к чек-листу по заявке. Данные будут получены из формы. · права: TaskCheckListResultAttachmentUpload · коды: 201, 500
  ← path: taskID:int, taskCheckListID:int; body: { Attachments?: TaskCheckListResultAttachment[] /* Вложения в чек- листе по заявке */, TaskCheckListID?: int /* Идентификатор чек- листа по заявке */, TaskCheckListResultID?: int /* Идентификатор результата чек- листа по заявке */ } → TaskCheckListResultAttachment.UploadResult
- `PUT /Tasks/{taskID}/complete` — Помечает заявку, как выполненную · права: TaskComplete · коды: 202
  ← path: taskID:int; body: TaskCompletion.AddData
- `GET /Tasks/{taskID}/completedWorks` — Возвращает список выполненных работ по заявке · права: CompletedWorkList · paginated · коды: 200, 206, 500
  ← path: taskID:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/attachments` — Возвращает список вложенных файлов во все выполненные работы в заявке · права: CompletedWorkAttachmentList · paginated · коды: 200, 206, 500
  ← path: taskID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/attributes` — Возвращает доп.поля для выполненных работ по заявке · права: CompletedWorkAttributeList · paginated · коды: 200, 206
  ← path: taskID:int; query: completedWorkID?:any → CompletedWorkAttributeResult[]
- `GET /Tasks/{taskID}/completedWorks/materials` — Список израсходованных материалов для выполненных работ по заявке · права: CompletedWorkMaterialsList · paginated · коды: 200, 204, 206, 500
  ← path: taskID:int → map<CompletedWorkMaterialResult>
- `GET /Tasks/{taskID}/completedWorks/materialsWithCodes` — Список израсходованных материалов для выполненных работ по заявке (включая коды маркировки). · права: CompletedWorkMaterialsList · paginated · коды: 200, 204, 206, 500
  ← path: taskID:int → map<CompletedWorkMaterialResult>
- `GET /Tasks/{taskID}/completedWorks/report/attachment` — Получает подпись к акту выполненной работы · права: CompletedWorkReportAttachmentGet · коды: 200, 204, 500
  ← path: taskID:int
- `POST /Tasks/{taskID}/completedWorks/report/attachment/v2/{attachmentID}` — Добавляет загруженный ранее вложенный файл к акту выполненной работы · права: CompletedWorkReportAttachmentAdd · коды: 201, 500
  ← path: taskID:int, attachmentID:int; body: AddSignedData
- `POST /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}` — Добавляет загруженный ранее вложенный файл к акту выполненной работы · права: CompletedWorkReportAttachmentAdd · коды: 201, 500
  ← path: taskID:int, attachmentID:int
- `DELETE /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}` — Помечает прикрепленный файл к акту выполненной работы как удаленный · права: CompletedWorkReportAttachmentDelete · коды: 202, 500
  ← path: taskID:int, attachmentID:int
- `GET /Tasks/{taskID}/completedWorks/technicians` — Список исполнителей для выполненных работ по заявке · права: CompletedWorkTechnicianList · коды: 200, 204
  ← path: taskID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments` — Возвращает список вложенных файлов по выполненной работе в заявке · права: CompletedWorkAttachmentList · paginated · коды: 200, 206, 500
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: CompletedWorkAttachmentDownload · paginated · коды: 206, 303, 500
  ← path: taskID:int, attachmentID:int, completedWorkID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Возвращает доп.поля для выполненной работы по заявке · права: CompletedWorkAttributeList · paginated · коды: 200, 206
  ← path: taskID:int, completedWorkID:int → CompletedWorkAttributeResult[]
- `PUT /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Устанавливает результаты для доп.полей по выполненной работе по заявке · права: CompletedWorkAttributeMerge · коды: 202
  ← path: taskID:int, completedWorkID:int; body: AttributeData[] → CompletedWorkAttributeMergeResult[]
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Помечает атрибуты выполенной работы заявки удаленный · права: CompletedWorkAttributeDelete · коды: 202
  ← path: taskID:int, completedWorkID:int; body: int[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/attachments` — Возвращает список файлов прикрепленных к атрибутам выполенной работы по заявке · права: CompletedWorkAttributeAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int, attributeID?:any → map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}` — Помечает атрибут выполенной работы заявки удаленный · права: CompletedWorkAttributeDelete · коды: 202
  ← path: taskID:int, completedWorkID:int, attributeID:int
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}/attachments` — Возвращает список файлов прикрепленных к атрибуту выполненной работы по заявке · права: CompletedWorkAttributeAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, completedWorkID:int, attributeID:int; query: thumbnailSize?:int → map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Список израсходованных материалов для выполненной работы по заявке · права: CompletedWorkMaterialsList · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkMaterialResult
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Удаляет материалы у выполненной работы по заявке · права: CompletedWorkMaterialDelete · коды: 202, 409
  ← path: taskID:int, completedWorkID:int; body: MaterialDelete
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Список исполнителей для выполненной работы по заявке · права: CompletedWorkTechnicianList · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkTechnicianResult
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Удаляет исполнителей у выполненной работы по заявке · права: CompletedWorkMaterialDelete · коды: 202, 409
  ← path: taskID:int, completedWorkID:int; body: int[]
- `POST /Tasks/{taskID}/completedWorks/{completedWorkID}/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к чек-листу по заявке. Данные будут получены из формы. · права: CompletedWorkAttributeAttachmentUpload · коды: 201, 500
  ← path: taskID:int, completedWorkID:int; body: { Attachments?: CompletedWorkAttributeAttachment[] /* Вложения в атрибуте выполненной работы по заявке */, AttributeID?: int /* Идентификатор атрибута выполненной работы по заявке */, CompletedWorkID?: int /* Идентификатор выполненной работы по заявке */ } → CompletedWorkAttachments.UploadResult
- `GET /Tasks/{taskID}/completedWorks/{id}` — Получает информацию о выполненной работе по заявкам · права: CompletedWorkGet · коды: 200, 500
  ← path: taskID:int, id:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/contacts` — Возвращает список контактов заявки · права: TaskContactsList · paginated · коды: 200, 206, 400
  ← path: taskID:int → map<TaskContacts.ListResult>
- `GET /Tasks/{taskID}/contacts/{contactID}` — Возвращает контакт заявки · права: TaskContactGet · коды: 200
  ← path: taskID:int, contactID:int → TaskContacts.GetResult
- `DELETE /Tasks/{taskID}/contacts/{contactID}` — Удаляет контактное лицо у заявки · права: TaskContactDelete · коды: 202, 409
  ← path: taskID:int, contactID:int
- `POST /Tasks/{taskID}/conversation` — Добавляет сообщения по заявкам. · права: TaskConversationAdd · коды: 201, 500
  ← path: taskID:int; body: TaskConversationData → TaskConversations.AddResult[]
- `POST /Tasks/{taskID}/conversation/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к сообщению по заявке. Данные будут получены из формы. · права: TaskConversationAttachmentUpload · коды: 201, 500
  ← path: taskID:int; body: { Attachments?: TaskConversationAttachment[] /* Вложения в сообщение по заявке */, IsExternal?: bool /* Чат с командой или Заказчиком */, Message?: str /* Сообщение по заявке */ } → TaskConversations.UploadResult
- `GET /Tasks/{taskID}/conversations` — Возвращает сообщения по заявке
<param name="taskID">Идентификатор заявки</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param><param name="searchText">Текст для поиска в сообщениях по заявке</param> · права: TaskConversationsList · paginated · коды: 200, 206
  ← path: taskID:int; query: thumbnailSize?:int, searchText?:str, isRead?:enum(true, false) → TaskMessage[]
- `HEAD /Tasks/{taskID}/conversations` — Возвращает заголовок списка сообщений по заявке
(для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="taskID">Идентификатор заявки</param><param name="searchText">Текст для поиска в сообщениях по заявке</param> · права: TaskConversationsList · коды: 200
  ← path: taskID:int; query: searchText?:str, isRead?:enum(true, false), isExternal?:enum(true, false)
- `GET /Tasks/{taskID}/conversations/{taskConversationID}` — Возвращает сообщение по заявке
<param name="taskID">Идентификатор заявки</param><param name="taskConversationID">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · права: TaskConversationGet · paginated · коды: 200, 206
  ← path: taskID:int, taskConversationID:int; query: thumbnailSize?:int → TaskMessage
- `GET /Tasks/{taskID}/conversations/{taskConversationID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: TaskConversationAttachmentDownload · paginated · коды: 206, 303, 500
  ← path: taskID:int, attachmentID:int, taskConversationID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/conversations/{taskConversationID}/delivery` — Возвращает информацию по доставке и прочтению сообщения по заявке.
<param name="taskID">Идентификатор заявки</param><param name="taskConversationID">Идентификатор сообщения</param> · права: TaskConversationDeliveryList · paginated · коды: 200, 206, 500
  ← path: taskID:int, taskConversationID:int → ListConversationDeliveryResult[]
- `GET /Tasks/{taskID}/materials` — Возвращает список необходимых материалов для заявки · права: TaskMaterialsList · paginated · коды: 200, 206
  ← path: taskID:int → map<TaskMaterials.ListResult>
- `GET /Tasks/{taskID}/meta` — Возвращает метаданные для формы заявки. · права: TaskMetadataGet · коды: 200, 500
  ← path: taskID:int → TaskTypeFormMetadataResult
- `GET /Tasks/{taskID}/ratings` — Возвращает отзывы/рейтинги инжененров по заявке. · права: TaskTechnicianRatingList · paginated · коды: 200, 206, 500
  ← path: taskID:int → RatingResult[]
- `GET /Tasks/{taskID}/ratings/avg` — Возвращает отзывы/рейтинги инжененров по заявке. · права: TaskTechnicianRatingList · paginated · коды: 200, 206, 500
  ← path: taskID:int → RatingResult[]
- `GET /Tasks/{taskID}/skills` — Возвращает список навыков заявки · права: TaskSkillList · paginated · коды: 200, 206, 500
  ← path: taskID:int → map<TaskSkillResult>
- `GET /Tasks/{taskID}/stages` — Возвращает историю перемещения заявки по стадиям. · права: TaskStagingHistoryList · paginated · коды: 200, 206, 500
  ← path: taskID:int; query: includeChangeset?:bool, actionLocationState?:ActionLocationState → ListStagingHistoryResult
- `GET /Tasks/{taskID}/stages/next` — Возвращает список доступных стадий, на котрые может быть переведена заявка. · права: TaskStagesList · paginated · коды: 200, 206, 500
  ← path: taskID:int → map<ListStagesResult>
- `GET /Tasks/{taskID}/tags` — Возвращает тэги по заявке. · права: TaskTagsList · paginated · коды: 200, 206, 500
  ← path: taskID:int → str[]
- `GET /Tasks/{taskID}/watchLists` — WatchList по заявке · права: TaskWatchListList · paginated · коды: 200, 206, 500
  ← path: taskID:int; query: searchText?:str → TaskWatchLists.ListResult[]
- `DELETE /Tasks/{taskId}/completedWorks/marking-codes` — Удаляет все коды маркировки по заявке (во всех выполненных работах). · права: CompletedWorkMaterialDelete · коды: 200, 204 · примеры
  ← path: taskId:int → TaskCompletedWorksMarkingCodesDeleteResult
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes` — Возвращает коды маркировки для выполненной работы (все материалы). · права: CompletedWorkMaterialsList · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int → MarkingCodesListResult
- `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетная привязка кодов маркировки к материалам выбранной выполненной работы. · права: CompletedWorkMaterialUpdate · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesUpsertRequest → CompletedWorkMaterialsMarkingCodesUpsertResult
- `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетная перепривязка (перенос) существующих активных кодов маркировки у материалов выбранной выполненной работы. · права: CompletedWorkMaterialUpdate · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesUpdateRequest → CompletedWorkMaterialsMarkingCodesUpdateResult
- `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетное удаление привязанных кодов маркировки у материалов выбранной выполненной работы. · права: CompletedWorkMaterialDelete · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesDeleteRequest → CompletedWorkMaterialsMarkingCodesDeleteResult
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Возвращает коды маркировки для конкретного материала в выполненной работе. · права: CompletedWorkMaterialsList · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; query: warehouseID?:any → MarkingCodesListResult
- `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Пакетная привязка кодов маркировки к материалу. · права: CompletedWorkMaterialUpdate · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesUpsertForMaterialRequest → MarkingCodesUpsertResult
- `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Пакетная перепривязка (перенос) существующих активных кодов маркировки на указанный материал. · права: CompletedWorkMaterialUpdate · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesUpdateForMaterialRequest → MarkingCodesUpdateResult
- `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Удаление привязанных кодов маркировки у материала. · права: CompletedWorkMaterialDelete · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesDeleteForMaterialRequest → MarkingCodesDeleteResult
- `GET /Tasks/{taskId}/marking-codes` — Возвращает коды маркировки для заявки (все выполненные работы). · права: TaskGet · коды: 200, 204 · примеры
  ← path: taskId:int → MarkingCodesListResult

## TemplateQuickResponse
- `GET /TemplateQuickResponse` — Возвращает список быстрых ответов · права: QuickResponseList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), taskTypeID?:any → map<TemplateQuickResponse.ListResult>
- `POST /TemplateQuickResponse` — Создаёт новый быстрый ответ · права: QuickResponseAdd · коды: 201, 409
  ← body: TemplateQuickResponse.AddData[] → int[]
- `PUT /TemplateQuickResponse` — Обновляет быстрый ответ. · права: QuickResponseUpdate · коды: 202, 500
  ← body: TemplateQuickResponse.UpdateData[]
- `DELETE /TemplateQuickResponse` — Помечает быстрые ответы, как удалённые · права: QuickResponseDelete · коды: 202, 409
  ← body: int[]
- `PUT /TemplateQuickResponse/taskTypes` — Создает или изменяет привязку быстрых ответов к типам заявок. · права: TaskTypeQuickResponseMerge · коды: 202, 500
  ← body: TemplateQuickResponse.MergeData[]
- `GET /TemplateQuickResponse/{id}` — Возвращает быстрый ответ · права: QuickResponseGet · коды: 200
  ← path: id:int → TemplateQuickResponse.GetResult

## UserTaskFavourites
- `POST /UserTaskFavourites` — Добавляет заявки в список избранных для текущего пользователя. · права: UserTaskFavouriteAdd · paginated · коды: 201, 206, 500
  ← body: int[]
- `DELETE /UserTaskFavourites` — Добавляет заявки в список избранных для текущего пользователя. · права: UserTaskFavouriteDelete · paginated · коды: 202, 206, 500
  ← body: int[]

## WorkTypes
- `GET /WorkTypes` — Возвращает список видов работ. · права: WorkTypeList · paginated · коды: 200, 206
  ← query: searchText?:str, assetID?:any, taskTypeID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false), erpID?:str → map<WorkTypes.ListResult>
- `POST /WorkTypes` — Создает вид работ · права: WorkTypeAdd · коды: 201
  ← query: relatedToAnyTaskType?:bool, relatedToAnyAsset?:bool, relatedToAnyTaskType?:enum(true, false); body: WorkType.AddData[] → int[]
- `PUT /WorkTypes` — Изменяет виды работ · права: WorkTypeUpdate · коды: 202
  ← body: WorkType.UpdateData[]
- `DELETE /WorkTypes` — Помечает виды работ, как удаленные · права: WorkTypeDelete · коды: 202
  ← body: int[]
- `PUT /WorkTypes/publish` — Публикует выполненные работы · права: WorkTypePublish · коды: 202
  ← body: int[]
- `PUT /WorkTypes/unpublish` — Отменяет публикацию выполненных работы · права: WorkTypeUnpublish · коды: 202
  ← body: int[]
- `GET /WorkTypes/{id}` — Возвращает данные для вида работы. · права: WorkTypeGet · paginated · коды: 200, 206, 500
  ← path: id:int → WorkTypes.GetResult
- `DELETE /WorkTypes/{id}` — Помечает вид работ как удаленный · права: WorkTypeDelete · коды: 202, 409
  ← path: id:int
- `PUT /WorkTypes/{id}/publish` — Помечает вид работ как опубликованный · права: WorkTypePublish · коды: 202
  ← path: id:int
- `GET /WorkTypes/{id}/taskTypes` — Возвращает список относящихся к виду работ типов задач · права: TaskTypesList · paginated · коды: 202, 206
  ← path: id:int → IdNameEntity<Byte>[]
- `POST /WorkTypes/{id}/taskTypes` — Привязать список типов задач к виду работ · права: TaskTypeUpdate · коды: 200
  ← path: id:int; body: int[]
- `DELETE /WorkTypes/{id}/taskTypes` — Удалить привязку типу задач к виду работ · права: TaskTypeUpdate · коды: 200
  ← path: id:int; body: int[]
- `PUT /WorkTypes/{id}/unpublish` — Помечает вид работ как опубликованный · права: WorkTypeUnpublish · коды: 202
  ← path: id:int
- `GET /WorkTypes/{parentWorkTypeID}/workTypes` — Возвращает список дочерних видов работ (вниз по графу). · права: WorkTypeList · paginated · коды: 200, 206, 500
  ← path: parentWorkTypeID:int; query: searchText?:str, assetID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false) → map<WorkTypes.ListResult>
- `GET /WorkTypes/{parentWorkTypeID}/workTypes/all` — Возвращает список всех дочерних видов работ (вниз по графу). · права: WorkTypeList · paginated · коды: 200, 206, 500
  ← path: parentWorkTypeID:int; query: searchText?:str, assetID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false) → map<WorkTypes.ListResult>
- `GET /WorkTypes/{workTypeID}/checkLists` — Возвращает список чек-листов вида работ · права: WorkTypeCheckListList · paginated · коды: 200, 206
  ← path: workTypeID:int → map<CheckLists.GetResult[]>
- `POST /WorkTypes/{workTypeID}/checkLists` — Добавляет чек-листы к типу работ · права: WorkTypeCheckListAdd · коды: 202
  ← path: workTypeID:int; body: int[]
- `DELETE /WorkTypes/{workTypeID}/checkLists` — Помечает чек-листы у типа работ как удаленные · права: WorkTypeCheckListDelete · коды: 202
  ← path: workTypeID:int; body: int[]
- `POST /WorkTypes/{workTypeID}/checkLists/{checkListID}` — Добавляет чек-лист к типу работ · права: WorkTypeCheckListAdd · коды: 202
  ← path: workTypeID:int, checkListID:int
- `DELETE /WorkTypes/{workTypeID}/checkLists/{checkListID}` — Помечает чек-лист у типа работ как удаленный · права: WorkTypeCheckListDelete · коды: 202
  ← path: workTypeID:int, checkListID:int
