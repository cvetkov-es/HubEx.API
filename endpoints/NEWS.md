# NEWS — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса NEWS (API for managing news and advertisements in HubEx): сигнатуры, параметры, права. Типы — schemas/NEWS.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/NEWS.md`; грабли — `notes/NEWS.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/NEWS`
> Примеры ответов вынесены в [../examples/NEWS.md](../examples/NEWS.md).

**Оглавление**

- Articles — строки 14–16

## Articles
- `GET /Articles` — Получение списка доступных пользователю новостей · коды: 200, 204, 206 · примеры
  ← query: isRead?:bool, isPublished?:bool → map<ResultsArticlesListResult>
