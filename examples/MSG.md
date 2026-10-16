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
