# COMMON — справочник ручек

> **Что здесь:** все ручки сервиса COMMON (API for managing common dictionaries in HubEx): сигнатуры, параметры, права. Типы — schemas/COMMON.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/COMMON.md`; грабли — `notes/COMMON.md` (если есть).

Base: `{BASE_URL}/COMMON`
> Примеры ответов вынесены в [../examples/COMMON.md](../examples/COMMON.md).

**Оглавление**

- Applications — строки 27–30
- Attachments — строки 32–71
- AttributeListOfValues — строки 73–76
- AttributeTypes — строки 78–84
- Attributes — строки 86–107
- Banks — строки 109–115
- Contacts — строки 117–135
- Countries — строки 137–140
- Currencies — строки 142–145
- Events — строки 147–150
- MeasurementUnits — строки 152–155
- PowerBIReports — строки 157–163
- SystemTags — строки 165–168
- Tags — строки 170–173
- Timezones — строки 175–181

## Applications
- `GET /Applications` — Возвращает список приложений. · paginated · коды: 200, 204, 206 · примеры
  → map<ApplicationResult>
  Метод используется для получения справочника приложений. Поддерживает диапазон через заголовок `Range`.

## Attachments
- `GET /Attachments` — Возвращает список вложений. · paginated · коды: 200, 204, 206 · примеры
  ← query: assetID?:int, taskID?:int, assetTemplateID?:int, attachmentID?:int, isDeleted?:bool → map<RAListResult>
  Поддерживает фильтрацию по связанным сущностям и флагам, а также ограничение результата через заголовок `Range`.
- `DELETE /Attachments` — Удаляет несколько вложений. · коды: 202, 500 · примеры
  ← body: int[]
  Помечает переданные вложения и их связи как удаленные.
- `GET /Attachments/content/{container}/{filePath}` — Скачивает файл по временной подписи файлового хранилища. · коды: 200, 500 · примеры
  ← path: filePath:str, container:str; query: temp_url_sig?:str, temp_url_expires?:int, filename?:str
  Метод доступен без авторизации, так как использует временную подпись файлового сервера.
- `GET /Attachments/downloadLink` — Подготавливает данные для скачивания архива вложений по заявкам. · paginated · коды: 200, 204, 206, 500 · примеры
  ← query: taskID?:int, isDeleted?:bool → FSRDownloadLinkResult
  Используется для формирования архива файлов по списку заявок. В одном запросе поддерживается не более 100 заявок.
- `POST /Attachments/upload/fromBody` — Загружает один файл из тела запроса. · коды: 201, 400 · примеры
  ← body: FromBodyUploadData → RAUploadResult
  Используется для сценариев, где содержимое файла и метаданные передаются в JSON-теле запроса.
- `POST /Attachments/upload/fromForm` — Загружает один файл из multipart/form-data. · коды: 201, 400 · примеры
  ← body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → RAUploadResult
  Используется для загрузки одного вложения из HTML-формы.
- `POST /Attachments/v2/upload/fromForm` — Загружает несколько файлов из multipart/form-data. · коды: 201, 400 · примеры
  ← body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → RAUploadResult[]
  Используется для пакетной загрузки вложений из формы.
- `GET /Attachments/{attachmentID}` — Возвращает временную ссылку для скачивания вложения. · коды: 200, 307, 400, 500 · примеры
  ← path: attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
  В зависимости от параметра `noRedirect` метод либо возвращает редирект на файл, либо отдает ссылку в теле ответа.
- `DELETE /Attachments/{attachmentID}` — Удаляет вложение по идентификатору. · коды: 202, 500 · примеры
  ← path: attachmentID:int
  Помечает вложение и все его связи как удаленные.
- `POST /Attachments/{attachmentID}/publish` — Публикует вложение для общего доступа. · коды: 202 · примеры
  ← path: attachmentID:int → PublishResult
  После публикации вложение получает публичную ссылку.
- `GET /Attachments/{attachmentID}/roles` — Возвращает роли, имеющие доступ к вложению. · paginated · коды: 200, 204, 206 · примеры
  ← path: attachmentID:int → map<str>
  Метод возвращает роли, для которых вложение доступно как защищенный файл. Поддерживает диапазон через заголовок `Range`.
- `GET /Attachments/{attachmentID}/this` — Возвращает данные вложения. · коды: 200, 204 · примеры
  ← path: attachmentID:int → RAGetResult
  Возвращает метаданные вложения без скачивания бинарного содержимого.
- `POST /Attachments/{attachmentID}/unpublish` — Снимает публикацию с вложения. · коды: 202 · примеры
  ← path: attachmentID:int
  После вызова публичная ссылка перестает быть доступной.

## AttributeListOfValues
- `POST /AttributeListOfValues` — Сохраняет список допустимых значений атрибута. · коды: 202, 400 · примеры
  ← body: COMMONALOVMergeData[]
  Метод принимает набор значений и объединяет его с текущими данными атрибута. Используется для создания, обновления и удаления значений в одном запросе.

## AttributeTypes
- `GET /AttributeTypes` — Возвращает список типов атрибутов. · paginated · коды: 200, 206 · примеры
  → map<RATListResult>
  Возвращает сгруппированный справочник типов пользовательских полей. Поддерживает диапазон через заголовок `Range`.
- `GET /AttributeTypes/v2` — Возвращает плоский список типов атрибутов с доменами. · paginated · коды: 200, 206 · примеры
  → ExtListResult[]
  В отличие от базового метода, возвращает записи в плоском виде, включая связанный домен, если он есть. Поддерживает диапазон через заголовок `Range`.

## Attributes
- `GET /Attributes` — Возвращает список атрибутов. · paginated · коды: 200, 204, 206 · примеры
  ← query: isDeleted?:bool, isPublic?:bool, isRelevantForTask?:bool, isRelevantForAsset?:bool, isRelevantForCheckList?:bool, isRelevantForCompletedWork?:bool, isRelevantForCompany?:bool, isRelevantForContract?:bool, IsRelevantForCustomer?:bool, IsRelevantForTechnician?:bool → map<AttributeResultList>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `POST /Attributes` — Создает атрибуты. · коды: 201, 400 · примеры
  ← body: COMMONAttributeAddData[]
  Метод принимает коллекцию пользовательских полей и создает их в текущем тенанте.
- `PUT /Attributes` — Обновляет атрибуты. · коды: 202, 400 · примеры
  ← body: COMMONAUpdateData[]
  Метод принимает коллекцию изменений и применяет их к существующим пользовательским полям.
- `DELETE /Attributes` — Удаляет несколько атрибутов. · коды: 202, 400 · примеры
  ← body: int[]
  Метод принимает коллекцию идентификаторов и удаляет соответствующие пользовательские поля.
- `GET /Attributes/{attributeID}` — Возвращает атрибут по идентификатору. · коды: 200, 204 · примеры
  ← path: attributeID:int → AttributeResultGet
  Возвращает пользовательское поле вместе со списком допустимых значений, если они настроены.
- `GET /Attributes/{attributeID}/listOfValues` — Возвращает допустимые значения атрибута. · paginated · коды: 200, 204, 206 · примеры
  ← path: attributeID:int → map<str>
  Метод используется для пользовательских полей со списком значений. Поддерживает диапазон через заголовок `Range`.
- `DELETE /Attributes/{id}` — Удаляет атрибут по идентификатору. · коды: 202, 400 · примеры
  ← path: id:int
  Является сокращенной формой группового удаления для одного пользовательского поля.

## Banks
- `GET /Banks` — Возвращает список банков. · paginated · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isActive?:bool → map<BankResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`.
- `GET /Banks/{bankId}` — Возвращает данные банка по идентификатору. · коды: 200, 404 · примеры
  ← path: bankId:int → BankResult
  Используется для открытия карточки банка или проверки существования записи.

## Contacts
- `GET /Contacts` — Возвращает список контактов. · paginated · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, contactID?:int → map<RContactsListResult>
  Поддерживает фильтрацию по query-параметрам и ограничение результата через заголовок `Range`. Если диапазон не передан, применяется стандартное ограничение на размер выборки.
- `POST /Contacts` — Создает контакты. · коды: 201, 400 · примеры
  ← body: COMMONCAddData[]
  Метод принимает коллекцию контактов и создает их в текущем тенанте.
- `PUT /Contacts` — Обновляет контакты. · коды: 202, 400 · примеры
  ← body: COMMONCUpdateData[]
  Метод принимает коллекцию изменений и применяет их к существующим контактам.
- `DELETE /Contacts` — Удаляет несколько контактов. · коды: 202, 400 · примеры
  ← body: int[]
  Метод принимает коллекцию идентификаторов и помечает соответствующие контакты как удаленные.
- `GET /Contacts/{contactID}` — Возвращает контакт по идентификатору. · коды: 200, 204 · примеры
  ← path: contactID:int → RCGetResult
  Используется для открытия карточки контакта.
- `DELETE /Contacts/{id}` — Удаляет контакт по идентификатору. · коды: 202, 400 · примеры
  ← path: id:int
  Является сокращенной формой группового удаления для одного контакта.

## Countries
- `GET /Countries` — Возвращает список стран. · paginated · коды: 200, 204, 206 · примеры
  → map<RCountriesListResult>
  Метод используется для заполнения справочников стран. Поддерживает диапазон через заголовок `Range`.

## Currencies
- `GET /Currencies` — Возвращает список валют. · paginated · коды: 200, 204, 206 · примеры
  → map<RCurrenciesListResult>
  Используется для заполнения справочников валют в интерфейсах HubEx. При передаче заголовка диапазона возвращает частичный набор записей.

## Events
- `GET /Events` — Возвращает список событий. · paginated · коды: 200, 204, 206 · примеры
  ← query: eventTransportTypeID?:int, isSystem?:bool, isHidden?:bool → map<REListResult>
  Позволяет отфильтровать события по типу транспорта, системному признаку и признаку скрытия. Поддерживает диапазон через заголовок `Range`.

## MeasurementUnits
- `GET /MeasurementUnits` — Возвращает список единиц измерения. · paginated · коды: 200, 204, 206 · примеры
  → map<MeasurementUnitResult>
  Используется для вывода справочника единиц измерения. При наличии заголовка диапазона возвращает частичный результат.

## PowerBIReports
- `GET /PowerBIReports` — Возвращает список Power BI отчетов. · paginated · коды: 200, 204, 206 · примеры
  → PowerBIReportResult[]
  Используется для получения списка отчетов, доступных пользователю. Поддерживает диапазон через заголовок `Range`.
- `GET /PowerBIReports/{id}` — Возвращает Power BI отчет по идентификатору. · коды: 200, 404 · примеры
  ← path: id:int → PowerBIReportResult
  Используется для получения детальной информации о конкретном отчете.

## SystemTags
- `GET /SystemTags` — Возвращает список системных тегов. · paginated · коды: 200, 204, 206 · примеры
  → IdNameResultOfShort[]
  Метод отдает системные теги, доступные пользователю в текущем тенанте. Поддерживает диапазон через заголовок `Range`.

## Tags
- `GET /Tags` — Возвращает список тегов. · paginated · коды: 200, 204, 206 · примеры
  ← query: searchText?:str → str[]
  Если указан `searchText`, в ответ попадают только теги, соответствующие условию поиска. Поддерживается ограничение диапазоном через заголовок `Range`.

## Timezones
- `GET /Timezones` — Возвращает список часовых поясов. · paginated · коды: 200, 204, 206 · примеры
  → map<RTListResult>
  Метод отдает справочник доступных часовых поясов. Поддерживает диапазон через заголовок `Range`.
- `GET /Timezones/info` — Возвращает информацию о часовом поясе. · коды: 200, 204 · примеры
  ← query: timezoneId?:int → TimezoneGetResult
  Метод возвращает детальную информацию по часовому поясу по его идентификатору.
