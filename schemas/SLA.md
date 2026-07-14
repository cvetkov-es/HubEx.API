# SLA — схемы

> **Что здесь:** определения типов запросов/ответов сервиса SLA. Ручки, ссылающиеся на них — `endpoints/SLA.md`.
> **Источник:** `snapshots/SLA.json` · файл генерируется пайплайном — руками не править.

```
type AddData { color: str, name: str, isDefault: bool, sortOrder?: int, erpID?: str }
type Attributes.ListResult { name?: str /* Имя атрибута */ }
type Criticalities.GetResult { name?: str /* Название критичности */, color?: str /* Цвет критичности */, isDefault?: bool, sortOrder?: int /* Номер сортировки */, erpID?: str /* Идентификатор объекта во внешней системе */ }
type DeadlineRuleActionData<DeadlineRuleAttributeData> { data: DeadlineRuleAttributeData[], deadlineRuleID: int }
type DeadlineRuleAddData { name: str, scheduleRuleID: int, isActive?: bool, runtime: float }
type DeadlineRuleAttributeData { attributeID: int, attrNumbValue: int }
type DeadlineRuleAttributeResult { deadlineRuleID?: int /* Идентификатор правила планового закрытия заявки */, attributeID?: int /* Идентификатор атрибута */, attrNumbValue?: int /* Значение атрибута */ }
type DeadlineRules.GetResult { id?: int /* Идентификатор правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, scheduleRuleID?: int, isActive?: bool /* Признак активности правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */ }
type DeadlineRules.ListResult { id?: int /* Идентификатор правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, scheduleRuleID?: int, isActive?: bool /* Признак активности правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */ }
type DeadlineRuleUpdateData { id: int, name: str, scheduleRuleID: int, isActive?: bool, runtime: float }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type PostResult { id?: int /* Идентификатор правила планового закрытия заявки */ }
type UpdateData { color: str, name: str, isDefault: bool, sortOrder?: int, erpID?: str, id?: int }
```
