# PROXY — схемы

> **Что здесь:** определения типов запросов/ответов сервиса PROXY. Ручки, ссылающиеся на них — `endpoints/PROXY.md`.

```
type GetResult { url?: str }
type KeyValuePairOfStringAndString { key?: str, value?: str }
type PostData { body?: str /* Тело запроса, закодированное в Base64 */, headers?: KeyValuePairOfStringAndString[] /* Передаваемые заголовки запроса */, method: str /* HTTP-метод отправляемого запроса */, url: str /* Адрес, на который будет отправлен запрос */ }
type PostResult { content?: str /* Тело ответа, закодированное в Base64 */, headers?: map<str[]> /* Заголовки ответа внешнего сервиса */, statusCode?: int /* HTTP-статус ответа внешнего сервиса */ }
```
