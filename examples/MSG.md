# MSG — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса MSG, вынесенные из `endpoints/MSG.md`. Сигнатуры и типы — там же и в `schemas/MSG.md`.

## ContentTypes

### `GET /ContentTypes`

## Пример запроса:
```text
GET /ContentTypes
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "HTML",
    "code": "HTML"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — типы контента не найдены.

## CriticalityForTriggers

### `POST /CriticalityForTriggers`

## Пример запроса:
```text
POST /CriticalityForTriggers
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "triggerID": 5,
    "data": [1, 2, 3]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

## MailBoxes

### `GET /MailBoxes`

## Пример запроса:
```text
GET /MailBoxes
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "Support inbox",
    "isActive": true,
    "email": "support@example.com",
    "calls": { "remaining": 2, "total": 5 },
    "lastCall": { "completed": "2026-08-20T10:00:00Z", "exception": null, "hasError": false }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — почтовые ящики не найдены.

### `POST /MailBoxes`

## Пример запроса:
```text
POST /MailBoxes
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[
  {
    "name": "Support inbox",
    "email": "support@example.com",
    "login": "user",
    "password": "secret",
    "host": "imap.example.com",
    "port": 993,
    "protocolID": 1,
    "secureConnection": true,
    "isActive": true,
    "senders": [
      {
        "recipient": "sender@example.com",
        "taskTemplateID": "TMPL-001",
        "isActive": true,
        "sendResponse": true,
        "taskSubjectRegex": ".*",
        "taskTextBodyRegex": ".*",
        "regexNotMatchActionID": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (201):
```json
[1]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса или отсутствует шаблон заявки у отправителя.

### `DELETE /MailBoxes`

## Пример запроса:
```text
DELETE /MailBoxes
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /MailBoxes/activate`

## Пример запроса:
```text
PUT /MailBoxes/activate
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /MailBoxes/activate/{id}`

## Пример запроса:
```text
PUT /MailBoxes/activate/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /MailBoxes/deactivate`

## Пример запроса:
```text
PUT /MailBoxes/deactivate
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /MailBoxes/deactivate/{id}`

## Пример запроса:
```text
PUT /MailBoxes/deactivate/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `GET /MailBoxes/regexactions`

## Пример запроса:
```text
GET /MailBoxes/regexactions
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "Пропустить"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — действия не найдены.

### `GET /MailBoxes/{id}`

## Пример запроса:
```text
GET /MailBoxes/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "name": "Support inbox",
  "isActive": true,
  "email": "support@example.com",
  "login": "user",
  "password": "secret",
  "host": "imap.example.com",
  "protocolID": 1,
  "port": 993,
  "secureConnection": true,
  "calls": { "remaining": 2, "total": 5 },
  "senders": [
    {
      "id": 10,
      "mailBoxID": 1,
      "recipient": "sender@example.com",
      "taskTemplateID": "TMPL-001",
      "isActive": true,
      "sendResponse": true,
      "taskSubjectRegex": ".*",
      "taskTextBodyRegex": ".*",
      "regexNotMatchAction": { "id": 1, "name": "Skip" },
      "lastTask": { "id": 100, "number": "T-100" },
      "calls": { "remaining": 1, "total": 3 },
      "lastCall": { "started": "2026-08-20T10:00:00Z", "completed": "2026-08-20T10:00:01Z", "exception": null, "hasError": false, "lastRecipient": "sender@example.com" }
    }
  ],
  "lastCall": { "started": "2026-08-20T10:00:00Z", "completed": "2026-08-20T10:00:01Z", "exception": null, "hasError": false }
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — почтовый ящик не найден.

### `DELETE /MailBoxes/{id}`

## Пример запроса:
```text
DELETE /MailBoxes/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `GET /MailBoxes/{id}/errors`

## Пример запроса:
```text
GET /MailBoxes/1/errors?occurredFrom=2026-08-01T00:00:00Z&occurredTill=2026-08-31T23:59:59Z
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
[
  {
    "tenantID": 1,
    "mailBoxID": 1,
    "name": "Support inbox",
    "email": "support@example.com",
    "occurred": "2026-08-20T10:00:00Z",
    "error": "Connection timeout"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — ошибки не найдены.

### `GET /MailBoxes/{mailBoxID}/senders`

## Пример запроса:
```text
GET /MailBoxes/1/senders
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "10": {
    "id": 10,
    "mailBoxID": 1,
    "recipient": "sender@example.com",
    "taskTemplateID": "TMPL-001",
    "isActive": true,
    "sendResponse": true,
    "taskSubjectRegex": ".*",
    "taskTextBodyRegex": ".*",
    "regexNotMatchAction": { "id": 1, "name": "Skip" },
    "lastTask": { "id": 100, "number": "T-100" },
    "calls": { "remaining": 1, "total": 3 },
    "lastCall": { "started": "2026-08-20T10:00:00Z", "completed": "2026-08-20T10:00:01Z", "exception": null, "hasError": false, "lastRecipient": "sender@example.com" }
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — отправители не найдены.

### `DELETE /MailBoxes/{mailBoxID}/senders`

## Пример запроса:
```text
DELETE /MailBoxes/1/senders
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[10, 11]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `DELETE /MailBoxes/{mailBoxID}/senders/{id}`

## Пример запроса:
```text
DELETE /MailBoxes/1/senders/10
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `GET /MailBoxes/{mailBoxID}/senders/{senderID}`

## Пример запроса:
```text
GET /MailBoxes/1/senders/10
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "id": 10,
  "mailBoxID": 1,
  "recipient": "sender@example.com",
  "taskTemplateID": "TMPL-001",
  "isActive": true,
  "sendResponse": true,
  "taskSubjectRegex": ".*",
  "taskTextBodyRegex": ".*",
  "regexNotMatchAction": { "id": 1, "name": "Skip" },
  "lastTask": { "id": 100, "number": "T-100" },
  "calls": { "remaining": 1, "total": 3 },
  "lastCall": { "started": "2026-08-20T10:00:00Z", "completed": "2026-08-20T10:00:01Z", "exception": null, "hasError": false, "lastRecipient": "sender@example.com" },
  "deleted": null
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — отправитель не найден.

## MessageTemplates

### `GET /MessageTemplates`

## Пример запроса:
```text
GET /MessageTemplates?isDeleted=false
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{ "1": { "id": 1, "description": "Welcome", "subject": "Hello", "validated": "2026-08-20T10:00:00Z", "isValid": true, "providerID": 1, "applicationID": 2, "navigateToID": 3, "contentTypeID": 1 } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateList`.
- 204 — шаблоны по фильтрам не найдены.

### `POST /MessageTemplates`

## Пример запроса:
```text
POST /MessageTemplates
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[{ "description": "Welcome", "providerID": 1, "applicationID": 2, "navigateToID": 3, "subject": "Hello", "content": "<p>Hi</p>", "contentTypeID": 1 }]
```
            
## Пример успешного ответа (201):
```json
[1, 2]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateAdd`.
- 400 — некорректные данные запроса.

### `PUT /MessageTemplates`

## Пример запроса:
```text
PUT /MessageTemplates
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[{ "id": 1, "description": "Welcome updated", "providerID": 1, "applicationID": 2, "navigateToID": 3, "subject": "Hello", "content": "<p>Hi</p>", "contentTypeID": 1 }]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateUpdate`.
- 400 — некорректные данные запроса.

### `DELETE /MessageTemplates`

## Пример запроса:
```text
DELETE /MessageTemplates
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateDelete`.
- 409 — шаблон не может быть удален из-за связанных данных.

### `GET /MessageTemplates/{id}`

## Пример запроса:
```text
GET /MessageTemplates/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "id": 1, "description": "Welcome", "subject": "Hello", "content": "<p>Hi</p>", "validated": "2026-08-20T10:00:00Z", "isValid": true, "provider": { "id": 1, "code": "Email", "name": "Email" }, "application": { "id": 2, "code": "Portal", "name": "Portal" }, "navigateTo": { "id": 3, "code": "Task", "name": "Task" }, "contentType": { "id": 1, "code": "Html", "name": "HTML" }, "deleted": null }
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateGet`.
- 204 — шаблон с указанным идентификатором не найден.

### `DELETE /MessageTemplates/{id}`

## Пример запроса:
```text
DELETE /MessageTemplates/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateDelete`.
- 409 — шаблон не может быть удален из-за связанных данных.

### `PUT /MessageTemplates/{id}/validate`

## Пример запроса:
```text
PUT /MessageTemplates/1/validate
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `MessageTemplateValidate`.
- 204 — шаблон с указанным идентификатором не найден.
- 400 — шаблон не прошел валидацию.

## NavigateTo

### `GET /NavigateTo`

## Пример запроса:
```text
GET /NavigateTo
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "code": "TASK",
    "name": "Заявка"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — переходы не найдены.

## Notifications

### `GET /Notifications`

## Пример запроса:
```text
GET /Notifications?includeIsViewed=false
Authorization: Bearer <token>
Range: items=0-24
```
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "id": 101,
    "providerID": 1,
    "subject": "Новая заявка",
    "content": "Создана заявка №123",
    "contentTypeID": 1,
    "created": "2026-08-20T10:00:00Z",
    "sent": "2026-08-20T10:00:01Z",
    "navigateTo": 3,
    "taskID": 123,
    "isViewed": false
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — уведомления не найдены.

### `POST /Notifications`

## Пример запроса:
```text
POST /Notifications?integratedSystemName=ExternalCRM
Authorization: Bearer <token>
```
            
Тело запроса отсутствует.
            
## Пример успешного ответа (202):
Тело ответа отсутствует. Запрос на интеграцию принят в обработку.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — не указано наименование системы для интеграции.

### `PUT /Notifications`

## Пример запроса:
```text
PUT /Notifications
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
{
  "notificationIDs": [101, 102],
  "isViewed": true
}
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — не указаны данные для установки признака просмотра.

### `HEAD /Notifications`

## Пример запроса:
```text
HEAD /Notifications?includeIsViewed=false
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
Тело ответа отсутствует. В заголовке `Content-Range` возвращается общее количество записей.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /Notifications/all`

## Пример запроса:
```text
PUT /Notifications/all
Authorization: Bearer <token>
```
            
Тело запроса отсутствует.
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `GET /Notifications/fields`

## Пример запроса:
```text
GET /Notifications/fields
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "TaskNumber": "Номер заявки",
  "UserName": "Имя пользователя"
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — поля не найдены.

## Protocols

### `GET /Protocols`

## Пример запроса:
```text
GET /Protocols
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "SMTP"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — протоколы не найдены.

## Providers

### `GET /Providers`

## Пример запроса:
```text
GET /Providers
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "SMS",
    "code": "SMS",
    "descriptionRu": "SMS-провайдер"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — провайдеры не найдены.

## RecipientSelectionRules

### `GET /RecipientSelectionRules`

## Пример запроса:
```text
GET /RecipientSelectionRules?isDeleted=false&triggerID=10
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{ "1": { "id": 1, "description": "Исполнитель и руководитель", "isCaller": false, "isTaskRequestor": true, "isTaskAssignee": true, "isPreviousTaskAssignee": false, "isTaskAssigneeManager": true, "isTaskContact": false, "isTaskAssetResponsiblePerson": false, "isTenantPowerUser": false, "isTaskWatchList": false, "isForRelevantUsers": false, "isForRelevantUsersByWorkType": false, "deleted": null } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — правила по фильтрам не найдены.

### `POST /RecipientSelectionRules`

## Пример запроса:
```text
POST /RecipientSelectionRules
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[{ "description": "Исполнитель и руководитель", "isCaller": false, "isTaskRequestor": true, "isTaskAssignee": true, "isPreviousTaskAssignee": false, "isTaskAssigneeManager": true, "isTaskContact": false, "isTaskAssetResponsiblePerson": false, "isTenantPowerUser": false, "isTaskWatchList": false, "isForRelevantUsers": false, "isForRelevantUsersByWorkType": false, "orgUnitsUpwardTillRoleID": 5, "customAssetResponsiblePerson": null, "customOrgUnitID": null, "isCustomOrgUnitManager": null, "isCustomOrgUnitStaff": null, "customUserID": null, "customRoleID": null, "customEmailList": null, "customPhoneList": null, "useUnverifiedContacts": false }]
```
            
## Пример успешного ответа (201):
```json
[1]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `PUT /RecipientSelectionRules`

## Пример запроса:
```text
PUT /RecipientSelectionRules
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[{ "id": 1, "description": "Исполнитель и руководитель", "isCaller": false, "isTaskRequestor": true, "isTaskAssignee": true, "isPreviousTaskAssignee": false, "isTaskAssigneeManager": true, "isTaskContact": false, "isTaskAssetResponsiblePerson": false, "isTenantPowerUser": false, "isTaskWatchList": false, "isForRelevantUsers": false, "isForRelevantUsersByWorkType": false, "orgUnitsUpwardTillRoleID": 5, "customAssetResponsiblePerson": null, "customOrgUnitID": null, "isCustomOrgUnitManager": null, "isCustomOrgUnitStaff": null, "customUserID": null, "customRoleID": null, "customEmailList": null, "customPhoneList": null, "useUnverifiedContacts": false }]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `DELETE /RecipientSelectionRules`

## Пример запроса:
```text
DELETE /RecipientSelectionRules
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 409 — правило не может быть удалено из-за связанных данных.

### `GET /RecipientSelectionRules/recipients`

## Пример запроса:
```text
GET /RecipientSelectionRules/recipients?isHidden=false
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{ "1": { "id": 1, "code": "TaskAssignee", "name": "Исполнитель заявки" } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — получатели по фильтрам не найдены.

### `GET /RecipientSelectionRules/{id}`

## Пример запроса:
```text
GET /RecipientSelectionRules/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "id": 1, "description": "Исполнитель и руководитель", "isCaller": false, "isTaskRequestor": true, "isTaskAssignee": true, "isPreviousTaskAssignee": false, "isTaskAssigneeManager": true, "isTaskContact": false, "isTaskAssetResponsiblePerson": false, "isTenantPowerUser": false, "isTaskWatchList": false, "isForRelevantUsers": false, "isForRelevantUsersByWorkType": false, "isCustomOrgUnitManager": null, "isCustomOrgUnitStaff": null, "customEmailList": null, "customPhoneList": null, "useUnverifiedContacts": false, "orgUnitsUpwardTillRole": { "id": 5, "name": "Manager", "description": "Руководитель" }, "customAssetResponsible": null, "customUser": null, "customOrgUnit": null, "customRole": null, "deleted": null }
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — правило с указанным идентификатором не найдено.

### `DELETE /RecipientSelectionRules/{id}`

## Пример запроса:
```text
DELETE /RecipientSelectionRules/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 409 — правило не может быть удалено из-за связанных данных.

## TriggerRecipientSelectionRules

### `POST /TriggerRecipientSelectionRules`

## Пример запроса:
```text
POST /TriggerRecipientSelectionRules
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "triggerID": 5,
    "data": [1, 2, 3]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

## Triggers

### `GET /Triggers`

## Пример запроса:
```text
GET /Triggers?isDeleted=false&isEnabled=true
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "timeoutSeconds": 60,
    "description": "Уведомление при создании заявки",
    "isNotifyDuringWorkHours": true,
    "isNotifyDuringDutyHours": false,
    "isNotifyDuringOtherHours": false,
    "isEnabled": true,
    "provider": {
      "id": 1,
      "name": "Email",
      "description": "Email-провайдер"
    },
    "event": {
      "id": 2,
      "name": "Создание заявки"
    },
    "messageTemplate": {
      "id": 3,
      "name": null,
      "description": "Шаблон уведомления"
    },
    "deleted": null
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — триггеры по фильтрам не найдены.

### `POST /Triggers`

## Пример запроса:
```text
POST /Triggers
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "description": "Уведомление при создании заявки",
    "timeoutSeconds": 60,
    "isNotifyDuringWorkHours": true,
    "isNotifyDuringDutyHours": false,
    "isNotifyDuringOtherHours": false,
    "eventID": 2,
    "messageTemplateID": 3
  }
]
```
            
## Пример успешного ответа (201):
```json
[1, 2]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `PUT /Triggers`

## Пример запроса:
```text
PUT /Triggers
Authorization: Bearer <token>
Content-Type: application/json
            
[
  {
    "id": 1,
    "description": "Уведомление при создании заявки",
    "timeoutSeconds": 60,
    "isNotifyDuringWorkHours": true,
    "isNotifyDuringDutyHours": false,
    "isNotifyDuringOtherHours": false,
    "eventID": 2,
    "messageTemplateID": 3
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `DELETE /Triggers`

## Пример запроса:
```text
DELETE /Triggers
Authorization: Bearer <token>
Content-Type: application/json
            
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.
- 409 — конфликт при удалении триггеров.

### `PUT /Triggers/activate`

## Пример запроса:
```text
PUT /Triggers/activate
Authorization: Bearer <token>
Content-Type: application/json
            
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `PUT /Triggers/deactivate`

## Пример запроса:
```text
PUT /Triggers/deactivate
Authorization: Bearer <token>
Content-Type: application/json
            
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `GET /Triggers/{id}`

## Пример запроса:
```text
GET /Triggers/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "timeoutSeconds": 60,
  "description": "Уведомление при создании заявки",
  "isNotifyDuringWorkHours": true,
  "isNotifyDuringDutyHours": false,
  "isNotifyDuringOtherHours": false,
  "isEnabled": true,
  "provider": {
    "id": 1,
    "name": "Email",
    "description": "Email-провайдер"
  },
  "event": {
    "id": 2,
    "name": "Создание заявки"
  },
  "messageTemplate": {
    "id": 3,
    "name": null,
    "description": "Шаблон уведомления"
  },
  "deleted": null
}
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — триггер с указанным идентификатором не найден.

### `DELETE /Triggers/{id}`

## Пример запроса:
```text
DELETE /Triggers/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 409 — конфликт при удалении триггера.

### `GET /Triggers/{id}/criticalities`

## Пример запроса:
```text
GET /Triggers/1/criticalities
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 1,
    "name": "Низкая"
  },
  {
    "id": 2,
    "name": "Высокая"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — критичности для триггера не найдены.

### `PUT /Triggers/{triggerID}/activate`

## Пример запроса:
```text
PUT /Triggers/1/activate
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /Triggers/{triggerID}/deactivate`

## Пример запроса:
```text
PUT /Triggers/1/deactivate
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

## Webhooks

### `GET /Webhooks`

## Пример запроса:
```text
GET /Webhooks
Authorization: Bearer <token>
Range: items=0-49
```
            
## Пример успешного ответа (200):
```json
{ "1": { "id": 1, "name": "Hook", "isActive": true, "callsRemaining": 3, "lastCall": { "completed": "2026-08-20T10:00:00Z", "exception": null } } }
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — webhook-и не найдены.

### `POST /Webhooks`

## Пример запроса:
```text
POST /Webhooks
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[{ "name": "Hook", "uri": "https://example.com/hook", "isActive": true, "events": [1], "taskStages": [10] }]
```
            
## Пример успешного ответа (201):
```json
[1]
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 400 — некорректные данные запроса.

### `DELETE /Webhooks`

## Пример запроса:
```text
DELETE /Webhooks
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /Webhooks/activate`

## Пример запроса:
```text
PUT /Webhooks/activate
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /Webhooks/activate/{id}`

## Пример запроса:
```text
PUT /Webhooks/activate/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /Webhooks/deactivate`

## Пример запроса:
```text
PUT /Webhooks/deactivate
Authorization: Bearer <token>
Content-Type: application/json
```
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `PUT /Webhooks/deactivate/{id}`

## Пример запроса:
```text
PUT /Webhooks/deactivate/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.

### `GET /Webhooks/{id}`

## Пример запроса:
```text
GET /Webhooks/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (200):
```json
{ "id": 1, "name": "Hook", "uri": "https://example.com/hook", "isActive": true, "callsRemaining": 3, "events": [{ "id": 1, "name": "TaskCreated" }], "taskStages": [{ "id": 10, "name": "New" }], "lastCall": { "started": "2026-08-20T09:59:00Z", "completed": "2026-08-20T10:00:00Z", "exception": null } }
```
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
- 204 — webhook с указанным идентификатором не найден.

### `DELETE /Webhooks/{id}`

## Пример запроса:
```text
DELETE /Webhooks/1
Authorization: Bearer <token>
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401/403 — отсутствие или недостаточность прав доступа.
