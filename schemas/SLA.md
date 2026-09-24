# SLA — схемы

> **Что здесь:** определения типов запросов/ответов сервиса SLA. Ручки, ссылающиеся на них — `endpoints/SLA.md`.

```
type DeadlineRuleActionDataOfDeadlineRuleAttributeData { data: SLADeadlineRuleAttributeDeadlineRuleAttributeData[], deadlineRuleID: int }
type ExceptionHandlingModelsErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type ResultsAttributesListResult { name?: str /* Имя атрибута */ }
type ResultsCriticalitiesGetResult { color?: str /* Цвет критичности */, erpID?: str /* Идентификатор объекта во внешней системе */, isDefault?: bool, name?: str /* Название критичности */, sortOrder?: int /* Номер сортировки */ }
type ResultsDeadlineRuleAttributesDeadlineRuleAttributeResult { attrNumbValue?: int /* Значение атрибута */, attributeID?: int /* Идентификатор атрибута */, deadlineRuleID?: int /* Идентификатор правила планового закрытия заявки */ }
type ResultsDeadlineRulesGetResult { id?: int /* Идентификатор правила планового закрытия заявки */, isActive?: bool /* Признак активности правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */, scheduleRuleID?: int /* График для правила планового закрытия заявки */ }
type ResultsDeadlineRulesListResult { id?: int /* Идентификатор правила планового закрытия заявки */, isActive?: bool /* Признак активности правила планового закрытия заявки */, name?: str /* Название правила планового закрытия заявки */, runtime?: float /* Время выполнение (в часах) для правила планового закрытия заявки */, scheduleRuleID?: int /* График для правила планового закрытия заявки */ }
type ResultsDeadlineRulesPostResult { id?: int /* Идентификатор правила планового закрытия заявки */ }
type SLACriticalityAddData { color: str, erpID?: str, isDefault: bool, name: str, sortOrder?: int }
type SLACriticalityUpdateData { color: str, erpID?: str, id?: int, isDefault: bool, name: str, sortOrder?: int }
type SLADeadlineRuleAttributeDeadlineRuleAttributeData { attrNumbValue: int, attributeID: int }
type SLADeadlineRuleDeadlineRuleAddData { isActive?: bool, name: str, runtime: float, scheduleRuleID: int }
type SLADeadlineRuleDeadlineRuleUpdateData { id: int, isActive?: bool, name: str, runtime: float, scheduleRuleID: int }
```
