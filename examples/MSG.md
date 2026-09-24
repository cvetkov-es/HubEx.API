# MSG — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса MSG, вынесенные из `endpoints/MSG.md`. Сигнатуры и типы — там же и в `schemas/MSG.md`.

## MailBoxes

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

## Notifications

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

## RecipientSelectionRules

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

## Webhooks

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
