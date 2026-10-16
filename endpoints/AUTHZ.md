# AUTHZ — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса AUTHZ (API авторизации HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHZ.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHZ.md`; грабли — `notes/AUTHZ.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/AUTHZ`
> Примеры ответов вынесены в [../examples/AUTHZ.md](../examples/AUTHZ.md).

**Оглавление**

- RefreshTokens — строки 14–17

## RefreshTokens
- `GET /RefreshTokens` — Возвращает refresh-токен с параметрами по умолчанию. · коды: 200, 204, 400 · примеры
  → JwtResultBase
  При заголовке `X-Use-Cookie: true` refresh-токен записывается в HttpOnly-cookie, тело ответа пустое.
