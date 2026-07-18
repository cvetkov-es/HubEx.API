# NEWS — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса NEWS (API for managing news and advertisements in HubEx): сигнатуры, параметры, права. Типы — schemas/NEWS.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/NEWS.md`; грабли — `notes/NEWS.md` (если есть).
> **Источник:** swagger сервиса NEWS · файл генерируется пайплайном — руками не править.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/NEWS`

**Оглавление**

- Articles — строки 14–16

## Articles
- `GET /Articles` — Возвращает список доступных пользователю новостей. · права: ArticleListForTenantMember · paginated · коды: 200, 206
  ← query: isRead?:enum(true, false), isPublished?:enum(true, false) → map<ListResult>
