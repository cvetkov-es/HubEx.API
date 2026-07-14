# NEWS — схемы

> **Что здесь:** определения типов запросов/ответов сервиса NEWS. Ручки, ссылающиеся на них — `endpoints/NEWS.md`.
> **Источник:** `snapshots/NEWS.json` · файл генерируется пайплайном — руками не править.

```
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type ListResult { id?: int, title?: str /* Заголовок новости */, text?: str /* Содержание новости, разметка */, footer?: str /* Нижний колонтитул новости */ }
type MergeDeliveryData { articleID: int }
```
