# SLA — схемы

> **Что здесь:** определения типов запросов/ответов сервиса SLA. Ручки, ссылающиеся на них — `endpoints/SLA.md`.

```
type AddData { color: str, erpID?: str, isDefault: bool, name: str, sortOrder?: int }
type Attributes.ListResult { name?: str /* Имя атрибута */ }
type Criticalities.GetResult { color?: str /* Цвет критичности */, erpID?: str /* Идентификатор объекта во внешней системе */, isDefault?: bool, name?: str /* Название критичности */, sortOrder?: int /* Номер сортировки */ }
type DeadlineRuleActionData<DeadlineRuleAttributeData> { data: DeadlineRuleAttributeData[], deadlineRuleID: int }
type DeadlineRuleAddData { isActive?: bool, name: str, runtime: float, scheduleRuleID: int }
type DeadlineRuleAttributeData { attrNumbValue: int, attributeID: int }
type DeadlineRuleAttributeResult { attrNumbValue?: int /* Значение атрибута */, attributeID?: int /* Идентификатор атрибута */, deadlineRuleID?: int /* Идентификатор правила планового закрытия заявки */ }
type DeadlineRules.GetResult { id?: int /* Идентификатор правила планового закрытия заявки */, isActive?: bool /* Признак активности правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */, scheduleRuleID?: int }
type DeadlineRules.ListResult { id?: int /* Идентификатор правила планового закрытия заявки */, isActive?: bool /* Признак активности правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */, scheduleRuleID?: int }
type DeadlineRuleUpdateData { id: int, isActive?: bool, name: str, runtime: float, scheduleRuleID: int }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type PostResult { id?: int /* Идентификатор правила планового закрытия заявки */ }
type UpdateData { color: str, erpID?: str, id?: int, isDefault: bool, name: str, sortOrder?: int }
```
