# UI — схемы

> **Что здесь:** определения типов запросов/ответов сервиса UI. Ручки, ссылающиеся на них — `endpoints/UI.md`.
> **Источник:** `snapshots/UI.json` · файл генерируется пайплайном — руками не править.

```
type AttributeDto { id?: int /* Идентификатор в системе */, name?: str /* Наименование в системе */, isInUse?: bool /* Признак того, что атрибут задействован в шаблоне */ }
type ComponentDto { id?: int /* Внутренний идентификатор в системе */, code?: str /* Внутренний код */, description?: str /* Описание */, isRequired?: bool /* Признак того, что элемент должен быть представлен в шаблоне (for future use) */, isInUse?: bool /* Признак того, что компонент задействован в шаблоне */ }
type ComponentResult { code?: str /* Код */, description?: str /* Описание */ }
type ErrorModel { traceIdentifier?: str, code?: str, message?: str, arguments?: map<str> }
type FieldTypeEnum enum(Component, Attribute)
type JToken JToken[]
type LayoutBlockDto { id?: int /* Внутренний идентификатор сущности dto */, index?: int /* Индекс блока */, name: str /* Имя блока для отображения */, fields: LayoutFieldDto[] /* Список полей размещённых в блоке */ }
type LayoutColumnDto { id?: int /* Внутренний идентификатор сущности dto */, index: int /* Индекс колонки */, blocks: LayoutBlockDto[] /* Список блоков размещённых в колонке */ }
type LayoutFieldDto { id?: int /* Внутренний идентификатор сущности dto */, index?: int /* Индекс поля */, label: str /* Подпись для поля */, type: FieldTypeEnum, code: str /* Код компонента или идентификатор атрибута */, color?: str /* Цвет */, img?: str /* Пиктограмма */ }
type LayoutTaskTypeDto { id?: int /* Идентификатор типа */, name?: str /* Имя типа */ }
type LayoutTemplateDto { id?: int /* Внутренний идентификатор сущности dto */, isDefault?: bool /* Признак того, что шаблон используется как настройка по умолчанию */, name?: str /* Название шаблона (for future use) */, columns: LayoutColumnDto[] /* Список колонок в представлении заявки */, taskTypes?: int[] /* Идентификаторы типов задач к которым применим шаблон */ }
type MergeData { filterCode: str, sortOrder: int }
type SubsystemViewProjection { subsystemID?: int, viewCode?: str, description?: str }
type TaskViewProjection { applicationID?: int, subsystemViewCode?: str, dataJson?: str, isDefault?: bool }
type TaskViewTemplateResult { name?: str /* Имя формы заявки */, code?: str /* Код с системе */, isDefault?: bool /* Является ли оно по умолчанию */ }
type UserFilterFavouriteEntity { tenantID?: int, userID?: int, applicationID?: int, resource?: str, filterCode?: str, sortOrder?: int }
```
