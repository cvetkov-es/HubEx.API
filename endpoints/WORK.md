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
- `POST /CheckListItems` — Изменяет элементы чек-листов · коды: 202
  ← body: WORKCLIMergeData[] → ICheckListItemMergeEntity
- `DELETE /CheckListItems` — Помечает результат чек-листа по заявке как удаленный · коды: 202
  ← body: WORKCLIDeleteData[]

## CheckLists
- `GET /CheckLists` — Возвращает список активных чек-листов · коды: 200
  ← query: searchText?:str → map<RCLListResult>
- `POST /CheckLists` — Создает чек-листы · коды: 201
  ← body: WORKCLAddData[] → int[]
- `PUT /CheckLists` — Изменяет чек-листы · коды: 202
  ← body: WORKCLUpdateData[]
- `DELETE /CheckLists` — Помечает чек-листы, как удаленные · коды: 202
  ← body: int[]
- `POST /CheckLists/{checkListID}/assign` — Проставляпет идентификаторы чек-листов в таблицах объектов и видов работ · коды: 202
  ← path: checkListID:int; body: CheckListAssignmentData
- `DELETE /CheckLists/{checkListID}/assign` — Удаляет идентификаторы чек-листов из таблиц объектов и видов работ · коды: 202
  ← path: checkListID:int; body: CheckListAssignmentData
- `GET /CheckLists/{checkListID}/items` — Возвращает элементы чек-листа · коды: 200
  ← path: checkListID:int → map<CheckListItemResult>
- `GET /CheckLists/{id}` — Возвращает чек-лист · коды: 200
  ← path: id:int → map<RCLGetResult>
- `DELETE /CheckLists/{id}` — Помечает чек-лист, как удаленный · коды: 202, 409
  ← path: id:int

## CompletedWorkAttachments
- `POST /CompletedWorkAttachments` — Добавляет загруженный ранее вложенный файл к выполненной работе · коды: 201, 500
  ← body: TaskActionDataOfWORKCWAAddData[] → RCWAAddResult[]
- `DELETE /CompletedWorkAttachments` — Помечает прикрепленный к выполненной работе файл как удаленный · коды: 202, 500
  ← body: TaskActionDataOfWORKCWADeleteData[]
- `POST /CompletedWorkAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из тела запроса. · коды: 201, 500
  ← body: CompletedWorkBodyUploadData → RCWAUploadResult
- `POST /CompletedWorkAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из формы. · коды: 201, 500
  ← query: TaskID?:int, CompletedWorkID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → RCWAUploadResult

## CompletedWorks
- `POST /CompletedWorks` — Создаёт выполненные работы по одной или нескольким заявкам · коды: 200, 201, 400, 409 · примеры
  ← body: TaskActionDataOfWORKCWAddData[] → RCWAddResult[]
- `PUT /CompletedWorks` — Изменяет выполненные работы по заявкам · коды: 202 · примеры
  ← body: TaskActionDataOfWORKCWUpdateData[]
- `DELETE /CompletedWorks` — Помечает выполненные работы по заявкам как удалённые · коды: 202 · примеры
  ← body: TaskActionDataOfShort[]

## RequestMethods
- `GET /RequestMethods` — Возвращает список методов подачи заявок. · коды: 200
  → map<RRMListResult>

## TaskActualities
- `GET /TaskActualities` — Возвращает список актуальностей заявок · коды: 200
  → map<RTAListResult>
- `POST /TaskActualities` — Создает актуальности заявки · коды: 201
  ← body: WORKTAAddData[] → int[]
- `PUT /TaskActualities` — Изменяет актуальности заявок · коды: 202
  ← body: WORKTAUpdateData[]
- `DELETE /TaskActualities` — Помечает актуальности заявок, как удаленные · коды: 202
  ← body: int[]
- `GET /TaskActualities/{id}` — Возвращает актуальность заявки · коды: 200
  ← path: id:int → RTAListResult
- `DELETE /TaskActualities/{id}` — Помечает актуальность заявки как удаленную · коды: 202, 409
  ← path: id:int

## TaskAssignmentHistory
- `POST /TaskAssignmentHistory` — Назначает новые заявки на пользователя. · коды: 201, 500
  ← body: DTAHPostData[] → RTAHAddResult[]

## TaskAttachments
- `POST /TaskAttachments` — Свзяывает заявку и вложение · коды: 201, 500
  ← body: TaskActionDataOfInt[] → RTAPostResult[]
- `DELETE /TaskAttachments` — Помечает связку заявки и вложения как удаленную · коды: 202, 500
  ← body: TaskActionDataOfInt[]
- `POST /TaskAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к заявке. Данные будут получены из тела запроса. · коды: 201, 500
  ← body: TaskBodyUploadData → RTAUploadResult
- `POST /TaskAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к заявке. Данные будут получены из формы. · коды: 201, 500
  ← query: TaskID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → RTAUploadResult

## TaskAttributes
- `GET /TaskAttributes` — Возвращает значения атрибутов по заявкам · коды: 200
  → TaskAttributesResult[]
- `POST /TaskAttributes` — Изменяет значения атрибутов по заявкам · коды: 202
  ← body: WORKTAActionData[]

## TaskContacts
- `POST /TaskContacts` — Добавляет контактные лица к заявке · коды: 201, 409
  ← body: TaskActionDataOfInt[] → RTCPostResult
- `DELETE /TaskContacts` — Удаляет контактные лица у заявки · коды: 202, 409
  ← body: TaskActionDataOfInt[]

## TaskConversationDeliveries
- `PUT /TaskConversationDeliveries/read` — Устанавливает отметки о прочтении сообщений по заявкам · коды: 202
  ← body: TaskActionDataOfSetReadData[]
- `PUT /TaskConversationDeliveries/read/All` — Устанавливает отметки о прочтении всех сообщений по заявкам · коды: 202

## TaskConversations
- `GET /TaskConversations` — Возвращает список сообщений по заявкам, доступным пользователю.
<param name="searchText">Текст для поиска в сообщениях по заявкам</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200
  ← query: searchText?:str, thumbnailSize?:int → TaskMessageLast[]
- `DELETE /TaskConversations` — Помечает сообщения по заявкам как удаленные. · коды: 202, 500
  ← body: WORKTCDeleteData[]
- `HEAD /TaskConversations` — Возвращает заголовок списка сообщений по заявке (для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="searchText">Текст для поиска в сообщениях по заявкам</param> · коды: 200
- `DELETE /TaskConversations/remove` — Помечает сообщения по заявкам как удаленные. · коды: 202, 500
  ← body: WORKTCDeleteData[]

## TaskFilter
- `GET /TaskFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · коды: 200
  ← query: selectedOnly?:bool → FilterListItemProjection[]
- `PUT /TaskFilter` — Обновляет список доступных, для выполняющего операцию пользователя, фильтров и порядок их сортировки · коды: 202
  ← body: COMMONUIFFilterData[]

## TaskListQueries
- `GET /TaskListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · коды: 200
  → map<TaskListQueryResult>
- `POST /TaskListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю · коды: 201
  ← body: WORKTLQAddData[] → int[]
- `PUT /TaskListQueries` — Изменяет сохраненный запрос · коды: 202
  ← body: WORKTLQUpdateData[]
- `DELETE /TaskListQueries` — Помечает сохраненные запрос как даленный · коды: 202
  ← body: int[]
- `DELETE /TaskListQueries/remove` — Помечает сохраненные запрос как даленный · коды: 202
  ← body: int[]
- `GET /TaskListQueries/{id}` — Возвращает сохраненный запрос · коды: 200
  ← path: id:int → map<TaskListQueryResult>
- `DELETE /TaskListQueries/{id}` — Помечает сохраненный запрос как даленный · коды: 202
  ← path: id:int
- `DELETE /TaskListQueries/{id}/remove` — Помечает сохраненный запрос как даленный · коды: 202
  ← path: id:int

## TaskMaterials
- `POST /TaskMaterials` — Добавляет, изменяет необходимые материалы к заявкам · коды: 201, 409
  ← body: TaskActionDataOfWORKTMMergeData[] → RTMPostResult
- `PUT /TaskMaterials` — Изменяет необходимые материалы в заявках · коды: 202, 409
  ← body: TaskActionDataOfWORKTMUpdateData[]
- `DELETE /TaskMaterials` — Удаляет необходимые материалы из заявок · коды: 202, 409
  ← body: TaskActionDataOfShort[]
- `PUT /TaskMaterials/takeOff` — Убирает признак взятия необходимых материалов из заявок · коды: 202, 409
  ← body: TaskActionDataOfShort[]
- `PUT /TaskMaterials/takeOn` — Проставляет признак взятия необходимых материалов из заявок · коды: 202, 409
  ← body: TaskActionDataOfTakeOnData[]

## TaskOrderBy
- `GET /TaskOrderBy` — Возвращает список методов сортировки заявок · коды: 200
  → map<RTOBListResult>

## TaskRatings
- `POST /TaskRatings` — Создает оценки по заявкам · коды: 202, 500
  ← body: WORKTTRMergeData[]

## TaskSkills
- `POST /TaskSkills` — Добавляет навыки к заявкам · коды: 201, 409
  ← body: TaskActionDataOfInt[] → RTSPostResult
- `DELETE /TaskSkills` — Удаялет навыки из заявок · коды: 202, 409
  ← body: TaskActionDataOfInt[]

## TaskStagingHistory
- `POST /TaskStagingHistory` — Добавляет актуальную запись в историю прохождения заявки по стадиям. · коды: 201, 404, 409, 500
  ← body: DTSHPostData
- `POST /TaskStagingHistory/batch` — Массовый перевод заявок по стадиям. · коды: 202, 409, 500
  ← body: BatchRequestPostData → BatchRequestResult
- `POST /TaskStagingHistory/multiple` — Массовый перевод заявок по стадиям. · коды: 202, 500
  ← body: DTSHPostData[] → BatchRequestResult

## TaskStatuses
- `GET /TaskStatuses` — Возвращает список статусов заявок · коды: 200, 500
  → map<RTSListResult>
- `POST /TaskStatuses` — Создает статус заявки · коды: 201
  ← body: WORKTSAddData[] → int[]
- `PUT /TaskStatuses` — Изменяет статусы заявок · коды: 202
  ← body: WORKTSUpdateData[]
- `DELETE /TaskStatuses` — Помечает статусы заявок, как удаленные · коды: 202
  ← body: int[]
- `GET /TaskStatuses/{id}` — Возвращает статус заявки · коды: 200
  ← path: id:int → RTSListResult
- `DELETE /TaskStatuses/{id}` — Помечает статус заявки как удаленный · коды: 202, 409
  ← path: id:int

## TaskTags
- `POST /TaskTags` — Привязывает тэг к заявке. Если указанный тэг отсутствует в справочнике, создает его. · коды: 201, 409
  ← body: WORKTaskTagAddData[]
- `DELETE /TaskTags` — Исключает тэг из заявки. В справочнике тэг остается. · коды: 202, 409
  ← body: WORKTTDeleteData[]

## TaskTemplateExcludedAssets
- `POST /TaskTemplateExcludedAssets` — Добавляет или изменяет исключенные объекты к плановой заявке · коды: 201, 409
  ← body: TaskTemplateActionDataOfInt[] → TaskTemplateExcludedAssetMergeResult
- `DELETE /TaskTemplateExcludedAssets` — Удаляет исключенные объекты у плановой заявки · коды: 202, 409
  ← body: TaskTemplateActionDataOfInt[]

## TaskTemplates
- `GET /TaskTemplates` — Возвращает список шаблонов заявок. · коды: 200
  ← query: searchText?:str, isPublic?:bool → map<RTaskTemplatesListResult>
- `POST /TaskTemplates` — Создает шаблоны заявок. · коды: 201, 500
  ← body: WORKTaskTemplateAddData[] → str[]
- `PUT /TaskTemplates` — Обновляет шаблоны заявок. · коды: 202, 500
  ← body: WORKTaskTemplateUpdateData[]
- `DELETE /TaskTemplates` — Помечает шаблоны заявок, как удаленные. · коды: 202, 500
  ← body: str[]
- `HEAD /TaskTemplates` — Возвращает заголовок списка шаблонов заявок. · коды: 200
  ← query: searchText?:str, isPublic?:bool
- `GET /TaskTemplates/download` — Возвращает архив qr-кодов в формате svg в соответствии с заданными фильтрами · коды: 200
  ← query: searchText?:str, isPublic?:bool
- `GET /TaskTemplates/{id}` — Возвращает шаблон заявки · коды: 200
  ← path: id:str → RTaskTemplatesGetResult
- `GET /TaskTemplates/{id}/assignment` — Возвращает список исполнителей, связанных с шаблоном · коды: 200, 500
  ← path: id:str → TaskTemplateAssignmentDetailsProjection
  Выполнение данного метода разрешено от **анонимного пользователя**.
- `POST /TaskTemplates/{id}/assignment` — Связывает исполнителей с шаблоном. · коды: 201, 500
  ← path: id:str; body: int[] → TaskTemplateAssignmentMergeProjection[]
- `GET /TaskTemplates/{id}/download` — Возвращает шаблон заявки · коды: 200
  ← path: id:str
- `GET /TaskTemplates/{id}/public` — Возвращает публичный шаблон заявки по идентификатору, который вычисляется как sha256(QrCode) · коды: 200, 500
  ← path: id:str → GetPublicResult
  Выполнение данного метода разрешено от **анонимного пользователя**.
- `PUT /TaskTemplates/{id}/publish` — Публикует шаблон заявок. · коды: 202
  ← path: id:str → str
- `GET /TaskTemplates/{id}/schedules` — Получить список сгенерированных событий шаблоной зявки · коды: 200
  ← path: id:str → GetSchedulesResult[]
- `POST /TaskTemplates/{id}/schedules` — Добавить / удалить шаблонные заявки для расписания · коды: 202
  ← path: id:str; body: int[]
- `PUT /TaskTemplates/{id}/unpublish` — Отменяет публикацию шаблона заявок · коды: 202
  ← path: id:str
- `DELETE /TaskTemplates/{taskTemplateID}/excludedAssets/{assetID}` — Удаляет исключенный объект у плановой заявки · коды: 202, 409
  ← path: taskTemplateID:str, assetID:int
- `PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/activate` — Активация раписания · коды: 202
  ← path: taskTemplateID:str, scheduleID:int
- `POST /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/appointments` — Регенерация событий для раписания · коды: 202
  ← path: taskTemplateID:str, scheduleID:int
- `PUT /TaskTemplates/{taskTemplateId}/schedules/{scheduleId}/deactivate` — Деактивация раписания · коды: 202
  ← path: taskTemplateID:str, scheduleID:int
- `GET /TaskTemplates/{tasktTemplateID}/excludedAssets` — Возвращает список исключенных объектов для плановой заявки · коды: 200
  ← path: tasktTemplateID:str → map<TaskTemplateExcludedAssetResult>

## TaskTypeDistrict
- `PUT /TaskTypeDistrict` — Изменение привязки типов заявки к участкам · коды: 202
  ← body: WORKTTDMergeData[]

## TaskTypeRoutes
- `POST /TaskTypeRoutes` — Создает маршруты типов заявок · коды: 201
  ← body: TSTGTSRAddData[] → int[]
- `PUT /TaskTypeRoutes` — Изменяет маршрут типов заявок · коды: 202
  ← body: TSTGTSRUpdateData[]
- `DELETE /TaskTypeRoutes` — Удаляет маршруты типов заявок · коды: 202
  ← body: int[]
- `DELETE /TaskTypeRoutes/{id}` — Удаляет маршрут типа заявки · коды: 202, 409
  ← path: id:int

## TaskTypes
- `GET /TaskTypes` — Возвращает список типов заявок, доступных пользователю. Доступность определяется привязкой пользователя к участкам. · коды: 200, 500
  → map<RTaskTypesListResult>
- `POST /TaskTypes` — Создает тип заявки · коды: 201
  ← query: relatedToAnyWorkType?:bool; body: WORKTaskTypeAddData[] → int[]
- `PUT /TaskTypes` — Изменяет типы заявок · коды: 202
  ← body: WORKTaskTypeUpdateData[]
- `DELETE /TaskTypes` — Помечает типы заявок, как удаленные · коды: 202
  ← body: int[]
- `GET /TaskTypes/{id}` — Возвращает тип заявки · коды: 200
  ← path: id:int → RTaskTypesListResult
- `DELETE /TaskTypes/{id}` — Помечает тип заявки как удаленный · коды: 202, 409
  ← path: id:int
- `GET /TaskTypes/{id}/districts` — Метод получения участков для вида работ · коды: 202
  ← path: id:int → map<TaskTypeDistrictList>
- `GET /TaskTypes/{id}/workTypes` — Возвращает список относящихся к типу задачи видов работ · коды: 202
  ← path: id:int → IdNameEntityOfShort[]
- `POST /TaskTypes/{id}/workTypes` — Привязать список видов работ к типу задачи · коды: 200
  ← path: id:int; body: int[]
- `DELETE /TaskTypes/{id}/workTypes` — Удалить привязку видов работ к типу задачи · коды: 200
  ← path: id:int; body: int[]
- `GET /TaskTypes/{taskTypeID}/route` — Возвращает маршрут типа заявки · коды: 200
  ← path: taskTypeID:int → RouteResult

## TaskWatchLists
- `POST /TaskWatchLists` — добавляет пользователей в watchlist по заявкам · коды: 201
  ← body: TaskActionDataOfInt[] → RTWLAddResult[]
- `DELETE /TaskWatchLists` — Исключает пользователей из watchlist'а по заявкам · коды: 202
  ← body: TaskActionDataOfInt[]

## Tasks
- `GET /Tasks` — Возвращает список заявок, доступных пользователю. · коды: 200
  ← query: searchText?:str → map<RTListResult>
- `POST /Tasks` — Создаёт заявку · коды: 201, 400, 409, 422 · примеры
  ← body: WORKTAddData → RAIdResultOfInt
- `DELETE /Tasks` — Помечает заявку как удаленную · коды: 202
  ← body: int[] → TaskDeleteResult[]
- `HEAD /Tasks` — Возвращает заголовок списка заявок для получения количества заявок, удовлетворяющих фильтру. · коды: 200
  ← query: searchText?:str
- `GET /Tasks/changeTypes` — Возвращает список поддерживаемых в логировании разделов (Tab) и секций этих разделов (Sections) · коды: 200, 500
  → ChangeTypeResult[]
- `PUT /Tasks/completedWorks/attributes` — Устанавливает результаты для доп.полей по выполненной работе по заявкам · коды: 202
  ← body: WORKCWAActionDataOfWORKCWAAttributeData[] → WORKCWAActionDataOfWORKCWAAttributeData[]
- `DELETE /Tasks/completedWorks/attributes` — Помечает атрибуты выполенной работы заявки удаленные · коды: 202
  ← body: WORKCWAActionDataOfShort[]
- `POST /Tasks/completedWorks/materials` — Добавляет израсходованные материалы к выполненной работе для заявки · коды: 201, 409
  ← body: TaskActionDataOfCompletedWorkMaterialDataOfMaterial[] → CompletedWorkMaterialPost[]
- `PUT /Tasks/completedWorks/materials` — Изменяет израсходованные материалы у выполненной работы для заявки · коды: 202, 409
  ← body: TaskActionDataOfCompletedWorkMaterialDataOfMaterial[]
- `DELETE /Tasks/completedWorks/materials` — Удаляет материалы у выполненных работ по заявке · коды: 202, 409
  ← body: TaskActionDataOfCompletedWorkMaterialDataOfMaterialDelete[]
- `POST /Tasks/completedWorks/report/attachment/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из тела запроса. · коды: 201, 500
  ← body: CompletedWorkReportBodyUploadData → RCWRAUploadResult
- `POST /Tasks/completedWorks/report/attachment/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к выполненной работе. Данные будут получены из формы. · коды: 201, 500
  ← query: TaskID?:int, JobTitle?:str, Signatory?:str, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → RCWRAUploadResult
- `POST /Tasks/completedWorks/technicians` — Добавляет исполнителей к выполненным работам по заявке · коды: 201, 409
  ← body: TaskActionDataOfCompletedWorkTechnicianDataOfTechnician[] → CompletedWorkTechnicianPost[]
- `PUT /Tasks/completedWorks/technicians` — Изменяет исполнителей у выполненных работы по заявке · коды: 202, 409
  ← body: TaskActionDataOfCompletedWorkTechnicianDataOfTechnician[]
- `DELETE /Tasks/completedWorks/technicians` — Удаляет исполнителей у выполненных работ по заявке · коды: 202, 409
  ← body: TaskActionDataOfCompletedWorkTechnicianDataOfInt[]
- `GET /Tasks/count` — Возвращает количество заявок по дням · коды: 200
  ← query: dateFrom?:datetime, dateTill?:datetime, searchText?:str → map<ListCountResult>
- `GET /Tasks/groupBy/geoHash` — Возвращает краткий список заявок, сгрупированных по хэш-коду геоообласти (кластеризация) · коды: 200
  ← query: searchText?:str, zoomLevel?:float, disableClustering?:bool, clusteringMode?:ClusteringMode → TaskGroupByResultOfClusterResult[]
- `GET /Tasks/new/meta` — Возвращает метаданные для формы заявки. · коды: 200, 500
  ← query: taskTypeID?:int[] → map<TaskTypeFormMetadataResult>
- `PUT /Tasks/restore` — Воскрешает удаленные заявки · коды: 202, 409
  ← body: int[]
- `GET /Tasks/short` — Возвращает краткий список заявок, доступных пользователю. · коды: 200
  ← query: searchText?:str → map<ListShortResult>
- `GET /Tasks/stages/next` — Возвращает список доступных стадий, на котрые могут быть переведены заявки из списка. · коды: 200, 500
  ← query: id?:int[] → map<ListStagesResult>
- `GET /Tasks/{taskID}` — Возвращает детальные сведения по заявке · коды: 200
  ← path: taskID:int; query: taskSnapshotID?:int, includeSchedule?:bool → DetailedInfoResult
- `PUT /Tasks/{taskID}` — Изменяет заявку · коды: 202, 422
  ← path: taskID:int; body: WORKTUpdateData
- `PATCH /Tasks/{taskID}` — Обновляет отдельные поля в заявке · коды: 202
  ← path: taskID:int; body: PatchData[]
- `DELETE /Tasks/{taskID}` — Помечает заявку как удаленную · коды: 202
  ← path: taskID:int → TaskDeleteResult[]
- `GET /Tasks/{taskID}/assignments` — Возвращает историю назначения заявки · коды: 200, 500
  ← path: taskID:int → ListAssignmentHistoryResult
- `GET /Tasks/{taskID}/attachment/{attachmentID}` — Прикрепленный файл к заявке
<param name="taskID">Идентификатор заявки</param><param name="attachmentID">Идентификатор прикрепленного файла к заявке</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200, 500
  ← path: taskID:int, attachmentID:int; query: thumbnailSize?:int → GetAttachmentResult
- `GET /Tasks/{taskID}/attachments` — Список прикрепленных файлов к заявке
<param name="taskID">Идентификатор заявки</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · коды: 200, 500
  ← path: taskID:int; query: thumbnailSize?:int → map<RCListAttachmentResult>
- `GET /Tasks/{taskID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · коды: 303
  ← path: taskID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/attributes` — Возвращает доп.поля по заявке · коды: 200
  ← path: taskID:int; query: isForActualTaskStageOnly?:bool → AttributeResult[]
- `POST /Tasks/{taskID}/autoStaginging` — Активирует запланированный автоматический переход по стадиям заявки · коды: 202, 404
  ← path: taskID:int
- `DELETE /Tasks/{taskID}/autoStaginging` — Прекращает запланированный автоматический переход по стадиям заявки · коды: 200, 404
  ← path: taskID:int
- `GET /Tasks/{taskID}/changes` — Возвращает историю изменения заявки · коды: 200, 500
  ← path: taskID:int → HistoryResult[]
- `GET /Tasks/{taskID}/checkCompanyCodeUsed` — Возвращает информацию используется ли код компании при генерации номера заявки · коды: 200
  ← path: taskID:int → bool
- `GET /Tasks/{taskID}/checkLists` — Возвращает список чек-листов в заявке · коды: 200
  ← path: taskID:int → map<TaskCheckListResult>
- `POST /Tasks/{taskID}/checkLists` — Добавляет чек-листы к заявке · коды: 201
  ← path: taskID:int; body: WORKTCLAddData[] → RTCLPostResult[]
- `DELETE /Tasks/{taskID}/checkLists` — Помечает чек-листы заявки как удаленные · коды: 202
  ← path: taskID:int; body: int[]
- `POST /Tasks/{taskID}/checkLists/{taskCheckListID}` — Добавляет чек-лист к заявке · коды: 201
  ← path: taskID:int, taskCheckListID:int → RTCLPostResult[]
- `DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}` — Помечает чек-лист заявки как удаленный · коды: 202
  ← path: taskID:int, taskCheckListID:int
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Возвращает результаты чек-листа для заявки · коды: 200
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultResult>
- `PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Устанавливает результаты для элементов чек-листа заявки · коды: 202
  ← path: taskID:int, taskCheckListID:int; body: WORKTCLRUpdateData[] → RTCLRPostResult[]
- `DELETE /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Помечает результы чек-листа заявки как удаленные · коды: 202
  ← path: taskID:int, taskCheckListID:int; body: int[]
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · коды: 200, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<RCListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Возвращает результаты чек-листа для заявки · коды: 200
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultV2Result>
- `PUT /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Устанавливает результаты для элементов чек-листа заявки · коды: 202
  ← path: taskID:int, taskCheckListID:int; body: UpdateDataV2[] → RTCLRPostResult[]
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · коды: 200, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<RCListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments/{attachmentID}` — Получает информацию о прикрепленном к чек-листу по завке файле · коды: 200, 204, 500
  ← path: taskID:int, taskCheckListID:int, taskChecklistResultID:int, attachmentID:int
- `POST /Tasks/{taskID}/checkLists/{taskCheckListID}/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к чек-листу по заявке. Данные будут получены из формы. · коды: 201, 500
  ← path: taskID:int, taskCheckListID:int; body: { Attachments?: TaskCheckListResultAttachment[] /* Вложения в чек- листе по заявке */, TaskCheckListID?: int /* Идентификатор чек- листа по заявке */, TaskCheckListResultID?: int /* Идентификатор результата чек- листа по заявке */ } → RTCLRAUploadResult
- `PUT /Tasks/{taskID}/complete` — Помечает заявку, как выполненную · коды: 202, 404, 409
  ← path: taskID:int; body: WORKTCAddData
- `GET /Tasks/{taskID}/completedWorks` — Возвращает список выполненных работ по заявке · коды: 200, 500
  ← path: taskID:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/attachments` — Возвращает список вложенных файлов во все выполненные работы в заявке · коды: 200, 500
  ← path: taskID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/attributes` — Возвращает доп.поля для выполненных работ по заявке · коды: 200
  ← path: taskID:int → CompletedWorkAttributeResult[]
- `GET /Tasks/{taskID}/completedWorks/materials` — Список израсходованных материалов для выполненных работ по заявке · коды: 200, 204, 500
  ← path: taskID:int → map<CompletedWorkMaterialResult>
- `GET /Tasks/{taskID}/completedWorks/materialsWithCodes` — Список израсходованных материалов для выполненных работ по заявке (включая коды маркировки). · коды: 200, 204, 500
  ← path: taskID:int → map<CompletedWorkMaterialResult>
- `GET /Tasks/{taskID}/completedWorks/report/attachment` — Получает подпись к акту выполненной работы · коды: 200, 204, 500
  ← path: taskID:int
- `POST /Tasks/{taskID}/completedWorks/report/attachment/v2/{attachmentID}` — Добавляет загруженный ранее вложенный файл к акту выполненной работы · коды: 201, 500
  ← path: taskID:int, attachmentID:int; body: AddSignedData
- `POST /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}` — Добавляет загруженный ранее вложенный файл к акту выполненной работы · коды: 201, 500
  ← path: taskID:int, attachmentID:int
- `DELETE /Tasks/{taskID}/completedWorks/report/attachment/{attachmentID}` — Помечает прикрепленный файл к акту выполненной работы как удаленный · коды: 202, 500
  ← path: taskID:int, attachmentID:int
- `GET /Tasks/{taskID}/completedWorks/technicians` — Список исполнителей для выполненных работ по заявке · коды: 200, 204
  ← path: taskID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments` — Возвращает список вложенных файлов по выполненной работе в заявке · коды: 200, 500
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · коды: 303, 500
  ← path: taskID:int, attachmentID:int, completedWorkID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Возвращает доп.поля для выполненной работы по заявке · коды: 200
  ← path: taskID:int, completedWorkID:int → CompletedWorkAttributeResult[]
- `PUT /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Устанавливает результаты для доп.полей по выполненной работе по заявке · коды: 202
  ← path: taskID:int, completedWorkID:int; body: WORKCWAAttributeData[] → CompletedWorkAttributeMergeResult[]
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Помечает атрибуты выполенной работы заявки удаленный · коды: 202
  ← path: taskID:int, completedWorkID:int; body: int[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/attachments` — Возвращает список файлов прикрепленных к атрибутам выполенной работы по заявке · коды: 200, 400
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → map<RCWAAListAttachmentResult[]>
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}` — Помечает атрибут выполенной работы заявки удаленный · коды: 202
  ← path: taskID:int, completedWorkID:int, attributeID:int
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}/attachments` — Возвращает список файлов прикрепленных к атрибуту выполненной работы по заявке · коды: 200, 400
  ← path: taskID:int, completedWorkID:int, attributeID:int; query: thumbnailSize?:int → map<RCWAAListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Список израсходованных материалов для выполненной работы по заявке · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkMaterialResult
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Удаляет материалы у выполненной работы по заявке · коды: 202, 409
  ← path: taskID:int, completedWorkID:int; body: MaterialDelete
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Список исполнителей для выполненной работы по заявке · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkTechnicianResult
- `DELETE /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Удаляет исполнителей у выполненной работы по заявке · коды: 202, 409
  ← path: taskID:int, completedWorkID:int; body: int[]
- `POST /Tasks/{taskID}/completedWorks/{completedWorkID}/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к чек-листу по заявке. Данные будут получены из формы. · коды: 201, 500
  ← path: taskID:int, completedWorkID:int; body: { Attachments?: CompletedWorkAttributeAttachment[] /* Вложения в атрибуте выполненной работы по заявке */, AttributeID?: int /* Идентификатор атрибута выполненной работы по заявке */, CompletedWorkID?: int /* Идентификатор выполненной работы по заявке */ } → RCWAUploadResult
- `GET /Tasks/{taskID}/completedWorks/{id}` — Получает информацию о выполненной работе по заявкам · коды: 200, 500
  ← path: taskID:int, id:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/contacts` — Возвращает список контактов заявки · коды: 200, 400
  ← path: taskID:int → map<RTCListResult>
- `GET /Tasks/{taskID}/contacts/{contactID}` — Возвращает контакт заявки · коды: 200
  ← path: taskID:int, contactID:int → RTCGetResult
- `DELETE /Tasks/{taskID}/contacts/{contactID}` — Удаляет контактное лицо у заявки · коды: 202, 409
  ← path: taskID:int, contactID:int
- `POST /Tasks/{taskID}/conversation` — Добавляет сообщения по заявкам. · коды: 201, 500
  ← path: taskID:int; body: TaskConversationData → RTCAddResult[]
- `POST /Tasks/{taskID}/conversation/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к сообщению по заявке. Данные будут получены из формы. · коды: 201, 500
  ← path: taskID:int; body: { Attachments?: TaskConversationAttachment[] /* Вложения в сообщение по заявке */, IsExternal?: bool /* Чат с командой или Заказчиком */, Message?: str /* Сообщение по заявке */ } → RTCUploadResult
- `GET /Tasks/{taskID}/conversations` — Возвращает сообщения по заявке
<param name="taskID">Идентификатор заявки</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param><param name="searchText">Текст для поиска в сообщениях по заявке</param> · коды: 200
  ← path: taskID:int; query: thumbnailSize?:int, searchText?:str → TaskMessage[]
- `HEAD /Tasks/{taskID}/conversations` — Возвращает заголовок списка сообщений по заявке
(для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="taskID">Идентификатор заявки</param><param name="searchText">Текст для поиска в сообщениях по заявке</param> · коды: 200
  ← path: taskID:int; query: searchText?:str
- `GET /Tasks/{taskID}/conversations/{taskConversationID}` — Возвращает сообщение по заявке
<param name="taskID">Идентификатор заявки</param><param name="taskConversationID">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз и доступных)</param> · коды: 200
  ← path: taskID:int, taskConversationID:int; query: thumbnailSize?:int → TaskMessage
- `GET /Tasks/{taskID}/conversations/{taskConversationID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · коды: 303, 500
  ← path: taskID:int, attachmentID:int, taskConversationID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/conversations/{taskConversationID}/delivery` — Возвращает информацию по доставке и прочтению сообщения по заявке.
<param name="taskID">Идентификатор заявки</param><param name="taskConversationID">Идентификатор сообщения</param> · коды: 200, 500
  ← path: taskID:int, taskConversationID:int → ListConversationDeliveryResult[]
- `GET /Tasks/{taskID}/materials` — Возвращает список необходимых материалов для заявки · коды: 200
  ← path: taskID:int → map<RTMListResult>
- `GET /Tasks/{taskID}/meta` — Возвращает метаданные для формы заявки. · коды: 200, 500
  ← path: taskID:int → TaskTypeFormMetadataResult
- `GET /Tasks/{taskID}/ratings` — Возвращает отзывы/рейтинги инжененров по заявке. · коды: 200, 500
  ← path: taskID:int → RatingResult[]
- `GET /Tasks/{taskID}/ratings/avg` — Возвращает отзывы/рейтинги инжененров по заявке. · коды: 200, 500
  ← path: taskID:int → RatingResult[]
- `GET /Tasks/{taskID}/skills` — Возвращает список навыков заявки · коды: 200, 500
  ← path: taskID:int → map<TaskSkillResult>
- `GET /Tasks/{taskID}/stages` — Возвращает историю перемещения заявки по стадиям. · коды: 200, 500
  ← path: taskID:int; query: includeChangeset?:bool, actionLocationState?:ActionLocationState → ListStagingHistoryResult
- `GET /Tasks/{taskID}/stages/next` — Возвращает список доступных стадий, на котрые может быть переведена заявка. · коды: 200, 500
  ← path: taskID:int → map<ListStagesResult>
- `GET /Tasks/{taskID}/tags` — Возвращает тэги по заявке. · коды: 200, 500
  ← path: taskID:int → str[]
- `GET /Tasks/{taskID}/watchLists` — WatchList по заявке · коды: 200, 500
  ← path: taskID:int; query: searchText?:str → RTWLListResult[]
- `DELETE /Tasks/{taskId}/completedWorks/marking-codes` — Удаляет все коды маркировки по заявке (во всех выполненных работах). · коды: 200, 204 · примеры
  ← path: taskId:int → TaskCompletedWorksMarkingCodesDeleteResult
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes` — Возвращает коды маркировки для выполненной работы (все материалы). · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int → MarkingCodesListResult
- `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетная привязка кодов маркировки к материалам выбранной выполненной работы. · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesUpsertRequest → CompletedWorkMaterialsMarkingCodesUpsertResult
- `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетная перепривязка (перенос) существующих активных кодов маркировки у материалов выбранной выполненной работы. · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesUpdateRequest → CompletedWorkMaterialsMarkingCodesUpdateResult
- `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes` — Пакетное удаление привязанных кодов маркировки у материалов выбранной выполненной работы. · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int; body: CompletedWorkMaterialsMarkingCodesDeleteRequest → CompletedWorkMaterialsMarkingCodesDeleteResult
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Возвращает коды маркировки для конкретного материала в выполненной работе. · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int → MarkingCodesListResult
- `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Пакетная привязка кодов маркировки к материалу. · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesUpsertForMaterialRequest → MarkingCodesUpsertResult
- `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Пакетная перепривязка (перенос) существующих активных кодов маркировки на указанный материал. · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesUpdateForMaterialRequest → MarkingCodesUpdateResult
- `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Удаление привязанных кодов маркировки у материала. · коды: 200, 400, 404, 409 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; body: MarkingCodesDeleteForMaterialRequest → MarkingCodesDeleteResult
- `GET /Tasks/{taskId}/marking-codes` — Возвращает коды маркировки для заявки (все выполненные работы). · коды: 200, 204 · примеры
  ← path: taskId:int → MarkingCodesListResult

## TemplateQuickResponse
- `GET /TemplateQuickResponse` — Возвращает список быстрых ответов · коды: 200
  ← query: searchText?:str → map<RTQRListResult>
- `POST /TemplateQuickResponse` — Создаёт новый быстрый ответ · коды: 201, 409
  ← body: WORKTQRAddData[] → int[]
- `PUT /TemplateQuickResponse` — Обновляет быстрый ответ. · коды: 202, 500
  ← body: WORKTQRUpdateData[]
- `DELETE /TemplateQuickResponse` — Помечает быстрые ответы, как удалённые · коды: 202, 409
  ← body: int[]
- `PUT /TemplateQuickResponse/taskTypes` — Создает или изменяет привязку быстрых ответов к типам заявок. · коды: 202, 500
  ← body: WORKTQRMergeData[]
- `GET /TemplateQuickResponse/{id}` — Возвращает быстрый ответ · коды: 200
  ← path: id:int → RTQRGetResult

## UserTaskFavourites
- `POST /UserTaskFavourites` — Добавляет заявки в список избранных для текущего пользователя. · коды: 201, 500
  ← body: int[]
- `DELETE /UserTaskFavourites` — Добавляет заявки в список избранных для текущего пользователя. · коды: 202, 500
  ← body: int[]

## WorkTypes
- `GET /WorkTypes` — Возвращает список видов работ. · коды: 200
  ← query: searchText?:str → map<RWTListResult>
- `POST /WorkTypes` — Создает вид работ · коды: 201
  ← query: relatedToAnyTaskType?:bool, relatedToAnyAsset?:bool; body: WORKWTAddData[] → int[]
- `PUT /WorkTypes` — Изменяет виды работ · коды: 202
  ← body: WORKWTUpdateData[]
- `DELETE /WorkTypes` — Помечает виды работ, как удаленные · коды: 202
  ← body: int[]
- `PUT /WorkTypes/publish` — Публикует выполненные работы · коды: 202
  ← body: int[]
- `PUT /WorkTypes/unpublish` — Отменяет публикацию выполненных работы · коды: 202
  ← body: int[]
- `GET /WorkTypes/{id}` — Возвращает данные для вида работы. · коды: 200, 500
  ← path: id:int → RWTGetResult
- `DELETE /WorkTypes/{id}` — Помечает вид работ как удаленный · коды: 202, 409
  ← path: id:int
- `PUT /WorkTypes/{id}/publish` — Помечает вид работ как опубликованный · коды: 202
  ← path: id:int
- `GET /WorkTypes/{id}/taskTypes` — Возвращает список относящихся к виду работ типов задач · коды: 202
  ← path: id:int → IdNameEntityOfByte[]
- `POST /WorkTypes/{id}/taskTypes` — Привязать список типов задач к виду работ · коды: 200
  ← path: id:int; body: int[]
- `DELETE /WorkTypes/{id}/taskTypes` — Удалить привязку типу задач к виду работ · коды: 200
  ← path: id:int; body: int[]
- `PUT /WorkTypes/{id}/unpublish` — Помечает вид работ как опубликованный · коды: 202
  ← path: id:int
- `GET /WorkTypes/{parentWorkTypeID}/workTypes` — Возвращает список дочерних видов работ (вниз по графу). · коды: 200, 500
  ← path: parentWorkTypeID:int; query: searchText?:str → map<RWTListResult>
- `GET /WorkTypes/{parentWorkTypeID}/workTypes/all` — Возвращает список всех дочерних видов работ (вниз по графу). · коды: 200, 500
  ← path: parentWorkTypeID:int; query: searchText?:str → map<RWTListResult>
- `GET /WorkTypes/{workTypeID}/checkLists` — Возвращает список чек-листов вида работ · коды: 200
  ← path: workTypeID:int → map<RCLGetResult[]>
- `POST /WorkTypes/{workTypeID}/checkLists` — Добавляет чек-листы к типу работ · коды: 202
  ← path: workTypeID:int; body: int[]
- `DELETE /WorkTypes/{workTypeID}/checkLists` — Помечает чек-листы у типа работ как удаленные · коды: 202
  ← path: workTypeID:int; body: int[]
- `POST /WorkTypes/{workTypeID}/checkLists/{checkListID}` — Добавляет чек-лист к типу работ · коды: 202
  ← path: workTypeID:int, checkListID:int
- `DELETE /WorkTypes/{workTypeID}/checkLists/{checkListID}` — Помечает чек-лист у типа работ как удаленный · коды: 202
  ← path: workTypeID:int, checkListID:int
