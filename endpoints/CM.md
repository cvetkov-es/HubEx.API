# CM — справочник ручек

> **Что здесь:** все ручки сервиса CM (API for CM in HubEx): сигнатуры, параметры, права. Типы — schemas/CM.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/CM.md`; грабли — `notes/CM.md` (если есть).

Base: `{BASE_URL}/CM`
> Примеры ответов вынесены в [../examples/CM.md](../examples/CM.md).

**Оглавление**

- Clients — строки 13–15

## Clients
- `POST /Clients/locations` — Сохранение данных о местоположении клиента · коды: 200, 404, 409 · примеры
  ← header: X-CLIENT-IDENTIFIER:str, X-Client-Utc-Offset?:int; body: DataClientsPostData[] → ResultsClientsLocationPostResult
