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

### `POST /Accounts/logout`

## Пример запроса:
`POST /Accounts/logout`
            
```json
{
  "uniqueClientIdentifier": "abc-123-def-456",
  "applicationID": 2
}
```
            
## Пример успешного ответа (200):
Тело ответа пустое.
            
## Негативные сценарии:
- 401 Unauthorized: токен не содержит идентификатор учётной записи или участника тенанта.
- 409 Conflict: отсутствует или некорректен заголовок Authorization, либо тело запроса не указано.

### `POST /Accounts/register`

## Пример запроса:
`POST /Accounts/register`
            
```json
{
  "email": "user%40example.com"
}
```
            
## Пример успешного ответа (200) — существующая учётная запись:
```json
{
  "id": 1001,
  "verificationRequestValidTill": "2026-08-21T12:00:00Z",
  "isEmailVerified": false,
  "isMobilePhoneVerified": false,
  "isPasswordDefined": false,
  "isNewAccount": false
}
```
            
## Пример успешного ответа (202) — новая учётная запись (email или SMS):
```json
{
  "id": 1001,
  "verificationRequestValidTill": "2026-08-21T12:00:00Z",
  "isEmailVerified": false,
  "isMobilePhoneVerified": false,
  "isPasswordDefined": false,
  "isNewAccount": true
}
```
Отправляется уведомление для верификации (письмо или SMS).
            
## Пример успешного ответа (202) — новая учётная запись (domainLogin):
Тело ответа аналогично примеру выше с `"isNewAccount": true`. Уведомление **не отправляется**.
            
## Негативные сценарии:
- 409 Conflict: тело запроса не указано, ошибки валидации, не указаны email/телефон/domainLogin или указаны некорректные данные.

### `PUT /Accounts/this/applications`

## Пример запроса:
`PUT /Accounts/this/applications`
            
```json
{
  "clientTypeID": 1,
  "agent": "Android 14",
  "applicationVersion": "3.5.0",
  "pushToken": "fcm-token-xyz"
}
```
            
## Пример успешного ответа (202):
Тело ответа пустое.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует идентификатор учётной записи и участника тенанта в токене.

### `DELETE /Accounts/this/applications`

## Пример запроса:
`DELETE /Accounts/this/applications`
            
```json
{
  "uniqueClientIdentifier": "abc-123-def-456",
  "applicationID": 2
}
```
            
## Пример успешного ответа (202):
Тело ответа пустое.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует идентификатор учётной записи и участника тенанта в токене.

## Messages

### `POST /Messages/requestPasswordChange`

## Пример запроса:
`POST /Messages/requestPasswordChange`
            
```json
{
  "credentials": "user%40example.com"
}
```
            
## Пример успешного ответа (202):
```json
{
  "id": 1001,
  "isEmailVerified": true,
  "isPhoneVerified": false,
  "verificationRequestValidTill": "2026-08-21T12:00:00Z",
  "isPasswordDefined": true,
  "isNewAccount": false,
  "verificationCodeRepeatTimeout": 60
}
```
            
## Негативные сценарии:
- 401 Unauthorized: учётная запись не найдена.
- 409 Conflict: указаны некорректные credentials или восстановление недоступно для указанного типа учётных данных.

### `POST /Messages/verifyEmail`

## Пример запроса:
`POST /Messages/verifyEmail`
            
```json
{
  "email": "user%40example.com"
}
```
            
## Пример успешного ответа (202):
```json
{
  "id": 1001,
  "isEmailVerified": false,
  "isPhoneVerified": false,
  "verificationRequestValidTill": "2026-08-21T12:00:00Z",
  "isPasswordDefined": false,
  "isNewAccount": false,
  "verificationCodeRepeatTimeout": 60
}
```
            
## Негативные сценарии:
- 401 Unauthorized: не указан идентификатор учётной записи (ни в токене, ни в теле запроса).
- 204 NoContent: учётная запись не найдена.
- 409 Conflict: указан некорректный адрес электронной почты.

### `POST /Messages/verifyPhone`

## Пример запроса:
`POST /Messages/verifyPhone`
            
```json
{
  "phone": "+79001234567"
}
```
            
## Пример успешного ответа (202):
```json
{
  "id": 1001,
  "isEmailVerified": false,
  "isPhoneVerified": false,
  "verificationRequestValidTill": "2026-08-21T12:00:00Z",
  "isPasswordDefined": false,
  "isNewAccount": false,
  "verificationCodeRepeatTimeout": 60
}
```
            
## Негативные сценарии:
- 401 Unauthorized: не указан идентификатор учётной записи (ни в токене, ни в теле запроса).
- 204 NoContent: учётная запись не найдена.
- 409 Conflict: указан некорректный номер телефона.

## Passwords

### `POST /Passwords/change`

## Пример запроса (по SMS-коду):
`POST /Passwords/change`
            
```json
{
  "password": "MyNewP%40ssw0rd",
  "code": "123456",
  "mobilePhone": "+79001234567"
}
```
            
## Пример запроса (по текущему паролю):
`POST /Passwords/change`
            
```json
{
  "password": "MyNewP%40ssw0rd",
  "currentPassword": "OldP%40ssw0rd"
}
```
            
## Пример запроса (по хэшу из e-mail):
`POST /Passwords/change`
            
```json
{
  "password": "MyNewP%40ssw0rd",
  "codeHash": "a1b2c3d4e5f6"
}
```
            
## Пример успешного ответа (202):
Тело ответа пустое.
            
## Негативные сценарии:
- 403 Forbidden: указан `currentPassword`, но пользователь не аутентифицирован.
- 409 Conflict: неверный текущий пароль или некорректный верификационный код.
