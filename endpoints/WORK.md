# WORK — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса WORK (API for managing tasks and works in HubEx): сигнатуры, параметры, права. Типы — schemas/WORK.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/WORK.md`; грабли — `notes/WORK.md` (если есть).
> **Источник:** swagger сервиса WORK · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/WORK`
> Примеры ответов вынесены в [../examples/WORK.md](../examples/WORK.md).

**Оглавление**

- CheckLists — строки 28–34
- RequestMethods — строки 36–38
- TaskActualities — строки 40–44
- TaskAttributes — строки 46–48
- TaskConversations — строки 50–55
- TaskFilter — строки 57–59
- TaskListQueries — строки 61–65
- TaskOrderBy — строки 67–69
- TaskStatuses — строки 71–75
- TaskTemplates — строки 77–97
- TaskTypes — строки 99–109
- Tasks — строки 111–230
- TemplateQuickResponse — строки 232–236
- WorkTypes — строки 238–250

## CheckLists
- `GET /CheckLists` — Возвращает список активных чек-листов · права: CheckListsList · paginated · коды: 200, 206
  ← query: searchText?:str, assetID?:any, workTypeID?:any, isAssignedToAsset?:enum(true, false), isAssignedToWorkType?:enum(true, false), searchText?:str → map<CheckLists.ListResult>
- `GET /CheckLists/{checkListID}/items` — Возвращает элементы чек-листа · права: CheckListItemsList · paginated · коды: 200, 206
  ← path: checkListID:int → map<CheckListItemResult>
- `GET /CheckLists/{id}` — Возвращает чек-лист · права: CheckListGet · коды: 200
  ← path: id:int → map<CheckLists.GetResult>

## RequestMethods
- `GET /RequestMethods` — Возвращает список методов подачи заявок. · права: RequestMethodsList · paginated · коды: 200, 206
  → map<RequestMethods.ListResult>

## TaskActualities
- `GET /TaskActualities` — Возвращает список актуальностей заявок · права: TaskActualitiesList · paginated · коды: 200, 206
  → map<TaskActualities.ListResult>
- `GET /TaskActualities/{id}` — Возвращает актуальность заявки · права: TaskActualityGet · коды: 200
  ← path: id:int → TaskActualities.ListResult

## TaskAttributes
- `GET /TaskAttributes` — Возвращает значения атрибутов по заявкам · права: TaskAttributeGet · paginated · коды: 200, 206
  ← query: taskID?:any, attributeID?:any → TaskAttributesResult[]

## TaskConversations
- `GET /TaskConversations` — Возвращает список сообщений по заявкам, доступным пользователю.
<param name="searchText">Текст для поиска в сообщениях по заявкам</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · права: TaskConversationsList · paginated · коды: 200, 206
  ← query: searchText?:str, thumbnailSize?:int, isRead?:enum(true, false) → TaskMessageLast[]
- `HEAD /TaskConversations` — Возвращает заголовок списка сообщений по заявке (для получения количества сообщений, удовлетворяющих условиям фильтрации)
<param name="searchText">Текст для поиска в сообщениях по заявкам</param> · права: TaskConversationsList · коды: 200

## TaskFilter
- `GET /TaskFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · права: TasksList · коды: 200
  ← query: selectedOnly?:bool, selectedOnly?:enum(true, false) → FilterListItemProjection[]

## TaskListQueries
- `GET /TaskListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · права: TaskListQueryListAll · paginated · коды: 200, 206
  → map<TaskListQueryResult>
- `GET /TaskListQueries/{id}` — Возвращает сохраненный запрос · права: TaskListQueryGet · коды: 200
  ← path: id:int → map<TaskListQueryResult>

## TaskOrderBy
- `GET /TaskOrderBy` — Возвращает список методов сортировки заявок · права: TaskOrderByList · paginated · коды: 200, 206
  → map<TaskOrderBy.ListResult>

## TaskStatuses
- `GET /TaskStatuses` — Возвращает список статусов заявок · права: TaskStatusesList · paginated · коды: 200, 206, 500
  → map<TaskStatuses.ListResult>
- `GET /TaskStatuses/{id}` — Возвращает статус заявки · права: TaskStatusGet · коды: 200
  ← path: id:int → TaskStatuses.ListResult

## TaskTemplates
- `GET /TaskTemplates` — Возвращает список шаблонов заявок. · права: TaskTemlatesList · paginated · коды: 200, 206
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, assetTypeID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isAllowForMailboxSender?:enum(true, false), isScheduled?:enum(true, false), isScheduleActive?:enum(true, false), taskTemplateID?:str → map<TaskTemplates.ListResult>
- `HEAD /TaskTemplates` — Возвращает заголовок списка шаблонов заявок. · права: TaskTemlatesList · коды: 200
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isAllowForMailboxSender?:enum(true, false), isScheduled?:enum(true, false), isScheduleActive?:enum(true, false), startWithAssetID?:any
- `GET /TaskTemplates/download` — Возвращает архив qr-кодов в формате svg в соответствии с заданными фильтрами · права: TaskTemlatesList · paginated · коды: 200, 206
  ← query: searchText?:str, isPublic?:bool, isPublished?:enum(true, false), assetID?:any, taskTypeID?:any, workTypeID?:any, companyID?:any, contractID?:any, criticalityID?:any, frequencyTypeID?:any, isScheduled?:enum(true, false), isScheduleActive?:enum(true, false)
- `GET /TaskTemplates/{id}` — Возвращает шаблон заявки · права: TaskTemplateGet · коды: 200
  ← path: id:str → TaskTemplates.GetResult
- `GET /TaskTemplates/{id}/assignment` — Возвращает список исполнителей, связанных с шаблоном · коды: 200, 500
  ← path: id:str → TaskTemplateAssignmentDetailsProjection
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /TaskTemplates/{id}/download` — Возвращает шаблон заявки · права: TaskTemplateGet · коды: 200
  ← path: id:str
- `GET /TaskTemplates/{id}/public` — Возвращает публичный шаблон заявки по идентификатору, который вычисляется как sha256(QrCode) · коды: 200, 500
  ← path: id:str → GetPublicResult
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /TaskTemplates/{id}/schedules` — Получить список сгенерированных событий шаблоной зявки · права: TaskTemplateScheduleList · paginated · коды: 200, 206
  ← path: id:str → GetSchedulesResult[]
- `GET /TaskTemplates/{tasktTemplateID}/excludedAssets` — Возвращает список исключенных объектов для плановой заявки · права: TaskTemplateExcludedAssetList · paginated · коды: 200, 206
  ← path: tasktTemplateID:str → map<TaskTemplateExcludedAssetResult>

## TaskTypes
- `GET /TaskTypes` — Возвращает список типов заявок, доступных пользователю. Доступность определяется привязкой пользователя к участкам. · права: TaskTypesList · paginated · коды: 200, 206, 500
  ← query: companyID?:any, districtID?:any, assetID?:any, workTypeID?:any → map<TaskTypes.ListResult>
- `GET /TaskTypes/{id}` — Возвращает тип заявки · права: TaskTypeGet · коды: 200
  ← path: id:int → TaskTypes.ListResult
- `GET /TaskTypes/{id}/districts` — Метод получения участков для вида работ · права: TaskTypeDistrictList · paginated · коды: 202, 206
  ← path: id:int → map<TaskTypeDistrictList>
- `GET /TaskTypes/{id}/workTypes` — Возвращает список относящихся к типу задачи видов работ · права: TaskTypesList · paginated · коды: 202, 206
  ← path: id:int → IdNameEntity<Int16>[]
- `GET /TaskTypes/{taskTypeID}/route` — Возвращает маршрут типа заявки · права: TaskTypeRouteGet · коды: 200
  ← path: taskTypeID:int → RouteResult

## Tasks
- `GET /Tasks` — Возвращает список заявок, доступных пользователю. · права: TasksList · paginated · коды: 200, 206
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), topLevelTasksForHierarchy?:enum(true, false), assetTypeID?:any, assetClassID?:any, districtID?:any, assetResponsibleUserID?:any, branchID?:any, erpID?:str, parentID?:any, assetSchemaID?:any, attributeValues?:str, lastModifiedFrom?:any, lastModifiedTill?:any, contactID?:any, payeeCompanyID?:any → map<Tasks.ListResult>
- `HEAD /Tasks` — Возвращает заголовок списка заявок для получения количества заявок, удовлетворяющих фильтру. · права: TasksList · коды: 200
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), assetTypeID?:any, assetClassID?:any, erpID?:str, parentID?:any, branchID?:any, assetSchemaID?:any, contactID?:any
- `GET /Tasks/changeTypes` — Возвращает список поддерживаемых в логировании разделов (Tab) и секций этих разделов (Sections) · права: TaskGet · коды: 200, 500
  → ChangeTypeResult[]
- `GET /Tasks/count` — Возвращает количество заявок по дням · права: TasksList · коды: 200
  ← query: dateFrom?:datetime, dateTill?:datetime, searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), assetTypeID?:any, assetClassID?:any, districtID?:any, assetResponsibleUserID?:any, branchID?:any, erpID?:str, parentID?:any → map<ListCountResult>
- `GET /Tasks/groupBy/geoHash` — Возвращает краткий список заявок, сгрупированных по хэш-коду геоообласти (кластеризация) · права: TasksList · коды: 200
  ← query: searchText?:str, zoomLevel?:float, disableClustering?:bool, clusteringMode?:ClusteringMode, requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, taskTemplateID?:str, requestMethodID?:any, disableClustering?:enum(true, false), clusteringMode?:any → TaskGroupByResult<ClusterResult>[]
- `GET /Tasks/new/meta` — Возвращает метаданные для формы заявки. · права: TaskMetadataGet · коды: 200, 500
  ← query: taskTypeID?:int[] → map<TaskTypeFormMetadataResult>
- `GET /Tasks/short` — Возвращает краткий список заявок, доступных пользователю. · права: TasksList · paginated · коды: 200, 206
  ← query: searchText?:str, isRated?:enum(true, false), requestedBy?:any, assignedTo?:any, approvalWith?:any, escalatedTo?:any, assetID?:any, startWithAssetID?:any, taskID?:any, taskNumber?:str, taskTypeID?:any, workTypeID?:any, taskStageID?:any, taskStatusID?:any, creationFrom?:any, creationTill?:any, assignationFrom?:any, assignationTill?:any, completionFrom?:any, completionTill?:any, closingFrom?:any, closingTill?:any, deadlineFrom?:any, deadlineTill?:any, isClosed?:enum(true, false), isFavourite?:enum(true, false), isCompleted?:enum(true, false), isAssigned?:enum(true, false), isDeleted?:enum(true, false), isOutdated?:enum(true, false), companyID?:any, contractID?:any, criticalityID?:any, orderBy?:any, sortDirection?:any, pointNorthEast?:any, pointSouthWest?:any, pointCenter?:any, radius?:any, geoHash?:str, ratingCriteriaId?:any, taskTemplateID?:str, requestMethodID?:any, hasAssigneeCheckedIn?:enum(true, false), isScheduled?:enum(true, false), branchID?:any, assetTypeID?:any, assetClassID?:any, erpID?:str, parentID?:any, assetSchemaID?:any, contactID?:any → map<ListShortResult>
- `GET /Tasks/stages/next` — Возвращает список доступных стадий, на котрые могут быть переведены заявки из списка. · права: TaskStagesList · коды: 200, 500
  ← query: id?:int[] → map<ListStagesResult>
- `GET /Tasks/{taskID}` — Возвращает детальные сведения по заявке · права: TaskGet · коды: 200
  ← path: taskID:int; query: taskSnapshotID?:int, includeSchedule?:bool → DetailedInfoResult
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
- `GET /Tasks/{taskID}/changes` — Возвращает историю изменения заявки · права: TaskGet · paginated · коды: 200, 206, 500
  ← path: taskID:int; query: dateRangeFrom?:any, dateRangeTill?:any, userID?:any, tab?:str, section?:str → HistoryResult[]
- `GET /Tasks/{taskID}/checkCompanyCodeUsed` — Возвращает информацию используется ли код компании при генерации номера заявки · права: IfUsedInTaskNumberGet · коды: 200
  ← path: taskID:int → bool
- `GET /Tasks/{taskID}/checkLists` — Возвращает список чек-листов в заявке · права: TaskCheckListsList · paginated · коды: 200, 206
  ← path: taskID:int → map<TaskCheckListResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results` — Возвращает результаты чек-листа для заявки · права: TaskCheckListResultsList · paginated · коды: 200, 206
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · права: TaskCheckListResultAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/v2` — Возвращает результаты чек-листа для заявки · права: TaskCheckListResultsList · paginated · коды: 200, 206
  ← path: taskID:int, taskCheckListID:int → map<TaskCheckListResultV2Result>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments` — Возвращает список файлов прикрепленных к пункту чек-листа по заявке · права: TaskCheckListResultAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, taskCheckListID:int, taskCheckListResultID:int; query: thumbnailSize?:int → map<Common.ListAttachmentResult>
- `GET /Tasks/{taskID}/checkLists/{taskCheckListID}/results/{taskCheckListResultID}/attachments/{attachmentID}` — Получает информацию о прикрепленном к чек-листу по завке файле · права: TaskCheckListResultAttachmentGet · коды: 200, 204, 500
  ← path: taskID:int, taskCheckListID:int, taskChecklistResultID:int, attachmentID:int
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
- `GET /Tasks/{taskID}/completedWorks/technicians` — Список исполнителей для выполненных работ по заявке · права: CompletedWorkTechnicianList · коды: 200, 204
  ← path: taskID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments` — Возвращает список вложенных файлов по выполненной работе в заявке · права: CompletedWorkAttachmentList · paginated · коды: 200, 206, 500
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int → ListAttachmentForCompletedWorkResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачки файла · права: CompletedWorkAttachmentDownload · paginated · коды: 206, 303, 500
  ← path: taskID:int, attachmentID:int, completedWorkID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes` — Возвращает доп.поля для выполненной работы по заявке · права: CompletedWorkAttributeList · paginated · коды: 200, 206
  ← path: taskID:int, completedWorkID:int → CompletedWorkAttributeResult[]
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/attachments` — Возвращает список файлов прикрепленных к атрибутам выполенной работы по заявке · права: CompletedWorkAttributeAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, completedWorkID:int; query: thumbnailSize?:int, attributeID?:any → map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/attributes/{attributeID}/attachments` — Возвращает список файлов прикрепленных к атрибуту выполненной работы по заявке · права: CompletedWorkAttributeAttachmentList · paginated · коды: 200, 206, 400
  ← path: taskID:int, completedWorkID:int, attributeID:int; query: thumbnailSize?:int → map<CompletedWorkAttributeAttachment.ListAttachmentResult[]>
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/materials` — Список израсходованных материалов для выполненной работы по заявке · права: CompletedWorkMaterialsList · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkMaterialResult
- `GET /Tasks/{taskID}/completedWorks/{completedWorkID}/technicians` — Список исполнителей для выполненной работы по заявке · права: CompletedWorkTechnicianList · коды: 200, 204
  ← path: taskID:int, completedWorkID:int → CompletedWorkTechnicianResult
- `GET /Tasks/{taskID}/completedWorks/{id}` — Получает информацию о выполненной работе по заявкам · права: CompletedWorkGet · коды: 200, 500
  ← path: taskID:int, id:int → CompletedWorkResult[]
- `GET /Tasks/{taskID}/contacts` — Возвращает список контактов заявки · права: TaskContactsList · paginated · коды: 200, 206, 400
  ← path: taskID:int → map<TaskContacts.ListResult>
- `GET /Tasks/{taskID}/contacts/{contactID}` — Возвращает контакт заявки · права: TaskContactGet · коды: 200
  ← path: taskID:int, contactID:int → TaskContacts.GetResult
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
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes` — Возвращает коды маркировки для выполненной работы (все материалы). · права: CompletedWorkMaterialsList · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int → MarkingCodesListResult
- `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes` — Возвращает коды маркировки для конкретного материала в выполненной работе. · права: CompletedWorkMaterialsList · коды: 200, 204 · примеры
  ← path: taskId:int, completedWorkId:int, materialId:int; query: warehouseID?:any → MarkingCodesListResult
- `GET /Tasks/{taskId}/marking-codes` — Возвращает коды маркировки для заявки (все выполненные работы). · права: TaskGet · коды: 200, 204 · примеры
  ← path: taskId:int → MarkingCodesListResult

## TemplateQuickResponse
- `GET /TemplateQuickResponse` — Возвращает список быстрых ответов · права: QuickResponseList · paginated · коды: 200, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), taskTypeID?:any → map<TemplateQuickResponse.ListResult>
- `GET /TemplateQuickResponse/{id}` — Возвращает быстрый ответ · права: QuickResponseGet · коды: 200
  ← path: id:int → TemplateQuickResponse.GetResult

## WorkTypes
- `GET /WorkTypes` — Возвращает список видов работ. · права: WorkTypeList · paginated · коды: 200, 206
  ← query: searchText?:str, assetID?:any, taskTypeID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false), erpID?:str → map<WorkTypes.ListResult>
- `GET /WorkTypes/{id}` — Возвращает данные для вида работы. · права: WorkTypeGet · paginated · коды: 200, 206, 500
  ← path: id:int → WorkTypes.GetResult
- `GET /WorkTypes/{id}/taskTypes` — Возвращает список относящихся к виду работ типов задач · права: TaskTypesList · paginated · коды: 202, 206
  ← path: id:int → IdNameEntity<Byte>[]
- `GET /WorkTypes/{parentWorkTypeID}/workTypes` — Возвращает список дочерних видов работ (вниз по графу). · права: WorkTypeList · paginated · коды: 200, 206, 500
  ← path: parentWorkTypeID:int; query: searchText?:str, assetID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false) → map<WorkTypes.ListResult>
- `GET /WorkTypes/{parentWorkTypeID}/workTypes/all` — Возвращает список всех дочерних видов работ (вниз по графу). · права: WorkTypeList · paginated · коды: 200, 206, 500
  ← path: parentWorkTypeID:int; query: searchText?:str, assetID?:any, workTypeID?:any, contractID?:any, criticalityID?:any, checkListID?:any, isPublished?:enum(true, false) → map<WorkTypes.ListResult>
- `GET /WorkTypes/{workTypeID}/checkLists` — Возвращает список чек-листов вида работ · права: WorkTypeCheckListList · paginated · коды: 200, 206
  ← path: workTypeID:int → map<CheckLists.GetResult[]>
