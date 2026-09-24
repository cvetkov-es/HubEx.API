# SC — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса SC (HubEx SC APIs): сигнатуры, параметры, права. Типы — schemas/SC.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SC.md`; грабли — `notes/SC.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/SC`
> Примеры ответов вынесены в [../examples/SC.md](../examples/SC.md).

**Оглавление**

- ServiceContract — строки 14–32

## ServiceContract
- `GET /ServiceContract` — Получение списка договоров обслуживания · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, taskID?:int, assetID?:int, includeUniversalContractsInAssetFilter?:bool, companyID?:int, contactID?:int, validFrom?:datetime, validTill?:datetime → map<ContractListResult>
- `HEAD /ServiceContract` — Получение общего количества договоров обслуживания · коды: 200, 206 · примеры
  ← query: searchText?:str, taskID?:int, assetID?:int, includeUniversalContractsInAssetFilter?:bool, companyID?:int, contactID?:int, validFrom?:datetime, validTill?:datetime
- `GET /ServiceContract/{contractID}` — Получение договора обслуживания по идентификатору · коды: 200, 404 · примеры
  ← path: contractID:int → ContractGetResult
- `GET /ServiceContract/{contractID}/assets` — Возвращает список объектов, привязанных к сервисному договору · коды: 200, 204, 206 · примеры
  ← path: contractID:int → map<AssetResultBase>
- `GET /ServiceContract/{contractID}/attachment/{attachmentID}` — Возвращает прикреплённый к договору файл-вложение · коды: 200, 204, 500 · примеры
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int → RAAttachmentResult
- `GET /ServiceContract/{contractID}/attachments` — Возвращает список файлов-вложений, прикреплённых к договору · коды: 200, 204, 206, 500 · примеры
  ← path: contractID:int; query: thumbnailSize?:int → map<AttachmentListResult>
- `GET /ServiceContract/{contractID}/attachments/{attachmentID}` — Возвращает временную ссылку для скачивания файла-вложения · коды: 200, 204, 307, 500 · примеры
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool → ANCRAttachmentResult
- `GET /ServiceContract/{contractID}/attributes` — Возвращает список пользовательских полей сервисного договора · коды: 200, 204, 206, 400 · примеры
  ← path: contractID:int → ContractAttributeResult[]
- `GET /ServiceContract/{contractID}/contacts` — Возвращает список контактов, привязанных к сервисному договору · коды: 200, 204, 206 · примеры
  ← path: contractID:int → map<ContactResultBase>
