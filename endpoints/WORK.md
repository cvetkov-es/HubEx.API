# WORK — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса WORK (API for managing tasks and works in HubEx): сигнатуры, параметры, права. Типы — schemas/WORK.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WORK.md`; грабли — `notes/WORK.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/WORK`
> Примеры ответов вынесены в [../examples/WORK.md](../examples/WORK.md).

**Оглавление**

- CheckLists — строки 27–33
- RequestMethods — строки 35–37
- TaskActualities — строки 39–43
- TaskAttributes — строки 45–47
- TaskConversations — строки 49–54
- TaskFilter — строки 56–58
- TaskListQueries — строки 60–64
- TaskOrderBy — строки 66–68
- TaskStatuses — строки 70–74
- TaskTemplates — строки 76–96
- TaskTypes — строки 98–108
- Tasks — строки 110–229
- TemplateQuickResponse — строки 231–235
- WorkTypes — строки 237–249

## CheckLists
- `GET /CheckLists` — Возвращает список активных чек-листов · коды: 200
  ← query: searchText?:str → map<RCLListResult>
- `GET /CheckLists/{checkListID}/items` — Возвращает элементы чек-листа · коды: 200
  ← path: checkListID:int → map<CheckListItemResult>
- `GET /CheckLists/{id}` — Возвращает чек-лист · коды: 200
  ← path: id:int → map<RCLGetResult>

## RequestMethods
- `GET /RequestMethods` — Возвращает список методов подачи заявок. · коды: 200
  → map<RRMListResult>

## TaskActualities
- `GET /TaskActualities` — Возвращает список актуальностей заявок · коды: 200
  → map<RTAListResult>
- `GET /TaskActualities/{id}` — Возвращает актуальность заявки · коды: 200
  ← path: id:int → RTAListResult

## TaskAttributes
- `GET /TaskAttributes` — Возвращает значения атрибутов по заявкам · коды: 200
  → TaskAttributesResult[]

## TaskConversations
- `GET /TaskConversations` — Возвращает список сообщений по заявкам, доступным пользователю.
<param name="searchText">Текст для поиска в сообщениях по заявкам</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200
  ← query: searchText?:str, thumbnailSize?:int → TaskMessageLast[]
- `HEAD /TaskConversations` — Возвращает заголовок списка сообщений по заявке (для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="searchText">Текст для поиска в сообщениях по заявкам</param> · коды: 200

## TaskFilter
- `GET /TaskFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · коды: 200
  ← query: selectedOnly?:bool → FilterListItemProjection[]

## TaskListQueries
- `GET /TaskListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · коды: 200
  → map<TaskListQueryResult>
- `GET /TaskListQueries/{id}` — Возвращает сохраненный запрос · коды: 200
  ← path: id:int → map<TaskListQueryResult>

## TaskOrderBy
- `GET /TaskOrderBy` — Возвращает список методов сортировки заявок · коды: 200
  → map<RTOBListResult>

## TaskStatuses
- `GET /TaskStatuses` — Возвращает список статусов заявок · коды: 200, 500
  → map<RTSListResult>
- `GET /TaskStatuses/{id}` — Возвращает статус заявки · коды: 200
  ← path: id:int → RTSListResult

## TaskTemplates
- `GET /TaskTemplates` — Возвращает список шаблонов заявок. · коды: 200
  ← query: searchText?:str, isPublic?:bool → map<RTaskTemplatesListResult>
- `HEAD /TaskTemplates` — Возвращает заголовок списка шаблонов заявок. · коды: 200
  ← query: searchText?:str, isPublic?:bool
- `GET /TaskTemplates/download` — Возвращает архив qr-кодов в формате svg в соответствии с заданными фильтрами · коды: 200
  ← query: searchText?:str, isPublic?:bool
- `GET /TaskTemplates/{id}` — Возвращает шаблон заявки · коды: 200
  ← path: id:str → RTaskTemplatesGetResult
- `GET /TaskTemplates/{id}/assignment` — Возвращает список исполнителей, связанных с шаблоном · коды: 200, 500
  ← path: id:str → TaskTemplateAssignmentDetailsProjection
  Выполнение данного метода разрешено от **анонимного пользователя**.
- `GET /TaskTemplates/{id}/download` — Возвращает шаблон заявки · коды: 200
  ← path: id:str
- `GET /TaskTemplates/{id}/public` — Возвращает публичный шаблон заявки по идентификатору, который вычисляется как sha256(QrCode) · коды: 200, 500
  ← path: id:str → GetPublicResult
  Выполнение данного метода разрешено от **анонимного пользователя**.
- `GET /TaskTemplates/{id}/schedules` — Получить список сгенерированных событий шаблоной зявки · коды: 200
  ← path: id:str → GetSchedulesResult[]
- `GET /TaskTemplates/{tasktTemplateID}/excludedAssets` — Возвращает список исключенных объектов для плановой заявки · коды: 200
  ← path: tasktTemplateID:str → map<TaskTemplateExcludedAssetResult>

## TaskTypes
- `GET /TaskTypes` — Возвращает список типов заявок, доступных пользователю. Доступность определяется привязкой пользователя к участкам. · коды: 200, 500
  → map<RTaskTypesListResult>
- `GET /TaskTypes/{id}` — Возвращает тип заявки · коды: 200
  ← path: id:int → RTaskTypesListResult
- `GET /TaskTypes/{id}/districts` — Метод получения участков для вида работ · коды: 202
  ← path: id:int → map<TaskTypeDistrictList>
- `GET /TaskTypes/{id}/workTypes` — Возвращает список относящихся к типу задачи видов работ · коды: 202
  ← path: id:int → IdNameEntityOfShort[]
- `GET /TaskTypes/{taskTypeID}/route` — Возвращает маршрут типа заявки · коды: 200
  ← path: taskTypeID:int → RouteResult

## Tasks
- `GET /Tasks` — Возвращает список заявок, доступных пользователю. · коды: 200
  ← query: searchText?:str → map<RTListResult>
- `HEAD /Tasks` — Возвращает заголовок списка заявок для получения количества заявок, удовлетворяющих фильтру. · коды: 200
  ← query: searchText?:str
- `GET /Tasks/changeTypes` — Возвращает список поддерживаемых в логировании разделов (Tab) и секций этих разделов (Sections) · коды: 200, 500
  → ChangeTypeResult[]
- `GET /Tasks/count` — Возвращает количество заявок по дням · коды: 200
  ← query: dateFrom?:datetime, dateTill?:datetime, searchText?:str → map<ListCountResult>
- `GET /Tasks/groupBy/geoHash` — Возвращает краткий список заявок, сгрупированных по хэш-коду геоообласти (кластеризация) · коды: 200
  ← query: searchText?:str, zoomLevel?:float, disableClustering?:bool, clusteringMode?:ClusteringMode → TaskGroupByResultOfClusterResult[]
- `GET /Tasks/new/meta` — Возвращает метаданные для формы заявки. · коды: 200, 500
  ← query: taskTypeID?:int[] → map<TaskTypeFormMetadataResult>
- `GET /Tasks/short` — Возвращает краткий список заявок, доступных пользователю. · коды: 200
  ← query: searchText?:str → map<ListShortResult>
- `GET /Tasks/stages/next` — Возвращает список доступных стадий, на котрые могут быть переведены заявки из списка. · коды: 200, 500
  ← query: id?:int[] → map<ListStagesResult>
- `GET /Tasks/{taskID}` — Возвращает детальные сведения по заявке · коды: 200
  ← path: taskID:int; query: taskSnapshotID?:int, includeSchedule?:bool → DetailedInfoResult
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
- `GET /Tasks/{taskID}/changes` — Возвращает историю изменения заявки · коды: 200, 500
  ← path: taskID:int → HistoryResult[]
- `GET /Tasks/{taskID}/checkCompanyCodeUsed` — Возвращает информацию используется ли код компании при генерации номера заявки · коды: 200
  ← path: taskID:int → bool
- `GET /Tasks/{taskID}/checkLists` — Возвращает список чек-листов в заявке · коды: 200
  ← path: taskID:int → map<TaskCheckListResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Возвращает результаты чек-листа для заявки · коды: 200
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · коды: 200, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<RCListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Возвращает результаты чек-листа для заявки · коды: 200
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultV2Result>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · коды: 200, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<RCListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments/{attachmentID}` — Получает информацию о прикрепленном к чек-листу по завке файле · коды: 200, 204, 500
  ← path: taskID:int, taskCheckListID:int, taskChecklistResultID:int, attachmentID:int
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
- `GET /Tasks/{taskID}/completedWorks/technicians` — Список исполнителей для выполненных работ по заявке · коды: 200, 204
  ← path: taskID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments` — Возвращает список вложенных файлов по выполненной работе в заявке · коды: 200, 500
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · коды: 303, 500
  ← path: taskID:int, attachmentID:int, completedWorkID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Возвращает доп.поля для выполненной работы по заявке · коды: 200
  ← path: taskID:int, completedWorkID:int → CompletedWorkAttributeResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/attachments` — Возвращает список файлов прикрепленных к атрибутам выполенной работы по заявке · коды: 200, 400
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → map<RCWAAListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}/attachments` — Возвращает список файлов прикрепленных к атрибуту выполненной работы по заявке · коды: 200, 400
  ← path: taskID:int, completedWorkID:int, attributeID:int; query: thumbnailSize?:int → map<RCWAAListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Список израсходованных материалов для выполненной работы по заявке · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkMaterialResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Список исполнителей для выполненной работы по заявке · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{id}` — Получает информацию о выполненной работе по заявкам · коды: 200, 500
  ← path: taskID:int, id:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/contacts` — Возвращает список контактов заявки · коды: 200, 400
  ← path: taskID:int → map<RTCListResult>
- `GET /Tasks/{taskID}/contacts/{contactID}` — Возвращает контакт заявки · коды: 200
  ← path: taskID:int, contactID:int → RTCGetResult
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
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes` — Возвращает коды маркировки для выполненной работы (все материалы). · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int → MarkingCodesListResult
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Возвращает коды маркировки для конкретного материала в выполненной работе. · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int → MarkingCodesListResult
- `GET /Tasks/{taskId}/marking-codes` — Возвращает коды маркировки для заявки (все выполненные работы). · коды: 200, 204 · примеры
  ← path: taskId:int → MarkingCodesListResult

## TemplateQuickResponse
- `GET /TemplateQuickResponse` — Возвращает список быстрых ответов · коды: 200
  ← query: searchText?:str → map<RTQRListResult>
- `GET /TemplateQuickResponse/{id}` — Возвращает быстрый ответ · коды: 200
  ← path: id:int → RTQRGetResult

## WorkTypes
- `GET /WorkTypes` — Возвращает список видов работ. · коды: 200
  ← query: searchText?:str → map<RWTListResult>
- `GET /WorkTypes/{id}` — Возвращает данные для вида работы. · коды: 200, 500
  ← path: id:int → RWTGetResult
- `GET /WorkTypes/{id}/taskTypes` — Возвращает список относящихся к виду работ типов задач · коды: 202
  ← path: id:int → IdNameEntityOfByte[]
- `GET /WorkTypes/{parentWorkTypeID}/workTypes` — Возвращает список дочерних видов работ (вниз по графу). · коды: 200, 500
  ← path: parentWorkTypeID:int; query: searchText?:str → map<RWTListResult>
- `GET /WorkTypes/{parentWorkTypeID}/workTypes/all` — Возвращает список всех дочерних видов работ (вниз по графу). · коды: 200, 500
  ← path: parentWorkTypeID:int; query: searchText?:str → map<RWTListResult>
- `GET /WorkTypes/{workTypeID}/checkLists` — Возвращает список чек-листов вида работ · коды: 200
  ← path: workTypeID:int → map<RCLGetResult[]>
