# SC — справочник ручек

> **Что здесь:** все ручки сервиса SC (HubEx SC APIs): сигнатуры, параметры, права. Типы — schemas/SC.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SC.md`; грабли — `notes/SC.md` (если есть).

Base: `{BASE_URL}/SC`

**Оглавление**

- ContractAttributes — строки 13–15
- ServiceContract — строки 17–69

## ContractAttributes
- `POST /ContractAttributes` — Обновляет сведения о пользовательских полях объектов · права: AssetAttributeMerge · коды: 202
  ← body: ActionData[]

## ServiceContract
- `GET /ServiceContract` — Метод получения списка договоров обслуживания · права: ContractList · paginated · коды: 200, 206
  ← query: searchText?:str, taskID?:any, assetID?:any, includeUniversalContractsInAssetFilter?:enum(true, false), companyID?:any, contactID?:any, validFrom?:any, validTill?:any, searchText?:str → map<ContractListResult>
- `POST /ServiceContract` — Метод для создания или обновления договора/договоров обслуживания · права: ContractMerge · коды: 201
  ← body: ContractMergeData[] → int[]
- `PUT /ServiceContract` — Метод изменения существующей заявки(ок) · права: ContractMerge · коды: 202
  ← body: ContractMergeData[]
- `DELETE /ServiceContract` — Метод для удаления договоров · права: ContractDelete · коды: 202
  ← body: int[]
- `HEAD /ServiceContract` — Метод получения общего количества договоров обслуживания · права: ContractList · коды: 200
  ← query: searchText?:str, taskID?:any, assetID?:any, includeUniversalContractsInAssetFilter?:enum(true, false), companyID?:any, contactID?:any, validFrom?:any, validTill?:any, searchText?:str
- `GET /ServiceContract/{contractID}` — Метод получения договора обслуживания по ID · права: ContractGet · коды: 200
  ← path: contractID:int → ContractGetResult
- `GET /ServiceContract/{contractID}/assets` — Метод получения списка объектов сервисного договора · права: ContractAssetsList · paginated · коды: 200, 206, 400
  ← path: contractID:int → map<AssetResultBase>
- `POST /ServiceContract/{contractID}/assets` — Добавить список объектов к договору · права: ContractAssetAdd · коды: 201, 409
  ← path: contractID:int; body: ContractAssetData[] → ContractAssetAddProjection[]
- `DELETE /ServiceContract/{contractID}/assets` — Метод удаления объектов связанных с договорами · права: ContractAssetDelete · коды: 202, 409
  ← path: contractID:int; body: int[]
- `PUT /ServiceContract/{contractID}/assets/{assetID}` — Добавить объект к договору · права: ContractAssetAdd · коды: 201, 409
  ← path: contractID:int, assetID:int; query: includeChildren?:bool → ContractAssetAddProjection
- `DELETE /ServiceContract/{contractID}/assets/{assetID}` — Метод удаления объекта сязанного с сервисным договором · права: ContractAssetDelete · коды: 202, 409
  ← path: contractID:int, assetID:int
- `GET /ServiceContract/{contractID}/attachment/{attachmentID}` — Метод получения прикрепленного к договору файла вложения · права: ContractAttachmentGet · коды: 200, 500
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int → AttachmentResult
- `GET /ServiceContract/{contractID}/attachments` — Метод получения списка файлов вложений прикрепленных к договору · права: ContractAttachmentsList · paginated · коды: 200, 206, 500
  ← path: contractID:int; query: thumbnailSize?:int → map<AttachmentListResult>
- `POST /ServiceContract/{contractID}/attachments` — Метод связывающий договор и вложение · права: ContractAttachmentAdd · коды: 201, 500
  ← path: contractID:int; body: int[] → AttachmentActionResultBase[]
- `DELETE /ServiceContract/{contractID}/attachments` — Метод помечает связку договора и вложения как удаленную · права: ContractAttachmentDelete · коды: 202, 500
  ← path: contractID:int; body: int[]
- `POST /ServiceContract/{contractID}/attachments/upload/fromBody` — Метод загружает файл на файловый сервер и привязывает его к договору. Данные будут получены из тела запроса. · права: ContractAttachmentUpload · коды: 201, 500
  ← path: contractID:int; body: FromBodyUploadData → UploadResult
- `POST /ServiceContract/{contractID}/attachments/upload/fromForm` — Метод загружает файл на файловый сервер и привязывает его к договору. Данные будут получены из формы. · права: ContractAttachmentUpload · коды: 201, 500
  ← path: contractID:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → UploadResult
- `GET /ServiceContract/{contractID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · права: ContractAttachmentDownload · paginated · коды: 206, 303
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /ServiceContract/{contractID}/attributes` — Возвращает список пользовтельских полей по договору · права: ContractAttributesList · paginated · коды: 200, 206, 400
  ← path: contractID:int → ContractAttributeResult[]
- `GET /ServiceContract/{contractID}/contacts` — Метод получения списка контактов ответственных по договору · права: ContractContactList · paginated · коды: 200, 206, 400
  ← path: contractID:int → map<ContactResultBase>
- `POST /ServiceContract/{contractID}/contacts` — Метод добавления контактов к договорам · права: ContractContactAdd · коды: 201, 409
  ← path: contractID:int; body: int[] → ContractContactAddProjection[]
- `DELETE /ServiceContract/{contractID}/contacts` — Метод удаления контактов привязанных к договорам · права: ContractContactDelete · коды: 202, 409
  ← path: contractID:int; body: int[]
- `PUT /ServiceContract/{contractID}/contacts/{contactID}` — Метод добавления контакта к договору · права: ContractContactAdd · коды: 201, 409
  ← path: contractID:int, contactID:int → ContractContactAddProjection
- `DELETE /ServiceContract/{contractID}/contacts/{contactID}` — Метод удаления контакта привязанного к договору по Id · права: ContractContactDelete · коды: 202, 409
  ← path: contractID:int, contactID:int
- `POST /ServiceContract/{contractID}/v2/attachments/upload/fromForm` — Метод загружает файлы на файловый сервер и привязывает его к договору. Данные будут получены из формы. · права: ContractAttachmentUpload · коды: 201, 500
  ← path: contractID:int; body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → UploadResult
- `DELETE /ServiceContract/{id}` — Метод для удаления договора · права: ContractDelete · коды: 202, 409
  ← path: id:int
