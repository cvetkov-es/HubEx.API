# AUTHZ — справочник ручек

> **Что здесь:** все ручки сервиса AUTHZ (API авторизации HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHZ.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHZ.md`; грабли — `notes/AUTHZ.md` (если есть).

Base: `{BASE_URL}/AUTHZ`
> Примеры ответов вынесены в [../examples/AUTHZ.md](../examples/AUTHZ.md).

**Оглавление**

- AccessTokens — строки 17–20
- Accounts — строки 22–25
- RefreshTokens — строки 27–33
- ServiceTokens — строки 35–39
- Tokens — строки 41–44

## AccessTokens
- `POST /AccessTokens` — Обновляет access-токен по refresh-токену, одноразовому токену или сервисному токену. · коды: 200, 400 · примеры
  ← body: RefreshData → TenantMemberAuthorizationResult
  Поддерживает три способа аутентификации (достаточно одного): - `refreshJwt` — JWT refresh-токен; - `oneTimeLoginToken` + `tenantID` — одноразовый токен входа; - `serviceToken` — сервисный токен. При заголовке `X-Use-Cookie: true` refresh-токен читается из cookie `RefreshTokenCookie`; в теле достаточно пустого JSON-объекта `{}` (поле `refreshJwt` необязательно). Отсутствие тела запроса не поддерживается. Опциональный заголовок `X-Application-ID` проверяет доступ к указанному приложению.

## Accounts
- `POST /Accounts/authorize` — Авторизует учётную запись в указанном тенанте. · коды: 200, 400 · примеры
  ← body: AuthorizeData → TenantMemberAuthorizationResult
  Тело запроса целиком можно опустить — тогда `tenantID` и `tenantMemberID` берутся из JWT текущего пользователя. Если тело передано, оба поля (`tenantID`, `tenantMemberID`) обязательны и должны быть больше 0.

## RefreshTokens
- `GET /RefreshTokens` — Возвращает refresh-токен с параметрами по умолчанию. · коды: 200, 204, 400 · примеры
  → JwtResultBase
  При заголовке `X-Use-Cookie: true` refresh-токен записывается в HttpOnly-cookie, тело ответа пустое.
- `POST /RefreshTokens` — Генерирует refresh-токен для текущего члена тенанта. · коды: 200, 201, 400 · примеры
  ← body: GenerateData → JwtResultBase
  При заголовке `X-Use-Cookie: true` refresh-токен записывается в HttpOnly-cookie, тело ответа пустое.

## ServiceTokens
- `POST /ServiceTokens` — Генерирует сервисные токены для указанных членов тенанта. · коды: 201, 204 · примеры
  ← body: int[] → PostResult[]
- `DELETE /ServiceTokens` — Удаляет сервисные токены указанных членов тенанта. · коды: 202 · примеры
  ← body: int[]

## Tokens
- `POST /Tokens/renew` — Продлевает срок действия текущего JWT access-токена. · коды: 200, 400 · примеры
  → JwtResultBase
  Токен извлекается из сохранённого Bearer-токена текущего запроса.
