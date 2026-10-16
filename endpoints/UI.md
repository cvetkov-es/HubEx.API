# UI — справочник ручек

> **Что здесь:** все ручки сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).

Base: `{BASE_URL}/UI`
> Примеры ответов вынесены в [../examples/UI.md](../examples/UI.md).

**Оглавление**

- Components — строки 20–22
- Filters — строки 24–28
- LayoutTemplates — строки 30–66
- Resources — строки 68–70
- SubsystemView — строки 72–76
- TaskViewTemplate — строки 78–80
- UserViews — строки 82–94
- Views — строки 96–100

## Components
- `GET /Components` — Возвращает полный список компонентов · paginated · коды: 200, 204, 206 · примеры
  → map<ResultsBaseComponentResult>

## Filters
- `GET /Filters` — Получение списка избранных фильтров пользователя · paginated · коды: 200, 204, 206 · примеры
  ← query: applicationID?:int, resource?:str, applicationID?:int, resource?:str → EntitiesUIUserFilterFavouriteEntity[]
- `POST /Filters/{resource}` — Сохранение избранных фильтров пользователя · коды: 202 · примеры
  ← path: resource:str; body: DataUIMergeData[]

## LayoutTemplates
- `GET /LayoutTemplates` — Получить список представлений · коды: 200, 204 · примеры
  ← query: taskTypeID?:int[], isDefault?:bool, taskTypeID?:int, isDefault?:bool → ApiDtoLayoutTemplateDto[]
  Список возвращается с полным набором атрибутов представления.
- `POST /LayoutTemplates` — Создать представление · коды: 201, 400, 409 · примеры
  ← body: ApiDtoLayoutTemplateDto → ApiDtoLayoutTemplateDto
  Создаёт представление со всеми связанными свойствами.
- `GET /LayoutTemplates/bytype/{id}` — Получить представление по типу заявки · коды: 200, 404 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
  Возвращает первое подходящее представление для типа заявки или дефолтное.
- `GET /LayoutTemplates/default` — Возвращает шаблон по умолчанию · коды: 200, 409 · примеры
  → ApiDtoLayoutTemplateDto
- `POST /LayoutTemplates/default` — Создаёт шаблон по умолчанию · коды: 200, 409 · примеры
  → ApiDtoLayoutTemplateDto
  Если шаблон с флагом `IsDefault = true` уже существует, возвращается ошибка `409 Conflict`.
- `GET /LayoutTemplates/{id}` — Получить конкретное представление · коды: 200, 404 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
- `PUT /LayoutTemplates/{id}` — Обновить представление и все связанные сущности · коды: 200, 400, 404 · примеры
  ← path: id:int; body: ApiDtoLayoutTemplateDto → ApiDtoLayoutTemplateDto
  Пересоздаёт представление полностью.
- `DELETE /LayoutTemplates/{id}` — Удалить представление и все связные сущности · коды: 202, 400, 404 · примеры
  ← path: id:int
- `GET /LayoutTemplates/{id}/Attributes` — Полный список доступных атрибутов системы с указанием использования в шаблоне · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoAttributeDto[]
  Возвращает полный список доступных дополнительных полей с указанием того, были ли они перемещены пользователем в данном шаблоне.
- `GET /LayoutTemplates/{id}/Components` — Полный список доступных компонентов системы с указанием использования в шаблоне · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoComponentDto[]
  Возвращает полный список доступных полей системы с указанием того, были ли они перемещены пользователем в данном шаблоне.
- `PUT /LayoutTemplates/{id}/reset` — Сбрасывает настройки шаблона к состоянию шаблона по умолчанию · коды: 200, 404, 409 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
  NB: при этом шаблон не становится дефолтным для тенанта.
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoLayoutTaskTypeDto[]
- `PUT /LayoutTemplates/{id}/taskTypes` — Сопоставить список типов задач представления · коды: 202, 400, 404 · примеры
  ← path: id:int; body: int[]
- `DELETE /LayoutTemplates/{id}/taskTypes` — Отвязать типы задач от шаблона · коды: 202, 400, 404 · примеры
  ← path: id:int; body: int[]

## Resources
- `GET /Resources` — Возвращает список ресурсов · paginated · коды: 200, 204, 206 · примеры
  → map<IdCodeNameResultOfByte>

## SubsystemView
- `GET /SubsystemView` — Получение списка форм всех подсистем · коды: 200, 204, 500 · примеры
  → ProjectionsUISubsystemViewProjection[]
- `GET /SubsystemView/{subsystemID}` — Получение списка форм подсистемы по идентификатору · коды: 200, 204, 404, 500 · примеры
  ← path: subsystemID:int → ProjectionsUISubsystemViewProjection[]

## TaskViewTemplate
- `GET /TaskViewTemplate` — Получение списка шаблонов формы заявки · paginated · коды: 200, 204, 206 · примеры
  → map<ResultsTaskViewTemplatesTaskViewTemplateResult>

## UserViews
- `GET /UserViews/Users/{id}` — Получение списка шаблонов пользователя · коды: 200, 204, 404, 500 · примеры
  ← path: id:int → ProjectionsUITaskViewProjection[]
- `GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Получение шаблона пользователя · коды: 200, 204, 404, 500 · примеры
  ← path: userID:int, applicationID:int, code:str → ProjectionsUITaskViewProjection
- `POST /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Добавление индивидуального шаблона пользователя · коды: 201, 404, 500 · примеры
  ← path: userID:int, applicationID:int, code:str; body: map<JsonLinqJToken>
  Тело запроса передается как JSON-объект (`JObject`) с произвольной структурой шаблона представления.
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Изменение индивидуального шаблона пользователя · коды: 202, 404, 500 · примеры
  ← path: userID:int, applicationID:int, code:str; body: map<JsonLinqJToken>
  Тело запроса передается как JSON-объект (`JObject`) с произвольной структурой шаблона представления.
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}/reset` — Сброс индивидуального шаблона пользователя · коды: 202, 404, 500 · примеры
  ← path: userID:int, applicationID:int, code:str

## Views
- `PUT /Views/Applications/{applicationID}/{code}` — Изменение дефолтного шаблона · коды: 202, 404, 500 · примеры
  ← path: applicationID:int, code:str; body: map<JsonLinqJToken>
- `PUT /Views/Applications/{applicationID}/{code}/reset` — Сброс дефолтного шаблона · коды: 202, 404, 500 · примеры
  ← path: applicationID:int, code:str
