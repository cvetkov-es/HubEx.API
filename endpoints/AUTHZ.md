# AUTHZ — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса AUTHZ (Authenticatin and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTHZ.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTHZ.md`; грабли — `notes/AUTHZ.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/AUTHZ`

**Оглавление**

- RefreshTokens — строки 13–16

## RefreshTokens
- `GET /RefreshTokens` — Возвращает refresh-токен с параметрами по умолчанию. · коды: 200
  → JwtResultBase
  Для выполнения данного метода пользователь должен быть **TenantMember**.
