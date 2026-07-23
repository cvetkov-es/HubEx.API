# SLA — схемы

> **Что здесь:** определения типов read-ответов (GET/HEAD) сервиса SLA. Ручки, ссылающиеся на них — `endpoints/SLA.md`.
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

```
type Attributes.ListResult { name?: str /* Имя атрибута */ }
type Criticalities.GetResult { color?: str /* Цвет критичности */, erpID?: str /* Идентификатор объекта во внешней системе */, isDefault?: bool, name?: str /* Название критичности */, sortOrder?: int /* Номер сортировки */ }
type DeadlineRules.GetResult { id?: int /* Идентификатор правила планового закрытия заявки */, isActive?: bool /* Признак активности правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */, scheduleRuleID?: int }
type DeadlineRules.ListResult { id?: int /* Идентификатор правила планового закрытия заявки */, isActive?: bool /* Признак активности правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */, scheduleRuleID?: int }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
```
