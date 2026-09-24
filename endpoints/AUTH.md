# AUTH — справочник ручек

> **Что здесь:** все ручки сервиса AUTH (Authentication and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTH.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTH.md`; грабли — `notes/AUTH.md` (если есть).

Base: `{BASE_URL}/AUTH`
> Примеры ответов вынесены в [../examples/AUTH.md](../examples/AUTH.md).

**Оглавление**

- Accounts — строки 28–41
- Пример запроса: — строки 43–44
- Пример успешного ответа (200): — строки 46–65
- Пример успешного ответа (206): — строки 67–68
- Негативные сценарии: — строки 70–80
- Пример запроса: — строки 82–83
- Пример успешного ответа (200): — строки 85–96
- Пример успешного ответа (206): — строки 98–99
- Негативные сценарии: — строки 101–104
- Messages — строки 106–112
- Passwords — строки 114–116
- VerificationCodes — строки 118–121
- Пример запроса (по хэшу из e-mail): — строки 123–130
- Пример запроса (по SMS-коду): — строки 132–140
- Пример успешного ответа (200): — строки 142–149
- Негативные сценарии: — строки 151–152

## Accounts
- `GET /Accounts` — Возвращает данные учетной записи по учетным данным · коды: 200, 204 · примеры
  ← query: credential?:str → GetResult
- `HEAD /Accounts` — Проверяет присутствие учетной записи по указанным полномочиям · коды: 200, 404, 409 · примеры
  ← query: credential?:str
- `POST /Accounts/logout` — Выход из системы. Метод можно вызывать с просроченным токеном. · коды: 200, 409 · примеры
  ← body: BaseLogoutData
- `POST /Accounts/register` — Создаёт аккаунт с указанной электронной почтой (если ещё не создан),
блокирует его по причине непройденной верификации почты и отправляет
нотификацию для отправки письма или SMS со ссылкой для верификации. · коды: 200, 202, 409 · примеры
  ← body: CreateData → AccountAddResultEntity
- `GET /Accounts/this/applications` — Приложения учетной записи · коды: 200, 204, 206
  → ApplicationListResult[]
  Поддерживает ограничение результата через query-параметры `offset` и `fetch`.
            
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
- `PUT /Accounts/this/applications` — Актуализация данных о приложениях текущей учетной записи · коды: 202 · примеры
  ← body: AUTHACAMergeData
- `DELETE /Accounts/this/applications` — Отвязка приложения и устройства от текущей учетной записи · коды: 202 · примеры
  ← body: AUTHACARemoveData
- `GET /Accounts/this/notifications` — Список уведомлений из лога · коды: 200, 204, 206
  → ListResult[]
  Поддерживает ограничение результата через query-параметры `offset` и `fetch`.
            
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

## Messages
- `POST /Messages/requestPasswordChange` — Отправляет запрос на изменение пароля на указанный адрес эл. почты; для аутентифицированного пользователя — на адрес эл. почты уч.записи · коды: 202, 409 · примеры
  ← body: RequestPasswordChangeData → VerificationResult
- `POST /Messages/verifyEmail` — Отправляет письмо проверки почты на указанный адрес эл. почты (если не был указан, то на адрес уч.записи) · коды: 202, 204, 409 · примеры
  ← body: VerifyEmailData → VerificationResult
- `POST /Messages/verifyPhone` — Отправляет SMS проверки номера телефона на указанный телефон (если не был указан, то на телефон учетной записи) · коды: 202, 204, 409 · примеры
  ← body: VerifyPhoneData → VerificationResult

## Passwords
- `POST /Passwords/change` — Изменяет пароль учётной записи. · коды: 202, 409 · примеры
  ← body: PasswordSetData

## VerificationCodes
- `POST /VerificationCodes/check` — Проверяет верификационный код. · коды: 200, 409
  ← body: CheckData → CheckResult
  Заголовок `Authorization` **не обязателен**. Для проверки по SMS достаточно тела запроса с `code` и `mobilePhone`.
            
## Пример запроса (по хэшу из e-mail):
`POST /VerificationCodes/check`
            
```json
{
  "codeHash": "a1b2c3d4e5f6"
}
```
            
## Пример запроса (по SMS-коду):
`POST /VerificationCodes/check`
            
```json
{
  "code": "123456",
  "mobilePhone": "+79001234567"
}
```
            
## Пример успешного ответа (200):
```json
{
  "accountID": 1001,
  "oneTimeLoginToken": "olt-abc123xyz",
  "verificationCodeRepeatTimeout": 60
}
```
            
## Негативные сценарии:
- 409 Conflict: тело запроса не указано, ошибки валидации, верификационный код не найден или недействителен.
