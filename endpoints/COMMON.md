# COMMON — справочник ручек

> **Что здесь:** все ручки сервиса COMMON (API for managing common dictionaries in HubEx): сигнатуры, параметры, права. Типы — schemas/COMMON.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/COMMON.md`; грабли — `notes/COMMON.md` (если есть).
> **Источник:** `snapshots/COMMON.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/COMMON`

## Applications
- `GET /Applications` — Возвращает список  веток · права: ApplicationList · paginated
  → map<ApplicationResult>

## Attachments
- `GET /Attachments` — Список вложенных файлов, доступных пользователю · права: AttachmentsList · paginated
  ← query: assetID?:any, taskID?:any, assetTemplateID?:any, attachmentID?:any, isDeleted?:enum(true, false) → map<Attachments.ListResult>
- `DELETE /Attachments` — Помечает вложения и все связи как удаленные · права: AttachmentDelete
  ← body: int[]
- `GET /Attachments/content/{container}/{filePath}`
  ← path: filePath:str, container:str; query: temp_url_sig?:str, temp_url_expires?:int, filename?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /Attachments/downloadLink` — Получить URL и список необходимых данных, для возможности скачивания архива с файлами для заявок (не более 100) · права: AttachmentsList · paginated
  ← query: taskID?:any, isDeleted?:enum(true, false) → DownloadLinkResult
- `POST /Attachments/upload/fromBody` — Загружает файл на файловый сервер. Данные будут получены из тела запроса. · права: AttachmentUpload
  ← body: FromBodyUploadData → UploadResult
- `POST /Attachments/upload/fromForm` — Загружает файл на файловый сервер. Данные будут получены из формы. · права: AttachmentUpload
  ← body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → UploadResult
- `POST /Attachments/v2/upload/fromForm` — Загружает несколько файлов на файловый сервер. Данные будут получены из формы. · права: AttachmentUpload
  ← body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → UploadResult
- `GET /Attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · права: AttachmentDownload · paginated
  ← path: attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `DELETE /Attachments/{attachmentID}` — Помечает вложение и все связи как удаленные · права: AttachmentDelete
  ← path: attachmentID:int
- `POST /Attachments/{attachmentID}/publish` — Метод публикации файла для ообщего доступа · права: AttachmentPublish
  ← path: attachmentID:int
- `GET /Attachments/{attachmentID}/roles` — Возвращает список ролей, для которых эксклюзивно доступен вложенный файл · права: RoleAttachmentsList · paginated
  ← path: attachmentID:int → map<str>
- `GET /Attachments/{attachmentID}/this` — Метод получения данных вложения · права: AttachmentsList
  ← path: attachmentID:int → Attachments.GetResult
- `POST /Attachments/{attachmentID}/unpublish` — Метод публикации файла для ообщего доступа · права: AttachmentPublish
  ← path: attachmentID:int

## AttributeListOfValues
- `POST /AttributeListOfValues` — Метод сохранения списка допустимых значений · права: AttributeListOfValueMerge
  ← body: MergeData[]

## AttributeTypes
- `GET /AttributeTypes` — Метод возвращает список доступных типов (доп.полей) атрибутов · права: AttributeTypeList · paginated
  → map<AttributeTypes.ListResult>
- `GET /AttributeTypes/v2` — Возвращает плоский список типов атрибутов (доп.полей) с доменами, если существует такое сопоставление · права: AttributeTypeList · paginated
  → ExtListResult[]

## Attributes
- `GET /Attributes` — Метод получения данных атрибута · права: AttributeList · paginated
  ← query: isDeleted?:enum(true, false), isPublic?:enum(true, false), isRelevantForTask?:enum(true, false), isRelevantForAsset?:enum(true, false), isRelevantForCheckList?:enum(true, false), isRelevantForCompletedWork?:enum(true, false), isRelevantForCompany?:enum(true, false), isRelevantForContract?:enum(true, false), IsRelevantForCustomer?:enum(true, false), IsRelevantForTechnician?:enum(true, false) → map<AttributeResultList>
- `POST /Attributes` — Метод создания атрибута · права: AttributeAdd
  ← body: Attribute.AddData[]
- `PUT /Attributes` — Метод изменения атрибутов · права: AttributeUpdate
  ← body: Attribute.UpdateData[]
- `DELETE /Attributes` — Метод удаления атрибутов · права: AttributeDelete
  ← body: int[]
- `GET /Attributes/{attributeID}` — Метод получения данных атрибута · права: AttributeGet
  ← path: attributeID:int → AttributeResultGet
- `GET /Attributes/{attributeID}/listOfValues` — Метод получения допустимых значений для атрибута · права: AttributeListOfValuesList · paginated
  ← path: attributeID:int → map<str>
- `DELETE /Attributes/{id}` — Метод удаления атрибута · права: AttributeDelete
  ← path: id:int

## Banks
- `GET /Banks` — Метод получения списка банков · права: BankList · paginated
  ← query: searchText?:str, isActive?:enum(true, false) → map<BankResult>
- `GET /Banks/{bankId}` — Метод получения данных банка · права: BankGet
  ← path: bankId:int → BankResult

## Contacts
- `GET /Contacts` — Метод получения данных контакта · права: ContactsList · paginated
  ← query: searchText?:str, isDeleted?:enum(true, false), contactID?:any → map<Contacts.ListResult>
- `POST /Contacts` — Метод создания контакта · права: ContactAdd
  ← body: Contact.AddData[]
- `PUT /Contacts` — Метод изменения контактов · права: ContactUpdate
  ← body: Contact.UpdateData[]
- `DELETE /Contacts` — Метод удаления контактов · права: ContactDelete
  ← body: int[]
- `GET /Contacts/{contactID}` — Метод получения данных контакта · права: ContactGet
  ← path: contactID:int → Contacts.GetResult
- `DELETE /Contacts/{id}` — Метод удаления контакта · права: ContactDelete
  ← path: id:int

## Countries
- `GET /Countries` — Метод получения списка стран · права: CountriesList · paginated
  → map<Countries.ListResult>

## Currencies
- `GET /Currencies` — Метод получения списка валют · права: CurrenciesList · paginated
  → map<Currencies.ListResult>

## Events
- `GET /Events` — Метод получения списка доступных событий · права: EventList · paginated
  ← query: eventTransportTypeID?:any, isSystem?:enum(true, false), isHidden?:enum(true, false) → Events.ListResult[]

## MeasurementUnits
- `GET /MeasurementUnits` — Метод получения списка единиц измерения · права: MeasurementUnitList · paginated
  → map<MeasurementUnitResult>

## PowerBIReports
- `GET /PowerBIReports` — Метод получения информации по PowerBI отчетам · права: PowerBIReportList · paginated
  → PowerBIReportResult[]
- `GET /PowerBIReports/{id}` — Метод получения данных отчета · права: PowerBIReportGet
  ← path: id:int → PowerBIReportResult

## SystemTags
- `GET /SystemTags` — Метод получения списка доступных системных тэгов · права: TagsList · paginated
  → IdNameResult<Int16>[]

## Tags
- `GET /Tags` — Метод получения списка доступных тэгов · права: TagsList · paginated
  ← query: searchText?:str → str[]

## Timezones
- `GET /Timezones` — Метод получения списка временных зон · права: TimezonesList · paginated
  → map<Timezones.ListResult>
- `GET /Timezones/info` — Метод получения часового пояса тенанта · права: TimezonesList · paginated
  ← query: timezoneId?:int → TimezoneGetResult
