# NEWS — справочник ручек

> **Что здесь:** все ручки сервиса NEWS (API for managing news and advertisements in HubEx): сигнатуры, параметры, права. Типы — schemas/NEWS.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/NEWS.md`; грабли — `notes/NEWS.md` (если есть).

Base: `{BASE_URL}/NEWS`
> Примеры ответов вынесены в [../examples/NEWS.md](../examples/NEWS.md).

**Оглавление**

- Articles — строки 13–17

## Articles
- `GET /Articles` — Получение списка доступных пользователю новостей · коды: 200, 204, 206 · примеры
  ← query: isRead?:bool, isPublished?:bool → map<ResultsArticlesListResult>
- `PUT /Articles` — Отметка новостей как прочитанных · коды: 202, 409 · примеры
  ← body: DataNEWSMergeDeliveryData[]
