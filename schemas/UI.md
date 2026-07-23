# UI — схемы

> **Что здесь:** определения типов запросов/ответов сервиса UI. Ручки, ссылающиеся на них — `endpoints/UI.md`.

```
type AttributeDto { id?: int /* Идентификатор в системе */, isInUse?: bool /* Признак того, что атрибут задействован в шаблоне */, name?: str /* Наименование в системе */ }
type ComponentDto { code?: str /* Внутренний код */, description?: str /* Описание */, id?: int /* Внутренний идентификатор в системе */, isInUse?: bool /* Признак того, что компонент задействован в шаблоне */, isRequired?: bool /* Признак того, что элемент должен быть представлен в шаблоне (for future use) */ }
type ComponentResult { code?: str /* Код */, description?: str /* Описание */ }
type ErrorModel { arguments?: map<str>, code?: str, message?: str, traceIdentifier?: str }
type FieldTypeEnum enum(Component, Attribute)
type JToken JToken[]
type LayoutBlockDto { fields: LayoutFieldDto[] /* Список полей размещённых в блоке */, id?: int /* Внутренний идентификатор сущности dto */, index?: int /* Индекс блока */, name: str /* Имя блока для отображения */ }
type LayoutColumnDto { blocks: LayoutBlockDto[] /* Список блоков размещённых в колонке */, id?: int /* Внутренний идентификатор сущности dto */, index: int /* Индекс колонки */ }
type LayoutFieldDto { code: str /* Код компонента или идентификатор атрибута */, color?: str /* Цвет */, id?: int /* Внутренний идентификатор сущности dto */, img?: str /* Пиктограмма */, index?: int /* Индекс поля */, label: str /* Подпись для поля */, type: FieldTypeEnum }
type LayoutTaskTypeDto { id?: int /* Идентификатор типа */, name?: str /* Имя типа */ }
type LayoutTemplateDto { columns: LayoutColumnDto[] /* Список колонок в представлении заявки */, id?: int /* Внутренний идентификатор сущности dto */, isDefault?: bool /* Признак того, что шаблон используется как настройка по умолчанию */, name?: str /* Название шаблона (for future use) */, taskTypes?: int[] /* Идентификаторы типов задач к которым применим шаблон */ }
type MergeData { filterCode: str, sortOrder: int }
type SubsystemViewProjection { description?: str, subsystemID?: int, viewCode?: str }
type TaskViewProjection { applicationID?: int, dataJson?: str, isDefault?: bool, subsystemViewCode?: str }
type TaskViewTemplateResult { code?: str /* Код с системе */, isDefault?: bool /* Является ли оно по умолчанию */, name?: str /* Имя формы заявки */ }
type UserFilterFavouriteEntity { applicationID?: int, filterCode?: str, resource?: str, sortOrder?: int, tenantID?: int, userID?: int }
```
