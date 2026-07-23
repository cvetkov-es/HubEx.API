# PROXY — схемы

> **Что здесь:** определения типов запросов/ответов сервиса PROXY. Ручки, ссылающиеся на них — `endpoints/PROXY.md`.

```
type GetResult { url?: str }
type KeyValuePair<String, String> { key?: str, value?: str }
type PostData { body?: str, headers?: KeyValuePair<String, String>[], method: str, url: str }
type PostResult { content?: str, headers?: map<str[]>, statusCode?: int }
```
