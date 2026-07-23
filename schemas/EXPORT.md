# EXPORT — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса EXPORT. Ручки, ссылающиеся на них — `endpoints/EXPORT.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type FieldResult { code?: str /* Код поля */, description?: str /* Описание поля */ }
```
