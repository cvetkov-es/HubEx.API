# AUTHZ — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса AUTHZ, вынесенные из `endpoints/AUTHZ.md`. Сигнатуры и типы — там же и в `schemas/AUTHZ.md`.

## AccessTokens

### `POST /AccessTokens`

## Пример запроса (refresh-токен):
```json
{
  "refreshJwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "accessJwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
            
## Пример запроса (X-Use-Cookie):
```json
{}
```
            
## Пример успешного ответа (200):
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600,
  "jwtValidTill": "2024-06-15T10:00:00Z",
  "profile": { "userID": 42, "firstName": "Иван", "lastName": "Иванов" },
  "permissions": {},
  "tenant": { "id": 10, "name": "Demo", "fullName": "Demo Tenant LLC", "uriName": "demo" },
  "tenantMember": { "id": 1001, "userID": 42, "accountID": 100 }
}
```
            
## Негативные сценарии:
- 401 Unauthorized — не удалось определить члена тенанта по переданным данным.
- 400 Bad Request — отсутствует тело при работе без cookie, некорректный или просроченный токен.
- 403 Forbidden — нет доступа к указанному приложению (заголовок `X-Application-ID`).

## Accounts

### `POST /Accounts/authorize`

## Пример запроса:
```json
{
  "tenantID": 10,
  "tenantMemberID": 1001
}
```
            
## Пример успешного ответа (200):
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600,
  "jwtValidTill": "2024-06-15T10:00:00Z",
  "profile": {
    "userID": 42,
    "firstName": "Иван",
    "lastName": "Иванов"
  },
  "permissions": { "TaskView": "Allow" },
  "tenantLicenses": [],
  "featureFlags": [],
  "roleTaskAttribute": []
}
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — JWT не содержит признака аутентифицированной учётной записи (`Authenticated`).
- 400 Bad Request — передано неполное или некорректное тело (например `{}` или только одно из полей).

## RefreshTokens

### `GET /RefreshTokens`

## Пример успешного ответа (200):
```json
{
  "access_token": "",
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 2592000,
  "jwtValidTill": "2024-07-15T10:00:00Z"
}
```
            
## Пример успешного ответа (204):
Refresh-токен не найден.
            
## Пример успешного ответа при X-Use-Cookie (200):
Тело ответа пустое, refresh-токен в cookie `RefreshTokenCookie`.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — JWT не содержит авторизации в тенанте (`TenantMember`).
- 400 Bad Request — ошибка настройки CORS при использовании cookie.

### `POST /RefreshTokens`

## Пример запроса:
```json
{
  "validity": "30.00:00:00"
}
```
            
## Пример успешного ответа (200/201):
```json
{
  "access_token": "",
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 2592000,
  "jwtValidTill": "2024-07-15T10:00:00Z"
}
```
            
## Пример успешного ответа при X-Use-Cookie (200/201):
Тело ответа пустое, refresh-токен в cookie `RefreshTokenCookie`.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — JWT не содержит авторизации в тенанте (`TenantMember`).
- 400 Bad Request — некорректные параметры или ошибка настройки CORS при использовании cookie.

## ServiceTokens

### `POST /ServiceTokens`

## Пример запроса:
```json
[1001, 1002]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "token": "svc_abc123def456",
    "created": "2024-06-15T09:00:00Z",
    "validTill": "2025-06-15T09:00:00Z"
  }
]
```
            
## Пример успешного ответа (204):
Тело ответа пустое — новые токены не были созданы.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав (`ServiceTokenAdd`).

### `DELETE /ServiceTokens`

## Пример запроса:
```json
[1001, 1002]
```
            
## Пример успешного ответа (202):
Тело ответа пустое.
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — недостаточно прав (`ServiceTokenRemove`).

## Tokens

### `POST /Tokens/renew`

## Пример успешного ответа (200):
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600,
  "jwtValidTill": "2024-06-15T10:00:00Z"
}
```
            
## Негативные сценарии:
- 401 Unauthorized — отсутствует или некорректен Bearer-токен.
- 403 Forbidden — JWT не содержит авторизации в тенанте (`TenantMember`).
- 400 Bad Request — access-токен не найден в контексте аутентификации.
