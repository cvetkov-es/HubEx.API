# AUTHZ — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса AUTHZ (API авторизации HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHZ.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHZ.md`; грабли — `notes/AUTHZ.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/AUTHZ`

**Оглавление**

- RefreshTokens — строки 17–20
- Пример успешного ответа (200): — строки 22–30
- Пример успешного ответа (204): — строки 32–33
- Пример успешного ответа при X-Use-Cookie (200): — строки 35–36
- Негативные сценарии: — строки 38–41

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
