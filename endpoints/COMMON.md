# COMMON — справочник ручек

> **Что здесь:** все ручки сервиса COMMON (API for managing common dictionaries in HubEx): сигнатуры, параметры, права. Типы — schemas/COMMON.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/COMMON.md`; грабли — `notes/COMMON.md` (если есть).

Base: `{BASE_URL}/COMMON`

**Оглавление**

- Applications — строки 26–28
- Attachments — строки 30–57
- AttributeListOfValues — строки 59–61
- AttributeTypes — строки 63–67
- Attributes — строки 69–83
- Banks — строки 85–89
- Contacts — строки 91–103
- Countries — строки 105–107
- Currencies — строки 109–111
- Events — строки 113–115
- MeasurementUnits — строки 117–119
- PowerBIReports — строки 121–125
- SystemTags — строки 127–129
- Tags — строки 131–133
- Timezones — строки 135–139

## Applications
- `GET /Applications` — Возвращает список  веток · права: ApplicationList · paginated · коды: 200, 206
  → map<ApplicationResult>

## Attachments
- `GET /Attachments` — Список вложенных файлов, доступных пользователю · права: AttachmentsList · paginated · коды: 200, 206
  ← query: assetID?:any, taskID?:any, assetTemplateID?:any, attachmentID?:any, isDeleted?:enum(true, false) → map<Attachments.ListResult>
- `DELETE /Attachments` — Помечает вложения и все связи как удаленные · права: AttachmentDelete · коды: 202, 500
  ← body: int[]
- `GET /Attachments/content/{container}/{filePath}` · коды: 200
  ← path: filePath:str, container:str; query: temp_url_sig?:str, temp_url_expires?:int, filename?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /Attachments/downloadLink` — Получить URL и список необходимых данных, для возможности скачивания архива с файлами для заявок (не более 100) · права: AttachmentsList · paginated · коды: 200, 206
  ← query: taskID?:any, isDeleted?:enum(true, false) → DownloadLinkResult
- `POST /Attachments/upload/fromBody` — Загружает файл на файловый сервер. Данные будут получены из тела запроса. · права: AttachmentUpload · коды: 201, 500
  ← body: FromBodyUploadData → UploadResult
- `POST /Attachments/upload/fromForm` — Загружает файл на файловый сервер. Данные будут получены из формы. · права: AttachmentUpload · коды: 201, 500
  ← body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → UploadResult
- `POST /Attachments/v2/upload/fromForm` — Загружает несколько файлов на файловый сервер. Данные будут получены из формы. · права: AttachmentUpload · коды: 201, 500
  ← body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → UploadResult
- `GET /Attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · права: AttachmentDownload · paginated · коды: 206, 307, 500
  ← path: attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `DELETE /Attachments/{attachmentID}` — Помечает вложение и все связи как удаленные · права: AttachmentDelete · коды: 202, 500
  ← path: attachmentID:int
- `POST /Attachments/{attachmentID}/publish` — Метод публикации файла для ообщего доступа · права: AttachmentPublish · коды: 202
  ← path: attachmentID:int → PublishResult
- `GET /Attachments/{attachmentID}/roles` — Возвращает список ролей, для которых эксклюзивно доступен вложенный файл · права: RoleAttachmentsList · paginated · коды: 200, 206
  ← path: attachmentID:int → map<str>
- `GET /Attachments/{attachmentID}/this` — Метод получения данных вложения · права: AttachmentsList · коды: 200
  ← path: attachmentID:int → Attachments.GetResult
- `POST /Attachments/{attachmentID}/unpublish` — Метод публикации файла для ообщего доступа · права: AttachmentPublish · коды: 202
  ← path: attachmentID:int

## AttributeListOfValues
- `POST /AttributeListOfValues` — Метод сохранения списка допустимых значений · права: AttributeListOfValueMerge · коды: 202
  ← body: MergeData[]

## AttributeTypes
- `GET /AttributeTypes` — Метод возвращает список доступных типов (доп.полей) атрибутов · права: AttributeTypeList · paginated · коды: 200, 206
  → map<AttributeTypes.ListResult>
- `GET /AttributeTypes/v2` — Возвращает плоский список типов атрибутов (доп.полей) с доменами, если существует такое сопоставление · права: AttributeTypeList · paginated · коды: 200, 206
  → ExtListResult[]

## Attributes
- `GET /Attributes` — Метод получения данных атрибута · права: AttributeList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false), isPublic?:enum(true, false), isRelevantForTask?:enum(true, false), isRelevantForAsset?:enum(true, false), isRelevantForCheckList?:enum(true, false), isRelevantForCompletedWork?:enum(true, false), isRelevantForCompany?:enum(true, false), isRelevantForContract?:enum(true, false), IsRelevantForCustomer?:enum(true, false), IsRelevantForTechnician?:enum(true, false) → map<AttributeResultList>
- `POST /Attributes` — Метод создания атрибута · права: AttributeAdd · коды: 201
  ← body: Attribute.AddData[]
- `PUT /Attributes` — Метод изменения атрибутов · права: AttributeUpdate · коды: 202
  ← body: Attribute.UpdateData[]
- `DELETE /Attributes` — Метод удаления атрибутов · права: AttributeDelete · коды: 202
  ← body: int[]
- `GET /Attributes/{attributeID}` — Метод получения данных атрибута · права: AttributeGet · коды: 200
  ← path: attributeID:int → AttributeResultGet
- `GET /Attributes/{attributeID}/listOfValues` — Метод получения допустимых значений для атрибута · права: AttributeListOfValuesList · paginated · коды: 200, 206
  ← path: attributeID:int → map<str>
- `DELETE /Attributes/{id}` — Метод удаления атрибута · права: AttributeDelete · коды: 202
  ← path: id:int

## Banks
- `GET /Banks` — Метод получения списка банков · права: BankList · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isActive?:enum(true, false) → map<BankResult>
- `GET /Banks/{bankId}` — Метод получения данных банка · права: BankGet · коды: 200, 404
  ← path: bankId:int → BankResult

## Contacts
- `GET /Contacts` — Метод получения данных контакта · права: ContactsList · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), contactID?:any → map<Contacts.ListResult>
- `POST /Contacts` — Метод создания контакта · права: ContactAdd · коды: 201
  ← body: Contact.AddData[]
- `PUT /Contacts` — Метод изменения контактов · права: ContactUpdate · коды: 202
  ← body: Contact.UpdateData[]
- `DELETE /Contacts` — Метод удаления контактов · права: ContactDelete · коды: 202
  ← body: int[]
- `GET /Contacts/{contactID}` — Метод получения данных контакта · права: ContactGet · коды: 200, 204, 404
  ← path: contactID:int → Contacts.GetResult
- `DELETE /Contacts/{id}` — Метод удаления контакта · права: ContactDelete · коды: 202
  ← path: id:int

## Countries
- `GET /Countries` — Метод получения списка стран · права: CountriesList · paginated · коды: 200, 206
  → map<Countries.ListResult>

## Currencies
- `GET /Currencies` — Метод получения списка валют · права: CurrenciesList · paginated · коды: 200, 206
  → map<Currencies.ListResult>

## Events
- `GET /Events` — Метод получения списка доступных событий · права: EventList · paginated · коды: 200, 206
  ← query: eventTransportTypeID?:any, isSystem?:enum(true, false), isHidden?:enum(true, false) → Events.ListResult[]

## MeasurementUnits
- `GET /MeasurementUnits` — Метод получения списка единиц измерения · права: MeasurementUnitList · paginated · коды: 200, 206
  → map<MeasurementUnitResult>

## PowerBIReports
- `GET /PowerBIReports` — Метод получения информации по PowerBI отчетам · права: PowerBIReportList · paginated · коды: 200, 206
  → PowerBIReportResult[]
- `GET /PowerBIReports/{id}` — Метод получения данных отчета · права: PowerBIReportGet · коды: 200, 404
  ← path: id:int → PowerBIReportResult

## SystemTags
- `GET /SystemTags` — Метод получения списка доступных системных тэгов · права: TagsList · paginated · коды: 200, 206
  → IdNameResult<Int16>[]

## Tags
- `GET /Tags` — Метод получения списка доступных тэгов · права: TagsList · paginated · коды: 200, 206
  ← query: searchText?:str → str[]

## Timezones
- `GET /Timezones` — Метод получения списка временных зон · права: TimezonesList · paginated · коды: 200, 206
  → map<Timezones.ListResult>
- `GET /Timezones/info` — Метод получения часового пояса тенанта · права: TimezonesList · paginated · коды: 200, 206
  ← query: timezoneId?:int → TimezoneGetResult
