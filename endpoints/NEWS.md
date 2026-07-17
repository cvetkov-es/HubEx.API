# NEWS — справочник ручек

> **Что здесь:** все ручки сервиса NEWS (API for managing news and advertisements in HubEx): сигнатуры, параметры, права. Типы — schemas/NEWS.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/NEWS.md`; грабли — `notes/NEWS.md` (если есть).
> **Источник:** swagger сервиса NEWS · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/NEWS`

**Оглавление**

- Articles — строки 13–17

## Articles
- `GET /Articles` — Возвращает список доступных пользователю новостей. · права: ArticleListForTenantMember · paginated · коды: 200, 206
  ← query: isRead?:enum(true, false), isPublished?:enum(true, false) → map<ListResult>
- `PUT /Articles` — Помечет новость как прочитанную у текущего пользователя · права: ArticleDeliveryMerge · коды: 202, 409
  ← body: MergeDeliveryData[]
