# NEWS — схемы

> **Что здесь:** определения типов запросов/ответов сервиса NEWS. Ручки, ссылающиеся на них — `endpoints/NEWS.md`.

```
type DataNEWSMergeDeliveryData { articleID: int }
type ExceptionHandlingModelsErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type ResultsArticlesListResult { footer?: str /* Нижний колонтитул новости */, id?: int, text?: str /* Содержание новости, разметка */, title?: str /* Заголовок новости */ }
```
