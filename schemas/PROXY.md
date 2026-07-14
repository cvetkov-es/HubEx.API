# PROXY — схемы

> **Что здесь:** определения типов запросов/ответов сервиса PROXY. Ручки, ссылающиеся на них — `endpoints/PROXY.md`.
> **Источник:** `snapshots/PROXY.json` · файл генерируется пайплайном — руками не править.

```
type GetResult { url?: str }
type KeyValuePair<String, String> { key?: str, value?: str }
type PostData { url: str, method: str, headers?: KeyValuePair<String, String>[], body?: str }
type PostResult { headers?: map<str[]>, content?: str, statusCode?: int }
```
