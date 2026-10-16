# AUTH — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса AUTH, вынесенные из `endpoints/AUTH.md`. Сигнатуры и типы — там же и в `schemas/AUTH.md`.

## Accounts

### `GET /Accounts`

## Пример запроса:
`GET /Accounts?credential=user@example.com`
            
## Пример успешного ответа (200):
```json
{
  "id": 1001,
  "credential": "user@example.com",
  "ban": {
    "dateTill": "2026-08-22T00:00:00Z",
    "banReason": { "id": 1, "name": "Email not verified" }
  },
  "isAnonymous": false,
  "isCrossTenantAdmin": false,
  "domainLogin": null,
  "socialProfiles": [
    {
      "id": 1,
      "name": "Google",
      "dateFrom": "2025-01-01T00:00:00Z",
      "dateTill": "2099-12-31T23:59:59Z"
    }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: учётная запись по указанным credential не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AccountGet`.

### `HEAD /Accounts`

## Пример запроса:
`HEAD /Accounts?credential=user@example.com`
            
## Пример успешного ответа (200):
Тело ответа пустое. Заголовок `Content-Range` не используется.
            
## Негативные сценарии:
- 409 Conflict: параметр `credential` не указан.
- 404 Not Found: учётная запись не найдена или не прошла верификацию (кроме случая `NotVerifiedException`, который возвращает 200).

### `GET /Accounts/this/applications`

## Пример запроса:
`GET /Accounts/this/applications?offset=0&fetch=25`
            
## Пример успешного ответа (200):
```json
[
  {
    "client": {
      "id": 1,
      "uniqueClientIdentifier": "abc-123-def-456",
      "agent": "Android 14",
      "clientType": { "id": 1, "name": "Mobile" }
    },
    "application": {
      "id": 2,
      "name": "HubEx Mobile",
      "version": "3.5.0"
    },
    "pushToken": "fcm-token-xyz",
    "timestamp": "2026-08-21T08:00:00Z"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона. Заголовок `Content-Range` указывает общее количество.
            
## Негативные сценарии:
- 204 NoContent: приложения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AccountClientApplicationList`.

### `GET /Accounts/this/notifications`

## Пример запроса:
`GET /Accounts/this/notifications?offset=0&fetch=25`
            
## Пример успешного ответа (200):
```json
[
  {
    "notificationID": 501,
    "providerID": 1,
    "subject": "Подтверждение адреса электронной почты",
    "content": "Для подтверждения перейдите по ссылке...",
    "sent": "2026-08-21T08:01:00Z"
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит только часть диапазона. Заголовок `Content-Range` указывает общее количество.
            
## Негативные сценарии:
- 204 NoContent: уведомления не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `NotificationLogList`.
