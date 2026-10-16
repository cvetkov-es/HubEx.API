# COMMON — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса COMMON, вынесенные из `endpoints/COMMON.md`. Сигнатуры и типы — там же и в `schemas/COMMON.md`.

## Applications

### `GET /Applications`

## Пример запроса:
```text
GET /Applications
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "code": "LIC", "nameRu": "Лицензия" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ApplicationList`.
- 204 — справочник приложений пуст.

## Attachments

### `GET /Attachments`

## Пример запроса:
```text
GET /attachments?taskID=1001&isDeleted=false
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{
  "123": {
    "id": 123,
    "fileName": "photo.png",
    "description": "Фото для тестов",
    "publicUrl": "https://files.example.com/attachments/123",
    "isUploaded": false,
    "isProtected": false,
    "size": 1024,
    "created": "2026-08-19T10:44:42Z"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentsList`.
- 204 — вложения по указанным критериям не найдены.

### `DELETE /Attachments`

## Пример запроса:
```text
DELETE /attachments
Authorization: Bearer <token>
```
```json
[101, 102]
```
            
## Пример успешного ответа (202):
(пустой response body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentDelete`.
- 500 — во время удаления произошла внутренняя ошибка.

### `GET /Attachments/content/{container}/{filePath}`

## Пример запроса:
GET /attachments/content/container1/path/to/file.png?temp_url_sig=<sig>&temp_url_expires=1730000000&filename=file.png
            
## Успешный сценарий:
- 200 — бинарное содержимое файла.
            
## Негативные сценарии:
- 500 — внутренняя ошибка при скачивании файла (ошибка во время подготовки/загрузки).

### `GET /Attachments/downloadLink`

## Пример запроса:
```text
GET /attachments/downloadLink?taskID=1001&taskID=1002&isDeleted=false
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "downloadUrl": "https://storage.example.com/container/folder.zip",
  "headers": [
    { "name": "X-Auth-Token", "value": "token-example" }
  ],
  "expiresAfter": "2026-08-19T14:32:00Z"
}
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentsList`.
- 204 — для указанных заявок не найдено вложений или не передан ни один `taskID`.
- 500 — внутренняя ошибка при подготовке архива.

### `POST /Attachments/upload/fromBody`

## Пример запроса (JSON):
POST /attachments/upload/fromBody
Authorization: Bearer <token>
            
{
  "file": "<base64>",
  "fileName": "photo.png",
  "contentType": "image/png",
  "description": "Фото",
  "isPublic": false,
  "isIgnorePossibleDuplication": false,
  "checkSum": "md5hash",
  "roles": [ 1 ],
  "coordinate": "55.75,37.61"
}
            
## Пример успешного ответа (201):
{ "attachmentID": 123, "checkSum": "md5hash", "fileName": "photo.png", "isProtected": true }
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentUpload`.
- 400 — некорректный base64/empty file/checkSum.

### `POST /Attachments/upload/fromForm`

## Пример запроса (multipart/form-data):
POST /attachments/upload/fromForm
Authorization: Bearer <token>
Content-Type: multipart/form-data
Поля: file=<binary>, description=<text>, isPublic=<true|false>, isIgnorePossibleDuplication=<true|false>, roles=<short[]>, coordinate=<string>
            
## Пример успешного ответа (201):
{ "attachmentID": 123, "checkSum": "md5hash", "fileName": "photo.png", "isProtected": false }
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentUpload`.
- 400 — некорректные входные данные/пустой файл/несоответствие формата.

### `POST /Attachments/v2/upload/fromForm`

## Пример запроса:
POST /attachments/v2/upload/fromForm
Authorization: Bearer <token>
Body: { "attachments": [ { "file": <binary>, "fileName": "a.txt", "description": "..." , "isPublic": true, "roles": [ 1 ] } ] }
            
## Пример успешного ответа (201):
[ { "attachmentID": 123, "checkSum": "md5hash", "fileName": "a.txt", "isProtected": true }, { "attachmentID": 124, "checkSum": "md5hash2", "fileName": "b.txt", "isProtected": false } ]
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentUpload`.
- 400 — некорректные данные.

### `GET /Attachments/{attachmentID}`

## Пример запроса:
GET /attachments/123?thumbnailSize=128&noRedirect=false
Authorization: Bearer <token>
            
## Пример успешного ответа:
- 307 — редирект на временную ссылку на скачивание (noRedirect=false).
- 200 — если noRedirect=true: ссылка на файл отдается в теле ответа (формат зависит от DownloadAttachmentAsync2).
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentDownload`.
- 400 — некорректный thumbnailSize.
- 500 — ошибка при подготовке ссылки.

### `DELETE /Attachments/{attachmentID}`

## Пример запроса:
```text
DELETE /attachments/123
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
(пустой response body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentDelete`.
- 500 — во время удаления произошла внутренняя ошибка.

### `POST /Attachments/{attachmentID}/publish`

## Пример запроса:
```text
POST /attachments/123/publish
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
```json
{ "attachmentID": 123, "publicUrl": "https://storage.example.com/public/attachment/123" }
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentPublish`.
- 400 — неверный `attachmentID` (<= 0).

### `GET /Attachments/{attachmentID}/roles`

## Пример запроса:
```text
GET /attachments/123/roles
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": "Админ", "2": "Пользователь" }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `RoleAttachmentsList`.
- 204 — для вложения не настроены роли доступа.

### `GET /Attachments/{attachmentID}/this`

## Пример запроса:
```text
GET /attachments/123/this
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "id": 123,
  "fileName": "photo.png",
  "description": "Фото для тестов",
  "publicUrl": "https://files.example.com/attachments/123",
  "isUploaded": false,
  "isProtected": false,
  "size": 1024,
  "created": "2026-08-19T10:44:42Z"
}
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentsList`.
- 204 — вложение не найдено.

### `POST /Attachments/{attachmentID}/unpublish`

## Пример запроса:
```text
POST /attachments/123/unpublish
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
(пустой response body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttachmentPublish`.
- 400 — неверный `attachmentID` (<= 0).

## AttributeListOfValues

### `POST /AttributeListOfValues`

## Пример запроса (JSON):
```text
POST /AttributeListOfValues
Authorization: Bearer <token>
```
```json
[
  {
    "attributeID": 12,
    "data": [
      { "key": "VAL_1", "value": "Значение 1" },
      { "key": "VAL_2", "value": "Значение 2" }
    ]
  }
]
```
            
## Пример успешного ответа (202):
(пустой ответ body, операция принята к обработке)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeListOfValueMerge`.
- 400 — некорректные данные (невалидный attributeID, пустые/битые значения).

## AttributeTypes

### `GET /AttributeTypes`

## Пример запроса:
```text
GET /AttributeTypes
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "3": { "code": "TASK_ATTR", "name": "Атрибут задачи" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeTypeList`.

### `GET /AttributeTypes/v2`

## Пример запроса:
```text
GET /AttributeTypes/v2
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
[ { "id": 3, "code": "TASK_ATTR", "name": "Атрибут задачи", "domain": { "id": 1, "name": "Задача", "code": "TASK" } } ]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeTypeList`.

## Attributes

### `GET /Attributes`

## Пример запроса:
GET /Attributes?isDeleted=false&isPublic=true&isRelevantForTask=true
Authorization: Bearer <token>
Range: items=1-50
            
## Пример успешного ответа (200):
{ "12": { "name": "Договор №", "type": { "id": 5, "code": "DOC_NUM", "name": "Номер договора" }, "domain": { "id": 2, "name": "Договор", "code": "CONTRACT" }, "isPublic": true, "deleted": null, "relevantFor": { "task": true, "asset": false, "checkList": false, "completedWork": false, "contract": true, "company": false, "customer": false, "technician": false }, "listOfValues": { "VAL_1": "Значение 1" } } }
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeList`.
- 204 — атрибуты по фильтрам не найдены.

### `POST /Attributes`

## Пример запроса (JSON):
POST /Attributes
Authorization: Bearer <token>
            
[
  {
    "name": "Договор №",
    "attributeTypeID": 5,
    "domainID": 2,
    "isPublic": true,
    "measurementUnitID": 1,
    "isRelevantForTask": true,
    "isRelevantForAsset": false,
    "isRelevantForCheckList": false,
    "isRelevantForCompletedWork": false,
    "isRelevantForContract": true,
    "isRelevantForCompany": false,
    "isRelevantForCustomer": false,
    "isRelevantForTechnician": false
  }
]
            
## Пример успешного ответа (201):
[501]
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeAdd`.
- 400 — некорректные данные (невалидные ID типов/доменов, пустые обязательные поля и т.п.).

### `PUT /Attributes`

## Пример запроса (JSON):
PUT /Attributes
Authorization: Bearer <token>
            
[
  {
    "id": 501,
    "name": "Договор № (обновлено)",
    "attributeTypeID": 5,
    "domainID": 2,
    "isPublic": true,
    "measurementUnitID": 1
  }
]
            
## Пример успешного ответа (202):
(пустой body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeUpdate`.
- 400 — некорректные данные/несуществующий ID.

### `DELETE /Attributes`

## Пример запроса (JSON):
DELETE /Attributes
Authorization: Bearer <token>
            
[501, 502]
            
## Пример успешного ответа (202):
(пустой body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeDelete`.
- 400 — некорректные идентификаторы.

### `GET /Attributes/{attributeID}`

## Пример запроса:
GET /Attributes/12
Authorization: Bearer <token>
            
## Пример успешного ответа (200):
{ "name": "Договор №", "type": { "id": 5, "code": "DOC_NUM", "name": "Номер договора" }, "domain": { "id": 2, "name": "Договор", "code": "CONTRACT" }, "isPublic": true, "measurementUnit": null, "deleted": null, "relevantFor": { "task": true, "asset": false, "checkList": false, "completedWork": false, "contract": true, "company": false, "customer": false, "technician": false }, "listOfValues": [ { "key": "VAL_1", "value": "Значение 1", "deleted": null } ] }
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeGet`.
- 204 — атрибут не найден/не доступен в текущем тенанте.

### `GET /Attributes/{attributeID}/listOfValues`

## Пример запроса:
```text
GET /Attributes/12/listOfValues
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "VAL_1": "Значение 1", "VAL_2": "Значение 2" }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeListOfValuesList`.
- 204 — для атрибута не найдено допустимых значений.

### `DELETE /Attributes/{id}`

## Пример запроса:
DELETE /Attributes/501
Authorization: Bearer <token>
            
## Пример успешного ответа (202):
(пустой body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `AttributeDelete`.
- 400 — некорректный ID.

## Banks

### `GET /Banks`

## Пример запроса:
```text
GET /Banks?searchText=central
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "id": 1, "name": "Центральный банк", "bic": "044525225", "correspondingAccount": "30101810400000000225", "swift": "SWIFT", "phone": "+74950001122", "eMail": "bank@example.com", "address": "Россия, Москва", "isActive": true } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `BankList`.
- 204 — банки по фильтрам не найдены.

### `GET /Banks/{bankId}`

## Пример запроса:
```text
GET /Banks/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "id": 1, "name": "Центральный банк", "bic": "044525225", "correspondingAccount": "30101810400000000225", "swift": "SABRRUMM", "phone": "+74951234567", "eMail": "info@sberbank.ru", "address": "Москва, ул. Тестовая, 1", "isActive": true }
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `BankGet`.
- 404 — банк с указанным id не найден.

## Contacts

### `GET /Contacts`

## Пример запроса:
```text
GET /Contacts?searchText=ivan
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "id": 1, "fullName": "Иван Иванов", "email": "ivan@example.com", "phone": "+79990001122", "position": "Менеджер", "description": "Описание", "deleted": null, "isUsed": true } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ContactsList`.
- 204 — подходящие контакты не найдены.

### `POST /Contacts`

## Пример запроса (JSON):
```text
POST /Contacts
Authorization: Bearer <token>
```
            
```json
[
  { "fullName": "Иван Иванов", "email": "ivan@example.com", "phone": "+79990001122", "position": "Менеджер", "description": "Описание" }
]
```
            
## Пример успешного ответа (201):
```json
[ 101 ]
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ContactAdd`.
- 400 — некорректные данные (невалидный email/телефон, пустые обязательные поля и т.п.).

### `PUT /Contacts`

## Пример запроса (JSON):
```text
PUT /Contacts
Authorization: Bearer <token>
```
            
```json
[
  { "id": 101, "fullName": "Иван Иванов (обновленный)", "email": "ivan@example.com", "phone": "+79990001122", "position": "Директор", "description": "Описание (обновлено)" }
]
```
            
## Пример успешного ответа (202):
(пустой response body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ContactUpdate`.
- 400 — некорректные данные/несуществующий ID.

### `DELETE /Contacts`

## Пример запроса (JSON):
```text
DELETE /Contacts
Authorization: Bearer <token>
```
            
```json
[101, 102]
```
            
## Пример успешного ответа (202):
(пустой response body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ContactDelete`.
- 400 — некорректные идентификаторы.

### `GET /Contacts/{contactID}`

## Пример запроса:
```text
GET /Contacts/123
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "id": 123, "fullName": "Иван Иванов", "email": "ivan@example.com", "phone": "+79990001122", "position": "Менеджер", "description": "Описание", "deleted": null }
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ContactGet`.
- 204 — контакт недоступен/отсутствует.

### `DELETE /Contacts/{id}`

## Пример запроса:
```text
DELETE /Contacts/101
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
(пустой response body)
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `ContactDelete`.
- 400 — некорректный id.

## Countries

### `GET /Countries`

## Пример запроса:
```text
GET /Countries
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "name": "Россия", "twoSymbolCode": "RU", "threeSymbolCode": "RUS" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `CountriesList`.
- 204 — список стран пуст (нет записей).

## Currencies

### `GET /Currencies`

## Пример запроса:
```text
GET /Currencies
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "name": "Российский рубль", "shortName": "RUB", "asciiCode": "RUB" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `CurrenciesList`.
- 204 — справочник валют пуст (записей нет).

## Events

### `GET /Events`

## Пример запроса:
```text
GET /Events?eventTransportTypeID=1&isSystem=true&isHidden=false
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "10": { "id": 10, "name": "Событие", "code": "EVENT_1" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `EventList`.
- 204 — подходящие события не найдены.

## MeasurementUnits

### `GET /MeasurementUnits`

## Пример запроса:
```text
GET /MeasurementUnits
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "name": "штука", "abbreviation": "шт", "designation": "piece" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `MeasurementUnitList`.
- 204 — справочник единиц измерения пуст.

## PowerBIReports

### `GET /PowerBIReports`

## Пример запроса:
```text
GET /PowerBIReports
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
[ { "id": 1, "name": "Отчет по продажам", "reportID": "RPT_001", "reportType": { "id": 2, "name": "Sales" } } ]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `PowerBIReportList`.
- 204 — отчетов по доступности нет.

### `GET /PowerBIReports/{id}`

## Пример запроса:
```text
GET /PowerBIReports/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "id": 1, "name": "Отчет по продажам", "reportID": "RPT_001", "reportType": { "id": 2, "name": "Sales" } }
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `PowerBIReportGet`.
- 404 — отчет с указанным id не найден.

## SystemTags

### `GET /SystemTags`

## Пример запроса:
```text
GET /SystemTags
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
[ { "id": 1, "name": "Системный тег" } ]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `TagsList`.
- 204 — системных тегов для текущего тенанта нет.

## Tags

### `GET /Tags`

## Пример запроса:
```text
GET /Tags?searchText=finance
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
[ "finance", "bank", "reporting" ]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `TagsList`.
- 204 — подходящие теги не найдены.

## Timezones

### `GET /Timezones`

## Пример запроса:
```text
GET /Timezones
Authorization: Bearer <token>
Range: items=1-50
```
            
## Пример успешного ответа (200):
```json
{ "1": { "name": "Москва", "utcTimeOffset": "+03:00" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `TimezonesList`.
- 204 — часовые пояса не найдены.

### `GET /Timezones/info`

## Пример запроса:
```text
GET /Timezones/info?timezoneId=1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "name": "Москва", "utcTimeOffsetMinutes": 180 }
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав `TimezonesList`.
- 204 — часовой пояс не найден.
