# COMMON — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса COMMON (API for managing common dictionaries in HubEx): сигнатуры, параметры, права. Типы — schemas/COMMON.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/COMMON.md`; грабли — `notes/COMMON.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/COMMON`

**Оглавление**

- Applications — строки 26–28
- Attachments — строки 30–43
- AttributeTypes — строки 45–49
- Attributes — строки 51–57
- Banks — строки 59–63
- Contacts — строки 65–69
- Countries — строки 71–73
- Currencies — строки 75–77
- Events — строки 79–81
- MeasurementUnits — строки 83–85
- PowerBIReports — строки 87–91
- SystemTags — строки 93–95
- Tags — строки 97–99
- Timezones — строки 101–105

## Applications
- `GET /Applications` — Возвращает список  веток · права: ApplicationList · paginated · коды: 200, 206
  → map<ApplicationResult>

## Attachments
- `GET /Attachments` — Список вложенных файлов, доступных пользователю · права: AttachmentsList · paginated · коды: 200, 206
  ← query: assetID?:any, taskID?:any, assetTemplateID?:any, attachmentID?:any, isDeleted?:enum(true, false) → map<Attachments.ListResult>
- `GET /Attachments/content/{container}/{filePath}` · коды: 200
  ← path: filePath:str, container:str; query: temp_url_sig?:str, temp_url_expires?:int, filename?:str
  Выполнение данного метода резрешино от **анонимного пользователя**.
- `GET /Attachments/downloadLink` — Получить URL и список необходимых данных, для возможности скачивания архива с файлами для заявок (не более 100) · права: AttachmentsList · paginated · коды: 200, 206
  ← query: taskID?:any, isDeleted?:enum(true, false) → DownloadLinkResult
- `GET /Attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · права: AttachmentDownload · paginated · коды: 206, 307, 500
  ← path: attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Attachments/{attachmentID}/roles` — Возвращает список ролей, для которых эксклюзивно доступен вложенный файл · права: RoleAttachmentsList · paginated · коды: 200, 206
  ← path: attachmentID:int → map<str>
- `GET /Attachments/{attachmentID}/this` — Метод получения данных вложения · права: AttachmentsList · коды: 200
  ← path: attachmentID:int → Attachments.GetResult

## AttributeTypes
- `GET /AttributeTypes` — Метод возвращает список доступных типов (доп.полей) атрибутов · права: AttributeTypeList · paginated · коды: 200, 206
  → map<AttributeTypes.ListResult>
- `GET /AttributeTypes/v2` — Возвращает плоский список типов атрибутов (доп.полей) с доменами, если существует такое сопоставление · права: AttributeTypeList · paginated · коды: 200, 206
  → ExtListResult[]

## Attributes
- `GET /Attributes` — Метод получения данных атрибута · права: AttributeList · paginated · коды: 200, 206
  ← query: isDeleted?:enum(true, false), isPublic?:enum(true, false), isRelevantForTask?:enum(true, false), isRelevantForAsset?:enum(true, false), isRelevantForCheckList?:enum(true, false), isRelevantForCompletedWork?:enum(true, false), isRelevantForCompany?:enum(true, false), isRelevantForContract?:enum(true, false), IsRelevantForCustomer?:enum(true, false), IsRelevantForTechnician?:enum(true, false) → map<AttributeResultList>
- `GET /Attributes/{attributeID}` — Метод получения данных атрибута · права: AttributeGet · коды: 200
  ← path: attributeID:int → AttributeResultGet
- `GET /Attributes/{attributeID}/listOfValues` — Метод получения допустимых значений для атрибута · права: AttributeListOfValuesList · paginated · коды: 200, 206
  ← path: attributeID:int → map<str>

## Banks
- `GET /Banks` — Метод получения списка банков · права: BankList · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isActive?:enum(true, false) → map<BankResult>
- `GET /Banks/{bankId}` — Метод получения данных банка · права: BankGet · коды: 200, 404
  ← path: bankId:int → BankResult

## Contacts
- `GET /Contacts` — Метод получения данных контакта · права: ContactsList · paginated · коды: 200, 204, 206
  ← query: searchText?:str, isDeleted?:enum(true, false), contactID?:any → map<Contacts.ListResult>
- `GET /Contacts/{contactID}` — Метод получения данных контакта · права: ContactGet · коды: 200, 204, 404
  ← path: contactID:int → Contacts.GetResult

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
