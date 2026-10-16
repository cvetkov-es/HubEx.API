# AUTH — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса AUTH (Authentication and authorization API for HubEx): сигнатуры, параметры, права. Типы — schemas/AUTH.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/AUTH.md`; грабли — `notes/AUTH.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/AUTH`
> Примеры ответов вынесены в [../examples/AUTH.md](../examples/AUTH.md).

**Оглавление**

- Accounts — строки 14–24

## Accounts
- `GET /Accounts` — Возвращает данные учетной записи по учетным данным · коды: 200, 204 · примеры
  ← query: credential?:str → GetResult
- `HEAD /Accounts` — Проверяет присутствие учетной записи по указанным полномочиям · коды: 200, 404, 409 · примеры
  ← query: credential?:str
- `GET /Accounts/this/applications` — Приложения учетной записи · paginated · коды: 200, 204, 206 · примеры
  → ApplicationListResult[]
  Поддерживает ограничение результата через query-параметры `offset` и `fetch`.
- `GET /Accounts/this/notifications` — Список уведомлений из лога · paginated · коды: 200, 204, 206 · примеры
  → ListResult[]
  Поддерживает ограничение результата через query-параметры `offset` и `fetch`.
