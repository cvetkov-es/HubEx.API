# AUTHZ — справочник ручек

> **Что здесь:** все ручки сервиса AUTHZ (Authenticatin and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHZ.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHZ.md`; грабли — `notes/AUTHZ.md` (если есть).

Base: `{BASE_URL}/AUTHZ`

**Оглавление**

- AccessTokens — строки 16–19
- Accounts — строки 21–24
- RefreshTokens — строки 26–32
- ServiceTokens — строки 34–38
- Tokens — строки 40–43

## AccessTokens
- `POST /AccessTokens` — Обновляет токен доступа к  ресурсам · коды: 200, 201
  ← body: RefreshData → JwtResultBase
  Выполнение данного метода резрешино от **анонимного пользователя**.

## Accounts
- `POST /Accounts/authorize` — Авторизация учетной записи в тенанте · коды: 200
  ← body: AuthorizeData → TenantMemberAuthorizationResult
  Для выполнения данного метода пользователь должен быть **Authenticated**.

## RefreshTokens
- `GET /RefreshTokens` — Возвращает refresh-токен с параметрами по умолчанию. · коды: 200
  → JwtResultBase
  Для выполнения данного метода пользователь должен быть **TenantMember**.
- `POST /RefreshTokens` — Генерирует обновляющий токен и возвращает его · коды: 200, 201
  ← body: GenerateData → JwtResultBase
  Для выполнения данного метода пользователь должен быть **TenantMember**.

## ServiceTokens
- `POST /ServiceTokens` — Генерирует новый токен доступа и возвращает его · права: ServiceTokenAdd · коды: 201
  ← body: int[] → PostResult
- `DELETE /ServiceTokens` — Удаляет токен доступа · права: ServiceTokenRemove · коды: 202
  ← body: int[]

## Tokens
- `POST /Tokens/renew` — Обновление JWT · коды: 200
  → JwtResultBase
  Для выполнения данного метода пользователь должен быть **TenantMember**.
