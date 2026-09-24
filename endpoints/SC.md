# SC — справочник ручек

> **Что здесь:** все ручки сервиса SC (HubEx SC APIs): сигнатуры, параметры, права. Типы — schemas/SC.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SC.md`; грабли — `notes/SC.md` (если есть).

Base: `{BASE_URL}/SC`
> Примеры ответов вынесены в [../examples/SC.md](../examples/SC.md).

**Оглавление**

- ContractAttributes — строки 14–16
- ServiceContract — строки 18–70

## ContractAttributes
- `POST /ContractAttributes` — Обновляет сведения о пользовательских полях договоров · коды: 202 · примеры
  ← body: SCCAActionData[]

## ServiceContract
- `GET /ServiceContract` — Получение списка договоров обслуживания · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, taskID?:int, assetID?:int, includeUniversalContractsInAssetFilter?:bool, companyID?:int, contactID?:int, validFrom?:datetime, validTill?:datetime → map<ContractListResult>
- `POST /ServiceContract` — Создание договоров обслуживания · коды: 201 · примеры
  ← body: ContractMergeData[] → int[]
- `PUT /ServiceContract` — Изменение договоров обслуживания · коды: 202 · примеры
  ← body: ContractMergeData[]
- `DELETE /ServiceContract` — Удаление договоров обслуживания · коды: 202, 409 · примеры
  ← body: int[]
- `HEAD /ServiceContract` — Получение общего количества договоров обслуживания · коды: 200, 206 · примеры
  ← query: searchText?:str, taskID?:int, assetID?:int, includeUniversalContractsInAssetFilter?:bool, companyID?:int, contactID?:int, validFrom?:datetime, validTill?:datetime
- `GET /ServiceContract/{contractID}` — Получение договора обслуживания по идентификатору · коды: 200, 404 · примеры
  ← path: contractID:int → ContractGetResult
- `GET /ServiceContract/{contractID}/assets` — Возвращает список объектов, привязанных к сервисному договору · коды: 200, 204, 206 · примеры
  ← path: contractID:int → map<AssetResultBase>
- `POST /ServiceContract/{contractID}/assets` — Добавляет список объектов к сервисному договору · коды: 201, 204, 409 · примеры
  ← path: contractID:int; body: ContractAssetData[] → ContractAssetAddProjection[]
- `DELETE /ServiceContract/{contractID}/assets` — Удаляет список объектов, привязанных к сервисному договору · коды: 202, 409 · примеры
  ← path: contractID:int; body: int[]
- `PUT /ServiceContract/{contractID}/assets/{assetID}` — Добавляет объект к сервисному договору · коды: 201, 204, 409 · примеры
  ← path: contractID:int, assetID:int; query: includeChildren?:bool → ContractAssetAddProjection[]
- `DELETE /ServiceContract/{contractID}/assets/{assetID}` — Удаляет объект, привязанный к сервисному договору · коды: 202, 409 · примеры
  ← path: contractID:int, assetID:int
- `GET /ServiceContract/{contractID}/attachment/{attachmentID}` — Возвращает прикреплённый к договору файл-вложение · коды: 200, 204, 500 · примеры
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int → RAAttachmentResult
- `GET /ServiceContract/{contractID}/attachments` — Возвращает список файлов-вложений, прикреплённых к договору · коды: 200, 204, 206, 500 · примеры
  ← path: contractID:int; query: thumbnailSize?:int → map<AttachmentListResult>
- `POST /ServiceContract/{contractID}/attachments` — Связывает договор с существующими вложениями · коды: 201 · примеры
  ← path: contractID:int; body: int[] → AttachmentActionResultBase[]
- `DELETE /ServiceContract/{contractID}/attachments` — Помечает связи договора и вложений как удалённые · коды: 202 · примеры
  ← path: contractID:int; body: int[]
- `POST /ServiceContract/{contractID}/attachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к договору (данные из тела запроса) · коды: 201, 400 · примеры
  ← path: contractID:int; body: FromBodyUploadData → UploadResult
- `POST /ServiceContract/{contractID}/attachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к договору (данные из формы) · коды: 201, 400 · примеры
  ← path: contractID:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → UploadResult
- `GET /ServiceContract/{contractID}/attachments/{attachmentID}` — Возвращает временную ссылку для скачивания файла-вложения · коды: 200, 204, 307, 500 · примеры
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool → ANCRAttachmentResult
- `GET /ServiceContract/{contractID}/attributes` — Возвращает список пользовательских полей сервисного договора · коды: 200, 204, 206, 400 · примеры
  ← path: contractID:int → ContractAttributeResult[]
- `GET /ServiceContract/{contractID}/contacts` — Возвращает список контактов, привязанных к сервисному договору · коды: 200, 204, 206 · примеры
  ← path: contractID:int → map<ContactResultBase>
- `POST /ServiceContract/{contractID}/contacts` — Добавляет список контактов к сервисному договору · коды: 201, 204, 409 · примеры
  ← path: contractID:int; body: int[] → ContractContactAddProjection[]
- `DELETE /ServiceContract/{contractID}/contacts` — Удаляет список контактов, привязанных к сервисному договору · коды: 202, 409 · примеры
  ← path: contractID:int; body: int[]
- `PUT /ServiceContract/{contractID}/contacts/{contactID}` — Добавляет контакт к сервисному договору · коды: 201, 204, 409 · примеры
  ← path: contractID:int, contactID:int → ContractContactAddProjection
- `DELETE /ServiceContract/{contractID}/contacts/{contactID}` — Удаляет контакт, привязанный к сервисному договору · коды: 202, 409 · примеры
  ← path: contractID:int, contactID:int
- `POST /ServiceContract/{contractID}/v2/attachments/upload/fromForm` — Загружает несколько файлов на файловый сервер и привязывает их к договору (данные из формы) · коды: 201, 400 · примеры
  ← path: contractID:int; body: { Attachments?: FromFormUploadData[] /* Данные загружаемого файла, полученные из формы */ } → UploadResult[]
- `DELETE /ServiceContract/{id}` — Удаление договора обслуживания по идентификатору · коды: 202, 409 · примеры
  ← path: id:int
