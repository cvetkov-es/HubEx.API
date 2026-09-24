# UI — схемы

> **Что здесь:** определения типов запросов/ответов сервиса UI. Ручки, ссылающиеся на них — `endpoints/UI.md`.

```
type ApiDtoAttributeDto { id?: int /* Идентификатор в системе */, isInUse?: bool /* Признак того, что атрибут задействован в шаблоне */, name?: str /* Наименование в системе */ }
type ApiDtoComponentDto { code?: str /* Внутренний код */, description?: str /* Описание */, id?: int /* Внутренний идентификатор в системе */, isInUse?: bool /* Признак того, что компонент задействован в шаблоне */, isRequired?: bool /* Признак того, что элемент должен быть представлен в шаблоне (for future use) */ }
type ApiDtoFieldTypeEnum enum(Component, Attribute)
type ApiDtoLayoutBlockDto { fields: ApiDtoLayoutFieldDto[] /* Список полей размещённых в блоке */, id?: int /* Внутренний идентификатор сущности dto */, index?: int /* Индекс блока */, name: str /* Имя блока для отображения */ }
type ApiDtoLayoutColumnDto { blocks: ApiDtoLayoutBlockDto[] /* Список блоков размещённых в колонке */, id?: int /* Внутренний идентификатор сущности dto */, index: int /* Индекс колонки */ }
type ApiDtoLayoutFieldDto { code: str /* Код компонента или идентификатор атрибута */, color?: str /* Цвет */, id?: int /* Внутренний идентификатор сущности dto */, img?: str /* Пиктограмма */, index?: int /* Индекс поля */, label: str /* Подпись для поля */, type: ApiDtoFieldTypeEnum }
type ApiDtoLayoutTaskTypeDto { id?: int /* Идентификатор типа */, name?: str /* Имя типа */ }
type ApiDtoLayoutTemplateDto { columns: ApiDtoLayoutColumnDto[] /* Список колонок в представлении заявки */, id?: int /* Внутренний идентификатор сущности dto */, isDefault?: bool /* Признак того, что шаблон используется как настройка по умолчанию */, name?: str /* Название шаблона (for future use) */, taskTypes?: int[] /* Идентификаторы типов задач к которым применим шаблон */ }
type DataUIMergeData { filterCode: str, sortOrder: int }
type EntitiesUIUserFilterFavouriteEntity { applicationID?: int, filterCode?: str, resource?: str, sortOrder?: int, tenantID?: int, userID?: int }
type ExceptionHandlingModelsErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type IdCodeNameResultOfByte { code?: str, id?: int, name?: str }
type JsonLinqJToken JsonLinqJToken[]
type ProjectionsUISubsystemViewProjection { description?: str, subsystemID?: int, viewCode?: str }
type ProjectionsUITaskViewProjection { applicationID?: int, dataJson?: str, isDefault?: bool, subsystemViewCode?: str }
type ResultsBaseComponentResult { code?: str /* Код */, description?: str /* Описание */ }
type ResultsTaskViewTemplatesTaskViewTemplateResult { code?: str /* Код с системе */, isDefault?: bool /* Является ли оно по умолчанию */, name?: str /* Имя формы заявки */ }
```
