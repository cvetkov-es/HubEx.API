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
