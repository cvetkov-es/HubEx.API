# UI — справочник ручек

> **Что здесь:** все ручки сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).
> **Источник:** `snapshots/UI.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/UI`

## Components
- `GET /Components` — Возвращает полный список компонентов · права: ComponentsList · paginated
  → map<ComponentResult>

## Filters
- `GET /Filters` — Метод получения списка избранных фильтров пользователя · права: UserFilterFavouriteList · paginated
  ← query: applicationID?:int, resource?:str → UserFilterFavouriteEntity[]
- `POST /Filters/{resource}` — Изменяем избранные пользовательские фильтры · права: UserFilterFavouriteMerge
  ← path: resource:str; body: MergeData[]

## LayoutTemplates
- `GET /LayoutTemplates` — Получить список представлений
  ← query: taskTypeID?:int[], isDefault?:bool → LayoutTemplateDto[]
  Список возвращается с полным набором атрибутов представления
- `POST /LayoutTemplates` — Создать представление
  ← body: LayoutTemplateDto → LayoutTemplateDto
  Создаёт представление со всеми связанными свойствами
- `GET /LayoutTemplates/bytype/{id}` — Получить представление по типу заявки
  ← path: id:int → LayoutTemplateDto
  Возвращает первое подходящее представление для типа заявки или дефолтное
- `GET /LayoutTemplates/default` — Возвращает шаблон по умолчанию
  → LayoutTemplateDto
- `POST /LayoutTemplates/default` — Создаёт шаблон по умолчанию. Если шаблон с флагом IsDefault = true существует - Conflict (409)
  → LayoutTemplateDto
- `GET /LayoutTemplates/{id}` — Получить конкретное представление
  ← path: id:int → LayoutTemplateDto
  Пересоздаёт представление полностью
- `PUT /LayoutTemplates/{id}` — Обновить представление и все связанные сущности
  ← path: id:int; body: LayoutTemplateDto → LayoutTemplateDto
  Пересоздаёт представление полностью
- `DELETE /LayoutTemplates/{id}` — Удалить представление и все связные сущности
  ← path: id:int
- `GET /LayoutTemplates/{id}/Attributes` — Полный список доступных полей системы с указанием того, были ли они перемещены пользователем или нет в данном шаблоне
  ← path: id:int → AttributeDto[]
- `GET /LayoutTemplates/{id}/Components` — Полный список доступных полей системы с указанием того, были ли они перемещены пользователем или нет в данном шаблоне
  ← path: id:int → ComponentDto[]
- `PUT /LayoutTemplates/{id}/reset` — Сбрасывает настройки шаблона к состоянию шаблона по умолчанию. 
NB: при этом шаблон не становится дефолтным для тенанта.
  ← path: id:int → LayoutTemplateDto
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления
  ← path: id:int → LayoutTaskTypeDto[]
- `PUT /LayoutTemplates/{id}/taskTypes` — Сопоставить список типов задачь представления
  ← path: id:int; body: int[]
- `DELETE /LayoutTemplates/{id}/taskTypes` — Отвязать типы задач от шаблона
  ← path: id:int; body: int[]

## Resources
- `GET /Resources` — Метод получения списка ресурсов · права: ResourcesList · paginated
  → map<TaskViewTemplateResult>

## SubsystemView
- `GET /SubsystemView` — Возвращает cписок форм подсистемы. · paginated
  ← path: subsystemID:int → SubsystemViewProjection[]
- `GET /SubsystemView/{subsystemID}` — Возвращает cписок форм подсистемы. · paginated
  ← path: subsystemID:int → SubsystemViewProjection[]

## TaskViewTemplate
- `GET /TaskViewTemplate` — Метод получения списка шаблонов формы заявки · права: TaskViewTemplateList · paginated
  → map<TaskViewTemplateResult>

## UserViews
- `GET /UserViews/Users/{id}` — Получение списка шаблонов пользователя · права: UserViewRead · paginated
  ← path: id:int → TaskViewProjection[]
- `GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Получение шаблона · права: UserViewRead · paginated
  ← path: userID:int, applicationID:int, code:str → TaskViewProjection
- `POST /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Добавление индивидуального шаблона пользователя · права: UserViewWrite · paginated
  ← path: userID:int, applicationID:int, code:str; body: map<JToken>
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Изменение индивидуального шаблона пользователя · права: UserViewWrite · paginated
  ← path: userID:int, applicationID:int, code:str; body: map<JToken>
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}/reset` — Сброс индивидуального шаблона пользователя · права: UserViewWrite · paginated
  ← path: userID:int, applicationID:int, code:str

## Views
- `PUT /Views/Applications/{applicationID}/{code}` — Изменение дефолтного шаблона · права: DefaultViewWrite · paginated
  ← path: applicationID:int, code:str; body: map<JToken>
- `PUT /Views/Applications/{applicationID}/{code}/reset` — Сброс дефолтного шаблона в значение из шаблонного тенанта · права: DefaultViewWrite · paginated
  ← path: applicationID:int, code:str
