# UI — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/UI`

**Оглавление**

- Components — строки 19–21
- Filters — строки 23–25
- LayoutTemplates — строки 27–44
- Resources — строки 46–48
- SubsystemView — строки 50–54
- TaskViewTemplate — строки 56–58
- UserViews — строки 60–64

## Components
- `GET /Components` — Возвращает полный список компонентов · права: ComponentsList · paginated · коды: 200, 206
  → map<ComponentResult>

## Filters
- `GET /Filters` — Метод получения списка избранных фильтров пользователя · права: UserFilterFavouriteList · paginated · коды: 200, 206
  ← query: applicationID?:int, resource?:str → UserFilterFavouriteEntity[]

## LayoutTemplates
- `GET /LayoutTemplates` — Получить список представлений · коды: 200, 204
  ← query: taskTypeID?:int[], isDefault?:bool → LayoutTemplateDto[]
  Список возвращается с полным набором атрибутов представления
- `GET /LayoutTemplates/bytype/{id}` — Получить представление по типу заявки · коды: 200, 404
  ← path: id:int → LayoutTemplateDto
  Возвращает первое подходящее представление для типа заявки или дефолтное
- `GET /LayoutTemplates/default` — Возвращает шаблон по умолчанию · коды: 200, 409
  → LayoutTemplateDto
- `GET /LayoutTemplates/{id}` — Получить конкретное представление · коды: 200, 404
  ← path: id:int → LayoutTemplateDto
  Пересоздаёт представление полностью
- `GET /LayoutTemplates/{id}/Attributes` — Полный список доступных полей системы с указанием того, были ли они перемещены пользователем или нет в данном шаблоне · коды: 200, 204, 404
  ← path: id:int → AttributeDto[]
- `GET /LayoutTemplates/{id}/Components` — Полный список доступных полей системы с указанием того, были ли они перемещены пользователем или нет в данном шаблоне · коды: 200, 204, 404
  ← path: id:int → ComponentDto[]
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления · коды: 200, 204, 404
  ← path: id:int → LayoutTaskTypeDto[]

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
