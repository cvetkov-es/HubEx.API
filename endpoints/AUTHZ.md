# AUTHZ — справочник ручек

> **Что здесь:** все ручки сервиса AUTHZ (API авторизации HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHZ.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHZ.md`; грабли — `notes/AUTHZ.md` (если есть).

Base: `{BASE_URL}/AUTHZ`
> Примеры ответов вынесены в [../examples/AUTHZ.md](../examples/AUTHZ.md).

**Оглавление**

- AccessTokens — строки 34–44
- Пример запроса (refresh-токен): — строки 46–52
- Пример запроса (X-Use-Cookie): — строки 54–57
- Пример успешного ответа (200): — строки 59–70
- Негативные сценарии: — строки 72–75
- Accounts — строки 77–81
- Пример запроса: — строки 83–89
- Пример успешного ответа (200): — строки 91–107
- Негативные сценарии: — строки 109–112
- RefreshTokens — строки 114–117
- Пример успешного ответа (200): — строки 119–127
- Пример успешного ответа (204): — строки 129–130
- Пример успешного ответа при X-Use-Cookie (200): — строки 132–133
- Негативные сценарии: — строки 135–141
- Пример запроса: — строки 143–148
- Пример успешного ответа (200/201): — строки 150–158
- Пример успешного ответа при X-Use-Cookie (200/201): — строки 160–161
- Негативные сценарии: — строки 163–166
- ServiceTokens — строки 168–172
- Tokens — строки 174–177
- Пример успешного ответа (200): — строки 179–186
- Негативные сценарии: — строки 188–191

## AccessTokens
- `POST /AccessTokens` — Обновляет access-токен по refresh-токену, одноразовому токену или сервисному токену. · коды: 200, 400
  ← body: RefreshData → TenantMemberAuthorizationResult
  Поддерживает три способа аутентификации (достаточно одного):
- `refreshJwt` — JWT refresh-токен;
- `oneTimeLoginToken` + `tenantID` — одноразовый токен входа;
- `serviceToken` — сервисный токен.
            
При заголовке `X-Use-Cookie: true` refresh-токен читается из cookie `RefreshTokenCookie`; в теле достаточно пустого JSON-объекта `{}` (поле `refreshJwt` необязательно). Отсутствие тела запроса не поддерживается.
            
Опциональный заголовок `X-Application-ID` проверяет доступ к указанному приложению.
            
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
- `POST /Accounts/authorize` — Авторизует учётную запись в указанном тенанте. · коды: 200, 400
  ← body: AuthorizeData → TenantMemberAuthorizationResult
  Тело запроса целиком можно опустить — тогда `tenantID` и `tenantMemberID` берутся из JWT текущего пользователя.
Если тело передано, оба поля (`tenantID`, `tenantMemberID`) обязательны и должны быть больше 0.
            
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
- `GET /RefreshTokens` — Возвращает refresh-токен с параметрами по умолчанию. · коды: 200, 204, 400
  → JwtResultBase
  При заголовке `X-Use-Cookie: true` refresh-токен записывается в HttpOnly-cookie, тело ответа пустое.
            
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
- `POST /RefreshTokens` — Генерирует refresh-токен для текущего члена тенанта. · коды: 200, 201, 400
  ← body: GenerateData → JwtResultBase
  При заголовке `X-Use-Cookie: true` refresh-токен записывается в HttpOnly-cookie, тело ответа пустое.
            
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
- `POST /ServiceTokens` — Генерирует сервисные токены для указанных членов тенанта. · коды: 201, 204 · примеры
  ← body: int[] → PostResult[]
- `DELETE /ServiceTokens` — Удаляет сервисные токены указанных членов тенанта. · коды: 202 · примеры
  ← body: int[]

## Tokens
- `POST /Tokens/renew` — Продлевает срок действия текущего JWT access-токена. · коды: 200, 400
  → JwtResultBase
  Токен извлекается из сохранённого Bearer-токена текущего запроса.
            
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
