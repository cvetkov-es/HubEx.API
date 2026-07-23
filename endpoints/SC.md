# SC — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса SC (HubEx SC APIs): сигнатуры, параметры, права. Типы — schemas/SC.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/SC.md`; грабли — `notes/SC.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/SC`

**Оглавление**

- ServiceContract — строки 13–31

## ServiceContract
- `GET /ServiceContract` — Метод получения списка договоров обслуживания · права: ContractList · paginated · коды: 200, 206
  ← query: searchText?:str, taskID?:any, assetID?:any, includeUniversalContractsInAssetFilter?:enum(true, false), companyID?:any, contactID?:any, validFrom?:any, validTill?:any, searchText?:str → map<ContractListResult>
- `HEAD /ServiceContract` — Метод получения общего количества договоров обслуживания · права: ContractList · коды: 200
  ← query: searchText?:str, taskID?:any, assetID?:any, includeUniversalContractsInAssetFilter?:enum(true, false), companyID?:any, contactID?:any, validFrom?:any, validTill?:any, searchText?:str
- `GET /ServiceContract/{contractID}` — Метод получения договора обслуживания по ID · права: ContractGet · коды: 200
  ← path: contractID:int → ContractGetResult
- `GET /ServiceContract/{contractID}/assets` — Метод получения списка объектов сервисного договора · права: ContractAssetsList · paginated · коды: 200, 206, 400
  ← path: contractID:int → map<AssetResultBase>
- `GET /ServiceContract/{contractID}/attachment/{attachmentID}` — Метод получения прикрепленного к договору файла вложения · права: ContractAttachmentGet · коды: 200, 500
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int → AttachmentResult
- `GET /ServiceContract/{contractID}/attachments` — Метод получения списка файлов вложений прикрепленных к договору · права: ContractAttachmentsList · paginated · коды: 200, 206, 500
  ← path: contractID:int; query: thumbnailSize?:int → map<AttachmentListResult>
- `GET /ServiceContract/{contractID}/attachments/{attachmentID}` — Метод получения TemporaryRedirect на временную ссылку для скачки файла · права: ContractAttachmentDownload · paginated · коды: 206, 303
  ← path: contractID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /ServiceContract/{contractID}/attributes` — Возвращает список пользовтельских полей по договору · права: ContractAttributesList · paginated · коды: 200, 206, 400
  ← path: contractID:int → ContractAttributeResult[]
- `GET /ServiceContract/{contractID}/contacts` — Метод получения списка контактов ответственных по договору · права: ContractContactList · paginated · коды: 200, 206, 400
  ← path: contractID:int → map<ContactResultBase>
