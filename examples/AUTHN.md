# AUTHN — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса AUTHN, вынесенные из `endpoints/AUTHN.md`. Сигнатуры и типы — там же и в `schemas/AUTHN.md`.

## Accounts

### `POST /Accounts/login`

## Пример запроса:
```text
POST /Accounts/login
Authorization: Basic dXNlcjE6cGFzc3dvcmQx
```
            
## Пример успешного ответа (200):
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refresh_token": null,
  "expires_in": 3600,
  "jwtValidTill": "2024-06-15T10:00:00Z",
  "accountUserTypeID": null,
  "tenantEntities": [
    {
      "tenantID": 10,
      "name": "Demo Tenant",
      "fullName": "Demo Tenant LLC",
      "hasUserProfile": true
    }
  ],
  "requests": [],
  "accountHasUserProfile": true,
  "isCrossTenantAdmin": false,
  "isAnonymous": false
}
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствуют или некорректны учётные данные Basic, пароль не задан или требуется смена пароля.
- 403 Forbidden — аккаунт заблокирован.
- 409 Conflict — аккаунт не найден или неверный пароль.

### `POST /Accounts/login/sso`

## Пример запроса:
```text
POST /Accounts/login/sso
Authorization: Bearer <keycloak-access-token>
X-Realm-ID: demo
```
            
## Пример успешного ответа (200):
Формат ответа совпадает с `POST /Accounts/login`.
            
## Негативные сценарии:
- 403 Forbidden — отсутствует заголовок `X-Realm-ID`.
- 401 Unauthorized — отсутствует или некорректен Bearer-токен Keycloak.
- 409 Conflict — аккаунт не найден в HubEx.

### `POST /Accounts/smsLogin`

## Пример запроса:
```json
{
  "phone": "+79001234567",
  "code": "123456"
}
```
            
## Пример успешного ответа (200):
Формат ответа совпадает с `POST /Accounts/login`.
            
## Негативные сценарии:
- 400 Bad Request — некорректное тело запроса.
- 401 Unauthorized — неверный SMS-код, код не был запрошен, истёкло время проверки или регистрация аккаунта не завершена.
- 404 Not Found — аккаунт не найден.
- 403 Forbidden — аккаунт заблокирован.

### `POST /Accounts/smsSend`

## Пример запроса:
```json
{
  "phone": "+79001234567"
}
```
            
## Пример успешного ответа (200):
Тело ответа пустое.
            
## Негативные сценарии:
- 400 Bad Request — некорректное тело запроса.
- 401 Unauthorized — регистрация аккаунта не завершена.
- 404 Not Found — аккаунт с указанным телефоном не найден.
- 403 Forbidden — аккаунт заблокирован.
- 429 Too Many Requests — превышен лимит отправки SMS (заголовок `X-SmsBanTill`).

## Passwords

### `POST /Passwords/set`

## Пример запроса (по SMS-коду):
```json
{
  "password": "MyNewP%40ssw0rd",
  "code": "123456",
  "mobilePhone": "+79001234567"
}
```
            
## Пример запроса (по хэшу из e-mail):
```json
{
  "password": "MyNewP%40ssw0rd",
  "codeHash": "a1b2c3d4e5f6"
}
```
            
## Пример успешного ответа (202):
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refresh_token": null,
  "expires_in": 3600,
  "jwtValidTill": "2024-06-15T10:00:00Z",
  "accountUserTypeID": 1
}
```
            
## Негативные сценарии:
- 400 Bad Request — не указаны обязательные поля или некорректное тело запроса.
- 401 Unauthorized — аккаунт по коду верификации не найден.
