# UI — справочник ручек

> **Что здесь:** все ручки сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).

Base: `{BASE_URL}/UI`

**Оглавление**

- Components — строки 19–21
- Filters — строки 23–27
- LayoutTemplates — строки 29–63
- Resources — строки 65–67
- SubsystemView — строки 69–73
- TaskViewTemplate — строки 75–77
- UserViews — строки 79–89
- Views — строки 91–95

## Components
- `GET /Components` — Возвращает полный список компонентов · права: ComponentsList · paginated · коды: 200, 206
  → map<ComponentResult>

## Filters
- `GET /Filters` — Метод получения списка избранных фильтров пользователя · права: UserFilterFavouriteList · paginated · коды: 200, 206
  ← query: applicationID?:int, resource?:str → UserFilterFavouriteEntity[]
- `POST /Filters/{resource}` — Изменяем избранные пользовательские фильтры · права: UserFilterFavouriteMerge · коды: 202
  ← path: resource:str; body: MergeData[]

## LayoutTemplates
- `GET /LayoutTemplates` — Получить список представлений · коды: 200, 204
  ← query: taskTypeID?:int[], isDefault?:bool → LayoutTemplateDto[]
  Список возвращается с полным набором атрибутов представления
- `POST /LayoutTemplates` — Создать представление · коды: 201, 400, 409
  ← body: LayoutTemplateDto → LayoutTemplateDto
  Создаёт представление со всеми связанными свойствами
- `GET /LayoutTemplates/bytype/{id}` — Получить представление по типу заявки · коды: 200, 404
  ← path: id:int → LayoutTemplateDto
  Возвращает первое подходящее представление для типа заявки или дефолтное
- `GET /LayoutTemplates/default` — Возвращает шаблон по умолчанию · коды: 200, 409
  → LayoutTemplateDto
- `POST /LayoutTemplates/default` — Создаёт шаблон по умолчанию. Если шаблон с флагом IsDefault = true существует - Conflict (409) · коды: 200, 409
  → LayoutTemplateDto
- `GET /LayoutTemplates/{id}` — Получить конкретное представление · коды: 200, 404
  ← path: id:int → LayoutTemplateDto
  Пересоздаёт представление полностью
- `PUT /LayoutTemplates/{id}` — Обновить представление и все связанные сущности · коды: 200, 400, 404
  ← path: id:int; body: LayoutTemplateDto → LayoutTemplateDto
  Пересоздаёт представление полностью
- `DELETE /LayoutTemplates/{id}` — Удалить представление и все связные сущности · коды: 202, 400, 404
  ← path: id:int
- `GET /LayoutTemplates/{id}/Attributes` — Полный список доступных полей системы с указанием того, были ли они перемещены пользователем или нет в данном шаблоне · коды: 200, 204, 404
  ← path: id:int → AttributeDto[]
- `GET /LayoutTemplates/{id}/Components` — Полный список доступных полей системы с указанием того, были ли они перемещены пользователем или нет в данном шаблоне · коды: 200, 204, 404
  ← path: id:int → ComponentDto[]
- `PUT /LayoutTemplates/{id}/reset` — Сбрасывает настройки шаблона к состоянию шаблона по умолчанию. 
NB: при этом шаблон не становится дефолтным для тенанта. · коды: 200, 404, 409
  ← path: id:int → LayoutTemplateDto
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления · коды: 200, 204, 404
  ← path: id:int → LayoutTaskTypeDto[]
- `PUT /LayoutTemplates/{id}/taskTypes` — Сопоставить список типов задачь представления · коды: 202, 400, 404
  ← path: id:int; body: int[]
- `DELETE /LayoutTemplates/{id}/taskTypes` — Отвязать типы задач от шаблона · коды: 202, 400, 404
  ← path: id:int; body: int[]

## Resources
- `GET /Resources` — Метод получения списка ресурсов · права: ResourcesList · paginated · коды: 200, 206
  → map<TaskViewTemplateResult>

## SubsystemView
- `GET /SubsystemView` — Возвращает cписок форм подсистемы. · paginated · коды: 200, 204, 206, 404, 500
  ← path: subsystemID:int → SubsystemViewProjection[]
- `GET /SubsystemView/{subsystemID}` — Возвращает cписок форм подсистемы. · paginated · коды: 200, 204, 206, 404, 500
  ← path: subsystemID:int → SubsystemViewProjection[]

## TaskViewTemplate
- `GET /TaskViewTemplate` — Метод получения списка шаблонов формы заявки · права: TaskViewTemplateList · paginated · коды: 200, 206
  → map<TaskViewTemplateResult>

## UserViews
- `GET /UserViews/Users/{id}` — Получение списка шаблонов пользователя · права: UserViewRead · paginated · коды: 200, 204, 206, 404, 500
  ← path: id:int → TaskViewProjection[]
- `GET /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Получение шаблона · права: UserViewRead · paginated · коды: 200, 204, 206, 404, 500
  ← path: userID:int, applicationID:int, code:str → TaskViewProjection
- `POST /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Добавление индивидуального шаблона пользователя · права: UserViewWrite · paginated · коды: 201, 204, 206, 404, 500
  ← path: userID:int, applicationID:int, code:str; body: map<JToken>
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}` — Изменение индивидуального шаблона пользователя · права: UserViewWrite · paginated · коды: 202, 204, 206, 404, 500
  ← path: userID:int, applicationID:int, code:str; body: map<JToken>
- `PUT /UserViews/Users/{userID}/Applications/{applicationID}/{code}/reset` — Сброс индивидуального шаблона пользователя · права: UserViewWrite · paginated · коды: 202, 204, 206, 404, 500
  ← path: userID:int, applicationID:int, code:str

## Views
- `PUT /Views/Applications/{applicationID}/{code}` — Изменение дефолтного шаблона · права: DefaultViewWrite · paginated · коды: 202, 204, 206, 404, 500
  ← path: applicationID:int, code:str; body: map<JToken>
- `PUT /Views/Applications/{applicationID}/{code}/reset` — Сброс дефолтного шаблона в значение из шаблонного тенанта · права: DefaultViewWrite · paginated · коды: 202, 204, 206, 404, 500
  ← path: applicationID:int, code:str
