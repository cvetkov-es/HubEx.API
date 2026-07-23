# NEWS — схемы

> **Что здесь:** определения типов запросов/ответов сервиса NEWS. Ручки, ссылающиеся на них — `endpoints/NEWS.md`.

```
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type ListResult { footer?: str /* Нижний колонтитул новости */, id?: int, text?: str /* Содержание новости, разметка */, title?: str /* Заголовок новости */ }
type MergeDeliveryData { articleID: int }
```
