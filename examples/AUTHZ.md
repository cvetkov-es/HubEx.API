# AUTHZ — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса AUTHZ, вынесенные из `endpoints/AUTHZ.md`. Сигнатуры и типы — там же и в `schemas/AUTHZ.md`.

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
