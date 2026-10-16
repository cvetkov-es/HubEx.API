# UI — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса UI (API for UI information): сигнатуры, параметры, права. Типы — schemas/UI.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/UI.md`; грабли — `notes/UI.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/UI`
> Примеры ответов вынесены в [../examples/UI.md](../examples/UI.md).

**Оглавление**

- Components — строки 20–22
- Filters — строки 24–26
- LayoutTemplates — строки 28–46
- Resources — строки 48–50
- SubsystemView — строки 52–56
- TaskViewTemplate — строки 58–60
- UserViews — строки 62–66

## Components
- `GET /Components` — Возвращает полный список компонентов · paginated · коды: 200, 204, 206 · примеры
  → map<ResultsBaseComponentResult>

## Filters
- `GET /Filters` — Получение списка избранных фильтров пользователя · paginated · коды: 200, 204, 206 · примеры
  ← query: applicationID?:int, resource?:str, applicationID?:int, resource?:str → EntitiesUIUserFilterFavouriteEntity[]

## LayoutTemplates
- `GET /LayoutTemplates` — Получить список представлений · коды: 200, 204 · примеры
  ← query: taskTypeID?:int[], isDefault?:bool, taskTypeID?:int, isDefault?:bool → ApiDtoLayoutTemplateDto[]
  Список возвращается с полным набором атрибутов представления.
- `GET /LayoutTemplates/bytype/{id}` — Получить представление по типу заявки · коды: 200, 404 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
  Возвращает первое подходящее представление для типа заявки или дефолтное.
- `GET /LayoutTemplates/default` — Возвращает шаблон по умолчанию · коды: 200, 409 · примеры
  → ApiDtoLayoutTemplateDto
- `GET /LayoutTemplates/{id}` — Получить конкретное представление · коды: 200, 404 · примеры
  ← path: id:int → ApiDtoLayoutTemplateDto
- `GET /LayoutTemplates/{id}/Attributes` — Полный список доступных атрибутов системы с указанием использования в шаблоне · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoAttributeDto[]
  Возвращает полный список доступных дополнительных полей с указанием того, были ли они перемещены пользователем в данном шаблоне.
- `GET /LayoutTemplates/{id}/Components` — Полный список доступных компонентов системы с указанием использования в шаблоне · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoComponentDto[]
  Возвращает полный список доступных полей системы с указанием того, были ли они перемещены пользователем в данном шаблоне.
- `GET /LayoutTemplates/{id}/taskTypes` — Получить список типов задач представления · коды: 200, 204, 404 · примеры
  ← path: id:int → ApiDtoLayoutTaskTypeDto[]

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
